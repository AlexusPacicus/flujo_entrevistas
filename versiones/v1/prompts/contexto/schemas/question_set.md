# QuestionSet — Schema v1.1 (contractual)

Conjunto cerrado y versionado de preguntas.
Define la presión. No evalúa, no entrevista, no se adapta.

## Propósito
- Fijar qué se pregunta, en qué orden y con qué exigencia.
- Permitir comparabilidad entre sesiones.
- Evitar improvisación, suavizado o coaching encubierto.

**Origen:**
Derivado de:
- ContextPack_RRHH o
- ContextPack_TÉCNICO
Generado offline por el agente generador correspondiente.

---

## Estructura general

```yaml
questionset_id: string
version: string
target: rrhh | tecnico
generated_from: context_id
difficulty_profile: bajo | medio | alto

questions:
  - question_id: string
    text: string
    target: rrhh | tecnico
    type: definicion | decision | tradeoff | limite | fallo
    objective: string
    closure_rule: 1_frase | 2_frases | binario
    max_time_sec: integer
    difficulty: bajo | medio | alto
```

---

## Definición de campos (uno a uno)

- **questionset_id**: Identificador único del set. Ej: qs_rrhh_v1_baseline
- **version**: Versión semántica del set. Ej: v1.0, v1.1
  - Cambia solo si cambia una pregunta, su orden o su regla de cierre.
- **target**: rrhh → entrevista de riesgo / narrativa; tecnico → entrevista de decisión / criterio
- **difficulty_profile**: Nivel global de exigencia del set. No afecta al contenido, solo a selección y orden durante la generación offline del QuestionSet. No tiene efecto durante la ejecución de la entrevista.

### Campos por pregunta
- **question_id**: ID estable. Nunca se reutiliza.
- **text**: Pregunta literal. Debe poder leerse sin contexto adicional.
  - Prohibido: subpreguntas, aclaraciones, ejemplos
- **type**: Clasificación estructural de la pregunta:
  - definicion → obliga a precisión
  - decision → obliga a tomar postura
  - tradeoff → expone coste/beneficio
  - limite → expone frontera del sistema
  - fallo → expone error o debilidad
- **objective**: Qué pretende exponer en abstracto. No es una pista para responder.
- **closure_rule**: Regla no negociable de cierre:
  - 1_frase
  - 2_frases
  - binario (sí / no + una frase)
  - El entrevistador corta si no se cumple.
- **max_time_sec**: Tiempo máximo permitido antes de corte. Ej: RRHH: 30–45 s; Técnico: 20–30 s
- **difficulty**: Dificultad local de la pregunta. Permite mezclar presión dentro del set.

---

## Reglas globales (críticas)
- ❌ Ninguna pregunta sugiere respuesta.
- ❌ Ninguna pregunta evalúa.
- ❌ Ninguna pregunta se adapta a la respuesta anterior.
- ❌ El orden no cambia durante la entrevista.
- ✔ El set es cerrado una vez generado.
- ✔ difficulty_profile solo aplica en generación offline. Durante la entrevista no se usa ni modifica nada.

### Prohibiciones explícitas
- ❌ “Explícame”
- ❌ “¿Por qué crees que…?”
- ❌ “Cuéntame”
- ❌ “Desde tu punto de vista”
Eso abre narrativa. Aquí se cierra.

---

## Ejemplo mínimo (RRHH)

```yaml
questionset_id: qs_rrhh_v1
version: v1.0
target: rrhh
difficulty_profile: medio

questions:
  - question_id: rrhh_q1
    text: "¿Qué decisión profesional reciente asumirías hoy como error?"
    target: rrhh
    type: fallo
    objective: "Exponer asunción de responsabilidad"
    closure_rule: 1_frase
    max_time_sec: 30
    difficulty: medio
```

---

## Regla de autoridad
El QuestionSet define la entrevista, no el entrevistador. El entrevistador solo ejecuta.

**Estado**
Con este schema:
- ✔ RRHH y Técnico usan el mismo contrato
- ✔ El flujo queda totalmente definido
- ✔ Ya puedes pasar a Transcript sin ambigüedades