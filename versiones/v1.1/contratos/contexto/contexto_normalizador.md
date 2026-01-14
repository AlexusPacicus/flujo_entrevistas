## contexto_normalizador — Contrato v1.1

### Rol
Normalizar un `ContextPack_BASE v1.1` **inválido** para hacerlo **formalmente válido**.

### Autoridad
- Puede:
  - Normalizar la forma de un ContextPack_BASE inválido
- No puede:
  - Crear contenido nuevo
  - Inferir o interpretar

### Input
- `ContextPack_BASE v1.1` en estado `INVALID`

### Operaciones permitidas
- Eliminar claves inválidas
- Eliminar valores inválidos
- Eliminar strings vacíos
- Eliminar elementos no-string en listas
- Normalizar tipos
- `null` → `[]` cuando el schema espera lista

### Operaciones prohibidas
- Crear hechos, decisiones o señales
- Reescribir contenido
- Añadir claves ausentes (salvo `[]` por normalización de tipo)

### Output
- `ContextPack_BASE v1.1`
- YAML válido
