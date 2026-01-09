ORQUESTADOR — CONTROL DE FLUJO (NO AGENTE)

OBJETIVO
Controlar la ejecución de agentes sin interpretar contenido.

# Flow v1 — Control de ejecución

START

CONTEXT_EMIT
- prompt: contexto_emisor

CONTEXT_VALIDATE
- prompt: contexto_validador
- if VALID → DERIVE_RRHH
- if INVALID → CONTEXT_NORMALIZE

CONTEXT_NORMALIZE
- prompt: contexto_normalizador
- then → CONTEXT_VALIDATE
- max_cycles: 3
- if still INVALID → ABORT

DERIVE_RRHH
- prompt: derivador_rrhh
- requires: ContextPack_BASE = VALID

DERIVE_TECNICO
- prompt: derivador_tecnico
- requires: ContextPack_BASE = VALID

ANALYZE_FLAGS
- prompt: flags

APPLY_MANDATES
- prompt: mandates

END

ABORT
- reason: ContextPack_BASE non conformant


REGLAS ABSOLUTAS

REGLA 1 — AUTORIDAD
Solo el agente `contexto_emisor` puede crear o modificar `ContextPack_BASE`.

REGLA 2 — BLOQUEO
Si `ContextPack_BASE` no es VALID, está PROHIBIDO ejecutar cualquier agente derivado.

REGLA 3 — VALIDACIÓN OBLIGATORIA
Todo `ContextPack_BASE` DEBE pasar por `contexto_validador`.
No existe BASE “provisional”.

REGLA 4 — CICLO DE CORRECCIÓN
Si el resultado del validador es INVALID:
- Ejecutar `contexto_normalizador`
- Revalidar
- Repetir el ciclo como máximo 3 veces

REGLA 5 — ABORTO
Si tras 3 ciclos sigue siendo INVALID:
- Abort execution
- No derivar RRHH ni Técnico
- Marcar BASE como no conforme

REGLA 6 — DERIVACIÓN
Solo si el validador devuelve EXACTAMENTE `VALID`:
- Ejecutar `derivador_rrhh`
- Ejecutar `derivador_tecnico`

REGLA 7 — INMUTABILIDAD
Los agentes derivados son read-only.
No pueden:
- Escribir BASE
- Corregir BASE
- Completar BASE

REGLA 8 — SILENCIO
El orquestador no explica errores.
El orquestador no propone correcciones.
El orquestador no interpreta contenido.
