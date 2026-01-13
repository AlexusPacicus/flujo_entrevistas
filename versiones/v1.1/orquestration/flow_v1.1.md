graph TD
    IN[Inputs<br/>(CV · README · Docs)]
        --> CE[contexto_emisor<br/>(SK function)]

    CE --> CVA{contexto_validador}

    CVA -- INVALID --> CN[contexto_normalizador<br/>(SK function)]
    CN --> CVA

    CVA -- VALID --> DRR[derivador_rrhh<br/>(SK function)]
    CVA -- VALID --> DRT[derivador_tecnico<br/>(SK function)]

    DRR --> QRR[question_set_rrhh<br/>(SK function)]
    DRT --> QRT[question_set_tecnico<br/>(SK function)]

    QRR --> IRR[interview_rrhh<br/>(SK function)]
    QRT --> IRT[interview_tecnico<br/>(SK function)]

    IRR --> AF[analyze_flags<br/>(SK function)]
    IRT --> AF

    AF --> AM[apply_mandates<br/>(SK function)]

    CVA -. after 3 INVALID .-> ABORT[ABORT]
