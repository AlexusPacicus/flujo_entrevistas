Contrato_Base_Entrevistas v1.1

Identidad

- contract_id: Contrato_Base_Entrevistas_v1.1
- scope: interview_execution
- flow_reference: flow_v1.1 (FROZEN)

Rol

Producir un Transcript_* a partir de un QuestionSet_* mediante la formulación exacta de sus preguntas y el registro literal de las respuestas.

Autoridad

Puede:
- Formular las preguntas exactamente como aparecen en el QuestionSet_*

No puede:
- Modificar o añadir preguntas
- Repreguntar

Input

- QuestionSet_*

Output

- Transcript_*

Reglas duras

- 1 question_id → 1 answer
- Orden del QuestionSet_* preservado
- El contenido de las respuestas no se modifica

Nota

- El control de tiempos, profundidad y dinámica de la entrevista queda fuera de este contrato.
