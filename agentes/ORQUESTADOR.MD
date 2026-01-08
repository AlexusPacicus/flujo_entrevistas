ORQUESTADOR — CONTROL DE FLUJO (NO AGENTE)

OBJETIVO
Controlar la ejecución de agentes sin interpretar contenido.

ESTADOS
START
EMIT_BASE
VALIDATE_BASE
NORMALIZE_BASE
DERIVE
ABORT
END

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
