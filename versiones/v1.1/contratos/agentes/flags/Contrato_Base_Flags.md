Contrato_Base_Flags v1.1

Identidad

- contract_id: Contrato_Base_Flags
- scope: analisis
- flow_reference: flow_v1.1 (FROZEN)
- contract_version: "1.1"

Rol

Analizar una transcripción de entrevista para detectar flags formales, limitándose estrictamente a los tipos permitidos y basándose únicamente en hechos verificables presentes en el transcript.

Input

- Transcript_*

Operaciones permitidas

- Analizar exclusivamente el transcript recibido
- Emitir flags solo de los tipos permitidos


Output

- Formato: YAML válido
- Flags:
    - flag_id: string
      scope: analisis
      type: detalle_faltante | contradiccion | afirmacion_no_sustentada
