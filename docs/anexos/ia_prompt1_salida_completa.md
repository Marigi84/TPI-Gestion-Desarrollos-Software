# Anexo – Salida completa del prompt 1 (copia de respaldo)

Copia sin modificar de la respuesta de la IA al prompt 1 del apartado 4. Chat original: https://claude.ai/share/352d14af-226a-4412-ab09-d076196a44e1 (16/10/2026).

````markdown
## 1. Ambigüedades, supuestos implícitos y datos faltantes

| # | Ambigüedad | Por qué es un problema | Pregunta para resolverla | A quién |
|---|---|---|---|---|
| 1 | "alumno" (cualquier alumno) | RD-04 limita el acceso a alumnos con regularidad vigente; la historia no lo dice. | ¿Qué condición define "regular vigente" y en qué campo del sistema de alumnos consta? ¿Tiene fecha de vencimiento? | Secretaría Académica / Sistemas |
| 2 | "el analítico" | Puede ser total o parcial. El total (de egreso) queda fuera de alcance. | ¿Confirmamos que es solo el analítico parcial y que el analítico de egreso queda excluido? | Secretaría Académica |
| 3 | "que me den" (voz pasiva, sin canal) | No indica si es autogestión web o emisión por un empleado. El trámite presencial está fuera de alcance. | ¿El alumno lo solicita y lo descarga él mismo desde el SGCA, sin intervención de personal? | Equipo / Secretaría Académica |
| 4 | "para presentarlo en un trámite" | El beneficio es vago. Además, si el destinatario exige firma digital avanzada, el PDF no le sirve (fuera de alcance). | ¿Qué validez tiene el PDF sin firma avanzada? ¿Lleva algún elemento de verificación, como un código o número de solicitud? | Secretaría Académica |
| 5 | La deuda administrativa no se menciona | RD-01 bloquea la emisión y la historia lo omite. | ¿Qué conceptos cuentan como deuda (aranceles, biblioteca, otros)? ¿El dato de deuda se lee del sistema de alumnos o de otro sistema? | Tesorería / Sistemas |
| 6 | Actualización del estado de deuda | Si el alumno paga, no se sabe cuándo se refleja el cambio y puede quedar bloqueado sin motivo. | ¿Con qué demora se actualiza la deuda en la fuente que lee el SGCA? | Tesorería / Sistemas |
| 7 | Contenido del analítico | No se define qué materias aparecen (aprobadas, desaprobadas, ausentes, equivalencias). | ¿Se incluyen solo materias aprobadas? ¿Las equivalencias aparecen y cómo se identifican? | Secretaría Académica |
| 8 | Escala de notas | RD-02 exige escala 1 a 10. Puede haber planes viejos o equivalencias con otra escala. | ¿Existen notas fuera de la escala 1–10 en el sistema? ¿Hay una regla de conversión oficial? | Secretaría Académica / Sistemas |
| 9 | Materias extracurriculares | RD-03 las excluye, pero no se sabe cómo se reconocen en los datos. | ¿Qué atributo del sistema de alumnos marca una materia como extracurricular? | Sistemas |
| 10 | Alumno con más de una carrera | No se sabe si se emite un analítico por carrera o uno combinado. | ¿El alumno elige la carrera? ¿Se emite un PDF por carrera? | Secretaría Académica |
| 11 | Notificación por correo | No se define el destinatario ni el contenido. | ¿Se envía al correo institucional o al personal? ¿Adjunta el PDF o solo avisa de la emisión? | Sistemas / Secretaría Académica |
| 12 | Registro de solicitud y emisión | No se definen los datos a registrar ni si se guardan las solicitudes rechazadas. | ¿Qué campos se registran (legajo, carrera, tipo, fecha y hora, resultado, motivo)? ¿Se registran los rechazos? | Secretaría Académica / Equipo |
| 13 | Reemisión y límites | No se sabe si puede pedirlo varias veces ni si el certificado tiene vigencia. | ¿Hay un límite de solicitudes? ¿El PDF indica una fecha de validez? | Secretaría Académica |
| 14 | Corte de datos | Puede haber actas abiertas o notas sin cerrar. | ¿Se incluyen solo notas con acta cerrada a la fecha de emisión? | Secretaría Académica / Sistemas |
| 15 | Formato del PDF | No hay modelo de membrete, leyendas ni datos personales a mostrar. | ¿Existe un modelo oficial del analítico parcial? ¿Qué datos del alumno debe mostrar? | Secretaría Académica / Diseñador UX |

## 2. Historia refinada

**Como** alumno con condición de regular vigente y sin deuda administrativa,
**quiero** solicitar desde el SGCA el certificado analítico parcial de una carrera en la que estoy inscripto y descargarlo en PDF,
**para** acreditar mis materias aprobadas y sus calificaciones ante un tercero sin depender de una emisión manual de la Secretaría Académica.

Notas de alcance:
- Incluye:
  - validación de RD-01 y RD-04 contra el sistema de alumnos, en modo lectura;
  - notas en escala 1–10 (RD-02);
  - exclusión de las materias extracurriculares (RD-03);
  - correo de notificación;
  - registro de la solicitud y de la fecha de emisión.
- No incluye: el certificado de alumno regular (va en otra historia), el analítico de egreso, la firma digital avanzada ni otros idiomas.
- **SUPUESTO:** solo se incluyen materias aprobadas con acta cerrada.
- **SUPUESTO:** si el alumno tiene más de una carrera, elige una y se emite un PDF por carrera.
- **SUPUESTO:** el correo se envía a la dirección institucional registrada en el sistema de alumnos y adjunta el PDF.
- **SUPUESTO:** también se registran las solicitudes rechazadas, con su motivo.

## 3. Verificación INVEST

| Criterio | Cumple | Justificación |
|---|---|---|
| Independiente | Sí | Comparte la validación de deuda y regularidad con la historia del certificado de alumno regular. Esa validación se implementa en la primera de las dos historias que se haga, sin bloquear el orden. |
| Negociable | Sí | Define el qué y el para qué. El diseño del PDF, la librería y el formato del correo quedan abiertos. |
| Valiosa | Sí | Elimina la emisión manual y le da al alumno el documento en el momento. |
| Estimable | Sí | El alcance está acotado y el stack es conocido. La estimación depende de responder las preguntas 5, 9 y 15 (fuente de la deuda, marca de extracurricular y modelo de PDF). |
| Pequeña (Small) | Sí | Entra en una iteración dentro de las 6 semanas. Si la estimación supera una iteración, se divide en dos: (a) validaciones y registro, (b) generación del PDF y correo. |
| Testeable | Sí | Las reglas RD-01 a RD-04 tienen resultados binarios y verificables con datos concretos (ver sección 4). |

## 4. Criterios de aceptación (Gherkin)

```gherkin
Característica: Solicitud y descarga del certificado analítico parcial

  Antecedentes:
    Dado que el alumno con legajo "45120" inició sesión en el SGCA
    Y está inscripto en la carrera "Licenciatura en Sistemas"
    Y su correo institucional es "45120@alumnos.univ.edu.ar"
    Y en el sistema de alumnos registra estas materias con acta cerrada:
      | Materia               | Estado      | Nota | Extracurricular |
      | Matemática I          | Aprobada    | 8    | No              |
      | Programación I        | Aprobada    | 10   | No              |
      | Base de Datos         | Desaprobada | 2    | No              |
      | Taller de Fotografía  | Aprobada    | 9    | Sí              |

  Escenario: Emisión exitosa del analítico parcial (camino feliz)
    Dado que el alumno tiene condición "regular" con vencimiento el "31/03/2027"
    Y no registra deuda administrativa
    Cuando solicita el "Analítico parcial" de "Licenciatura en Sistemas" el "16/10/2026"
    Entonces se genera un archivo PDF descargable
    Y el PDF lista exactamente 2 materias: "Matemática I" con nota 8 y "Programación I" con nota 10
    Y el PDF no contiene "Taller de Fotografía" ni "Base de Datos"
    Y se envía un correo a "45120@alumnos.univ.edu.ar" con el PDF adjunto
    Y se registra la solicitud con legajo "45120", tipo "Analítico parcial", resultado "Emitido" y fecha de emisión "16/10/2026"

  Escenario: Rechazo por deuda administrativa (RD-01)
    Dado que el alumno tiene condición "regular" con vencimiento el "31/03/2027"
    Y registra una deuda administrativa de $15.000
    Cuando solicita el "Analítico parcial" de "Licenciatura en Sistemas"
    Entonces no se genera ningún PDF
    Y se muestra el mensaje "No podés obtener certificados porque registrás deuda administrativa. Comunicate con Tesorería."
    Y no se envía ningún correo
    # SUPUESTO: los rechazos se registran
    Y se registra la solicitud con resultado "Rechazada" y motivo "Deuda administrativa"

  Escenario: Rechazo por regularidad vencida (RD-04)
    Dado que el alumno tiene condición "regular" con vencimiento el "31/03/2026"
    Y no registra deuda administrativa
    Cuando solicita el "Analítico parcial" el "16/10/2026"
    Entonces no se genera ningún PDF
    Y se muestra el mensaje "Solo los alumnos con condición de regular vigente pueden solicitar certificados."
    Y se registra la solicitud con resultado "Rechazada" y motivo "Regularidad no vigente"

  Escenario: Rechazo por condición distinta de regular (RD-04)
    Dado que el alumno tiene condición "libre"
    Y no registra deuda administrativa
    Cuando solicita el "Analítico parcial"
    Entonces no se genera ningún PDF
    Y se registra la solicitud con resultado "Rechazada" y motivo "Regularidad no vigente"

  Escenario: Sistema de alumnos no disponible
    Dado que el sistema de alumnos no responde a la consulta del SGCA
    Cuando el alumno solicita el "Analítico parcial"
    Entonces no se genera ningún PDF
    Y se muestra el mensaje "No pudimos verificar tus datos. Intentá nuevamente más tarde."
    Y no se registra ninguna fecha de emisión

  Escenario: Falla en el envío del correo
    # SUPUESTO: una falla del correo no impide la descarga
    Dado que el alumno es regular vigente y no registra deuda administrativa
    Y el servidor de correo rechaza el envío
    Cuando solicita el "Analítico parcial"
    Entonces se genera el PDF y queda disponible para descarga
    Y se registra la solicitud con resultado "Emitido" y estado de notificación "Fallida"

  Esquema del escenario: Notas en los límites de la escala 1 a 10 (RD-02)
    Dado que el alumno es regular vigente y no registra deuda administrativa
    Y tiene aprobada "Física I" con nota <nota>
    Cuando solicita el "Analítico parcial"
    Entonces el PDF muestra "Física I" con nota <nota>

    Ejemplos:
      | nota |
      | 4    |
      | 10   |
```

Nota: el ejemplo de nota 4 es **SUPUESTO**. La nota mínima de aprobación debe confirmarla la Secretaría Académica (pregunta 7).
````
