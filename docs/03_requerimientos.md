# 3. Ingeniería de Requerimientos – SGCA (Sistema de Gestión de Certificados Académicos)

Este apartado define cómo se relevan, clasifican, priorizan y especifican los requerimientos del SGCA. Es la base del
**documento de especificación de requerimientos**, entregable interno 1 del alcance, previsto para la semana 1
(02/11 al 06/11/2026). Cada requerimiento tiene un código (RF, RNF, RD) que se reutiliza en riesgos, estimación, pruebas
y criterios de aceptación.

---

## 3.1 Técnicas de elicitación

El conocimiento del negocio está repartido entre pocas personas de Secretaría, el área de Sistemas y los alumnos, y el
plazo total es de 6 semanas. Por eso se eligen técnicas rápidas, baratas y que se complementan entre sí. Todas se
ejecutan en la semana 1.

| # | Técnica | A quién se aplica | Qué se busca | Por qué se elige |
|---|---|---|---|---|
| 1 | **Entrevistas semiestructuradas** (4 de 45 min) | S01, S05, S04, S03 | Reglas de negocio: qué es una deuda, qué datos lleva cada certificado, cómo se accede al sistema de alumnos. | Pocas personas clave tienen el conocimiento y no está escrito. Permite repreguntar y detectar desacuerdos entre áreas. |
| 2 | **Observación del trámite actual** (medio día) | S05 | Pasos reales de una solicitud manual, errores frecuentes y tareas que nadie menciona. | La gente omite lo que le parece obvio. Además fija la situación de partida para medir la mejora del objetivo general (≥ 95 % sin intervención manual). |
| 3 | **Análisis de documentos** | Certificados actuales, reglamento académico, modelo de datos del sistema de alumnos | Reglas de dominio (escala 1–10, materias extracurriculares) y datos disponibles para la integración. | Son fuentes objetivas y no consumen tiempo de los interesados. |
| 4 | **Encuesta breve** (hasta 8 preguntas cerradas) | S10 | Tipo de certificado más pedido, dispositivo que usan y qué esperan del trámite. | Los alumnos son muchos y no se puede entrevistar uno por uno. Los resultados respaldan el diseño para desktop y móvil (RF-01). |
| 5 | **Prototipo de baja fidelidad** | S09 con S10 y S01 | Validar el flujo de solicitud antes de programar. | Es más fácil reaccionar ante una pantalla dibujada que describir un requisito. En 6 semanas no hay margen para rehacer. |
| 6 | **Taller de priorización** (1 reunión) | S01 con el equipo (S06, S07, S08) | Acordar qué es imprescindible y qué puede quedar afuera (MoSCoW, ver 3.3). | Quien decide las prioridades es Secretaría. Se logra el acuerdo en una sola reunión y queda registrado. |

**Técnicas descartadas:** grupos focales con alumnos y talleres largos de modelado conjunto. Consumen más tiempo del
disponible y el caso es de baja complejidad.

**Uso de IA:** la IA se usa solo como asistente para refinar redacciones y detectar ambigüedades (ver apartado de Uso de
IA en Requerimientos). No reemplaza ninguna de las técnicas anteriores y todo lo que produce lo revisa una persona.

## 3.2 Clasificación y listado de requerimientos

Se trabaja con tres tipos de requerimiento:

- **RF – Requerimientos funcionales:** lo que el sistema hace.
- **RNF – Requerimientos no funcionales:** cómo lo hace. Cada uno tiene un criterio medible.
- **RD – Requerimientos de dominio:** reglas de la universidad que el sistema debe respetar sin importar la tecnología.

Como pide la consigna, se listan **3 RF y 2 RNF**. Cada uno agrupa funciones relacionadas para que las siete inclusiones
de producto del alcance (portal, API, validación de deudas, PDF, correo, registro e integración en lectura) tengan al
menos un requerimiento. Las pruebas, la documentación y el UAT no son requerimientos del producto y aparecen en el
apartado de Planificación.

### 3.2.1 Requerimientos de dominio (RD)

| ID | Regla | Fuente |
|---|---|---|
| RD-01 | Un alumno con deuda administrativa no puede obtener ningún certificado. | Consigna del caso |
| RD-02 | El certificado analítico parcial muestra las calificaciones en escala de 1 a 10. | Consigna del caso |
| RD-03 | El certificado analítico parcial excluye las materias extracurriculares. | Consigna del caso |
| RD-04 | Solo los alumnos con condición de regular vigente pueden solicitar certificados. | **Supuesto a validar.** Surge del objetivo general del alcance; la consigna no lo define (pregunta abierta 13). |

### 3.2.2 Requerimientos funcionales (RF)

| ID | Requerimiento | Fuente | Inclusiones del alcance | Reglas |
|---|---|---|---|---|
| RF-01 | **Solicitar y descargar el certificado.** El alumno autenticado elige el tipo de certificado (alumno regular o analítico parcial), envía la solicitud desde el portal y descarga el PDF desde el portal o desde el link del correo. Solo accede a sus propios certificados. El portal funciona en desktop (≥ 1024 px) y en móvil (≤ 480 px). | S01, S10 | Portal web, API | — |
| RF-02 | **Validar la elegibilidad.** Antes de emitir, el sistema consulta en modo solo lectura en el sistema de alumnos la condición de regular y las deudas del alumno. Si no cumple, bloquea la emisión y explica el motivo. | S01, S03, S04 | Validación de deudas, integración en modo lectura | RD-01, RD-04 |
| RF-03 | **Emitir el certificado.** El sistema genera el PDF con diseño institucional (en el analítico parcial, solo materias aprobadas, con notas de 1 a 10 y sin extracurriculares), registra la solicitud en PostgreSQL y envía al alumno un correo con el link de descarga. El registro guarda el alumno, el tipo de certificado, el estado (en proceso, emitida, rechazada o con error), el estado del correo (enviado o fallido) y la fecha; la fecha de emisión se completa al generar el PDF. | S01, S02 | Generación del PDF, notificación por correo, registro en PostgreSQL | RD-02, RD-03 |

### 3.2.3 Requerimientos no funcionales (RNF)

| ID | Categoría | Requerimiento | Cómo se mide | Fuente |
|---|---|---|---|---|
| RNF-01 | Desempeño | El certificado en PDF se genera en **30 segundos o menos**. | Logs del piloto del 09/12 al 11/12/2026 (métrica de desempeño asociada del alcance). | S01 |
| RNF-02 | Fiabilidad de la integración | La integración nunca escribe en el sistema de alumnos y falla en **menos del 1 %** de las consultas. | Reporte automatizado de la suite de pruebas con 500 consultas (objetivo específico de calidad de la integración). | S03 |

## 3.3 Priorización con MoSCoW

Criterios: **Must** si el módulo no puede entregarse ni firmarse sin el requerimiento. **Should** si es importante pero hay
una alternativa. **Could** si es deseable y solo entra si sobra tiempo. **Won't** si queda fuera de esta entrega.
Todos los RF salen de las inclusiones del alcance y por eso son Must. Las ideas que surgieron fuera del alcance quedan
como Won't para no generar *scope creep*.

| Categoría | Requerimiento | Justificación | Si no entra |
|---|---|---|---|
| **Must** | RF-01 Solicitar y descargar | Es el motivo del módulo. | El alumno no puede obtener el certificado. |
| **Must** | RF-02 Validar la elegibilidad | La consigna exige validar deudas (RD-01) y la integración es la fuente de los datos. | Se emitirían certificados a alumnos con deuda. |
| **Must** | RF-03 Emitir el certificado | Es el producto que recibe el alumno; el registro y el correo los exige la consigna. | No hay entregable ni auditoría. |
| **Won't** | Otros tipos de certificado (matrícula, titulación, constancia de cursos) | Excluido en el alcance (1.4). | Se trata como solicitud de cambio. |
| **Won't** | Firma digital avanzada, otros idiomas o apostilla | Excluido en el alcance (1.4). | Se trata como solicitud de cambio. |
| **Won't** | Pago en línea de deudas | Excluido en el alcance (1.4). El alumno regulariza su deuda por los canales actuales. | Se trata como solicitud de cambio. |
| **Won't** | Pantalla para que Secretaría consulte las solicitudes | No está en las inclusiones del alcance (1.3). Los registros quedan en la base de datos para auditoría. | Se trata como solicitud de cambio. |
| **Won't** | Reenvío del correo a pedido del alumno | No está en las inclusiones del alcance (1.3). El alumno puede descargar desde el portal. | Se trata como solicitud de cambio. |

Cualquier cambio sobre un Must se evalúa con el proceso de gestión de cambios del alcance: se estima su impacto en tiempo
y costo antes de aceptarlo.

## 3.4 Historias de usuario

Las historias parten de una versión inicial ambigua (por ejemplo, "Como alumno quiero que me den el analítico para
presentarlo en un trámite") y se refinan hasta cumplir INVEST. En cada una se eliminó la ambigüedad sobre el tipo de
alumno, el tipo de certificado, el resultado esperado y el tiempo. La HU-02 y el CU-01 se refinaron con apoyo de IA, y el
proceso completo (instrucción, salida y corrección humana) está en el apartado de Uso de IA en Requerimientos.

### HU-01 – Solicitar certificado de alumno regular

> **Como** alumno regular,
> **quiero** solicitar mi certificado de alumno regular desde el portal,
> **para** descargarlo en PDF sin tener que ir a Secretaría.

**Requerimientos:** RF-01, RF-02, RF-03 · **Reglas:** RD-01, RD-04 · **Prioridad:** Must

**Verificación INVEST**

| Criterio | Cumple | Justificación |
|---|---|---|
| **I**ndependiente | Sí | Se puede desarrollar y probar sin depender de la HU-02. |
| **N**egociable | Sí | El diseño del PDF y el texto del correo se pueden ajustar con Secretaría sin cambiar el objetivo. |
| **V**aliosa | Sí | El alumno obtiene su certificado sin trámite presencial. |
| **E**stimable | Sí | Alcance, reglas y datos están definidos (RF-01 a RF-03). |
| **P**equeña | Sí | Cubre un solo tipo de certificado con un flujo acotado: solicitar, validar, emitir y descargar. |
| **T**esteable | Sí | Cada criterio de aceptación es verificable con una prueba. |

**Criterios de aceptación (BDD)**

```gherkin
# language: es
Escenario: Emisión exitosa
  Dado que soy un alumno regular sin deudas administrativas
  Y que estoy autenticado en el portal
  Cuando solicito el certificado de alumno regular
  Entonces el sistema genera el certificado en PDF en 30 segundos o menos
  Y me muestra el botón de descarga
  Y me envía un correo con el link de descarga
  Y la solicitud queda registrada con mi usuario, el tipo de certificado y la fecha de emisión

Escenario: Bloqueo por deuda administrativa
  Dado que soy un alumno regular con deuda administrativa
  Cuando solicito el certificado de alumno regular
  Entonces el sistema no genera el certificado
  Y me explica el motivo del bloqueo
  Y la solicitud queda registrada como rechazada por deuda

Escenario: Sistema de alumnos no disponible
  Dado que el sistema de alumnos no responde
  Cuando solicito el certificado de alumno regular
  Entonces el sistema me informa que no puede procesar la solicitud en este momento y que intente más tarde
  Y no se genera ningún certificado
  Y la solicitud queda registrada con error

Escenario: Falla el envío del correo
  Dado que el servicio de correo no está disponible
  Cuando se emite mi certificado de alumno regular
  Entonces el certificado queda disponible para descargar en el portal
  Y el sistema registra la notificación como fallida
```

### HU-02 – Solicitar certificado analítico parcial

> **Como** alumno regular,
> **quiero** solicitar desde el portal mi certificado analítico parcial y descargarlo en PDF,
> **para** acreditar mis materias aprobadas y sus notas ante un tercero sin depender de una emisión manual de Secretaría Académica.

**Requerimientos:** RF-01, RF-02, RF-03 · **Reglas:** RD-01, RD-02, RD-03, RD-04 · **Prioridad:** Must

**Verificación INVEST**

| Criterio | Cumple | Justificación |
|---|---|---|
| **I**ndependiente | Sí | Comparte con la HU-01 la validación de deuda y de regularidad, que se implementa en la primera de las dos historias que se haga. Cada una se prueba por separado. |
| **N**egociable | Sí | El orden y el formato de las materias en el PDF se pueden ajustar con Secretaría. |
| **V**aliosa | Sí | Elimina la emisión manual de Secretaría y le da al alumno el documento en el momento. |
| **E**stimable | Sí | Las reglas RD-01 a RD-04 están definidas y los datos vienen del sistema de alumnos. La estimación depende de las preguntas abiertas 1, 3 y 10 (fuente de la deuda, modelo del PDF y cómo se reconoce una materia extracurricular). |
| **P**equeña | Sí | Cubre un solo tipo de certificado y agrega solo dos reglas (RD-02 y RD-03) al flujo de la HU-01. Si al estimar resulta grande, se divide en (a) validaciones y registro y (b) generación del PDF y correo. |
| **T**esteable | Sí | Los escenarios incluyen datos concretos de materias y notas. |

**Criterios de aceptación (BDD)**

```gherkin
# language: es
Escenario: Analítico con materias aprobadas, desaprobadas y extracurriculares
  Dado que soy un alumno regular sin deudas administrativas
  Y que el sistema de alumnos registra estas materias:
    | Materia              | Estado      | Nota | Extracurricular |
    | Matemática I         | Aprobada    | 8    | No              |
    | Programación I       | Aprobada    | 10   | No              |
    | Base de Datos        | Desaprobada | 2    | No              |
    | Taller de Fotografía | Aprobada    | 9    | Sí              |
  Cuando solicito el certificado analítico parcial
  Entonces el sistema genera el PDF en 30 segundos o menos
  Y el PDF lista exactamente 2 materias: Matemática I con nota 8 y Programación I con nota 10
  Y el PDF no contiene Base de Datos ni Taller de Fotografía

Escenario: Alumno sin materias aprobadas
  Dado que soy un alumno regular sin materias aprobadas
  Cuando solicito el certificado analítico parcial
  Entonces el sistema me informa que no hay materias aprobadas para incluir
  Y no genera ningún certificado
  Y la solicitud queda registrada como rechazada

Esquema del escenario: Nota fuera de la escala de 1 a 10
  Dado que soy un alumno regular sin deudas administrativas
  Y que el sistema de alumnos informa una materia aprobada con nota <nota>
  Cuando solicito el certificado analítico parcial
  Entonces el sistema no genera el certificado
  Y la solicitud queda registrada con error para su revisión

  Ejemplos:
    | nota |
    | 0    |
    | 11   |

Escenario: Alumno sin condición de regular vigente
  Dado que no tengo condición de regular vigente
  Cuando solicito el certificado analítico parcial
  Entonces el sistema no genera el certificado
  Y me explica el motivo del rechazo
  Y la solicitud queda registrada como rechazada

Escenario: Bloqueo por deuda administrativa
  Dado que soy un alumno regular con deuda administrativa
  Cuando solicito el certificado analítico parcial
  Entonces el sistema no genera el certificado
  Y me explica el motivo del bloqueo
  Y la solicitud queda registrada como rechazada por deuda
```

## 3.5 Caso de uso formal

### CU-01 – Solicitar certificado analítico

| Campo | Contenido |
|---|---|
| **ID y nombre** | CU-01 · Solicitar certificado analítico (parcial) |
| **Actor principal** | Alumno regular |
| **Actores secundarios** | Sistema de alumnos (solo lectura) · Servicio de correo electrónico |
| **Descripción** | El alumno pide su certificado analítico parcial y obtiene un PDF con sus materias aprobadas, sin materias extracurriculares y con notas de 1 a 10. |
| **Disparador** | El alumno elige "Certificado analítico parcial" en el portal. |
| **Precondiciones** | 1. El alumno está autenticado en el portal. <br> 2. El alumno tiene un registro (legajo) en el sistema de alumnos. |
| **Postcondición de éxito** | El PDF queda disponible para descargar, la solicitud queda registrada como emitida con su fecha de emisión y se envía el correo con el link, o se registra que el envío falló. |
| **Postcondición de fracaso** | No se emite ningún certificado, la solicitud queda registrada con su estado y motivo (rechazada o con error) y el alumno recibe un mensaje con el motivo. |
| **Reglas de negocio** | RD-01, RD-02, RD-03, RD-04 |
| **Requerimientos relacionados** | RF-01, RF-02, RF-03 · RNF-01, RNF-02 |

**Flujo principal**

| Paso | Actor | Acción |
|---|---|---|
| 1 | Alumno | Selecciona "Certificado analítico parcial". |
| 2 | Sistema | Muestra un resumen de la solicitud y pide confirmación. |
| 3 | Alumno | Confirma la solicitud. |
| 4 | Sistema | Registra la solicitud con estado "en proceso". |
| 5 | Sistema | Consulta al sistema de alumnos la situación administrativa del alumno. |
| 6 | Sistema | Verifica que el alumno tenga condición de regular vigente (RD-04) y no tenga deudas administrativas (RD-01). |
| 7 | Sistema | Consulta las materias aprobadas con sus notas. |
| 8 | Sistema | Descarta las materias extracurriculares (RD-03) y verifica que las notas estén entre 1 y 10 (RD-02). |
| 9 | Sistema | Genera el PDF con diseño institucional. |
| 10 | Sistema | Actualiza la solicitud a "emitida" y guarda la fecha de emisión. |
| 11 | Sistema | Muestra al alumno el botón de descarga y envía el correo con el link. |
| 12 | Alumno | Descarga el PDF. Fin del caso de uso. |

**Flujo alternativo**

| ID | Paso | Situación | Resultado |
|---|---|---|---|
| A1 | 3 | El alumno cancela la confirmación. | Vuelve al inicio del portal. No se registra ninguna solicitud. |
| A2 | 12 | El alumno descarga desde el link que recibió por correo en lugar de usar el botón del portal. | El sistema entrega el mismo PDF. |

**Excepciones**

| ID | Paso | Situación | Respuesta del sistema |
|---|---|---|---|
| E1 | 6 | El alumno tiene deuda administrativa. | No emite el certificado, informa el motivo y registra la solicitud como "rechazada por deuda". Fin. |
| E2 | 5 a 7 | El sistema de alumnos no está disponible. | Informa que no puede procesar la solicitud y que intente más tarde. Registra la solicitud con "error". Fin. |
| E3 | 7 | El alumno no tiene materias aprobadas. | Informa que no hay materias para incluir. Registra la solicitud como "rechazada". Fin. |
| E4 | 8 | Una nota está fuera de la escala de 1 a 10. | No emite el certificado y registra "error" para su revisión. Fin. |
| E5 | 11 | Falla el envío del correo. | El certificado queda disponible en el portal y se avisa al alumno que no se pudo enviar el correo. Registra el fallo para reintentar el envío. El caso de uso continúa. |
| E6 | 6 | El alumno no tiene condición de regular vigente. | No emite el certificado, informa el motivo y registra la solicitud como "rechazada". Fin. |
| E7 | 9 | Falla la generación del PDF. | Informa que ocurrió un error y que intente más tarde. Registra la solicitud con "error". Fin. |
| E8 | 4 y 10 | La base de datos no está disponible. | No habilita la descarga ni envía el correo. Informa que ocurrió un error y que intente más tarde. El error queda en el registro técnico del sistema, porque no se puede guardar la solicitud. Fin. |

El diagrama de secuencia del CU-01 está en el apartado de Uso de IA en Requerimientos.

## 3.6 Validación y puntos abiertos

**Cómo se valida la especificación**

- Cada requerimiento es atómico, tiene un código y un criterio de verificación.
- Secretaría Académica (S01) revisa y aprueba la lista de requerimientos y las prioridades antes de cerrar la semana 1.
- El tester (S08) revisa que todos los criterios de aceptación se puedan probar.
- La matriz de trazabilidad (3.7) muestra que ninguna inclusión del alcance queda sin requerimiento y ningún requerimiento queda sin prueba.

**Preguntas abiertas.** Quedan para confirmar con los interesados en la semana 1 y se pasan como supuestos al apartado de
Riesgos, supuestos y restricciones.

| # | Pregunta | A quién |
|---|---|---|
| 1 | ¿De dónde sale el dato de deuda administrativa: del sistema de alumnos o de Tesorería? ¿Qué detalle se le muestra al alumno y a quién se lo deriva? | S03, S04 |
| 2 | ¿Cómo se autentican los alumnos? Se asume que se usan las credenciales institucionales existentes. | S03 |
| 3 | ¿Qué datos exactos y qué diseño lleva cada certificado? | S01 |
| 4 | ¿El analítico parcial incluye solo las materias aprobadas hasta la fecha de la solicitud? ¿Se incluyen las equivalencias? | S01 |
| 5 | ¿El link de descarga tiene vencimiento y exige tener la sesión iniciada? | S01, S03 |
| 6 | ¿El analítico parcial incluye las materias del ciclo en curso cuyas actas todavía no están cerradas? | S01 |
| 7 | ¿El correo se envía a la dirección registrada en el sistema de alumnos? | S03 |
| 8 | ¿Hay un límite de solicitudes del mismo tipo por alumno o puede pedir el mismo certificado varias veces? ¿El PDF indica una fecha de validez? | S01 |
| 9 | Si un alumno cursa más de una carrera, ¿elige una al solicitar y se emite un PDF por carrera? | S01 |
| 10 | ¿Qué dato del sistema de alumnos permite reconocer una materia extracurricular? ¿Existen notas fuera de la escala de 1 a 10 (por ejemplo, en planes viejos o equivalencias)? | S03 |
| 11 | ¿Con qué demora se actualiza el dato de deuda en la fuente que lee el SGCA? Si el alumno paga, ¿cuándo deja de estar bloqueado? | S03, S04 |
| 12 | ¿Los terceros que reciben el certificado lo aceptan sin firma digital avanzada, que está excluida del alcance? | S01 |
| 13 | ¿Con qué criterio se determina que la condición de regular está vigente? ¿Un alumno que no es regular puede iniciar sesión en el portal? | S01, S03 |

## 3.7 Matriz de trazabilidad

| Requerimiento | Inclusiones del alcance | Objetivo del alcance | Fuente | Se verifica con |
|---|---|---|---|---|
| RF-01 | Portal web · API | Cobertura funcional | S01, S10 | HU-01, HU-02, CU-01 pasos 1 a 3 y 12, A2 |
| RF-02 | Validación de deudas · integración en modo lectura | Cobertura funcional · calidad de la integración | S01, S03, S04 | HU-01 (deuda y sistema no disponible), HU-02 (deuda y sin condición de regular), CU-01 E1, E2 y E6 |
| RF-03 | Generación del PDF · notificación por correo · registro en PostgreSQL | Cobertura funcional · auditoría | S01, S02 | HU-01 (emisión y falla del correo), HU-02 (materias y notas), CU-01 pasos 4 y 8 a 11, E5, E7 y E8 |
| RNF-01 | Generación del PDF | Métrica de desempeño asociada | S01 | Logs del piloto (09/12 al 11/12) |
| RNF-02 | Integración en modo lectura | Calidad de la integración | S03 | Suite de pruebas (500 consultas) |

---

## Trazabilidad

| Elemento | Se conecta con |
|---|---|
| Requerimientos y reglas | Cada RF o RNF cubre inclusiones del Alcance y sale de un interesado del apartado de Stakeholders. |
| Preguntas abiertas y RD-04 | Pasan como supuestos y riesgos al apartado de Riesgos, supuestos y restricciones. |
| RF y historias de usuario | Base de los Puntos de Función (apartado de Estimación de tiempos y costos) y de las tareas del apartado de Planificación. |
| RNF-01 y RNF-02 | Se controlan como KPIs en el apartado de Seguimiento y control. |
| HU-02 y CU-01 | Se refinaron con IA y se corrigieron a mano (apartado de Uso de IA en Requerimientos). |
| HU, CU y criterios BDD | Se convierten en las pruebas del UAT (apartado de Cierre del proyecto). |
