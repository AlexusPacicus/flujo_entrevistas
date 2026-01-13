contract_id: ContextPack_BASE
scope: base_context
status: canonical
flow_reference: flow_v1.1 (FROZEN)

context_id: string
contract_version: "1.1"
created_at: string

sources:
  cv: string
  readmes: []
  docs: []
  emails: []

facts: []
technical_decisions: []
risk_signals: []

contexto_validador — reglas finales v1.1
Autoridad:
Solo el agente contexto_emisor puede crear o modificar ContextPack_BASE

VALID si:
contract_version == "1.1"
Existen las claves obligatorias:
context_id
contract_version
created_at
sources
Tipos correctos si la clave existe:
strings: string no vacío
listas: lista (puede estar vacía)
Las listas contienen solo strings no vacíos
No hay mutación tras VALID fuera de contexto_normalizador
INVALID si falla cualquiera de las anteriores.
No se permiten:
checks semánticos
checks de origen
autocompletado

contexto_normalizador — Contrato v1.1
Objetivo
Convertir INVALID en VALID
Sin añadir información
Sin inferir
Sin alterar el significado
Operaciones permitidas (únicamente estas):
Eliminar claves inválidas
Eliminar claves desconocidas
Eliminar valores inválidos
Eliminar strings vacíos
Eliminar elementos no-string en listas
Normalizar tipos
Si se espera lista y el valor es null: reemplazar por []
No rellenar
No crear contenido nuevo
No completar listas por ausencia
Operaciones prohibidas:
Crear hechos, riesgos o decisiones
Reescribir textos
Fusionar listas
Deduplicar por semántica
Añadir claves ausentes, salvo [] por normalización de tipo
Inmutabilidad
Tras VALID, normalizador no se ejecuta
Solo actúa cuando validador devuelve INVALID
Resultado esperado
Salida = ContextPack_BASE v1.1
Forma formalmente válida para contexto_validador
El normalizador no garantiza coherencia semántica, solo validez formal
