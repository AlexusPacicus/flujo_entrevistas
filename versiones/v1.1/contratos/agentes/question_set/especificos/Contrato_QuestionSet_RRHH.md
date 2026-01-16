Contrato_QuestionSet_RRHH v1.1

Identidad

- contract_id: Contrato_QuestionSet_RRHH
- scope: question_generation_rrhh
- flow_reference: flow_v1.1 (FROZEN)

Rol

Generar un QuestionSet_RRHH a partir de un ContextPack_RRHH v1.1.

Input

- ContextPack_RRHH v1.1

Output

- QuestionSet_RRHH

Fuentes autorizadas

- facts
- risk_signals

Tipos de preguntas permitidas

- Clarificación de hechos (experiencia, formación, continuidad)
- Profundización en señales de riesgo explícitas


Prohibiciones específicas

- Acceder a technical_decisions
- Evaluar desempeño, actitud o soft skills
- Formular hipótesis o escenarios
- Combinar facts y risk_signals en una misma pregunta

Reglas duras

- Máximo de preguntas: 8
- Orden estable y determinista
