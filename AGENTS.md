<!-- BEGIN:nextjs-agent-rules -->
# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` before writing any code. Heed deprecation notices.
<!-- END:nextjs-agent-rules -->

<!-- EDUGRADE-ANTIGRAVITY-V1 BEGIN -->

## EduGrade Flow — coordinación de desarrollo con Antigravity (v1.0)

Este repositorio es **EduGrade Flow**, una automatización de captura, revisión y generación de actas/boletas; **no** es TrackFlow. Conserva las reglas de Next.js que aparecen más arriba y todas las restricciones del repositorio.

### Fuente de verdad y contexto

- Antes de planificar: leer `.agents/state/STATUS.md` y `.agents/state/HANDOFF.md`, y consultar `.agents/state/DECISIONS.md` si hay decisiones relevantes.
- Verificar `git status`, rama, cambios sin seguimiento y baseline antes de ejecutar modificaciones. No afirmar que el estado documentado coincide con la máquina sin comprobarlo.
- Para la tarea concreta leer únicamente las secciones pertinentes de `README.md`, `docs/03-requerimientos.md`, `docs/05-modelo-datos.md`, `docs/07-validaciones.md`, `docs/08-roadmap.md`, `docs/12-ai-ui-rules.md` y código afectado. Los documentos representan requisitos o historia; el código y las pruebas demuestran implementación.
- Activar el procedimiento `.agents/skills/edugrade-orchestration/SKILL.md` para tareas de desarrollo con varias fases, delegación, revisión, cierre o handoff.

### Autoridad y roles

- Usuario + ChatGPT: autorizan alcance, arquitectura, criterios de aceptación, cambios sensibles, operaciones Git de escritura y aceptación funcional final.
- **ORQUESTADOR** (agente principal; puede seleccionarse `edugrade-orchestrator`): prepara el baseline, define unidades verificables, delega al único `edugrade-implementer`, revisa por sí mismo los diffs/pruebas y clasifica gates. No implementa cambios funcionales directamente por comodidad.
- **IMPLEMENTADOR** (subagente `edugrade-implementer`): modifica exclusivamente archivos delegados, ejecuta pruebas proporcionadas o proporcionadas por el proyecto y entrega un handoff. No declara finalización global.
- No se añade un tercer agente de QA. La independencia del QA se logra porque **el orquestador vuelve a inspeccionar y reproducir** las pruebas, no porque el implementador apruebe su propio trabajo.
- La aprobación de un plan completo permite avanzar entre unidades aprobadas que pasan sus gates, sin microautorizaciones repetitivas. No concede autorización fuera de alcance.

### Límites y evidencia

- Nunca implementar sobre `main`: las ramas, cambios de rama, staging, commits, push y merge requieren acción o autorización específica del usuario.
- No introducir en código, fixtures, estado, logs o commits nombres reales, CURP, calificaciones reales, correos reales, tokens, contraseñas ni datos sensibles de alumnos o docentes. Utilizar datos ficticios.
- No modificar esquema, dependencias, arquitectura, datos persistidos o archivos protegidos fuera del alcance autorizado. Detenerse ante riesgo de borrado/corrupción, contrato contradictorio o baseline incompatible.
- Respetar las reglas académicas exactas de `docs/05-modelo-datos.md` y `docs/07-validaciones.md` y de UI de `docs/12-ai-ui-rules.md`; no sustituirlas por suposiciones.
- Una demo en `useState`, una prueba con mocks o `npm run lint` exitoso **no equivale** a persistencia real, integración, exportación `.xlsx` ni aceptación manual.
- QA proporcional al riesgo: comprobar diff, archivos nuevos, rutas positivas y negativas pertinentes, pruebas con comandos/resultados/exit codes y límites explícitos. `SKIP`/`XFAIL` no son `PASS`.
- Los agentes pueden corregir errores ordinarios dentro del alcance y repetir pruebas, pero no suavizar validaciones ni cambiar criterios para conseguir un PASS.
- Al cerrar una unidad, actualizar `.agents/state/STATUS.md`, `.agents/state/BACKLOG.md` (si aplica) y `.agents/state/HANDOFF.md` con hechos verificados. Registrar únicamente decisiones **aprobadas** en `DECISIONS.md`; no incluir secretos.
- El estado `GATE_TECNICO_APROBADO` no sustituye `PENDIENTE_VALIDACION_MANUAL` ni la aprobación del usuario.

<!-- EDUGRADE-ANTIGRAVITY-V1 END -->
