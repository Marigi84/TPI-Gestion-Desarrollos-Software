# 6. Estimación de tiempos y costos – SGCA

**Proyecto:** Módulo web de solicitud y descarga de certificados académicos
**Plazo del caso:** 6 semanas — 02/11/2026 a 11/12/2026 (30 días hábiles)
**Equipo:** 2 desarrolladores, 1 tester, 1 diseñador UX
**Presupuesto base:** USD 18.000 · **Tecnología obligatoria:** Node.js, React, PostgreSQL

Este apartado aplica tres métodos que se complementan: **PERT** para la tarea más incierta,
**Puntos de Función** para el tamaño funcional del módulo de emisión y **juicio experto** para contrastar.
El presupuesto se construye a partir de esas horas.

---

## 6.1 Base de la estimación

| Parámetro | Valor | Origen |
|---|---|---|
| Plazo | 6 semanas · 30 días hábiles | Caso y `01_alcance.md` |
| Capacidad del equipo | 4 personas × 40 h/semana × 6 semanas = **960 h** | Caso |
| Capacidad de desarrollo | 2 desarrolladores × 240 h = **480 h** | Equipo del caso |
| Tarifa desarrollador | USD 1.800/mes ÷ 160 h = **USD 11,25/h** | Supuesto de mercado |
| Tarifa tester / UX | USD 1.400/mes ÷ 160 h = **USD 8,75/h** | Supuesto de mercado |
| Productividad | **8 h por punto de función** | Supuesto a validar con históricos |
| Tecnología | Node.js / React / PostgreSQL | Restricción RE-02 del apartado 5 |

**Supuestos que sostienen la estimación** (si cambian, cambia el número):

- La deuda administrativa se consulta en modo lectura desde el sistema de alumnos (**S-01** del apartado 5).
- El sistema de alumnos entrega materias, notas y la marca de extracurricular (**S-02**).
- El criterio de regularidad vigente se confirma en la semana 1 (**RD-04 / pregunta abierta 13** del apartado 3).
- No hay cambios de alcance aprobados durante las 6 semanas.

---

## 6.2 PERT sobre la tarea crítica

**Tarea elegida:** *Integrar en modo lectura el SGCA con el sistema de alumnos* (RF-02 y RNF-02).

**Por qué es la tarea crítica:**

- Es la única fuente de datos para validar deudas y regularidad: sin ella no se emite ningún certificado.
- Depende de terceros (S03 Sistemas y S04 Tesorería): credenciales, permisos y formato de datos.
- Tiene la mayor incertidumbre del proyecto: API heredada, sin documentación completa y equipo sin experiencia previa en ese sistema.
- Si se retrasa más de 8 días, se corre la fecha de cierre (apartado 7).

| Escenario | Qué representa | Días |
|---|---|---|
| **Optimista (O)** | Credenciales el día 1, API documentada y datos completos | 3 |
| **Más probable (M)** | Algunas idas y vueltas con Sistemas, pero se resuelve | 6 |
| **Pesimista (P)** | Permisos demorados, cambios en el contrato de la API y curva de aprendizaje | 12 |

```
TE = (O + 4 × M + P) / 6
TE = (3 + 4 × 6 + 12) / 6
TE = (3 + 24 + 12) / 6
TE = 39 / 6
TE = 6,5 días
```

**Desviación estándar:**

```
σ = (P − O) / 6 = (12 − 3) / 6 = 1,5 días
```

**Lectura del resultado:** se planifica la tarea en **6,5 días**, con un rango razonable de **5 a 8 días**
(TE ± σ). El 4 de la fórmula pondera el escenario más probable, que es el que ocurre en la mayoría de los casos.

**Medidas que se derivan del PERT:**

- Reservar **1,5 días de holgura** para esta tarea en el cronograma.
- Hacer una **prueba de humo de integración en la semana 2**, no en la semana 4, para detectar el escenario
  pesimista temprano.
- Escalar el pedido de credenciales el **día 1** de la semana de integración (mitigación de R-01).

---

## 6.3 Puntos de Función del módulo "Generar certificado PDF"

**Alcance del conteo:** se toma el módulo de emisión completo (RF-03): el alumno solicita, el sistema valida,
genera el PDF, registra la emisión y notifica. Es la unidad funcional que entrega el certificado al usuario.
Si se contara solo el render del PDF, serían 4 PF; se descarta porque dejaría afuera la solicitud, el registro
y la notificación, que son parte del mismo entregable.

**Criterio de pesos (IFPUG):** se asigna complejidad **baja** a todos los componentes porque tienen pocos
datos elementales, una sola tabla referenciada y lógica simple (sin cálculos ni archivos múltiples).

| Componente | Elemento del módulo | Complejidad | Puntos |
|---|---|---|---|
| Entrada Externa (EE) | Formulario de solicitud (tipo de certificado y confirmación) | Baja | 3 |
| Salida Externa (EO) | Certificado en PDF con diseño institucional | Baja | 4 |
| Salida Externa (EO) | Correo de notificación con link de descarga | Baja | 4 |
| Consulta | Consulta del estado de la solicitud | Baja | 3 |
| Archivo Lógico Interno (ALI) | Registro de solicitudes, validación y fecha de emisión | Baja | 7 |
| Archivo de Interfaz Externa (AIE) | Lectura de datos del sistema de alumnos | Baja | 5 |
| **Total** | | | **26 PF** |

**Conversión a esfuerzo:**

```
26 PF × 8 h/PF = 208 horas de desarrollo
```

**Triangulación con los otros métodos:**

- **Juicio experto:** 2 desarrolladores × 40 h/semana × 2,6 semanas ≈ **208 h**. Coincide.
- **Capacidad:** 208 h representan el **43 % de las 480 h de desarrollo** disponibles. El resto se reparte
  entre integración, correcciones, pruebas y documentación.
- **Plazo:** 208 h ÷ 2 devs = 104 h por desarrollador ≈ **2,6 semanas** de trabajo efectivo, dentro de las 6.

> Los PF miden esfuerzo de **desarrollo**. No incluyen diseño UX, testing ni gestión; esos costos se cubren
> con las horas del resto del equipo en el presupuesto.

---

## 6.4 Presupuesto simplificado

### 6.4.1 Personal

Se calcula por hora para evitar el redondeo de "1,5 meses": 6 semanas = 240 h por persona.

| Rol | Personas | Horas | Tarifa/h | Subtotal |
|---|---|---|---|---|
| Desarrollador/a | 2 | 480 | USD 11,25 | USD 5.400 |
| Tester / QA | 1 | 240 | USD 8,75 | USD 2.100 |
| Diseñador/a UX | 1 | 240 | USD 8,75 | USD 2.100 |
| **Total personal** | **4** | **960** | | **USD 9.600** |

### 6.4.2 Infraestructura y herramientas

| Rubro | Cálculo | Subtotal |
|---|---|---|
| Entorno cloud (staging + producción) Node.js / PostgreSQL | USD 150 × 1,5 meses | USD 225 |
| Servicio de correo transaccional | USD 60 × 1,5 meses | USD 90 |
| Dominio + certificado SSL | anual, prorrateado | USD 40 |
| Herramientas (gestión, repositorio, diseño) | plan del equipo | USD 180 |
| **Total infraestructura** | | **USD 535** |

### 6.4.3 Otros costos operativos

| Rubro | Detalle | Subtotal |
|---|---|---|
| Curva de aprendizaje / capacitación | plantillas institucionales de PDF y contrato de la API | USD 300 |
| Pruebas de carga y seguridad | antes del UAT | USD 250 |
| **Total otros** | | **USD 550** |

### 6.4.4 Total y contingencia

```
Subtotal             = 9.600 + 535 + 550        = USD 10.685,00
Contingencia (10 %)  = 10.685,00 × 0,10          = USD  1.068,50
Presupuesto total    = 10.685,00 + 1.068,50      = USD 11.753,50
```

| Concepto | USD |
|---|---|
| Presupuesto estimado | **11.753,50** |
| Presupuesto base del caso | 18.000,00 |
| **Holgura disponible** | **6.246,50 (34,7 %)** |

La diferencia **no es sobrante**: es la reserva que absorbe los riesgos R-01 y R-02 del apartado 5 y cualquier
cambio de alcance aprobado. Se consume solo con registro y justificación.

---

## 6.5 Datos históricos para mejorar la estimación con IA

La IA no reemplaza el cálculo: lo **valida** contra proyectos anteriores y avisa cuando el número se aparta
del patrón histórico. Para eso pediría a la universidad y al equipo:

1. **Duración real vs. estimada** de tareas de proyectos anteriores, para detectar en qué actividades se desvía.
2. **Horas por punto de función** históricas: si fueron 6 h y no 8, las 208 h se ajustan de inmediato.
3. **Esfuerzo real por rol**, para verificar las tarifas y las horas por perfil.
4. **Velocity histórica por sprint**, para pronosticar entregas y detectar subestimaciones.
5. **Cantidad y tipo de errores por fase**, para prever el esfuerzo de corrección y testing.
6. **Factores que generaron desviaciones** en proyectos similares (tecnología heredada, dependencia de terceros,
   requisitos cambiantes): es exactamente el perfil de la integración de este proyecto.
7. **Defectos por punto de función**, para convertir la meta de calidad en un número objetivo.

**Cómo se usaría:** el modelo compara este proyecto con casos parecidos y devuelve un **rango con probabilidad**
(por ejemplo, "80 % de probabilidad de que la integración tarde entre 5 y 8 días"), no una fecha única. El equipo
revisa ese rango, lo contrasta con el PERT y decide. Todo dato que se registre ahora (duración, esfuerzo, defectos)
mejora la estimación del próximo proyecto.

---

## 6.6 Coherencia con el caso y con los otros apartados

| Restricción del caso | Cómo se cumple |
|---|---|
| Plazo de 6 semanas | 30 días hábiles; la tarea crítica ocupa 6,5 días; el módulo de emisión, 2,6 semanas de desarrollo |
| Equipo de 4 personas | 960 h totales; 480 h de desarrollo para 208 h de PF |
| Presupuesto USD 18.000 | Total estimado USD 11.753,50; holgura del 34,7 % |
| Node.js / React / PostgreSQL | No altera el conteo de PF (mide función, no tecnología); solo define tarifas y herramientas |
| Escala 1–10 y sin extracurriculares | Reglas de negocio (RD-02, RD-03): no agregan componentes, ya están dentro del PDF |

| Elemento | Se conecta con |
|---|---|
| Tarea PERT (6,5 días) | RF-02 / RNF-02 del apartado 3 y R-01 del apartado 5; es la tarea crítica del apartado 7 |
| 26 PF y 208 h | Módulo "Generar certificado PDF" (RF-03) |
| Presupuesto 11.753,50 | Presupuesto base de USD 18.000 del alcance |
| Contingencia 10 % | Riesgos R-01 (fuente de deuda) y R-02 (datos académicos) |
| Datos históricos | Validación con IA y métricas del apartado 8 |

---

## 6.7 Sensibilidad: qué pasa si un supuesto falla

| Supuesto | Si falla | Efecto en la estimación |
|---|---|---|
| 8 h por PF | El equipo rinde 10 h/PF | 260 h (+52 h): sigue dentro de las 480 h, pero se reduce el margen de corrección |
| Tarifas de mercado | Aumentan un 20 % | Personal USD 11.520; total ≈ USD 13.865: todavía por debajo de USD 18.000 |
| La deuda está en el sistema de alumnos (S-01) | Está en Tesorería | Segunda integración: +80 h y riesgo directo sobre las 6 semanas (cambio de alcance) |
| Credenciales disponibles en la semana prevista | Se demoran 10 días | La tarea de 6,5 días se duplica y se corre el hito de integración (R-01) |

---

## 6.8 Conclusión de la estimación

El proyecto es **viable en plazo y costo**: la tarea más incierta entra en 6,5 días con un rango de 5 a 8,
el módulo de emisión demanda 208 h de las 480 disponibles y el presupuesto total (USD 11.753,50) deja una
holgura de USD 6.246,50 frente al techo de USD 18.000. El riesgo no está en el volumen de trabajo, sino en la
**dependencia de terceros** para la integración: por eso el PERT se concentra ahí y la contingencia queda
reservada para ese escenario.
