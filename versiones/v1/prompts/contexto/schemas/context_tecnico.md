ContextPack_TÉCNICO — Schema v1 (derivado, RO)
Vista técnica / decisión.
Sin narrativa personal.
Origen
Derivado determinista de ContextPack_BASE.
Campos
context_id: string
derived_from: context_id

technical_facts:
  - fact_id: string
    text: string
    source_ref: source_id

technical_decisions:
  - decision_id: string
    statement: string
    scope: system | model | data | infra | proceso
    source_ref: source_id

technical_assumptions:
  - assumption_id: string
    description: string
    evidence_ref: source_id

technical_frictions:
  - friction_id: string
    description: string
    related_decisions: [decision_id]
Reglas de derivación
technical_facts ← facts solo técnicos
technical_decisions ← technical_decisions (1:1)
technical_assumptions ← supuestos técnicos
technical_frictions ← fricciones ligadas a decisiones técnicas
Excluir:
cronología
motivación
historia personal
señales RRHH
Prohibiciones
❌ Explicar decisiones
❌ Completar supuestos
❌ Evaluar calidad técnica
Reglas globales (no negociables)
Ambos schemas son read-only.
Ningún agente escribe ni reinterpreta.
La suma de ambas vistas no añade información al BASE.
El Analizador es el único que contrasta contra ContextPack_BASE.
