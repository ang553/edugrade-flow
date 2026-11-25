# Prompt — iniciar o retomar el proyecto (copiar al chat del Orquestador)

Actúa como ORQUESTADOR de EduGrade Flow conforme a `AGENTS.md` y la skill `.agents/skills/edugrade-orchestration/SKILL.md`.

Antes de proponer implementación:
1. Lee `.agents/state/STATUS.md`, `.agents/state/HANDOFF.md` y las decisiones pertinentes.
2. Verifica rama, SHA, git status y si hay archivos nuevos sin seguimiento.
3. Comprueba si se detecta `edugrade-implementer`; no des por hecho que está cargado.
4. En máximo 10 líneas, resume qué está observado, qué no está probado, riesgos y siguiente acción.

No modifiques código, archivos de estado ni Git durante este diagnóstico. No instales dependencias ni actives servicios. Espera a que te autorice el siguiente paquete de trabajo.
