Contrato_Derivador_RRHH v1.1

Identidad

- contract_id: Contrato_Derivador_RRHH
- scope: derivation_rrhh
- flow_reference: flow_v1.1 (FROZEN)
- contract_version: "1.1"
- status: canonical

Rol

Derivar contractualmente un ContextPack_BASE v1.1 en un ContextPack_RRHH v1.1 mediante la selección y copia literal de campos, cumpliendo estrictamente:
- Las reglas establecidas en los contratos base heredados.
- Las reglas explícitamente definidas en este contrato.

Input

- ContextPack_BASE v1.1

Output

- ContextPack_RRHH v1.1
  - contract_id: "ContextPack_RRHH"
  - scope: "rrhh_context"
  - flow_reference: "flow_v1.1 (FROZEN)"
  - context_id: string
  - contract_version: "1.1"
  - facts: list
  - risk_signals: list

Reglas de derivación

Campos incluidos (1:1):
- context_id
- facts
- risk_signals

Campos excluidos:
- technical_decisions
- sources
- Cualquier campo no listado como incluido

Campos constantes (no derivados del input):
- contract_id = "ContextPack_RRHH"
- scope = "rrhh_context"
- flow_reference = "flow_v1.1 (FROZEN)"
- contract_version = "1.1"

Regla dura:
- El orden del output es exactamente el definido en el schema de salida.
