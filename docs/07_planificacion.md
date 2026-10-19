# 7. Planificación – SGCA

> **Estado:** borrador avanzado. La estructura de tareas, dependencias, hitos y entregables ya está definida. Las duraciones definitivas y el cronograma/Gantt se completarán cuando se cierre el apartado 6 de Estimación de tiempos y costos, para mantener coherencia entre ambos puntos.

## 7.1 Tareas y dependencias

| ID | Tarea | Dependencia | Relación con alcance/requerimientos |
|---|---|---|---|
| T1 | Relevar y aprobar requerimientos | — | Entregable interno de especificación de requerimientos; base de RF, RNF, HU y CU. |
| T2 | Diseñar arquitectura e integración | T1 | Integración en modo lectura con el sistema de alumnos; backend Node.js y PostgreSQL. |
| T3 | Diseñar experiencia e interfaz UX | T1 | Portal web para solicitud y descarga; soporte desktop y móvil definido en alcance. |
| T4 | Desarrollar backend y lógica de negocio | T2 | RF-02 y RF-03: validación de elegibilidad, generación de PDF, registro y notificación. |
| T5 | Desarrollar frontend | T3, T2 | RF-01: selección, solicitud y descarga de certificados desde el portal. |
| T6 | Integrar sistema de alumnos y servicio de correo | T4 | Consulta de datos académicos y de deuda en modo lectura; envío del link por correo. |
| T7 | Ejecutar pruebas y corregir defectos | T4, T5, T6 | Criterios BDD, RNF, plan de pruebas y preparación del UAT. |
| T8 | Desplegar, ejecutar UAT y obtener conformidad | T7 | Entregable externo del SGCA funcionando y proceso de aceptación/sign-off. |

> **Duraciones:** pendientes de completar con base en el apartado 6 de Estimación de tiempos y costos.

---

## 7.2 Hitos SMART

### H-01. Requerimientos aprobados
Al finalizar la **semana 1**, Secretaría Académica habrá revisado y aprobado los requerimientos funcionales, no funcionales, historias de usuario y criterios de aceptación del SGCA.

### H-02. Diseño funcional y técnico validado
Al finalizar la **semana 2**, estarán validados el flujo de solicitud, la interfaz principal y el diseño de integración en modo lectura con el sistema de alumnos.

### H-03. Versión funcional integrada disponible para pruebas
Al finalizar la **semana 4**, estará disponible una versión funcional que permita solicitar certificados, validar elegibilidad, generar el PDF y registrar la solicitud, lista para pruebas integrales.

### H-04. UAT aprobado y sistema listo para cierre
Al finalizar la **semana 6**, el SGCA habrá superado las pruebas de aceptación de usuario y contará con la conformidad formal correspondiente.

> Las semanas se revisarán al cerrar la estimación para asegurar que el cronograma sea consistente con las duraciones calculadas.

---

## 7.3 Entregables

### Entregables internos

**E1. Documento de especificación de requerimientos**  
Incluye requerimientos funcionales y no funcionales, reglas de dominio, historias de usuario, criterios BDD y Caso de Uso.

**E2. Plan de pruebas e informe de defectos**  
Se utiliza para verificar funcionalidad, integración y criterios de aceptación antes del UAT.

### Entregables externos

**E3. SGCA desplegado y aceptado**  
Incluye las funcionalidades de solicitud, validación, generación de PDF, registro y notificación operativas.

**E4. Guía rápida de usuario y transferencia**  
Destinada a facilitar el uso del sistema y su entrega a la universidad.

---

## 7.4 Cronograma

El cronograma y el Gantt simple se completarán una vez definido el apartado 6 de **Estimación de tiempos y costos**, ya que las duraciones de las tareas deben ser coherentes con las estimaciones del proyecto.

Hasta ese momento, se mantiene como línea base la secuencia de dependencias definida en 7.1 y el plazo máximo de **6 semanas** establecido por el caso.
