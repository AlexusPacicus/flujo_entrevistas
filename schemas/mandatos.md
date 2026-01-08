Propósito
Transformar Flags en órdenes de corrección ejecutables.
No explica. No evalúa. No justifica.
Origen
Agente de Ataque — Corrección.
Input
Flags v1
Estructura
mandates_id: string
generated_at: ISO-8601
flags_id: string

mandates:
  - mandate_id: string
    question_id: string
    target: rrhh | tecnico
    source_flag: string
    action: string
    constraint: string
    priority: alta | media | baja
Definición de campos (obligatorios)
mandates_id
ID único del bloque de mandatos.
generated_at
Timestamp ISO-8601.
flags_id
Referencia directa al Flags que origina los mandatos.
mandates[]
Por cada corrección:
mandate_id
ID único del mandato.
question_id
Debe existir en Flags.by_question.
target
rrhh o tecnico. Debe coincidir con Flags.
source_flag
Flag que dispara el mandato.
Valores permitidos:
closure_ok
authority_level
verbal_risk
drift_detected
action
Orden imperativa, concreta, 1 frase.
Sin explicación.
    constraint
    Tipo de cierre heredado del QuestionSet original.
    El mandato NO puede modificar el tipo de cierre, solo reforzar su cumplimiento.
    Valores permitidos: binario, 1_frase, ≤20s, ≤30s.
    priority
    alta | media | baja.
Reglas de generación (críticas)
1 flag relevante → 1 mandato
- El campo `constraint` DEBE heredar el `closure_rule` definido en el QuestionSet para la misma `question_id`.
- El mandato NO puede cambiar un cierre binario a 1_frase ni viceversa.
Mandatos SOLO para:
closure_ok=false
authority_level=baja
verbal_risk=alto
drift_detected=true
Prohibido generar mandatos para:
hedging_detected aislado
over_explanation aislado
Reglas de estilo (no negociables)
action:
Imperativo
Máx. 1 frase
Sin teoría
Prohibido:
justificar el flag
evaluar nivel
usar “deberías”, “mejor”, “intenta”
Regla de autoridad
Flags describen.
Mandatos ordenan.
Nada más.

| source_flag     | condition | action                                             | constraint          | priority |
| --------------- | --------- | -------------------------------------------------- | ------------------- | -------- |
| closure_ok      | false     | Cierra la respuesta de forma explícita.            | hereda_closure_rule | alta     |
| authority_level | baja      | Toma una decisión clara y afirmativa.              | hereda_closure_rule | alta     |
| verbal_risk     | alto      | Elimina justificación y responde con una decisión. | hereda_closure_rule | alta     |
| drift_detected  | true      | Responde al objeto literal de la pregunta.         | hereda_closure_rule | media    |
