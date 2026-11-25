---
trigger: always_on
description: Restricciones académicas, privacidad y fidelidad de la interfaz de EduGrade Flow.
---

# Invariantes de EduGrade Flow

- **Objetivo único del producto:** secretaría configura grupos, alumnos, materias, maestros y periodos; maestro captura y envía calificaciones; sistema valida; secretaría revisa y solicita correcciones o valida; se generan acta por grupo/materia y boleta por alumno en Excel. No añadir módulos escolares ajenos sin solicitud expresa.
- La aplicación actual fue documentada como MVP simulado: no atribuir persistencia, autenticación ni exportación real antes de verificarlas.
- **Privacidad:** solo datos ficticios/anonimizados en código, pruebas, capturas, documentación y repositorio público. La futura aplicación con datos reales exige control de acceso y protección diseñados y aprobados antes de incorporarlos.
- Seguir `docs/07-validaciones.md`, `docs/05-modelo-datos.md` y `docs/03-requerimientos.md` para reglas de escalas, ventanas, periodos, unicidad y asignaciones; no interpolar reglas de negocios desconocidas.
- Escalas documentadas: `secundaria` 1–10 y `preparatoria` 0–100; situaciones de Inglés por nivel deben conservar el grupo oficial en reportes, sujeto al contrato de datos vigente.
- La interfaz debe permanecer en español, institucional, orientada al trabajo administrativo, según `docs/12-ai-ui-rules.md`. Priorizar claridad de tablas y validaciones antes que decoración.
- Revisión independiente por orquestador: una declaración de "pruebas pasadas" sin evidencia no es un gate aprobado.
