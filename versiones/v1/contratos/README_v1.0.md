# Flujo de Entrevistas — Contrato v1.0

## Propósito

Define las reglas de ejecución, agentes involucrados y condiciones de aborto para el sistema automatizado de entrevistas. Actúa como fuente de verdad contractual para todos los prompts y schemas del proyecto.

## Alcance

Gobierna los siguientes directorios y artefactos:

- `/prompts/` — definiciones de agentes y schemas
- `/orquestration/flow_v1.MD` — diagrama de flujo
- `/runs/` — salidas generadas (solo lectura)
- `/data/` — fuentes de contexto
- `/contratos/` — documentación contractual

## Fases incluidas

1. **Contexto** — Generación del ContextPack consolidado
2. **Derivación** — Filtrado para entrevistas RRHH y técnica
3. **Preguntas** — Generación de question sets literales
4. **Entrevista** — Ejecución de entrevistas por tipo
5. **Análisis** — Detección de desviaciones y flags
6. **Corrección** — Emisión de mandatos correctivos

## Limitaciones

- El ContextPack base no distingue información factual de analítica.
- No existe enforcement automático de versiones entre agentes.
- No hay validación semántica cruzada entre transcripts y question sets.
- Los tipos de fuentes no están tipados explícitamente.

## Estado y uso

- **Estado**: activo
- **Versión de schemas**: 1.0
- **Función**: baseline operativo para ejecución de entrevistas automatizadas

Todo agente debe declarar `contract_version: 1.0`. Si existe mismatch de versión, output inválido o ausencia de artefactos obligatorios, el flujo aborta.

## Próxima versión

- Control de versiones por schema
- División del ContextPack en capas factual y analítica
- Trazabilidad obligatoria en flags y mandates
- Alineación de enums `closure_rule` / `constraint`
