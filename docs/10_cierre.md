# 10. Cierre del proyecto – SGCA

**Proyecto:** Módulo web de solicitud y descarga de certificados académicos
**Período:** 02/11/2026 a 11/12/2026 (6 semanas)
**Cierre formal:** 11/12/2026
**Equipo:** 2 desarrolladores, 1 tester, 1 diseñador UX
**Presupuesto base:** USD 18.000

---

## 10.1 Definition of Done (DoD)

El módulo se considera terminado cuando cumple **todos** estos criterios. Al 11/12/2026 se verificaron
todos con la evidencia indicada.

| Dimensión | Criterio de Done | Evidencia | Estado |
|---|---|---|---|
| Funcional | Se emiten y descargan los 2 certificados (alumno regular y analítico parcial) y cada alumno accede solo a los suyos (RF-01). | Casos de prueba de HU-01 y HU-02 | ✅ |
| Funcional | La elegibilidad se valida en modo lectura; con deuda o sin regularidad vigente se bloquea y se explica el motivo (RF-02). | Pruebas de bloqueo y excepción E1/E6 del CU-01 | ✅ |
| Funcional | El PDF respeta la escala 1–10 y excluye extracurriculares; la solicitud se registra con su fecha de emisión y se envía el correo (RF-03). | Muestras de PDF, registro en PostgreSQL y correos de prueba | ✅ |
| No funcional | El PDF se genera en **30 segundos o menos** (RNF-01). | Logs del piloto 09–11/12 | ✅ |
| No funcional | La integración falla en **menos del 1 %** de las 500 consultas y nunca escribe en el sistema de alumnos (RNF-02). | Reporte de la suite de 500 consultas | ✅ |
| Calidad | **20 de 20** pruebas aprobadas; **0 defectos críticos o altos** abiertos; densidad ≤ 0,3 (6 defectos / 26 puntos de función = 0,23). | Plan de pruebas e informe de defectos | ✅ |
| Documentación | README, guía rápida, documentación técnica y plan de pruebas entregados. | Repositorio y carpeta de entrega | ✅ |
| Aceptación | UAT ejecutado y acta de conformidad firmada por Secretaría Académica. | Acta de Sign-off del 11/12/2026 | ✅ |
| Despliegue | Módulo en producción y garantía correctiva de 30 días iniciada. | Ambiente productivo y acta | ✅ |

---

## 10.2 UAT (User Acceptance Testing)

**Objetivo:** validar el módulo en un ambiente equivalente a producción, con usuarios reales y datos de
prueba, antes de la aceptación formal.

**Participantes:**

| Rol | Quién | Responsabilidad |
|---|---|---|
| Dueño del negocio | S01 Secretaría Académica | Valida el circuito completo y firma la conformidad |
| Operadores | S05 Personal administrativo | Ejecutan los casos y detectan mejoras de uso |
| Usuarios finales | S10 Alumnos (grupo piloto) | Prueban la solicitud y descarga desde el portal |
| Ejecución técnica | S08 Tester | Prepara los casos, registra defectos y evidencia |
| Coordinación | S06 Gestor del proyecto | Convoca, controla tiempos y registra decisiones |
| Infraestructura | S03 Área de Sistemas | Habilita el ambiente y los accesos de lectura |

**Alcance:** 20 pruebas del plan, escenarios BDD de HU-01 y HU-02, caso de uso CU-01, suite de 500
consultas, control de acceso a certificados ajenos, reglas del PDF (escala 1–10 y extracurriculares) y
envío de correo.

**Criterios de entrada:** T7 finalizada, build desplegado en staging, datos de prueba cargados y 0
defectos críticos o altos abiertos.

**Ejecución:** 09 al 11/12/2026, con seguimiento diario de defectos y reclasificación por severidad.

**Criterios de salida:** 100 % de las pruebas Must aprobadas, 0 defectos críticos o altos abiertos, y
defectos medios o bajos con solución alternativa aceptada por S01.

**Resultado:** 20 de 20 pruebas aprobadas; 500 consultas con 0,4 % de fallas; 6 defectos encontrados
durante el proyecto, todos corregidos; sin defectos críticos ni altos al cierre.

**Evidencia:** plan de pruebas ejecutado, informe de defectos, PDF de muestra, reporte de la suite de
500 consultas y acta de UAT.

---

## 10.3 Firma de conformidad (Sign-off)

**Proceso:**

1. El tester entrega el informe de UAT con resultados y evidencia.
2. Secretaría Académica revisa el informe y confirma que el circuito cumple lo acordado.
3. Se labra el **acta de conformidad** con el alcance entregado y los defectos abiertos (ninguno crítico).
4. Firman S01 (conformidad funcional) y S02 (conformidad presupuestaria, si corresponde).
5. Se libera el módulo a producción y se comunica a los alumnos.
6. Se inicia la garantía y el traspaso al soporte de S03.

**Contenido del acta:**

| Campo | Contenido |
|---|---|
| Proyecto y versión | SGCA – versión 1.0 |
| Fecha | 11/12/2026 |
| Entregables aceptados | Módulo en producción, guía rápida, documentación técnica y plan de pruebas |
| Resultado de UAT | 20/20 pruebas aprobadas; 0 defectos críticos o altos |
| Condiciones | Garantía correctiva de 30 días (11/12/2026 a 10/01/2027); no incluye mantenimiento evolutivo |
| Firmantes | S01 Secretaría Académica y S02 Autoridades |

**Después de la firma:** el módulo queda en producción, la garantía cubre defectos que impidan cumplir
los criterios de aceptación, y el soporte pasa a S03 y S01 según el traspaso documentado.

---

## 10.4 Informe Final

### 10.4.1 Resumen ejecutivo

El SGCA se entregó en las 6 semanas previstas (02/11 a 11/12/2026) y dentro del presupuesto: costo final
de **USD 11.238,50** frente a un base de USD 18.000. Se implementaron los dos certificados, la validación
de deudas y regularidad, la generación del PDF con las reglas del caso, la notificación por correo, el
registro con fecha de emisión y la integración de solo lectura. El UAT cerró con 20/20 pruebas aprobadas
y sin defectos críticos ni altos. El principal riesgo fue la dependencia de terceros para la integración,
que se materializó en un día de atraso y se recuperó sin mover la fecha de cierre.

### 10.4.2 Desvíos

| Área | Planificado | Real | Desvío | Acción |
|---|---|---|---|---|
| Plazo | Ruta crítica 29,5 días; cierre 11/12 | T6 terminó 1 día tarde (02/12) | +1 día en T6 | Se comprimió T7 de 5 a 4 días; T8 se ejecutó del 09 al 11/12 |
| Costo | USD 11.148,50 | USD 11.238,50 | +USD 90 (8 h de desarrollo) | Absorbido por la contingencia de USD 1.013,50 |
| Alcance | 3 RF y 2 RNF, sin cambios | Igual | 0 cambios aprobados | Los pedidos fuera de alcance quedaron como Won't |
| Calidad | 20 pruebas; densidad ≤ 0,3 | 20/20; 6 defectos (0,23) | Sin desvío | Todos los defectos corregidos antes del UAT |

### 10.4.3 Deuda técnica

| Ítem | Por qué quedó | Impacto | Prioridad |
|---|---|---|---|
| Panel de consulta para Secretaría | Excluido del alcance; la consulta se hace por base de datos | Operación manual para el personal administrativo | Media |
| Reenvío automático del correo | Solo se implementó el reintento manual | Si falla el correo, el alumno descarga desde el portal | Baja |
| Documentación de la API del sistema de alumnos | Depende de S03 y de documentación inexistente | Mayor tiempo de mantenimiento e integración | Media |
| Pruebas de carga limitadas a 500 consultas | El alcance fijó ese volumen | No se conoce el comportamiento con mayor demanda | Baja |
| Automatización de pruebas E2E | Las pruebas se ejecutaron manualmente | Más tiempo en cada regresión | Media |

### 10.4.4 Liberación de recursos

- **Personas:** los 4 integrantes se liberan el 11/12/2026. Un desarrollador queda al 20 % durante la
  garantía (30 días) para correcciones; el resto del equipo se reasigna.
- **Infraestructura:** producción y el servicio de correo se mantienen. El ambiente de staging se apaga
  al finalizar la garantía.
- **Accesos:** se revocan las credenciales de desarrollo; el SGCA conserva una cuenta de solo lectura y
  S03 mantiene la administración del sistema de alumnos.
- **Traspaso:** S01 y S05 operan el módulo; S03 soporta la infraestructura. La documentación y la guía
  rápida quedan entregadas.
- **Presupuesto:** costo final USD 11.238,50; contingencia utilizada USD 90; saldo de contingencia
  USD 923,50.

### 10.4.5 Lecciones aprendidas (resumen con IA y validación humana)

Se pidió a la IA que sintetizara las lecciones a partir del informe final, los reportes semanales y el
registro de riesgos, sin inventar datos. **Resumen generado:**

> Las tres lecciones principales son: acordar los accesos de terceros en la primera semana, porque su
> demora fue el único desvío de plazo; reservar un margen de cronograma mayor al 0,5 día, porque el PERT
> de la integración admite hasta 8 días; y definir el límite del módulo antes de contar Puntos de
> Función, porque la interpretación cambió el resultado de 4 a 26 puntos.

**Validación humana:** la IA propuso también lecciones genéricas ("mejorar la comunicación" y "capacitar
al equipo"). Se descartaron por no tener evidencia en el proyecto. Se conservaron solo las que se pueden
respaldar con hechos y se agregó la lección sobre el uso de IA, que la IA no había identificado.

| Lección | Evidencia | Acción para el próximo proyecto |
|---|---|---|
| Acordar accesos de terceros en la semana 1 | T6 se retrasó 1 día por credenciales (R-01) | Incluir el acceso como hito de la semana 1 |
| Reservar margen de cronograma | La ruta crítica usó 29,5 de 30 días | Reservar al menos un 10 % de buffer |
| Definir el límite del módulo antes de estimar | El conteo pasó de 4 a 26 puntos según la interpretación | Validar el alcance del conteo con la cátedra/cliente |
| Usar la IA con contexto y códigos, y validar siempre | La IA inventó "PDF adjunto" y un ID de caso de uso | Mantener la revisión humana como paso obligatorio |
| Documentar la API de terceros desde el inicio | La documentación incompleta quedó como deuda técnica | Pedir la documentación en el relevamiento |

---

## 10.5 Trazabilidad

| Elemento | Se conecta con |
|---|---|
| DoD | Objetivos del Alcance y RF/RNF de Requerimientos |
| UAT | HU-01, HU-02, CU-01 y las 20 pruebas del plan |
| Sign-off | S01 y S02 de Stakeholders; entregables del Alcance |
| Desvíos | R-01 (Riesgos), PERT y presupuesto (Estimación); cronograma (Planificación) |
| Deuda técnica | Exclusiones del Alcance y decisiones técnicas del proyecto |
| Lecciones aprendidas | Uso de IA en Requerimientos y reportes de Seguimiento y control |
