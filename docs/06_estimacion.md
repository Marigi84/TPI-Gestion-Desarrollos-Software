# 6. Estimación de tiempos y costos – SGCA

**Proyecto:** Módulo web de solicitud y descarga de certificados académicos

**Plazo del caso:** 6 semanas — 02/11/2026 a 11/12/2026

**Equipo:** 2 desarrolladores, 1 tester, 1 diseñador UX

**Presupuesto base:** USD 18.000 · **Tecnología obligatoria:** Node.js, React, PostgreSQL

---

## 6.1 Base de la estimación

| Parámetro | Valor |
|---|---|
| Plazo | 6 semanas = 30 días hábiles |
| Capacidad del equipo | 4 personas × 40 h/semana × 6 semanas = **960 h** |
| Capacidad de desarrollo | 2 desarrolladores × 240 h = **480 h** |
| Tarifa desarrollador | USD 1.800/mes ÷ 160 h = **USD 11,25/h** |
| Tarifa tester / UX | USD 1.400/mes ÷ 160 h = **USD 8,75/h** |
| Productividad | **8 h por punto de función** (supuesto a validar con históricos) |
| Tecnología | Node.js / React / PostgreSQL (restricción RE-02, apartado 5) |

**Supuestos que sostienen la estimación:**

- **S-01 – Disponibilidad de la información de deudas (apartado 5):** se asume que la deuda
  administrativa está disponible y se puede consultar en modo lectura desde el sistema de alumnos.
  Si el dato está en Tesorería, cambia el alcance y esta estimación.
- **S-02 – Disponibilidad de la información académica (apartado 5):** se asume que el sistema de
  alumnos entrega las materias, las calificaciones y el dato que indica si una materia es
  extracurricular (el que permite excluirla del analítico).
- No se aprueban cambios de alcance durante las 6 semanas.

---

## 6.2 PERT sobre la tarea crítica

**Tarea:** integrar en modo lectura el SGCA con el sistema de alumnos (RF-02 y RNF-02, apartado 3).

**Por qué es la tarea crítica:**

- Es la única fuente para validar deudas y regularidad: sin ella no se emite ningún certificado.
- Depende de un tercero (S03, Área de Sistemas) para los accesos y el formato de los datos.
- Es la de mayor incertidumbre: API heredada, sin documentación completa y equipo sin experiencia previa.

| Escenario | Qué representa | Días |
|---|---|---|
| **Optimista (O)** | Accesos el primer día, API documentada y datos completos | 3 |
| **Más probable (M)** | Coordinación normal con Sistemas para obtener accesos y validar el formato de los datos | 6 |
| **Pesimista (P)** | Accesos demorados, cambios en el contrato de la API y curva de aprendizaje | 12 |

```
TE = (O + 4 × M + P) / 6
TE = (3 + 4 × 6 + 12) / 6
TE = (3 + 24 + 12) / 6
TE = 39 / 6
TE = 6,5 días
```

**Resultado:** la tarea se planifica en **6,5 días**. Es la tarea de la ruta crítica del cronograma
(apartado 7, Planificación): si se extiende, se corre la fecha de cierre del proyecto.

---

## 6.3 Puntos de Función del módulo "Generar certificado PDF"

**Qué se cuenta:** el módulo de emisión completo (RF-03): el alumno solicita, el sistema valida, genera
el PDF, registra la emisión y notifica. Es la unidad funcional que entrega el certificado. Si se contara
solo el render del PDF serían 4 puntos de función, pero quedarían afuera la solicitud, el registro y la notificación.

**Criterio de pesos:** se usa la tabla de IFPUG que presenta el material de la materia: complejidad baja
para componentes con pocos datos, una sola tabla y lógica simple.

| Componente | Elemento del módulo | Complejidad | Puntos |
|---|---|---|---|
| Entrada Externa (EE) | Formulario de solicitud (tipo de certificado y confirmación) | Baja | 3 |
| Salida Externa (EO) | Certificado en PDF con diseño institucional | Baja | 4 |
| Salida Externa (EO) | Correo de notificación con link de descarga | Baja | 4 |
| Consulta | Consulta del estado de la solicitud | Baja | 3 |
| Archivo Lógico Interno (ALI) | Registro de solicitudes, validación y fecha de emisión | Baja | 7 |
| Archivo de Interfaz Externa (AIE) | Lectura de datos del sistema de alumnos | Baja | 5 |
| **Total** | | | **26 puntos de función** |

```
26 puntos de función × 8 h por punto = 208 horas de desarrollo
```

**Contraste con juicio experto:** 2 desarrolladores × 40 h/semana × 2,6 semanas ≈ **208 h**. Coincide.
Esas 208 h representan el **43 % de las 480 h de desarrollo** disponibles; el resto cubre integración,
correcciones, pruebas y documentación.

> Los puntos de función miden esfuerzo de desarrollo. No incluyen diseño UX, testing ni gestión: eso se cubre con las
> horas del resto del equipo en el presupuesto.

---

## 6.4 Presupuesto simplificado

### Personal

Se calcula por hora (6 semanas = 240 h por persona), sin redondear meses.

| Rol | Personas | Horas | Tarifa/h | Subtotal |
|---|---|---|---|---|
| Desarrollador/a | 2 | 480 | USD 11,25 | USD 5.400 |
| Tester / QA | 1 | 240 | USD 8,75 | USD 2.100 |
| Diseñador/a UX | 1 | 240 | USD 8,75 | USD 2.100 |
| **Total personal** | **4** | **960** | | **USD 9.600** |

### Infraestructura y herramientas

| Rubro | Cálculo | Subtotal |
|---|---|---|
| Entorno cloud (staging + producción) Node.js / PostgreSQL | USD 150 × 1,5 meses | USD 225 |
| Servicio de correo transaccional | USD 60 × 1,5 meses | USD 90 |
| Dominio + certificado SSL | anual, prorrateado | USD 40 |
| Herramientas (gestión, repositorio, diseño) | plan del equipo | USD 180 |
| **Total infraestructura** | | **USD 535** |

### Otros costos operativos

| Rubro | Detalle | Subtotal |
|---|---|---|
| Curva de aprendizaje / capacitación | plantillas institucionales de PDF y contrato de la API | USD 300 |
| Pruebas de carga y seguridad | antes del UAT | USD 250 |
| **Total otros** | | **USD 550** |

### Total y contingencia

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

La diferencia no es sobrante: es la reserva para los riesgos R-01 (fuente del dato de deuda) y R-02
(datos académicos incompletos) del apartado 5, y para cualquier cambio de alcance aprobado.

---

## 6.5 Datos históricos para mejorar la estimación con IA

La IA no reemplaza el cálculo: lo valida contra proyectos anteriores. Para eso se pediría:

1. **Duración real vs. estimada** de tareas anteriores, para ver dónde se desvía el equipo.
2. **Horas por punto de función** históricas: si fueron 6 h y no 8, las 208 h se ajustan.
3. **Esfuerzo real por rol**, para verificar las tarifas y las horas de cada perfil.
4. **Velocity histórica por sprint**, para pronosticar entregas.
5. **Errores por fase**, para prever el esfuerzo de corrección y testing.
6. **Factores de desviación** en proyectos similares (tecnología heredada, dependencia de terceros,
   requisitos cambiantes): el perfil exacto de esta integración.
7. **Defectos por punto de función**, para convertir la meta de calidad en un número.

Con esos datos, el modelo devuelve un **rango con probabilidad** (por ejemplo, "80 % de que la
integración tarde entre 5 y 8 días"), no una fecha única. El equipo lo contrasta con el PERT y decide.

---

## 6.6 Coherencia con el caso

| Restricción del caso | Cómo se cumple |
|---|---|
| Plazo de 6 semanas | 30 días hábiles; la tarea crítica ocupa 6,5 días; el módulo de emisión, 2,6 semanas de desarrollo |
| Equipo de 4 personas | 960 h totales; 480 h de desarrollo para 208 h de puntos de función |
| Presupuesto USD 18.000 | Total estimado USD 11.753,50; holgura del 34,7 % |
| Node.js / React / PostgreSQL | No altera el conteo de puntos de función (mide función, no tecnología); solo define tarifas y herramientas |
| Escala 1–10 y sin extracurriculares | Reglas de negocio (RD-02, RD-03): no agregan componentes al conteo |

| Elemento | Se conecta con |
|---|---|
| Tarea PERT (6,5 días) | RF-02 / RNF-02 (apartado 3), R-01 (apartado 5) y la ruta crítica del apartado 7 |
| 26 puntos de función y 208 h | Módulo "Generar certificado PDF" (RF-03) |
| Presupuesto 11.753,50 | Presupuesto base de USD 18.000 (apartado 1) |
| Contingencia 10 % | R-01 y R-02 (apartado 5) |
| Datos históricos | Validación con IA y KPIs del apartado 8 |

---

## 6.7 Conclusión

El proyecto es viable en plazo y costo: la tarea más incierta entra en 6,5 días, el módulo de emisión
demanda 208 h de las 480 disponibles y el presupuesto total (USD 11.753,50) deja una holgura de
USD 6.246,50 frente al techo de USD 18.000. El riesgo no está en el volumen de trabajo, sino en la
dependencia de terceros para la integración.
