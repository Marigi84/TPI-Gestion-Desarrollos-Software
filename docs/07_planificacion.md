# 7. Planificación – SGCA

## 7.1 Tareas, dependencias y duraciones

| ID | Tarea | Duración | Dependencia | Relación con alcance/requerimientos |
|---|---|---:|---|---|
| T1 | Relevar y aprobar requerimientos | 5 días | — | Entregable interno de especificación de requerimientos; base de RF, RNF, HU y CU. |
| T2 | Diseñar arquitectura e integración | 3 días | T1 | Integración en modo lectura con el sistema de alumnos; backend Node.js y PostgreSQL. |
| T3 | Diseñar experiencia e interfaz UX | 4 días | T1 | Portal web para solicitud y descarga; soporte desktop y móvil definido en alcance. |
| T4 | Desarrollar backend y lógica de negocio | 7 días | T2 | RF-02 y RF-03: validación de elegibilidad, generación de PDF, registro y notificación. |
| T5 | Desarrollar frontend | 6 días | T2, T3 | RF-01: selección, solicitud y descarga de certificados desde el portal. |
| T6 | Integrar sistema de alumnos | 6,5 días | T4 | Consulta de datos académicos y administrativos en modo lectura. |
| T7 | Ejecutar pruebas y corregir defectos | 5 días | T4, T5, T6 | Criterios BDD, RNF, plan de pruebas y preparación del UAT. |
| T8 | Desplegar, ejecutar UAT y obtener conformidad | 3 días | T7 | Entregable externo del SGCA funcionando y proceso de aceptación/sign-off. |

La duración de **T6** toma como referencia la estimación PERT del apartado de Estimación de tiempos y costos.

---

## 7.2 Hitos SMART

### H-01. Requerimientos aprobados
Al finalizar la **semana 1**, Secretaría Académica habrá revisado y aprobado los requerimientos funcionales, no funcionales, historias de usuario y criterios de aceptación del SGCA.

### H-02. Diseño funcional y técnico validado
Al finalizar la **semana 2**, estarán validados el flujo de solicitud, la interfaz principal y el diseño de integración en modo lectura con el sistema de alumnos.

### H-03. Versión funcional integrada disponible para pruebas
A más tardar durante los **primeros dos días hábiles de la semana 5**, estará disponible una versión funcional que permita solicitar certificados, validar elegibilidad, generar el PDF, registrar la solicitud y operar las integraciones necesarias, lista para pruebas integrales.

### H-04. UAT aprobado y sistema listo para cierre
Al finalizar la **semana 6**, el SGCA habrá superado las pruebas de aceptación de usuario y contará con la conformidad formal correspondiente.

---

## 7.3 Entregables

### Entregables internos

**ENT-01. Documento de especificación de requerimientos — Semana 1**  
Incluye requerimientos funcionales y no funcionales, reglas de dominio, historias de usuario, criterios BDD y Caso de Uso.

**ENT-02. Plan de pruebas e informe de defectos — Semana 4**  
Al finalizar la semana 4 queda preparado el plan de pruebas con su matriz de trazabilidad. El informe de defectos se completa durante la ejecución de las pruebas y queda consolidado antes del UAT.

### Entregables externos

**ENT-03. SGCA desplegado y aceptado — Semana 6**  
Incluye las funcionalidades de solicitud, validación, generación de PDF, registro y notificación operativas, junto con la conformidad correspondiente.

**ENT-04. Guía rápida de usuario y transferencia — Semanas 5 y 6**  
La Guía Rápida queda disponible en la semana 5 y la sesión de transferencia a Secretaría Académica se realiza durante la semana 6.

---

## 7.4 Cronograma y Gantt simple

| Tarea | S1 | S2 | S3 | S4 | S5 | S6 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| T1 Relevar y aprobar requerimientos | █ |  |  |  |  |  |
| T2 Diseñar arquitectura e integración |  | █ |  |  |  |  |
| T3 Diseñar experiencia e interfaz UX |  | █ |  |  |  |  |
| T4 Desarrollar backend y lógica de negocio |  | █ | █ |  |  |  |
| T5 Desarrollar frontend |  | █ | █ |  |  |  |
| T6 Integrar sistema de alumnos |  |  |  | █ | █ |  |
| T7 Ejecutar pruebas y corregir defectos |  |  |  |  | █ | █ |
| T8 Desplegar, ejecutar UAT y obtener conformidad |  |  |  |  |  | █ |

---

## 7.5 Ruta crítica y verificación del plazo

Con las duraciones y dependencias definidas, la ruta crítica es:

**T1 → T2 → T4 → T6 → T7 → T8**

Su duración total es:

```text
5 + 3 + 7 + 6,5 + 5 + 3 = 29,5 días hábiles
```

El proyecto dispone de aproximadamente **30 días hábiles** dentro de las 6 semanas, por lo que el cronograma entra en el plazo previsto con un margen global aproximado de **0,5 día hábil**.

La rama formada por **T3 y T5** termina antes que la secuencia crítica y dispone de aproximadamente **6,5 días de holgura**, siempre que no se produzcan demoras que afecten el inicio de T7.

La integración representada por **T6** forma parte de la ruta crítica. Por lo tanto, cualquier demora significativa en esa tarea puede desplazar la fecha final del proyecto.
