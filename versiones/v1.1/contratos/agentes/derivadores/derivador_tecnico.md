Contrato_Derivador_TECNICO v1.1

Identidad

- contract_id: Contrato_Derivador_TECNICO
- scope: derivation_tecnico
- flow_reference: flow_v1.1 (FROZEN)
- contract_version: "1.1"
- status: canonical

Rol

Derivar contractualmente un ContextPack_BASE v1.1 en un ContextPack_TECNICO v1.1 mediante la selección y copia literal de campos, cumpliendo estrictamente:
- Las reglas establecidas en los contratos base heredados.
- Las reglas explícitamente definidas en este contrato.

Input

- ContextPack_BASE v1.1

Output

- ContextPack_TECNICO v1.1
  - contract_id: "ContextPack_TECNICO"
  - scope: "technical_context"
  - flow_reference: "flow_v1.1 (FROZEN)"
  - context_id: string
  - contract_version: "1.1"
  - technical_decisions: list
  - facts: list

Reglas de derivación

Campos incluidos (1:1):
- context_id
- technical_decisions
- facts

Campos excluidos:
- risk_signals
- sources
- Cualquier campo no listado como incluido

Campos constantes (no derivados del input):
- contract_id = "ContextPack_TECNICO"
- scope = "technical_context"
- flow_reference = "flow_v1.1 (FROZEN)"
- contract_version = "1.1"

Regla dura:
- El orden del output es exactamente el definido en el schema de salida.
