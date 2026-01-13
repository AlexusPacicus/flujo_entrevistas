# Flags — Schema v1.1 (contractual)

Salida clasificadora. No explica, no aconseja, no decide.
Marca estados observables a partir del Transcript contrastado con el ContextPack_BASE.

## Propósito
- Convertir discurso en señales objetivas.
- Habilitar corrección dirigida (Attackers).
- Permitir comparación entre sesiones.

**Origen:**
Generado por el Agente de Análisis — Clasificador.

**Inputs:**
- Transcript_RRHH
- Transcript_TÉCNICO
- ContextPack_BASE (solo contraste)

---

## Estructura general

```yaml
flags_id: string
generated_at: ISO-8601

summary:
  overall_closure: ok | fail
  overall_authority: baja | media | alta
  overall_verbal_risk: bajo | medio | alto

by_question:
  - question_id: string
    target: rrhh | tecnico
    closure_ok: boolean
    authority_level: baja | media | alta
    verbal_risk: bajo | medio | alto
    over_explanation: boolean
    contradiction_with_context: boolean
    hedging_detected: boolean
    drift_detected: boolean
```

---

## Definición de campos

- **flags_id**: ID único del resultado de análisis.
- **summary**: Agregados descriptivos, no decisionales.
  - **overall_closure**: ok si ≥ 80% de preguntas tienen closure_ok=true; fail en caso contrario.
  - **overall_authority**: moda ponderada de authority_level.
  - **overall_verbal_risk**: máximo observado (conservador). No hay “apto/no apto”.
- **by_question[]**: Por cada pregunta
  - **closure_ok**: true si forced_closure=false; false en caso contrario.
  - **authority_level**: Estimación estructural, no técnica:
    - alta → afirmaciones claras, sin deriva
    - media → alguna vaguedad
    - baja → indecisión, exceso de matiz
  - **verbal_risk**: Riesgo comunicativo:
    - alto → ambigüedad, justificación excesiva, contradicción
    - medio → algún marcador débil
    - bajo → controlado
  - **over_explanation**: true si excede longitud sin aportar cierre; false en caso contrario
  - **contradiction_with_context**: true si contradice hechos/decisiones del ContextPack_BASE; false si es consistente o no comparable
  - **hedging_detected**: true si hay marcadores de duda (“creo”, “depende”, “más o menos”); false si el lenguaje es afirmativo
  - **drift_detected**: true si no responde a la pregunta literal; false si mantiene foco

---

## Reglas globales (críticas)
- ❌ No inferir intención
- ❌ No explicar el flag
- ❌ No recomendar acción
- ✔ Flags binarios o categóricos
- ✔ Basados en evidencia del Transcript

### Prohibiciones explícitas
- ❌ “Buena/mala respuesta”
- ❌ “Le falta nivel”
- ❌ “Debería decir”
Eso pertenece solo a Corrección (Attackers).

---

## Ejemplo mínimo

```yaml
flags_id: fl_001
generated_at: 2026-01-07T18:20:00Z

summary:
  overall_closure: fail
  overall_authority: media
  overall_verbal_risk: medio

by_question:
  - question_id: tec_q3
    target: tecnico
    closure_ok: false
    authority_level: baja
    verbal_risk: alto
    over_explanation: true
    contradiction_with_context: false
    hedging_detected: true
    drift_detected: false
```

---

## Regla de autoridad
Flags describen. Attackers corrigen. Nada más.

Reglas de cálculo (obligatorias)
1️⃣ closure_ok
closure_ok = NOT(forced_closure)
Fuente única: Transcript
Prohibido recalcular por tiempo, palabras o frases desde Flags.
2️⃣ authority_level (por pregunta)
Derivado solo de flags objetivos.
alta
closure_ok=true
hedging_detected=false
drift_detected=false
media
exactamente uno de los anteriores en negativo
baja
dos o más en negativo
3️⃣ verbal_risk (por pregunta)
Agregado determinista.
alto
contradiction_with_context=true
o (over_explanation=true y hedging_detected=true)
medio
exactamente uno de los anteriores
bajo
ninguno
4️⃣ Agregados summary
overall_closure
ok si ≥ 80 % de closure_ok=true
fail en caso contrario
overall_authority
moda ponderada:
alta=3, media=2, baja=1
overall_verbal_risk
máximo observado en by_question
5️⃣ Regla conservadora global
Ante duda → marcar riesgo, nunca neutralizar.

drift_detected = true si:
1) Para closure_rule=binario:
   - answer_text NO es exactamente "Sí" o "No" (ignorando mayúsculas/minúsculas)
2) Para cualquier otro closure_rule:
   - answer_text NO contiene ningún token núcleo (no-stopword) del question_text.

Reglas:
- closure_rule se obtiene del QuestionSet (solo lectura).
- Tokens núcleo (no-stopword) = palabras no vacías del question_text.
- Excluir stopwords: qué, cómo, cuál, cuándo, por qué, el, la, un, una.
- Coincidencia literal (no semántica).
- En caso de duda → true (regla conservadora ya definida).
