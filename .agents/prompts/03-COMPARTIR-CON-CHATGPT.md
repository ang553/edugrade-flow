# Prompt — preparar un resumen portable para otro chat

Quiero revisar una decisión de EduGrade Flow con ChatGPT en otra conversación.

Sin cambiar código ni Git, presenta un handoff breve con: objetivo aprobado, rama y SHA observados, archivos cambiados y razón, pruebas (comando/resultado/exit code), decisiones abiertas, bloqueos, riesgos y primera acción para retomar.

Utiliza `.agents/state/HANDOFF.md` si está actualizado, pero contrástalo con Git y el código actual. No confundas estados documentados con evidencia.

No incluyas datos personales reales, secretos ni variables de entorno. Identifica los fragmentos/diffs adicionales que debo compartir para que otro chat pueda revisar el caso sin reconstruir toda la historia.
