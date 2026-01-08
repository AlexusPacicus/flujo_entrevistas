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
- Exponer criterio, capacidad de decisión, profundidad, control conceptual