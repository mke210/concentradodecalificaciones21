# Concentrado de Calificaciones 21

Plataforma web de la **Esc. Sec. Gral. "21 de Noviembre"** para que cada docente capture sus calificaciones por trimestre, descargue el concentrado en el formato oficial de Excel y la dirección vea estadísticas de aprobación en tiempo real.

Es un solo archivo (`index.html`) que usa Firebase Authentication y Realtime Database (proyecto `registro-de-calificaciones-21`).

## Roles

| Rol | Qué puede hacer |
|---|---|
| **Administrador** (elprofechan@gmail.com) | Todo lo del docente + configurar la escuela, las secretarías, los docentes, las asignaciones, las cuentas y las listas de alumnos |
| **Docente** | Ve solo sus grupos, captura calificaciones, ER, inasistencias y conducta de cada trimestre, importa su Excel y descarga el concentrado vacío o lleno |
| **Dirección** (melchor21@21nov.com) | Solo ve las estadísticas y el avance de captura. Puede filtrar por profesor, grado, grupo, asignatura, tipo y sexo, imprimir y exportar a Excel |
| **Secretaría** | Descarga los concentrados de la letra de grupos que atiende (A, B, C…) |

## Puesta en marcha (una sola vez)

1. **Firebase → Authentication → Método de acceso**: activa **Correo electrónico/contraseña**.
2. **Firebase → Realtime Database → Reglas**: copia todo el contenido de `database.rules.json`, pégalo y presiona **Publicar**.
3. **GitHub**: sube `index.html`, `database.rules.json` y `README.md` al repositorio `concentradodecalificaciones21`. En *Settings → Pages* elige la rama `main` y la carpeta `/ (root)`. La dirección será `https://TU-USUARIO.github.io/concentradodecalificaciones21/`.
4. **Firebase → Authentication → Configuración → Dominios autorizados**: agrega `TU-USUARIO.github.io`.
5. Entra con **elprofechan@gmail.com** y tu contraseña. La primera vez la cuenta se crea sola como administrador y se carga el catálogo de los 30 docentes del horario.
6. El subdirector entra con **melchor21@21nov.com** y su contraseña. La primera vez su cuenta se crea sola con el rol de Dirección.

> Las contraseñas **no** están escritas en el código (el repositorio es público). Cada quien puede cambiar la suya en **Configuración**.

## Primeros pasos del administrador

1. **Administración → Datos → Alumnos desde Credenciales**: sube el respaldo JSON de la base de Credenciales. Se crean las listas de todos los grupos con nombre, grado, grupo y matrícula. No se copian domicilios, teléfonos, tutores, fotos ni datos médicos. El turno de cada grupo también se toma de ahí. Las listas de alumnos no van en el código (el repositorio es público): se cargan desde este archivo.
2. **Administración → Docentes → Dar de alta accesos**: tú escribes el correo y la contraseña de cada docente; también hay un botón que genera contraseñas de 6 dígitos. Al terminar se muestran los datos para copiarlos o enviarlos por WhatsApp. La contraseña no se guarda en la plataforma.
3. **Administración → Secretarías**: escribe el nombre completo de cada secretaría (Víctor = A, Julia = B, Zulma = C, Daza = D, Lafit = E, Ruth = F, Leonor = G, Carmelita = H, Carlos = I). Ese nombre sale en el renglón **ADMVO.**
4. **Administración → Docentes → Eliminar**: cuando hay cambios de personal, quitas al docente y su acceso. Sus concentrados (con lo capturado) pueden pasar al docente que lo sustituye, o eliminarse.
5. **Administración → Escuela**: tamaño de hoja del concentrado (Carta por defecto, u Oficio). Cada grupo sale en su propia hoja.
6. **Administración → Usuarios → Nueva cuenta**: crea las cuentas de las secretarías con el rol *Secretaría* y su letra.

**Orden oficial de las listas (secretarías):** en Administración → Datos, “Cargar orden oficial” recibe un archivo de texto con el orden de las listas impresas (una línea con el grupo, por ejemplo 3A, y debajo los alumnos, uno por renglón). Muestra un resumen por grupo (reconocidos, no encontrados y los que están en la plataforma pero no en la lista) y, al aplicar, todos los concentrados de ese grupo quedan en ese orden. Solo se guarda un número de lugar en cada alumno: las calificaciones no se mueven ni se pierden. Los alumnos que falten en la plataforma no se crean; los que no vienen en la lista quedan al final. El archivo con nombres no debe subirse al repositorio.

**Historial de cambios:** registra solo los cambios que se hacen **después de que un trimestre quedó bloqueado** (al imprimir, al descargar el Excel o al empezar el siguiente trimestre). La captura normal antes del bloqueo no se registra. De cada cambio queda la fecha y hora, quién lo hizo (docente o administrador), el concentrado, el alumno, qué cambió y el valor anterior y el nuevo: calificaciones, ER, inasistencias, conducta, “Rellenar/Quitar 0 / B” e importaciones de Excel en el trimestre bloqueado. También quedan los bloqueos y desbloqueos. Si el administrador desbloquea un trimestre, las correcciones que haga el docente mientras está abierto también se registran, hasta que se vuelve a bloquear. Los cambios a la lista, el orden, el nombre o sexo del alumno y la secretaría se registran cuando el concentrado ya tiene algún trimestre bloqueado. El administrador ve todo en “Historial de cambios”, con filtros por docente, concentrado, tipo, persona, fechas y alumno, y lo puede imprimir o exportar a Excel. Cada docente ve los cambios de sus concentrados, incluidas las correcciones del administrador, en el mismo menú o con el botón “Historial” de cada hoja. Los registros no se pueden modificar ni borrar desde la plataforma, salvo el administrador al iniciar un nuevo ciclo.

**Nuevo ciclo escolar:** en Administración → Datos, “Borrar e iniciar nuevo ciclo” borra las calificaciones (con ER, faltas, conducta y bloqueos), los grupos de cada docente y las listas de alumnos, y cambia el ciclo escolar. Se puede elegir qué se borra. Las cuentas, los docentes, las secretarías y los datos de la escuela se conservan. Para confirmar hay que escribir BORRAR; conviene descargar antes el respaldo.

**Datos de ejemplo (para probar):** en Administración → Datos, “Cargar datos de ejemplo” llena los 27 grupos con 7 asignaturas por grado. Incluye calificaciones de los tres trimestres, aprobados, reprobados, ER, faltas y conductas R/D, con docentes marcados “(EJEMPLO)”, para que la dirección vea las estadísticas. Si el grupo ya tiene su lista de Credenciales, se usan esos alumnos. “Eliminar datos de ejemplo” lo borra todo sin tocar lo que capturen los docentes.

**Informe trimestral (dirección y administrador):** es el formato “Análisis de la información del trimestre” (aprobados, reprobados y promedio de aprovechamiento). Trae un renglón por profesor, asignatura, grado y grupo, con existencia, número y porcentaje de aprobados y reprobados y promedio de grupo; en los talleres, cada grupo sale por separado. Se elige el trimestre (1°, 2°, 3° o final) y el turno (matutino, mixto o ambos). Se revisa en pantalla y se imprime o se descarga en Word (.docx, carta horizontal, con el encabezado y los títulos de columna en cada página). Los renglones del encabezado, el lugar, la fecha y las firmas se editan en “Datos del encabezado y firmas”; también se puede subir el logotipo institucional que va a la izquierda.

## Primeros pasos del docente (Mis grupos)

1. Confirma su **nombre completo** (sale en PROFR.).
2. Registra **sus grados y grupos**: elige la asignatura o el taller, el grado y los grupos. Se crea un concentrado (una hoja tamaño carta) por cada grupo, tanto en asignaturas como en talleres. En los talleres, el docente elige en cada grupo a sus alumnos. Los talleres que antes juntaban grupos (1° "A Y B") se separan solos en 1° A y 1° B, conservando alumnos, calificaciones y bloqueos. El horario de la escuela se le sugiere y lo puede agregar con un botón.
3. Elige **su o sus secretarías**: para cada concentrado, quién lo recibe. Ese nombre sale en ADMVO. de ese grado y grupo. En una asignatura, por defecto es la secretaría que atiende ese grupo.

Si dos docentes registran la misma asignatura en el mismo grupo, la plataforma lo impide y avisa quién lo tiene.

## Cómo funciona la captura

- Al abrir un grupo se ve la **hoja con el formato oficial** del concentrado: encabezado, columnas 1°/ER/2°/ER/3°, PROM. FINAL, inasistencias, conducta, los renglones de HOMBRES a PROMEDIO y las firmas. Se escribe directo en la hoja y se guarda solo.
- **Trimestre**: se elige 1°, 2° o 3°; en la hoja se iluminan las columnas de ese trimestre (calificación y ER, y su inasistencia y conducta). Solo se capturan las columnas de ese trimestre y de los anteriores. **Imprimir** y **Excel** sacan la hoja con lo capturado hasta ese trimestre; el 3° incluye el promedio final.
- **Calificaciones enteras del 5 al 10** (también en ER). Los porcentajes se redondean a entero. El promedio del grupo se trunca a un decimal (8.19 → 8.1).
- **ER (examen de recuperación)** en el 1° y 2° trimestre: se habilita solo si la calificación es menor a 6. Si se escribe una calificación en ER, esa es la que cuenta aunque no sea aprobatoria, y la calificación normal queda bloqueada. Ejemplos: 5 con ER 6 cuenta 6; 5 con ER 5 cuenta 5. Para corregir la calificación normal, primero se borra el ER.
- **Promedio final** del alumno: promedio de los tres trimestres, tomando el ER cuando lo hay, truncado a un decimal (8.33 → 8.3; 5.67 → 5.6, reprobado; 6, 6 y 6 → 6). En el renglón PROMEDIO, la columna PROM. FINAL muestra el promedio final del grupo: el promedio de los promedios del 1o, 2o y 3er trimestre.
- **Conducta**: E, MB, B, R y M (mala). La **M** aparece en rojo en la hoja, en la impresión y en el Excel.
- **Bloqueo de trimestres**: antes de **Imprimir** o descargar el **Excel** de un trimestre aparece un aviso para revisar las calificaciones. Si el docente acepta, lo ya capturado de ese trimestre (y de los anteriores) queda bloqueado. Con “Cancelar y revisar” no se bloquea nada. Al capturar la primera calificación del 2o trimestre se bloquea el 1o, y al empezar el 3o se bloquea el 2o (también con aviso). En un trimestre bloqueado el docente solo puede llenar casillas vacías (por ejemplo el ER). El administrador puede corregir las calificaciones bloqueadas o desbloquear el trimestre con “🔓 Desbloquear”. Las reglas de la base de datos también lo impiden, no solo la pantalla.
- **Mi lista de alumnos**: en las asignaturas, la lista del grupo se carga sola (de Credenciales). En los talleres, el docente elige a sus alumnos de cada grupo y se quedan guardados. En ambos puede moverlos de orden (↑ ↓), regresarlos al orden alfabético o quitarlos (✕).
- **Importar Excel**: lee un concentrado con el formato oficial y reconoce a los alumnos aunque el nombre esté en otro orden o con otra ortografía.
- El **sexo** se estima por el nombre (Credenciales no lo trae); se corrige con el botón H/M junto al nombre.
- **Excel vacío**: el formato con nombres y con las fórmulas listas, para llenarlo a mano.

## Estructura de la base de datos

```
config/                 encabezado, ciclo, turnos por letra, secretarias {A..I}
docentes/{id}           nombre, alias, admvoTaller, email
asignaciones/{id}       docenteId, materia, grado, grupos "A,B", tipo regular|taller, turno?, admvo?
alumnos/{grado+grupo}/{id}   nombre, sexo H|M, matricula?, baja?
miembros/{asignacion}/{alumno}  "1A"   (integrantes de talleres)
calif/{asignacion}/{alumno}     t1 er1 t2 er2 t3 · i1 i2 i3 · c1 c2 c3
usuarios/{uid}          email, nombre, rol, docenteId?, esProfesor, letra?
solicitudes/{uid}       cuentas sin rol que pidieron acceso
bloqueos/{asignacion}/{trimestre}   fecha y quién bloqueó
historial/{asignacion}/{id}         t, quien, campo, alumno, antes, despues, detalle
```

Las reglas permiten que cada docente escriba solo en sus asignaciones. La dirección y las secretarías solo leen. Los alumnos y las calificaciones nunca se borran al dar de baja.

---
powered by elprofe chan
