# EduGrade Flow — Backlog propuesto (NO AUTORIZA implementación)

| ID | Objetivo | Estado | Gate / Evidencia actual |
|---|---|---|---|
| SET-01 | Instalar y verificar configuración Antigravity de dos roles | GATE_TECNICO_APROBADO | Reglas, skill y `edugrade-implementer` verificados en lectura (`PILOT-01`) y escritura (`FIX-TS-01`) |
| FIX-TS-01 | Corregir 2 errores `TS2322` preexistentes en `revision/page.tsx` y `Button.tsx` | GATE_TECNICO_APROBADO / PENDIENTE_VALIDACION_MANUAL | `lint` (`0`), `tsc` (`0`) y `build` (`0`) reproducidos por Orquestador; diff de 2 líneas |
| ENV-01 | Verificar ejecución local interactiva en navegador | PENDIENTE | Build estático en verde; falta validación interactiva (`npm run dev`) si se autoriza |
| PLAN-01 | Contrastar requisitos de secretaría con repo, preparar fases aprobables | PROPUESTO | Documento/plan revisado por Usuario + ChatGPT |
| DATA-01 | Persistencia y modelo académico real | NO AUTORIZADO | Pruebas de persistencia y validación de datos pertinentes |
| FLOW-01 | Flujo maestro → secretaría con correcciones y aprobación | NO AUTORIZADO | Integración real y pruebas de permisos/estados |
| XLSX-01 | Actas por grupo/materia y boletas por alumno en Excel | NO AUTORIZADO | Archivos `.xlsx` correctos con datos ficticios y pruebas |

**Nota:** las fases propuestas no son compromisos técnicos ni elección de stack. No asumir base de datos, autenticación o librería de Excel antes de evaluar y aprobar alternativas.
