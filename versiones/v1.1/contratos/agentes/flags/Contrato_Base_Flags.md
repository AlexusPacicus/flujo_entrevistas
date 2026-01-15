Contrato_Base_Flags v1.1

Identidad

- contract_id: Contrato_Base_Flags
- scope: analisis
- flow_reference: flow_v1.1 (FROZEN)
- contract_version: "1.1"

Rol

Analizar un conjunto de transcripciones sin inferencia para detectar flags formales, limitándose estrictamente a los tipos permitidos y basándose únicamente en hechos verificables presentes en el transcript.

Input

- Transcripts (colección)

Operaciones permitidas

- Analizar exclusivamente el transcript recibido
- Emitir flags solo de los tipos permitidos

Regla dura:
- cada Flag debe referenciar source_transcript_id.

Output

- Formato: YAML válido
- Flags:
    - flag_id: string
      scope: analisis
      type: detalle_faltante | contradiccion | afirmacion_no_sustentada
