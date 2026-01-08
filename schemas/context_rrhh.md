# ContextPack_RRHH — Schema v1 (derivado, RO)

Vista narrativa / riesgo. No técnica. No interpretativa.

**Origen:**
Derivado determinista de ContextPack_BASE.

---

## Campos

```yaml
context_id: string
derived_from: context_id

facts_summary:
  - fact_id: string
    text: string
    source_ref: source_id

timeline:
  - period: string
    role: string
    context: string
    source_ref: source_id

non_technical_decisions:
  - decision_id: string
    statement: string
    source_ref: source_id

personal_assumptions:
  - assumption_id: string
    description: string
    evidence_ref: source_id

risk_signals:
  - signal_id: string
    type: gap | jump | ambiguity | dependency
    description: string
    source_ref: source_id
```

---

## Reglas de derivación
- facts_summary ← facts (resumen literal, sin reescritura)
- non_technical_decisions ← solo decisiones fuera de scope=system|model|data|infra
- personal_assumptions ← supuestos no técnicos
- Excluir:
  - métricas
  - trade-offs técnicos
  - deuda técnica
  - arquitectura

---

## Prohibiciones
- ❌ Añadir contexto
- ❌ Inferir motivaciones
- ❌ Etiquetar “bueno/malo”