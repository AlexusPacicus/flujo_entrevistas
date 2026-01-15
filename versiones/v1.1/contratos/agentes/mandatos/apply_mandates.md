Contrato_Apply_Mandates v1.1

Identidad

- contract_id: Contrato_Apply_Mandates
- scope: mandate_application (se mantiene por compatibilidad con el flow)
- flow_reference: flow_v1.1 (FROZEN)
- contract_version: "1.1"

Rol

Aplicar mandatos formales a partir de flags, mediante mapeo determinista y no inferencial.

Un Mandato es una instrucción formal derivada 1:1 de un Flag, sin evaluación, prioridad ni interpretación.

No puede crear Mandatos sin un Flag de origen explícito.

Input

- Flags

Output

- Mandatos
