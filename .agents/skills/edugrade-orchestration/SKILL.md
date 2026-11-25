---
name: edugrade-orchestration
description: Protocolo de ejecución con orquestador e implementador en EduGrade Flow. Utilizar para planificar entregas, delegar, aplicar gates de QA, documentar decisiones y preparar handoffs entre sesiones o para otros chats.
---

# Protocolo operativo EduGrade V1 — inspirado en TrackFlow V2.1

## Prioridades

1. Instrucciones explícitas y alcance aprobado por Usuario + ChatGPT.
2. `AGENTS.md` y `.agents/rules/edugrade-domain.md` del repo.
3. Contratos del proyecto (`docs/03-requerimientos.md`, `docs/05-modelo-datos.md`, `docs/07-validaciones.md`, `docs/12-ai-ui-rules.md`) en su ámbito.
4. Estado y decisiones de `.agents/state/`, contrastados con código, Git y pruebas reales.

Un documento que describe una función no prueba que exista. En caso de conflicto, no inventar una resolución: elevar la decisión.

## Bootstrap de sesión

1. Leer `STATUS.md` y `HANDOFF.md`; revisar `DECISIONS.md` si aplica.
2. Inspeccionar `git status --short --branch`, `git log -1 --oneline`, diffs y archivos sin seguimiento; confirmar la rama y el baseline.
3. Identificar objetivo actual, condiciones autorizadas, riesgos y dependencias. No repetir una auditoría completa de código salvo que el contexto cambie materialmente.
4. Si `node_modules` no existe, informar que no se pueden verificar las guías locales de Next.js 16, lint, build o pruebas aún; proponer `npm ci` con autorización para preparar el entorno.

## Plan con gates (solo después de aprobación)

Para cada paquete define:

- ID estable y **resultado funcional** esperado (no una colección artificial de microtareas).
- Archivos permitidos y prohibidos; dependencias; riesgo y datos sensibles.
- Contratos/invariantes aplicables.
- Caso positivo y negativo representativos.
- Pruebas técnicas y aceptación manual exigible; condiciones de salida.

La aprobación global de un plan permite ejecutar las fases dentro del alcance y avanzar cuando su gate pasa. No aprueba cambios de arquitectura, datos, permisos, dependencias o alcance no contemplados.

## Delegación a implementador

Invocar `edugrade-implementer` mediante el mecanismo nativo `invoke_subagent` cuando esté disponible, dando un brief autocontenido. No asumir que comparte historial conversacional. Delegación secuencial, mismo workspace solo si hay exclusividad de escritura; no usar paralelismo al inicio.

**Contrato del brief:** `ID | objetivo | baseline | archivos permitidos/prohibidos | documentación relevante | invariantes | positivo/negativo | tests | entrega`. Prohibir Git de escritura y cambios de estado por el implementador.

Si el runtime carece de `invoke_subagent`, NO fingir una delegación: trabajar de modo único bajo las mismas reglas o solicitar que se verifique la personalización, dejando registrado el límite.

## QA adversarial por el orquestador

- Inspeccionar código y diff **por cuenta propia**, incluidos untracked.
- Ejecutar o reproducir verificaciones materiales y registrar resultados exactos; evaluar caminos positivo y negativo proporcionados al riesgo.
- `npm run lint`, `npx tsc --noEmit` y `npm run build` son ejemplos de chequeos técnicos cuando exista entorno, **no sustituyen** pruebas de flujo de guardado/revisión/Excel ni UI interactiva.
- Los fakes prueban comportamiento simulado, no persistencia, integración ni control real de permisos.
- No declarar integración o aceptación manual sin evidencia. Un bloqueo de entorno es `BLOQUEADO_ENTORNO`, no un PASS.
- Corregir dentro del alcance a través del implementador, repetir validación afectada y regresión proporcional. Escalar decisiones arquitectónicas, datos o permisos.

## Gates y resultados

Usar solo cuando corresponda: `IMPLEMENTADO`, `VALIDADO_SIMULADO`, `VALIDADO_INTEGRACION_REAL`, `GATE_TECNICO_APROBADO`, `PENDIENTE_VALIDACION_MANUAL`, `BLOQUEADO_FALLO_TECNICO`, `BLOQUEADO_ENTORNO`, `BLOQUEADO_AUTORIZACION`. No mezclar "implementado" con "validado". `SKIP`/`XFAIL` se documentan, no se cuentan como PASS.

## Handoff y continuidad

Al terminar el bloque autorizado (o al detectar un bloqueo):

1. Actualizar `STATUS.md` con observaciones comprobadas y distinguirlas de propuestas.
2. Actualizar `BACKLOG.md` si cambió una tarea y `DECISIONS.md` únicamente con decisiones aprobadas.
3. Actualizar `HANDOFF.md` (breve y autocontenido, idealmente <100 líneas) con fecha, rama, hash, alcance, cambios, QA exacto, riesgos, aprobaciones pendientes y **primera acción concreta de continuación**.
4. Para compartir con ChatGPT en otro chat, proporcionar el `HANDOFF.md` y solo el diff/evidencia sanitaria pertinente, nunca credenciales ni datos escolares reales.
5. No crear commits ni push. La aceptación manual final pertenece al usuario con ChatGPT.

## Condiciones de detención

- Baseline Git distinto o cambios ajenos incompatibles.
- Riesgo de pérdida/exposición/corrupción de datos.
- Solicitud de credenciales, datos personales, servicios o migración no autorizados.
- Requisito o criterio fuera de alcance, contrato contradictorio o QA obligatorio no demostrable.
- Fallo crítico que no cabe corregir dentro del alcance.

Informar evidencia, impacto, alternativas y autorización necesaria antes de continuar.
