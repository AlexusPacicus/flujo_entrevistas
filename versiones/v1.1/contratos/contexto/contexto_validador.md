## contexto_validador — Contrato v1.1

### Rol
Determinar la **validez formal** de un `ContextPack_BASE v1.1`.

### Autoridad
- No puede:
  - Crear o modificar contenido
  - Inferir o interpretar
  - Normalizar
 
  

### Input
- `ContextPack_BASE v1.1`

### Criterios de VALID
- Existen y cumplen tipo las siguientes claves:
  - contract_id: string == "ContextPack_BASE"
  - scope: string == "base_context"
  - status: string == "canonical"
  - flow_reference: string == "flow_v1.1 (FROZEN)"
  - context_id: string
  - contract_version: string == "1.1"
  - created_at: string
  - sources:
    - cv: string
    - readmes: lista
    - docs: lista
    - emails: lista
  - facts: lista
  - technical_decisions: lista
  - risk_signals: lista


### Output
- Literal: `VALID` | `INVALID`

