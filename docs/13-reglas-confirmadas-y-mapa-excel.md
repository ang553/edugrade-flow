# EduGrade Flow — Reglas confirmadas y mapa de Excel

**Estado:** documento de consolidación, pendiente de revisión e integración al repositorio.
**Fecha de referencia:** 24 de noviembre de 2026.
**Finalidad:** preservar las decisiones de negocio ya acordadas y los hallazgos estructurales del Excel de referencia; distinguir hechos confirmados de decisiones aún pendientes.

## 1. Problema y alcance (confirmados)

Se busca sustituir la repetición de formularios alumno por alumno y la revisión/transcripción manual que secretaría realiza para generar actas y boletas. El alcance es exclusivamente:

1. Secretaría configura ciclo escolar, periodos, grupos oficiales, alumnos, materias y asignaciones docentes; asigna niveles de inglés cuando aplique.
2. Maestro accede únicamente a lo que tiene asignado, captura o pega calificaciones y envía.
3. El sistema calcula, valida y guarda la información.
4. Secretaría consulta pendientes/errores/duplicados, solicita correcciones y valida.
5. Secretaría genera **acta de grupo y materia** y **boleta individual por alumno**, en Excel.

No incluir pagos, asistencia como módulo independiente, gestión escolar integral ni funcionalidades ajenas a ese flujo. Las **inasistencias como campo de captura y del documento** sí forman parte del alcance.

Fuentes del repositorio: `docs/01-problema.md`, `docs/02-flujo-actual.md`, `docs/03-requerimientos.md`, `docs/04-flujo-propuesto.md`.

## 2. Reglas de negocio ya establecidas

| Área | Regla consolidada |
|---|---|
| Roles | Secretaría/Admin configura, revisa, valida y puede autorizar excepciones; maestro captura sus asignaciones. |
| Captura por periodo | La ventana depende de **ciclo escolar + trimestre + nivel educativo**: secundaria y preparatoria pueden tener aperturas/cierres distintos. |
| Escalas | **Secundaria: 1–10**; **Preparatoria: 0–100**. Los rangos deben validarse en el servidor al persistir. |
| Criterios actuales | Inasistencias, participación, proyecto, trabajos y examen. Calificación final = participación + proyecto + trabajos + examen; **inasistencias no se suma**. |
| Pegado desde Excel | Permite bloques por filas; el orden en la demo es inasistencias, participación, proyecto, trabajos, examen. Deben revisarse errores, alineación de alumnos y celdas faltantes. |
| Duplicados | Una sola calificación válida por **alumno + materia + trimestre + ciclo escolar**; conservar el grupo oficial como dato para reportes. |
| Excepciones | Los periodos cerrados o capturas ya enviadas no deben editarse libremente; secretaría autoriza correcciones controladas. |
| Revisión administrativa | Secretaría debe ver capturas por grupo, maestro, materia, estado y alumno, con validación masiva únicamente de registros elegibles. |
| Inglés por niveles | Se captura según **nivel de inglés**, sin perder el **grupo oficial** de cada alumno. Acta agrupa por grupo oficial y boleta muestra la materia como **Inglés**. |
| Baja en preparatoria | La demo advierte sobre final menor a 60 y deja confirmar al maestro; **esto es una advertencia, no una invalidación automática ni un umbral institucional de aprobación confirmado**. |
| Salidas | **Acta por grupo/materia** y **boleta individual por alumno**, ambos archivos `.xlsx`. |

Fuentes: `docs/03-requerimientos.md`, `docs/05-modelo-datos.md`, `docs/07-validaciones.md` y decisiones documentadas de la demo.

## 3. Evidencia estructural del libro de referencia

**Fuente privada:** `3A CALIFICACIONES 2025-2026.xlsx` (no incluir en repositorio público).

El libro inspeccionado contiene dos hojas: una **ACTA** y una **BOLETA INTERNA individual** (la pestaña individual tiene un nombre propio que no se reproduce aquí).

### ACTA — estructura observada

- Título: **Reporte de calificaciones**.
- Encabezado: maestro, materia, grupo, periodo, ciclo y fecha.
- Tabla: número de lista, **Alumno**, **Inasistencias**, **Participación**, **Proyecto**, **Trabajos**, **Examen**, **Calificación**.
- En esta muestra aparecen 34 renglones numerados de alumnos.
- Incluye promedio de calificaciones y espacios para firma de dirección y maestro.
- La celda de promedio usa una fórmula AVERAGE; la fecha usa TODAY.

### BOLETA — estructura observada

- Título: **Boleta interna**.
- Datos generales de alumno, grupo, ciclo escolar y fecha.
- Materias y columnas de **I, II y III trimestre**, **calificación ordinaria** y **faltas** por trimestre.
- Fila de promedios; sección de conducta; espacio para nombre y firma de tutor/padre.
- Algunas fórmulas calculan promedios de trimestres.
- Se lee el texto **“La calificación mínima aprobatoria es 70”**. Es una regla impresa en esta boleta de referencia; **no asumir automáticamente que se aplica a todos los niveles sin verificarlo**.

### Advertencia técnica sobre el archivo

Hay **rangos con nombre que apuntan a otros libros** (`[1]BD` y `[2]BD`). No es seguro tratar el `.xlsx` recuperado como generador autónomo sin resolver esas dependencias. Para EduGrade Flow debe crearse un proceso de exportación sustentado en datos validados y una plantilla segura/anónima, sin depender de conexiones externas del archivo original.

## 4. Pendientes por confirmar antes de codificar Excel definitivo

Estos puntos **no están aprobados por el mero hecho de aparecer en la plantilla**:

- Reglas exactas de **redondeo, decimales, promedio y calificación ordinaria** por nivel y trimestre.
- Aplicabilidad del umbral **70 aprobatorio** a secundaria, preparatoria o sólo al formato mostrado.
- Si las dos plantillas recuperadas son **formatos definitivos** o ejemplos de trabajo de secretaría.
- Si el acta requiere filas variables, impresión, tamaño, nombres de firma y rangos por grupo.
- Fuente y tratamiento de **reporte de conducta**, faltas por trimestre y campos vacíos en la boleta. No agregar un módulo independiente de conducta/asistencia.
- Necesidad y formato de otras fórmulas/plantillas originales externas vinculadas desde el archivo.

## 5. Protección de datos y ubicación

- **No incluir el Excel original en un repositorio público**: puede contener nombres, datos escolares y vínculos a otros archivos.
- Conservar el original por separado en almacenamiento privado autorizado; nunca usarlo como fixture de pruebas públicas.
- Documentar la estructura en este `.md` sin nombres ni calificaciones de personas.
- Si se necesita un `.xlsx` dentro del repositorio, crear **una plantilla nueva completamente ficticia y sin vínculos externos**, revisada antes de commitear.
- No mezclar datos reales con datos ficticios en desarrollo público.

## 6. Consecuencia para el plan de desarrollo

1. Completar `FIX-TS-01` y validar el orquestador Antigravity.
2. Resolver las **reglas pendientes** para la generación fiel de ACTA y BOLETA.
3. Construir un recorrido real mínimo con un grupo ficticio: configuración → captura guardada → revisión → Excel acta.
4. Completar autenticación/permisos, correcciones, inglés por niveles y boleta real.
5. Probar precisión con ejemplos ficticios y registrar evidencia del ahorro de tiempo para el portafolio.

**Nota:** este documento no sustituye la documentación existente ni autoriza cambios técnicos, commits o subida del Excel privado. Sirve como anexo de reglas y fuente de referencia para revisión humana.
