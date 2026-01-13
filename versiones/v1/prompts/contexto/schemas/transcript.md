# Transcript — Schema v1 (contractual)

Registro crudo de la entrevista.
No interpreta, no evalúa, no corrige.
Sirve para medir discurso, no contenido.

## Propósito
- Capturar exactamente qué se preguntó y qué se respondió.
- Permitir métricas objetivas (tiempo, longitud, cierre).
- Alimentar al Analizador sin contaminarlo.

**Origen:**
Generado por:
- Agente RRHH — Entrevista
- Agente Técnico — Entrevista
A partir de un QuestionSet cerrado.

---

## Estructura general

```yaml
transcript_id: string
questionset_id: string
target: rrhh | tecnico
started_at: ISO-8601
ended_at: ISO-8601

entries:
  - entry_id: string
    question_id: string
    question_text: string
    answer_text: string
    word_count: integer
    time_sec: integer
    forced_closure: boolean
```

---

## Definición de campos

- **transcript_id**: Identificador único de la sesión.
- **questionset_id**: Referencia directa al QuestionSet usado. Permite reproducibilidad.
- **target**: rrhh o tecnico. Nunca mixto.
- **started_at / ended_at**: Marcas temporales. No se infiere duración: se calcula.
- **entries[]**: Por cada pregunta respondida
  - **entry_id**: ID único por pregunta respondida.
  - **question_id**: Debe existir en el QuestionSet. Si no existe → error de contrato.
  - **question_text**: Texto literal de la pregunta. Evita dependencia externa al QuestionSet.
  - **answer_text**: Respuesta sin editar. Incluye muletillas, cortes y repeticiones.
  - **word_count**: Conteo literal de palabras. No estimado.
  - **time_sec**: Tiempo real de respuesta en segundos. Desde fin de pregunta hasta cierre/corte.
  - **forced_closure**: true → el entrevistador cortó por regla; false → el candidato cerró a tiempo

---

## Reglas globales (no negociables)
- ❌ No resúmenes
- ❌ No etiquetas
- ❌ No correcciones
- ❌ No normalización del texto
- ✔ El transcript es evidencia, no juicio

### Prohibiciones explícitas
- ❌ Añadir “mejoras” a la respuesta
- ❌ Quitar repeticiones
- ❌ Limpiar lenguaje
- ❌ Interpretar intención
Si se toca el texto, el sistema miente.

---

## Ejemplo mínimo

```yaml
transcript_id: tr_tecnico_001
questionset_id: qs_tecnico_v1
target: tecnico
started_at: 2026-01-07T18:00:00Z
ended_at: 2026-01-07T18:12:00Z

entries:
  - entry_id: e1
    question_id: tec_q3
    question_text: "¿Qué señal eliminarías primero si el modelo degrada?"
    answer_text: "Eliminaría primero la señal X porque introduce ruido..."
    word_count: 14
    time_sec: 18
    forced_closure: false
```

---

## Regla de autoridad
El Transcript no puede cambiarse una vez cerrado. Si hay error, se crea otro transcript.