Contrato_Base_QuestionSet v1.1 

Identidad

- contract_id: Contrato_Base_QuestionSet
- scope: question_generation
- flow_reference: flow_v1.1 (FROZEN)

Rol

Generar un QuestionSet a partir de un ContextPack especializado.

Autoridad

Puede:
- Formular preguntas a partir de elementos explícitos del input

No puede:
- Acceder a contextos distintos del definido en el contrato específico
- Priorizar, evaluar o usar conocimiento externo

Input

- ContextPack_* v1.1 (definido en el contrato específico)

Output

- QuestionSet_*

Reglas duras

- 1 pregunta ← 1 elemento del input (source_ref obligatorio)
- Orden determinista
- El agente no puede acceder a contextos distintos del definido en el contrato específico.
- Las fuentes autorizadas y tipos de preguntas se definen solo en los contratos específicos.
