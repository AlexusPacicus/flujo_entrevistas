# Flujo de Entrevistas

El propósito de este flujo es servir como herramienta de apoyo para entrevistas, además de resultar la base para avanzar hacia un auditor de proyectos.

## INPUTS
- CV
- README(s)
- Docs (0..n)

## REGLAS
- RRHH primero
- Ningún agente aconseja
- Ningún agente decide
- Corrección ≠ explicación

## FLUJO GENERAL
1. Contexto (describe)
2. RRHH (pregunta)
3. Técnico (pregunta)
4. Análisis (clasifica)
5. Corrección (manda)

---
┌───────────────────────────┐
│           INPUTS          │
│  CV · README(s) · Docs    │
└──────────────┬────────────┘
               │
               v
┌───────────────────────────┐
│ (1) AGENTE DE CONTEXTO    │
│       DESCRIPTIVO         │
└──────────────┬────────────┘
               │
      ┌────────┴─────────┐
      │                  │
      v                  v
┌───────────────┐   ┌────────────────┐
│ ContextPack   │   │ ContextPack    │
│     RRHH      │   │   TÉCNICO      │
│ (derivado,RO) │   │ (derivado,RO)  │
└──────┬────────┘   └───────┬────────┘
       │                    │
       v                    v
┌───────────────┐   ┌────────────────┐
│ (2R-G) AGENTE │   │ (2T-G) AGENTE  │
│ PREGUNTAS     │   │ PREGUNTAS      │
│ RRHH          │   │ TÉCNICAS       │
└──────┬────────┘   └───────┬────────┘
       │                    │
       v                    v
┌───────────────┐   ┌────────────────┐
│ (3R) AGENTE   │   │ (3T) AGENTE    │
│ RRHH          │   │ TÉCNICO        │
│ ENTREVISTA    │   │ ENTREVISTA     │
└──────┬────────┘   └───────┬────────┘
       │                    │
       └──────────┬─────────┘
                  v
        ┌────────────────────────┐
        │ (4) AGENTE DE ANÁLISIS │
        │      CLASIFICADOR     │
        │ (contrasta con BASE)  │
        └──────────┬────────────┘
                   v
        ┌────────────────────────┐
        │ (5) AGENTES DE ATAQUE  │
        │       CORRECCIÓN       │
        └────────────────────────┘


## DETALLE DE AGENTES Y FLUJO

### (1) AGENTE DE CONTEXTO — DESCRIPTIVO
- **Output:**
  - ContextPack_BASE
  - ContextPack_RRHH (derivado, solo lectura)
  - ContextPack_TÉCNICO (derivado, solo lectura)

### (2R-G) AGENTE DE PREGUNTAS RRHH
- **Input:** ContextPack_RRHH
- **Output:** QuestionSet_RRHH (cerrado, versionado)

### (2T-G) AGENTE DE PREGUNTAS TÉCNICAS
- **Input:** ContextPack_TÉCNICO
- **Output:** QuestionSet_Técnico (cerrado, versionado)

### (3R) AGENTE RRHH — ENTREVISTA
- **Input:** QuestionSet_RRHH
- **Output:** Transcript_RRHH

### (3T) AGENTE TÉCNICO — ENTREVISTA
- **Input:** QuestionSet_Técnico
- **Output:** Transcript_Técnico

(4) AGENTE DE ANÁLISIS — CLASIFICADOR  
Detecta desviaciones, ambigüedad y falta de cierre.
- **Input:**
  - Transcript_RRHH
  - Transcript_TÉCNICO
  - ContextPack_BASE (solo contraste)
- **Output:** Flags

### (5) AGENTES DE ATAQUE — CORRECCIÓN
- **Input:** Flags
- **Output:** Mandatos

---

## CONTEXTPACKS

### ContextPack_BASE
- Hechos relevantes
- Decisiones técnicas declaradas (citadas)
- Supuestos implícitos
- Fricciones potenciales (descriptivas)
- Cronología profesional
- Señales sensibles (riesgo)

> Ningún agente puede acceder al ContextPack_BASE directamente salvo el Agente de Contexto.

### ContextPack_RRHH (derivado)
**Incluye:**
- Hechos relevantes (resumidos)
- Cronología profesional
- Decisiones no técnicas (cambios, salidas, motivaciones declaradas)
- Supuestos personales implícitos
- Señales de riesgo (vacíos, saltos, ambigüedades)

**Excluye:**
- Detalle técnico profundo
- Métricas finas
- Trade-offs técnicos

**Objetivo:**
- Exponer coherencia, control verbal, riesgo reputacional, estabilidad

### ContextPack_TÉCNICO (derivado)
**Incluye:**
- Hechos técnicos relevantes
- Decisiones técnicas declaradas (citadas)
- Supuestos técnicos implícitos
- Fricciones técnicas (trade-offs, límites, deuda)

**Excluye:**
- Narrativa personal
- Motivación
- Historia emocional

**Objetivo:**
- Exponer criterio, capacidad de decisión, profundidad, control conceptual<<<<<<< HEAD
# flujo_entrevistas
El propósito de este flujo es servir como herramienta de apoyo para entrevistas, además de resultar la base para avanzar hacia un auditor de proyectos.
=======
# Flujo de Entrevistas

## Qué es

Sistema de entrevistas estructuradas basado en agentes.
Separa contexto, preguntas, entrevista, análisis y corrección en fases independientes.

Cada agente tiene un rol contractual:
- **No aconseja**
- **No decide**
- **Corrección ≠ explicación**

## Qué problema resuelve

| Problema | Solución |
|----------|----------|
| Entrevistas sin estructura | Fases secuenciales con contratos definidos |
| Evaluación subjetiva | Flags objetivos derivados del transcript |
| Feedback ambiguo | Mandatos imperativos sin justificación |
| Contexto contaminado | ContextPacks derivados y de solo lectura |

## Flujo

```
┌───────────────────────────┐
│           INPUTS          │
│  CV · README(s) · Docs    │
└──────────────┬────────────┘
               │
               v
┌───────────────────────────┐
│ (1) AGENTE DE CONTEXTO    │
│       DESCRIPTIVO         │
└──────────────┬────────────┘
               │
      ┌────────┴─────────┐
      │                  │
      v                  v
┌───────────────┐   ┌────────────────┐
│ ContextPack   │   │ ContextPack    │
│     RRHH      │   │   TÉCNICO      │
│ (derivado,RO) │   │ (derivado,RO)  │
└──────┬────────┘   └───────┬────────┘
       │                    │
       v                    v
┌───────────────┐   ┌────────────────┐
│ (2R-G) AGENTE │   │ (2T-G) AGENTE  │
│ PREGUNTAS     │   │ PREGUNTAS      │
│ RRHH          │   │ TÉCNICAS       │
└──────┬────────┘   └───────┬────────┘
       │                    │
       v                    v
┌───────────────┐   ┌────────────────┐
│ (3R) AGENTE   │   │ (3T) AGENTE    │
│ RRHH          │   │ TÉCNICO        │
│ ENTREVISTA    │   │ ENTREVISTA     │
└──────┬────────┘   └───────┬────────┘
       │                    │
       └──────────┬─────────┘
                  v
        ┌────────────────────────┐
        │ (4) AGENTE DE ANÁLISIS │
        │      CLASIFICADOR      │
        │ (contrasta con BASE)   │
        └──────────┬─────────────┘
                   v
        ┌────────────────────────┐
        │ (5) AGENTES DE ATAQUE  │
        │       CORRECCIÓN       │
        └────────────────────────┘
```

### Secuencia

1. **Contexto** → describe inputs, genera ContextPacks
2. **RRHH** → pregunta primero (siempre)
3. **Técnico** → pregunta después
4. **Análisis** → clasifica transcripts contra ContextPack_BASE
5. **Corrección** → emite mandatos

## Agentes y responsabilidades

| Agente | Input | Output | Rol |
|--------|-------|--------|-----|
| (1) Contexto Descriptivo | CV, README(s), Docs | ContextPack_BASE, ContextPack_RRHH, ContextPack_TÉCNICO | Describe |
| (2R-G) Preguntas RRHH | ContextPack_RRHH | QuestionSet_RRHH | Genera preguntas |
| (2T-G) Preguntas Técnicas | ContextPack_TÉCNICO | QuestionSet_Técnico | Genera preguntas |
| (3R) RRHH Entrevista | QuestionSet_RRHH | Transcript_RRHH | Registra |
| (3T) Técnico Entrevista | QuestionSet_Técnico | Transcript_Técnico | Registra |
| (4) Análisis Clasificador | Transcripts + ContextPack_BASE | Flags | Clasifica |
| (5) Ataque Corrección | Flags | Mandatos | Ordena |

### ContextPacks

| Pack | Incluye | Excluye |
|------|---------|---------|
| BASE | Hechos, decisiones técnicas citadas, supuestos implícitos, fricciones, cronología, señales de riesgo | — |
| RRHH (derivado, RO) | Hechos resumidos, cronología, decisiones no técnicas, supuestos personales, señales de riesgo | Detalle técnico, métricas, trade-offs técnicos |
| TÉCNICO (derivado, RO) | Hechos técnicos, decisiones técnicas citadas, supuestos técnicos, fricciones técnicas | Narrativa personal, motivación, historia emocional |

> El ContextPack_BASE solo es accesible por el Agente de Contexto y el Agente de Análisis (para contraste).

## Contratos clave

### Flags describen

Señales objetivas derivadas del transcript. No explican, no aconsejan, no deciden.

```yaml
by_question:
  - question_id: string
    closure_ok: boolean
    authority_level: baja | media | alta
    verbal_risk: bajo | medio | alto
    over_explanation: boolean
    contradiction_with_context: boolean
    hedging_detected: boolean
    drift_detected: boolean
```

### Mandatos ordenan

Órdenes de corrección derivadas de flags. Imperativas, una frase, sin justificación.

```yaml
mandates:
  - mandate_id: string
    question_id: string
    source_flag: string
    action: string          # Orden imperativa, 1 frase
    constraint: string      # Heredado del QuestionSet
    priority: alta | media | baja
```

### Regla de autoridad

| Artefacto | Función | Prohibido |
|-----------|---------|-----------|
| Transcript | Evidencia cruda | Interpretar, editar, resumir |
| Flags | Descripción objetiva | Explicar, aconsejar, evaluar nivel |
| Mandatos | Orden imperativa | Justificar, sugerir, usar "deberías" |

## Ejemplo de ejecución

Referencia: `runs/tecnico/`

### Transcript inicial → Flags → Mandatos → Transcript corregido

```
transcript.yaml          # Respuestas originales
    ↓
flags_v1.yaml            # Análisis: drift_detected en 4 preguntas
    ↓
mandates_v1.yaml         # Mandatos: "Responde al objeto literal de la pregunta"
    ↓
transcript_v2.yaml       # Respuestas corregidas (solo preguntas afectadas)
    ↓
flags_v2.yaml            # Fuente de verdad final
```

### Notas sobre los artefactos

| Artefacto | Descripción |
|-----------|-------------|
| `transcript_v2.yaml` | **Parcial por diseño.** Solo contiene preguntas con mandatos. No reemplaza el transcript original. |
| `flags_v2.yaml` | **Fuente de verdad final.** Refleja el estado tras corrección. |

### Ejemplo: Mandato → Corrección

**Antes** (`transcript.yaml`):
```yaml
question_text: "¿Mantendrías el diseño del sistema específicamente para usuarios españoles?"
answer_text: "Para responder a esto habría que considerar varios factores. En primer lugar..."
```

**Mandato** (`mandates_v1.yaml`):
```yaml
source_flag: drift_detected
action: Responde al objeto literal de la pregunta.
constraint: binario
```

**Después** (`transcript_v2.yaml`):
```yaml
answer_text: "Sí"
```

## Reglas del sistema

- RRHH siempre primero
- Ningún agente aconseja
- Ningún agente decide
- Corrección ≠ explicación
- Flags describen, Mandatos ordenan
- El transcript es evidencia, no juicio
- Si se toca el texto del transcript, el sistema miente

## Estructura del repositorio

```
├── agentes/           # Contextos de agentes
├── data/              # Inputs (CV, docs)
├── prompts/           # Prompts de entrevista
├── runs/              # Ejecuciones (transcripts, flags, mandatos)
│   └── tecnico/       # Ejemplo técnico completo
└── schemas/           # Contratos de datos
```

## Schemas

| Schema | Descripción |
|--------|-------------|
| `context_base.md` | Estructura del ContextPack_BASE |
| `context_rrhh.md` | Estructura del ContextPack_RRHH |
| `context_tecnico.md` | Estructura del ContextPack_TÉCNICO |
| `question_set.md` | Estructura del QuestionSet |
| `transcript.md` | Estructura del Transcript |
| `flags.md` | Estructura de Flags |
| `mandatos.md` | Estructura de Mandatos |
>>>>>>> 39f55e7 (Initial interview flow prototype with example technical run)
