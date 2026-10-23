# 8. Seguimiento y control – SGCA

## 8.1 KPIs

Se usa **1 sprint = 1 semana** (6 sprints en total).

| KPI | Qué mide y cómo se calcula | Meta | Umbral de alerta | Fuente | Decisión que habilita |
|---|---|---|---|---|---|
| **Velocity** | Puntos de historia completados por sprint. Backlog de 120 puntos (8 tareas × 15 puntos promedio; unidad de seguimiento del tablero). | ≥ 20 puntos | < 16 durante 2 sprints | Tablero | Ajustar el alcance del sprint o reasignar trabajo |
| **Lead Time** | Días desde que se pide un cambio hasta que se entrega. | ≤ 5 días | > 8 días | Tablero | Escalar el bloqueo o revisar la dependencia |
| **Cycle Time** | Días desde que una tarea empieza a desarrollarse hasta que se termina. | ≤ 2 días hábiles | > 4 días | Tablero | Reducir el trabajo en curso y atacar el cuello de botella |
| **Densidad de defectos** | Defectos encontrados en QA ÷ 26 puntos de función del módulo. | ≤ 0,3 (≤ 8 defectos) | > 0,5 (> 13 defectos) | Plan de pruebas | Frenar la liberación y reforzar las pruebas |

**Por qué estos cuatro y no otros:** cubren las tres dimensiones del proyecto (entrega, flujo y calidad) con datos que ya genera el equipo, sin sumar trabajo de medición. No se usan DORA porque el proyecto tiene un solo despliegue al final, ni SPACE porque requiere encuestas que no entran en 6 semanas. Son métricas simples, adecuadas a un proyecto de baja complejidad.

**Justificación de cada una:**

- **Velocity:** indica si el equipo avanza al ritmo necesario para llegar a H-03 y H-04.
- **Lead Time:** mide el tiempo real que espera el usuario, no solo el trabajo del equipo.
- **Cycle Time:** muestra dónde se traba el flujo, sobre todo en la integración, que es la ruta crítica.
- **Densidad de defectos:** mide la calidad del producto terminado y habilita o frena la liberación.

Los puntos de historia se usan solo para medir velocity; no reemplazan los Puntos de Función de la
estimación ni los días del cronograma.

---

## 8.2 Reporte de avance semanal simulado

### Semana 3 — corte 20/11/2026

**Semáforo general: 🟡 Amarillo.**
El avance es del 60 % frente al 62 % planificado. H-03 está en riesgo porque T6 no puede iniciar sin las credenciales del sistema de alumnos; el resto del trabajo funcional avanza.

#### Hitos

| Hito | Fecha | Estado |
|---|---|---|
| **H-01** Requerimientos aprobados | 06/11/2026 | ✅ Cumplido |
| **H-02** Diseño funcional y técnico validado | 13/11/2026 | ✅ Cumplido |
| **H-03** Versión funcional integrada para pruebas | 30/11 al 01/12/2026 | ⚪ Pendiente (T6 sin iniciar) |
| **H-04** UAT aprobado y sistema listo para cierre | 11/12/2026 | ⚪ No iniciado |

#### En curso

- **Validación de deudas (T4):** 6 de 8 casos aprobados; faltan los casos de deuda cancelada el mismo día.
- **Registro de solicitudes (T4):** operativo en PostgreSQL; faltan índices de consulta.
- **Plantilla del certificado (T4):** en revisión con Secretaría Académica (escala 1–10 y exclusión de extracurriculares).
- **Frontend (T5):** descarga y estados de la solicitud en revisión final.
- **Integración (T6):** no iniciada; debe arrancar el 23/11 y depende de las credenciales de S03. Por eso no se pudo ejecutar la suite de 500 consultas del objetivo 2.

#### Bloqueos

- **B1 (crítico):** el Área de Sistemas (S03) no emitió las credenciales de lectura del sistema de alumnos desde el 17/11. Afecta T6, la ruta crítica.
- **B2:** falta el listado definitivo de materias extracurriculares que debe excluir el analítico (S01).

#### Próximos pasos

1. Escalar B1 en el comité del 23/11 y acordar la entrega de credenciales para el 24/11 (impacto: 1 día en T6).
2. Cerrar los 8 casos de validación de deudas y T4/T5 antes del 23/11.
3. Iniciar T6 el 23/11 ni bien lleguen las credenciales.
4. Recalcular el pronóstico de H-03 con la velocity de las últimas tres semanas.

#### Indicadores del período

| KPI | Valor | Meta | Estado |
|---|---|---|---|
| Velocity | 17 puntos | ≥ 20 | 🟡 |
| Lead Time | 6,2 días | ≤ 5 días | 🟡 |
| Cycle Time | 2,4 días | ≤ 2 días | 🟡 |
| Densidad de defectos | 0 (sin defectos registrados) | ≤ 0,3 | 🟢 |

---

## 8.3 Alertas automáticas del dashboard con IA

### Alerta 1 — Pronóstico de desvío de hito

**Qué datos mira:** velocity de los últimos sprints, puntos pendientes y Lead Time de las tareas de la ruta crítica.

**Cuándo dispara:** si la velocity cae por debajo de la meta y la proyección indica que un hito no se cumple.

**Mensaje de ejemplo:**

> ⚠️ Con una velocity de 17 puntos y 40 % del alcance pendiente, la probabilidad de cumplir H-03 el 01/12 es del 55 %. Fecha probable: 04/12 (+3 días). Opciones: reducir el alcance del sprint o reasignar un desarrollador a la integración.

**Acción:** el comité decide si ajusta el alcance del sprint o refuerza la tarea crítica.

### Alerta 2 — Tarea bloqueada en la ruta crítica

**Qué datos mira:** días que una tarea lleva bloqueada o en el mismo estado, y su duración estimada (PERT).

**Cuándo dispara:** si una tarea de la ruta crítica no puede iniciar o supera su duración esperada sin cambiar de estado. La integración tiene una duración PERT de 6,5 días.

**Mensaje de ejemplo:**

> 🚨 T6 (integración) no puede iniciar: las credenciales de S03 no llegaron. Su duración estimada es de 6,5 días y es la tarea crítica del cronograma. Riesgo directo sobre H-03. Acción: escalar los accesos con S03 hoy.

**Acción:** el gestor escala el bloqueo y registra la decisión en el reporte.

---

## 8.4 Control de la planificación

| KPI | Elemento del plan que controla | Pregunta que responde |
|---|---|---|
| Velocity | Avance de sprints e hitos H-03 y H-04 | ¿Llegamos con la fecha comprometida? |
| Lead Time | Fecha de entrega al alumno | ¿El certificado llega a tiempo? |
| Cycle Time | Ruta crítica, especialmente T6 | ¿Dónde se está trabando el trabajo? |
| Densidad de defectos | Calidad de la versión para H-04 | ¿Podemos liberar sin riesgo? |

Con estos cuatro indicadores, el comité semanal puede detectar un desvío antes de que afecte un hito y tomar una decisión concreta: reasignar, escalar un bloqueo, ajustar el alcance del sprint o frenar la liberación.

---

## Trazabilidad

| Elemento | Se conecta con |
|---|---|
| Velocity y Lead Time | Objetivo general y cronograma (Alcance y Planificación) |
| Cycle Time | Tarea crítica de 6,5 días y dependencia de S03 (Riesgos, supuestos y restricciones; Estimación de tiempos y costos) |
| Densidad de defectos | Objetivo 1 (20 pruebas) y 26 puntos de función (Alcance y Estimación de tiempos y costos) |
| Reporte semanal | Acción 1 de alineación de stakeholders (Stakeholders) |
| Alertas de IA | R-02 y dependencia de S03 (Riesgos, supuestos y restricciones) y comité semanal |
