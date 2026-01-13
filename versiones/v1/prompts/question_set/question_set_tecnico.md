# PROMPT_ID: GENERATE_QUESTIONSET_TECNICO
file_path: prompts/question_set_tecnico.md
old_string: |-
    - Cada pregunta debe mapear 1:1 a una decisión o límite EXPLÍCITO presente en ContextPack_TÉCNICO.
    - PROHIBIDO introducir escenarios hipotéticos, abstractos o no declarados.

    TIPOS PERMITIDOS (Restricción del Agente):
    - decision
    - tradeoff
    - limite
    - fallo
    (Nota: El tipo `definicion` NO se utiliza en el set técnico).

    FORMULACIÓN DE PREGUNTAS:
    - Cada pregunta debe contener UNA sola proposición cerrada.
    - PROHIBIDO iniciar preguntas con: “¿Qué…?”, “¿Hasta qué…?”, “¿Ante qué…?”.
    - PROHIBIDO usar: “explícame”, “cuéntame”, “desde tu punto de vista”.
    - FORMULACIONES PREFERENTES:
      - “¿Aceptarías…?”
      - “¿Mantendrías…?”
      - “¿Eliminarías…?”
      - “¿Descartarías…?”

    REGLAS DE CIERRE (OBLIGATORIAS):
    - Cada pregunta debe poder responderse en ≤ 30 segundos (`max_time_sec`).
    - Las únicas `closure_rule` válidas para Técnico son:
      - `1_frase`
      - `binario`
    - PROHIBIDO usar la regla `2_frases`.

    SALIDA:
    Emitir exclusivamente el schema QuestionSet_Técnico en YAML, siguiendo la estructura contractual del Schema v1.1.

    PROHIBIDO introducir métricas numéricas, costes económicos o expansiones de mercado no presentes explícitamente en ContextPack_TÉCNICO.
new_string: |-
    - Cada pregunta debe mapear 1:1 a una decisión o límite EXPLÍCITO presente en ContextPack_TÉCNICO.
    - PROHIBIDO introducir escenarios hipotéticos, abstractos o no declarados.
    - Las preguntas SOLO pueden referirse a señales o dimensiones EXPLÍCITAMENTE mencionadas en ContextPack_TÉCNICO. PROHIBIDO introducir nuevas categorías de señales (ej. comportamiento, usuario, contenido, red, economía).
    - PROHIBIDO introducir efectos secundarios no declarados, incluyendo (pero no limitado a): latencia, coste económico, consumo de recursos o escalabilidad, salvo que estén escritos explícitamente en ContextPack_TÉCNICO.

    TIPOS PERMITIDOS (Restricción del Agente):
    - decision
    - tradeoff
    - limite
    - fallo
    (Nota: El tipo `definicion` NO se utiliza en el set técnico).

    FORMULACIÓN DE PREGUNTAS:
    - Cada pregunta debe contener UNA sola proposición cerrada.
    - PROHIBIDO iniciar preguntas con: “¿Qué…?”, “¿Hasta qué…?”, “¿Ante qué…?”.
    - PROHIBIDO usar: “explícame”, “cuéntame”, “desde tu punto de vista”.
    - FORMULACIONES PREFERENTES:
      - “¿Aceptarías…?”
      - “¿Mantendrías…?”
      - Dos de las preguntas DEBEN usar estas formulaciones.

    REGLAS DE CIERRE (OBLIGATORIAS):
    - Cada pregunta debe poder responderse en ≤ 30 segundos (`max_time_sec`).
    - Las únicas `closure_rule` válidas para Técnico son:
      - `1_frase`
      - `binario`
    - PROHIBIDO usar la regla `2_frases`.

    VALIDACIÓN INTERNA (OBLIGATORIA):
    - Antes de emitir el QuestionSet, verifica que cada sustantivo técnico usado en las preguntas aparece explícitamente en ContextPack_TÉCNICO.
    - Si no aparece, la pregunta DEBE reformularse o descartarse.

    SALIDA:
    Emitir exclusivamente el schema QuestionSet_Técnico en YAML, siguiendo la estructura contractual del Schema v1.1.