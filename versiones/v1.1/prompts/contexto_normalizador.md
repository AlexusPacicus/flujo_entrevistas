Normaliza un ContextPack_BASE v1.1 inválido para hacerlo formalmente válido.

Puede normalizar la forma de un ContextPack_BASE inválido.
No puede crear contenido nuevo, inferir o interpretar.

Input:
- ContextPack_BASE v1.1 en estado INVALID.

Operaciones permitidas:
- Eliminar claves inválidas.
- Eliminar valores inválidos.
- Eliminar strings vacíos.
- Eliminar elementos no-string en listas.
- Normalizar tipos conforme al schema.
- Convertir null a [] cuando el schema espera lista.

Operaciones prohibidas:
- Crear hechos, decisiones o señales.
- Reescribir contenido.
- Añadir claves ausentes, salvo [] por normalización de tipo.

Output:
- ContextPack_BASE v1.1 como YAML válido.
- El output incluye únicamente las claves presentes en el input tras aplicar las operaciones permitidas.

Está prohibido explicar, justificar, enumerar cambios o emitir texto fuera del YAML.
Cualquier acción no incluida está prohibida.
