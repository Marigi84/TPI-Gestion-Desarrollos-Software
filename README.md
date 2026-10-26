# SGCA – Sistema de Gestión de Certificados Académicos

## Descripción

El SGCA es un módulo web para una universidad que permite a los alumnos solicitar y descargar certificados académicos en formato PDF.

El sistema contempla dos certificados:

- Certificado de alumno regular.
- Certificado analítico parcial.

Antes de emitir un certificado, el SGCA valida que el alumno no tenga deudas administrativas, consulta la información académica en modo lectura, registra la solicitud y envía una notificación por correo electrónico.

## Tecnologías

- Backend: Node.js
- Frontend: React
- Base de datos: PostgreSQL

## Estructura propuesta del repositorio

- `src/`: código fuente.
- `docs/`: documentación funcional, técnica y de gestión.
- `tests/`: pruebas y evidencias.
- `config/`: archivos de configuración.
- `assets/`: recursos visuales.
- `README.md`: descripción general y acceso inicial al proyecto.

## Documentación principal

La documentación del proyecto se gestiona bajo el enfoque Docs as Code, utilizando Markdown, Git y Pull Requests.

Los principales documentos se encuentran en `docs/` e incluyen alcance, stakeholders, requerimientos, uso de IA, riesgos, estimación, planificación, seguimiento y control, documentación y cierre del proyecto.

## Documentación para el usuario

La Guía Rápida del alumno se encuentra en:

`docs/guia_rapida_alumno.md`

El diagrama del proceso de solicitud se encuentra en:

`docs/diagramas/solicitud_certificado.md`
