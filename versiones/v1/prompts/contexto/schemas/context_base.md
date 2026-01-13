# ContextPack_BASE_v1.md

## 1. Definición Formal
Este documento constituye el contrato semántico ejecutable de `ContextPack_BASE` versión 1. Define de manera unívoca los criterios de validez, estructura y gobernanza de datos para la consolidación de hechos técnicos y profesionales.

## 2. Ámbito de Aplicación (Scope)
Todo artefacto conforme a este contrato debe incluir obligatoriamente el bloque de alcance. La ausencia de este bloque o de cualquiera de sus campos implica estado **INVALID**.
- **scope**:
  - **intent**: presentation | audit
  - **coverage**: urls

## 3. Especificación del Schema
El artefacto debe seguir estrictamente la estructura YAML definida a continuación:

```yaml
context_id: string
created_at: ISO-8601
scope:
  intent: presentation | audit
  coverage: urls
sources:
  - source_id: string
    type: cv | readme | doc
    reference: string
facts:
  - fact_id: string
    text: string
    source_ref: source_id
technical_decisions:
  - decision_id: string
    statement: string
    scope: system | model | data | infra | proceso
    source_ref: source_id
assumptions:
  - assumption_id: string
    description: string
    evidence_ref: source_id
frictions:
  - friction_id: string
    description: string
    related_decisions: [decision_id]
timeline:
  - period: string
    role: string
    context: string
    source_ref: source_id
risk_signals:
  - signal_id: string
    type: gap | jump | ambiguity | dependency
    description: string
    source_ref: source_id
```

## 4. Gobernanza de Fuentes
Se establecen restricciones estrictas de origen de datos por sección:
1. **facts**: Exclusivamente derivados de fuentes `type: cv`.
2. **technical_decisions**: Exclusivamente derivados de fuentes `type: readme`.
3. **assumptions**: Derivados únicamente de fuentes `type: cv` o `type: readme`.
4. **risk_signals**: Limitado exclusivamente a fuentes `type: cv` y `type: doc/email`. Queda prohibido el uso de fuentes `type: readme` para esta sección.
5. **Prohibición**: Las fuentes `type: doc/email` tienen prohibido alimentar las secciones `facts`, `technical_decisions` y `assumptions`.

## 5. Reglas de Validez Semántica
1. **facts**: Hechos verificables. Se prohíben datos de contacto, información de relleno o síntesis subjetiva.
2. **technical_decisions**: Declaraciones explícitas. Se prohíbe la reformulación técnica o la inferencia de intención.
3. **assumptions**: Solo permitidas si la información no existe de forma explícita en `facts` o `technical_decisions`. Formato obligatorio: "Se asume [X] porque [Y] aparece en [Z]".
4. **frictions**: Solo pueden declararse a partir de trade-offs explícitos entre elementos de `technical_decisions`.
5. **risk_signals**: Limitadas a la descripción de huecos (gaps) profesionales, saltos cronológicos, ambigüedades o dependencias críticas del candidato. Queda prohibido:
   - Derivar señales de riesgo desde la detección de vacíos genérica en las fuentes.
   - Convertir limitaciones técnicas declaradas en señales de riesgo.
6. **timeline**: Solo periodos temporales escritos literalmente en la fuente.

## 6. Reglas de Completitud Mínima
1. El artefacto debe contener todas las secciones definidas en el schema.
2. Las secciones sin datos detectados deben inicializarse como listas vacías `[]`.
3. No se permite la omisión de metadatos obligatorios ni del bloque `scope`.

## 7. Reglas de Abortado Explícito (INVALID)
Un ContextPack_BASE será declarado **INVALID** si presenta cualquiera de las siguientes condiciones:
1. Incumplimiento de la estructura YAML o del schema de tipos.
2. Ausencia del bloque `scope` o campos `intent`/`coverage` incompletos.
3. Presencia de información no contenida en las fuentes proporcionadas (inferencia detectada).
4. Violación de las reglas de gobernanza de fuentes (Sección 4).
5. Inclusión de lenguaje evaluativo, motivacional o recomendaciones.
6. Secciones con lógica de integridad fallida:
   - `facts[]` vacío.
   - `technical_decisions[]` con datos y `frictions[]` vacío.
   - `assumptions[]` con datos y `technical_decisions[]` vacío.
   - `facts[]`, `technical_decisions[]`, `frictions[]` y `assumptions[]` simultáneamente vacíos.

## 8. Regla de No-Deducción
Toda información no presente de forma explícita en las fuentes autorizadas se considera inexistente. Queda estrictamente prohibida la deducción lógica, la generalización o la mejora narrativa. Cualquier rastro de inferencia detectada por el validador implica estado **INVALID**.

## 9. Regla de Inmutabilidad
Una vez emitido un ContextPack_BASE bajo el estado **VALID**, su contenido factual es inmutable. Cualquier corrección requiere la invalidación del artefacto actual y la generación de una nueva versión con un `context_id` único. Solo el Agente de Contexto posee autoridad de escritura; los demás componentes operan exclusivamente en modo de lectura.
