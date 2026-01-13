graph TD
    IN[Inputs] --> CE[contexto_emisor]

    CE --> CVA{contexto_validador}

    CVA -- INVALID --> CN[contexto_normalizador]
    CN --> CVA

    CVA -- VALID --> DRR[derivador_rrhh]
    CVA -- VALID --> DRT[derivador_tecnico]

    DRR --> QRR[question_set_rrhh]
    DRT --> QRT[question_set_tecnico]

    QRR --> IRR[entrevista_rrhh]
    QRT --> IRT[entrevista_tecnico]

    IRR --> AF[analyze_flags]
    IRT --> AF

    AF --> AM[apply_mandates]

    CVA -.-> ABORT[ABORT]
