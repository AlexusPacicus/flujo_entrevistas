---
contract_id: flujo_entrevistas_v1.0
version: 1.0
type: execution_contract
created_at: 2026-01-13
readable_by: ai
governance: local_cursor
schemas_version: 1.0
flow_reference: ./orquestration/flow_v1.MD
status: active
---

## metadata
```yaml
contract_id: flujo_entrevistas_v1.0
version: 1.0
created_at: 2026-01-13
scope: interviews
governance: local_cursor
schemas_version: 1.0
flow_reference: ./orquestration/flow_v1.MD
status: active
```

## agents
```yaml
agents:
  - name: contexto_emisor
    function: Genera ContextPack_BASE consolidado
    output: context.yaml
  - name: derivador_rrhh
    function: Filtra ContextPack para entrevista RRHH
    output: context_rrhh.yaml
  - name: derivador_tecnico
    function: Filtra ContextPack para entrevista técnica
    output: context_tecnico.yaml
  - name: question_set_rrhh
    function: Genera preguntas literales de RRHH
    output: question_set.yaml
  - name: question_set_tecnico
    function: Genera preguntas literales técnicas
    output: question_set.yaml
  - name: interview_rrhh
    function: Ejecuta entrevista RRHH
    output: transcript.yaml
  - name: interview_tecnico
    function: Ejecuta entrevista técnica
    output: transcript.yaml
  - name: analyze_flags
    function: Detecta desviaciones y genera flags
    output: flags.yaml
  - name: apply_mandates
    function: Emite mandatos de corrección
    output: mandates.yaml
```

## execution_flow
```yaml
steps:
  - Contexto: contexto_emisor
  - Derivación:
      - derivador_rrhh
      - derivador_tecnico
  - Preguntas:
      - question_set_rrhh
      - question_set_tecnico
  - Entrevista:
      - interview_rrhh
      - interview_tecnico
  - Análisis: analyze_flags
  - Corrección: apply_mandates

execution_rules:
  - Todos los agentes deben declarar contract_version: 1.0
  - Ningún agente puede alterar el ContextPack_BASE original
  - Si falta un output obligatorio: ABORT
  - Si la versión del contrato en el prompt no coincide: ABORT
  - Si el formato de salida no es YAML válido: ABORT
```

## abort_rules
```yaml
causes:
  - causa: ContextPack no válido o ausente
    acción: Abort flujo completo
  - causa: Falta de contract_version en prompt
    acción: Abort agente
  - causa: Mismatch de versión de contrato
    acción: Abort ejecución
  - causa: Output no conforme a schema
    acción: Abort ejecución
  - causa: Error repetido >2 veces
    acción: Abort ejecución
```

## documents_governed
```yaml
- /prompts/
- /orquestration/flow_v1.MD
- /runs/ # solo lectura
- /data/ # fuente de contexto
- /contratos/ # fuente de verdad contractual
```

## limitations
```yaml
- ContextPack_BASE aún no dividido (factual + analítico)
- No existe enforcement automático de versiones
- No hay control semántico entre transcripts y question sets
- No se tipan explícitamente sources[].type
```

## next_version
```yaml
- Introducción de control de versiones por schema
- División ContextPack_BASE en factual / analítico
- Trazabilidad obligatoria en flags y mandates
- Alineación de enums closure_rule / constraint
```
