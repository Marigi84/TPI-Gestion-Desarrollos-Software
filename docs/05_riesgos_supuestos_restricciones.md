# 5. Riesgos, supuestos y restricciones – SGCA

## 5.1 Supuestos

### S-01. Disponibilidad de información de deudas

Se asume que la información de deudas administrativas estará disponible y podrá ser consultada por el SGCA en modo lectura durante el procesamiento de las solicitudes.

### S-02. Disponibilidad de información académica

Se asume que el sistema de alumnos dispondrá de la información académica necesaria para generar el certificado analítico parcial, incluyendo materias, calificaciones e identificación de materias extracurriculares.

---

## 5.2 Riesgos

| ID | Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|---|
| R-01 | Que la información de deudas administrativas no esté disponible, se encuentre desactualizada o no pueda ser consultada correctamente durante la integración. | Media | Alto | Validar en las primeras etapas del proyecto cuál es la fuente oficial de la información, quién es responsable de mantenerla actualizada y cómo será consultada por el SGCA. Realizar pruebas tempranas de integración. |
| R-02 | Que el sistema de alumnos no provea todos los datos académicos necesarios o no permita identificar correctamente las materias extracurriculares y las calificaciones requeridas para generar el analítico parcial. | Media | Alto | Verificar tempranamente la estructura y disponibilidad de los datos académicos, acordar con el área de Sistemas la identificación de materias extracurriculares y validar con Secretaría Académica las reglas necesarias para generar el certificado. |

---

## 5.3 Restricciones

### RE-01. Plazo

El proyecto deberá completarse dentro de un plazo máximo de **6 semanas**.

### RE-02. Tecnología

El desarrollo deberá realizarse utilizando obligatoriamente **Node.js para el backend, React para el frontend y PostgreSQL como base de datos**.

---

## 5.4 Relación entre supuesto, riesgo y restricción

Se supone que la información de deudas administrativas estará disponible y podrá ser consultada por el SGCA. Si este supuesto no se cumple, surge el riesgo de no poder validar correctamente si un alumno está habilitado para obtener su certificado.

Esta situación se agrava por la restricción de contar con un plazo máximo de seis semanas, ya que cualquier demora en resolver el acceso, disponibilidad o calidad de estos datos puede afectar directamente el cronograma del proyecto.
