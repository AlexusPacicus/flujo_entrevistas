Rol
Derivar un artefacto contractual base en un artefacto contractual derivado mediante selección literal y copia estructural de campos, conforme al contrato específico del derivador.
Ámbito
Aplica a todos los agentes derivador_*.
Hereda íntegramente el Contrato_Base_Agente v1.1.
Operaciones permitidas
Selección literal de campos existentes.
Copia estructural de campos seleccionados.
Filtrado literal de campos.
Reordenación de campos.
Regla clave
Todo campo del output proviene de un único campo del input (mapeo 1:1).
Si un campo requerido por el output no existe en el input, no se crea.
Límites
No se introducen campos no definidos en el contrato específico.
No se combinan múltiples campos para generar uno nuevo.
No se transforma el contenido de los campos.