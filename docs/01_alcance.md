# 1. Alcance del proyecto – SGCA (Sistema de Gestión de Certificados Académicos)

**Proyecto:** Módulo web de solicitud y descarga de certificados académicos
**Cliente:** Universidad (Secretaría Académica)
**Plazo:** 6 semanas simuladas — 02/11/2026 a 11/12/2026
**Equipo:** 2 desarrolladores, 1 tester, 1 diseñador UX
**Presupuesto base:** USD 18.000
**Tecnología obligatoria:** backend Node.js, frontend React, base de datos PostgreSQL

---

## 1.1 Objetivo general (SMART)

Implementar, entre el 02/11/2026 y el 11/12/2026 (6 semanas), el módulo web **SGCA** para que los alumnos
regulares de la universidad soliciten y descarguen los certificados de *alumno regular* y *analítico parcial*
en PDF, validando deudas administrativas y notificando por correo, emitiéndose el **≥ 95 %** de las
solicitudes **sin intervención manual**, con un presupuesto no mayor a **USD 18.000**, integrándose en
modo lectura con el sistema de alumnos existente.

| Criterio SMART | Cómo se cumple |
|---|---|
| **E**specífico | Un solo módulo web, dos tipos de certificado, tres validaciones concretas (deudas, PDF, correo) |
| **M**edible | ≥ 95 % de solicitudes emitidas sin intervención manual, tiempo de generación, presupuesto gastado |
| **A**lcanzable | Equipo de 4 personas, tecnología conocida (Node/React/Postgres), integración solo lectura |
| **R**elevante | Resuelve la cola manual de solicitudes en Secretaría Académica |
| **T**emporal | 6 semanas, fecha de cierre: 11/12/2026 |

## 1.2 Objetivos específicos (SMART)

1. **Cobertura funcional:** Que el 100 % de las dos solicitudes soportadas (alumno regular y analítico
   parcial) esté operativo en el ambiente de pruebas antes del **04/12/2026**, verificado por el tester con
   las 20 pruebas del plan de pruebas.
2. **Calidad de la integración:** Reducir a **menos del 1 %** las fallas de sincronización en 500 consultas
   de prueba contra el sistema de alumnos (modo lectura), medido con el reporte automatizado de la suite
   de pruebas, antes del **04/12/2026**.
3. **Auditoría y desempeño:** Que el **100 %** de las solicitudes quede registrada en PostgreSQL con
   usuario, tipo de certificado y fecha de emisión, y que el PDF se genere en **≤ 30 segundos**, medido
   por logs en el piloto del **09/12/2026 al 11/12/2026**.

## 1.3 Inclusiones (lo que el equipo se compromete a entregar)

- Portal web en React para solicitar y descargar los **2 tipos de certificado**: alumno regular y analítico
  parcial, **responsive en 2 tamaños definidos**: desktop (≥ 1024 px) y móvil (≤ 480 px).
- API en Node.js con las operaciones: consultar elegibilidad, registrar solicitud, generar PDF, notificar por correo.
- **Validación de deudas administrativas** previa a la emisión (si tiene deudas, bloquea y explica el motivo).
- **Generación del certificado en PDF** con diseño institucional, respetando la escala 1–10 y excluyendo
  materias extracurriculares en el analítico parcial.
- **Notificación por correo electrónico** al alumno con link de descarga.
- **Registro de la solicitud y la fecha de emisión** en PostgreSQL (trazabilidad auditable).
- **Integración en modo lectura** con el sistema de alumnos existente (el SGCA nunca escribe en él).
- Pruebas funcionales y de integración, corrección de defectos y documentación técnica (Docs as Code).
- Guía Rápida para el alumno, README del repositorio y sesión de traspaso a Secretaría Académica.
- UAT y firma de conformidad (Sign-off) al cierre.

## 1.4 Exclusiones (fuera del alcance, de forma explícita)

- Aplicación móvil nativa ni soporte responsive fuera de los 2 tamaños definidos en las inclusiones (desktop ≥ 1024 px, móvil ≤ 480 px).
- Emisión de certificados distintos de los dos tipos acordados (matrícula, titulación, constancia de cursos).
- Alta, baja o modificación de datos académicos: **el sistema de alumnos es solo lectura**.
- Corrección de notas, promociones o historial académico por parte del SGCA.
- Integraciones con otros sistemas no especificados (becas, biblioteca, tesis, pagos en línea).
- Trámite presencial asistido por personal (la entrega es 100 % digital).
- Mantenimiento evolutivo posterior a la entrega + 30 días de garantía por defectos.
- Certificados en otros idiomas, apostillados o con firma digital avanzada.
- Capacitación masiva a todo el alumnado (solo se entrega la Guía Rápida y una sesión de traspaso).

## 1.5 Entregables

**Externos (se entregan al cliente / usuario final):**

1. **Módulo SGCA desplegado en el ambiente productivo** (el sistema ya en uso por los alumnos): un sitio
   web donde el alumno puede solicitar y descargar en PDF los 2 certificados (alumno regular y analítico
   parcial), con todas las validaciones funcionando de punta a punta: si el alumno tiene deudas, el sistema
   lo bloquea y explica el motivo; si no, genera el PDF y le envía el link por correo. Se entrega con el
   **acta de conformidad firmada por Secretaría Académica (Sign-off)**.
2. **Guía Rápida del alumno** (1 página) + sesión de traspaso con Secretaría Académica.

**Internos (quedan como artefactos de gestión para el equipo):**

1. **Documento de especificación de requerimientos** (RF, RNF, historias de usuario, caso de uso y criterios de aceptación).
2. **Plan de pruebas y reporte de defectos** con la matriz de trazabilidad requisito ↔ prueba.

## 1.6 ¿Por qué una buena gestión del alcance evita el scope creep? (10 líneas)

El scope creep es la incorporación silenciosa de cambios que nadie estimó ni aprobó. Un alcance bien
definido pone por escrito, antes de empezar, qué entra y qué no entra, de modo que cualquier pedido nuevo
tiene contra qué compararse. Cuando la Secretaría pide "agregar el certificado de matrícula", el equipo no
discute de memoria: abre el documento de alcance, ve que esa opción está en las exclusiones y activa el
proceso de gestión de cambios, que exige estimar impacto en tiempo y costo antes de aceptar. Así, el plazo
de 6 semanas y el presupuesto de USD 18.000 se protegen con un mecanismo formal y no con discusiones de
última hora. Además, un alcance claro mejora la comunicación con los interesados: todos saben qué se
espera y cuándo, lo que reduce malentendidos, retrabajos y conflictos. En resumen: sin línea base de
alcance no hay punto de referencia para detectar la desviación, y lo que no se detecta, se paga con
sobrecosto y fecha incumplida.

---

## Trazabilidad

| Elemento | Se conecta con |
|---|---|
| Objetivo general → objetivos específicos | Cada objetivo específico tiene métrica y fecha (ver documento 4: KPIs) |
| Inclusiones → RF del documento de requerimientos | Cada inclusión debe tener al menos un RF o RNF |
| Exclusiones → matriz de riesgos | Un pedido de exclusión es un cambio, no una tarea del cronograma |
| Entregables → hitos del cronograma | Externos en semanas 5 y 6; internos en semanas 1 y 4 |
| Presupuesto USD 18.000 → documento 3 | El presupuesto aprobado es el techo del cálculo de costos |
