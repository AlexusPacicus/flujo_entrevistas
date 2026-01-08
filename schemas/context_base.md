# ContextPack_BASE — Schema v1 (contractual)

Núcleo factual único. Fuente de verdad. Describe, no interpreta.

---

## 1️⃣ Metadatos (obligatorios)

```yaml
context_id: string
created_at: ISO-8601
sources:
  - source_id: string
    type: cv | readme | doc
    reference: string   # nombre de archivo / sección / URL
```

---

## 2️⃣ Hechos relevantes (facts[])
Hechos verificables, no opiniones.

```yaml
facts:
  - fact_id: string
    text: string
    source_ref: source_id
```

---

## 3️⃣ Decisiones técnicas declaradas (technical_decisions[])
Declaraciones explícitas del candidato. Citas obligatorias.

```yaml
technical_decisions:
  - decision_id: string
    statement: string        # cita literal o casi literal
    scope: system | model | data | infra | proceso
    source_ref: source_id
```

Reglas:
- Si no está escrito, no existe.
- No se completa ni se “mejora”.

---

## 4️⃣ Supuestos implícitos (assumptions[])
Supuestos detectados, no validados.

```yaml
assumptions:
  - assumption_id: string
    description: string
    evidence_ref: source_id
```

Formato obligatorio: “Se asume X porque Y aparece en Z”

---

## 5️⃣ Fricciones potenciales (frictions[])
Tensiones descriptivas: trade-offs, límites, deuda sin juicio.

```yaml
frictions:
  - friction_id: string
    description: string
    related_decisions: [decision_id]
```

Ejemplos válidos:
- “Optimiza recall sobre precisión”
- “Dependencia de dataset pequeño”
- “Reglas heurísticas acopladas al dominio”

---

## 6️⃣ Cronología profesional (timeline[])
Línea temporal seca. Sin narrativa.

```yaml
timeline:
  - period: string          # ej. 2023–2024
    role: string
    context: string         # empresa / proyecto / estudio
    source_ref: source_id
```

---

## 7️⃣ Señales sensibles / riesgo (risk_signals[])
No juicios, solo marcas de posible fricción RRHH.

```yaml
risk_signals:
  - signal_id: string
    type: gap | jump | ambiguity | dependency
    description: string
    source_ref: source_id
```

Ejemplos válidos:
- “Salto temporal no explicado”
- “Cambio brusco de dominio”
- “Dependencia fuerte de una persona/herramienta”

---

## 8️⃣ Prohibiciones explícitas (no negociables)
- ❌ Recomendaciones
- ❌ Evaluaciones
- ❌ Motivaciones
- ❌ Reescritura del discurso
- ❌ “Debería”, “convendría”, “es mejor”

---

## 9️⃣ Regla de autoridad
Solo el Agente de Contexto puede escribir o modificar este schema; todos los demás agentes pueden leer `ContextPack_BASE` exclusivamente en modo de solo lectura, incluido su uso para contraste y verificación frente a otros artefactos.
