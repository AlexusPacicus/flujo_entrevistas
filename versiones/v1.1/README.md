# Sistema de Flujo de Entrevistas v1.1

## STATUS: FROZEN

Versión: v1.1  
Estado: FROZEN  
Referencia de flujo: `orquestration/flow_v1.1.md`

---

## Descripción

Sistema de orquestación de entrevistas basado en contratos.  
Transforma inputs externos en artefactos contractuales mediante agentes deterministas.  
El flujo está definido en `flow_v1.1.md`.

---

## Estructura

```
contratos/
  agentes/
    Contrato_Base_Agente_v1.1.md
    derivadores/
    entrevista/
    flags/
    mandatos/
    question_set/
  contexto/
    ContextPack_BASE.md
    contexto_emisor.md
    contexto_validador.md
    contexto_normalizador.md

orquestration/
  flow_v1.1.md

prompts/
  contexto/
  derivadores/
  entrevista/
  flags/
  mandatos/
  question_set/
```

---

## Agentes

| Agente | Input | Output |
|--------|-------|--------|
| contexto_emisor | Inputs externos | ContextPack_BASE |
| contexto_validador | ContextPack_BASE | VALID \| INVALID |
| contexto_normalizador | ContextPack_BASE (INVALID) | ContextPack_BASE |
| derivador_rrhh | ContextPack_BASE | ContextPack_RRHH |
| derivador_tecnico | ContextPack_BASE | ContextPack_TECNICO |
| question_set_rrhh | ContextPack_RRHH | QuestionSet_RRHH |
| question_set_tecnico | ContextPack_TECNICO | QuestionSet_TECNICO |
| entrevista_rrhh | QuestionSet_RRHH | Transcript_RRHH |
| entrevista_tecnico | QuestionSet_TECNICO | Transcript_TECNICO |
| analyze_flags | Transcripts | Flags |
| apply_mandates | Flags | Mandatos |

---

## Artefactos

- ContextPack_BASE
- ContextPack_RRHH
- ContextPack_TECNICO
- QuestionSet_RRHH
- QuestionSet_TECNICO
- Transcript_RRHH
- Transcript_TECNICO
- Flags
- Mandatos

---

## Principios Duros

- Contratos tienen autoridad sobre prompts.
- No hay inferencia.
- No hay interpretación.
- No hay enriquecimiento.
- Transformaciones deterministas: mismo input produce mismo output.
- Los agentes no gestionan flujo, errores ni reintentos.
- El planner decide llamadas; las funciones no controlan el flujo.
- Si la información no está completa, se considera inexistente.
- Toda acción no permitida explícitamente está prohibida.

---

## Reglas de Ejecución

- ABORT si contexto_validador devuelve INVALID tras 3 ciclos consecutivos.
- En ABORT: no hay derivación, no se generan QuestionSets, no se realizan entrevistas, no se crean flags.
- RRHH y Técnico corren en paralelo tras VALID.
- El fallo en una rama no bloquea la otra.
- El flow no explica errores.
- No existe retry fuera del normalizador.

---

## Convenciones de Naming

### Agentes/Funciones
- Formato: snake_case
- Patrón: verbo + objeto
- Sin prefijos

### Artefactos
- Formato: PascalCase
- Sufijo claro

### Archivos
- Flow: flow_v1.1.md
- Prompts: mismo nombre que función

---

## Versionado

- Cambios editoriales no semánticos: permitidos en v1.1.
- Cualquier cambio de significado requiere nueva versión.
- Cambios en el grafo, orden o nodos: nueva versión obligatoria.

---

## Referencias

- Flujo: `orquestration/flow_v1.1.md`
- Contrato base de agentes: `contratos/agentes/Contrato_Base_Agente_v1.1.md`
- Schema ContextPack: `contratos/contexto/ContextPack_BASE.md`
