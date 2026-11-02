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
5. **Administración → Escuela**: tamaño de hoja del concentrado (Oficio por defecto, o Carta).
6. **Administración → Usuarios → Nueva cuenta**: crea las cuentas de las secretarías con el rol *Secretaría* y su letra.

**Datos de ejemplo (para probar):** en Administración → Datos, “Cargar datos de ejemplo” llena los 27 grupos con 7 asignaturas por grado. Incluye calificaciones de los tres trimestres, aprobados, reprobados, ER, faltas y conductas R/D, con docentes marcados “(EJEMPLO)”, para que la dirección vea las estadísticas. Si el grupo ya tiene su lista de Credenciales, se usan esos alumnos. “Eliminar datos de ejemplo” lo borra todo sin tocar lo que capturen los docentes.

## Primeros pasos del docente (Mis grupos)

1. Confirma su **nombre completo** (sale en PROFR.).
2. Registra **sus grados y grupos**: elige la asignatura o el taller, el grado y los grupos. En una asignatura se crea un concentrado por cada grupo; en un taller, los grupos marcados se juntan en uno solo (p. ej. 3° "A, B Y C"). El horario de la escuela se le sugiere y lo puede agregar con un botón.
3. Elige **su o sus secretarías**: para cada concentrado, quién lo recibe. Ese nombre sale en ADMVO. de ese grado y grupo. En una asignatura, por defecto es la secretaría que atiende ese grupo.

Si dos docentes registran la misma asignatura en el mismo grupo, la plataforma lo impide y avisa quién lo tiene.

## Cómo funciona la captura

- Al abrir un grupo se ve la **hoja con el formato oficial** del concentrado: encabezado, columnas 1°/ER/2°/ER/3°, PROM. FINAL, inasistencias, conducta, los renglones de HOMBRES a PROMEDIO y las firmas. Se escribe directo en la hoja y se guarda solo.
- **Trimestre**: se elige 1°, 2° o 3°; en la hoja se iluminan las columnas de ese trimestre (calificación y ER, y su inasistencia y conducta). Solo se capturan las columnas de ese trimestre y de los anteriores. **Imprimir** y **Excel** sacan la hoja con lo capturado hasta ese trimestre; el 3° incluye el promedio final.
- **Solo números enteros** (0 a 10). Los porcentajes y el promedio del grupo se redondean a entero.
- **ER (examen de recuperación)** en el 1° y 2° trimestre: se habilita solo si la calificación es menor a 6. Si se escribe una calificación en ER, esa es la que cuenta aunque no sea aprobatoria, y la calificación normal queda bloqueada. Ejemplos: 5 con ER 6 cuenta 6; 5 con ER 5 cuenta 5. Para corregir la calificación normal, primero se borra el ER.
- **Promedio final** del alumno: promedio de los tres trimestres, tomando el ER cuando lo hay. Si sale menor a 6 se trunca (5.67 → 5). De 6 en adelante solo sube si el decimal pasa de .5 (6.33 → 6, 6.67 → 7).
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
```

Las reglas permiten que cada docente escriba solo en sus asignaciones. La dirección y las secretarías solo leen. Los alumnos y las calificaciones nunca se borran al dar de baja.

---
powered by elprofe chan
