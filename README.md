# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-12
Este diagrama entidad-relación (o modelo relacional) representa la estructura lógica de una **base de datos para una red social**, diseñada para gestionar usuarios, sus interacciones (publicaciones, comentarios, reacciones, etiquetas) y las conexiones de seguimiento entre ellos.

A continuación se detalla qué representa cada tabla y cómo se relacionan entre sí:

### 1. Entidades Principales (Tablas)

* **`USUARIO`**: Almacena la información de los perfiles registrados en la plataforma.
* *Campos:* `ID_USUARIO` (Clave Primaria), `FECHA_ALTA`, `NOMBRE`, `CORREO`, `CONTRASEÑA` y `BIOGRAFIA`.




* **`PUBLICACION`**: Contiene los posts o contenidos multimedia compartidos por los usuarios.
* *Campos:* `ID_PUBLICACION` (Clave Primaria), `URL`, `HORA`, `FECHA`, `LEYENDA` y `ID_USUARIO` (Clave Foránea que indica qué usuario creó la publicación).




* **`COMENTARIO`**: Registra los mensajes o respuestas dejados en las publicaciones.
* *Campos:* `ID_COMENTARIO` (Clave Primaria), `FECHA`, `HORA`, `TEXTO`, `ID_USUARIO` (quién hizo el comentario) y `ID_PUBLICACION` (a qué post pertenece).




* **`REACCION`**: Almacena las interacciones de tipo "Me gusta" u otras reacciones sobre las publicaciones.
* *Campos:* `ID_REACCION` (Clave Primaria), `TIPO_REACCION` e `ID_PUBLICACION` (Clave Foránea).




* **`ETIQUETA`**: Define las categorías o *tags* temáticos que se pueden asociar a las publicaciones.


* *Campos:* `ID_ETIQUETA` (Clave Primaria) y `NOMBRE`.




* **`SIGUE`**: Modela una relación de muchos a muchos (N:M) autorreferencial para gestionar la red de seguidores.
* *Campos:* `ID_USUARIO_SEGUIDOR` (quién sigue) e `ID_USUARIO_SEGUIDIDO` (a quién siguen), los cuales forman conjuntamente la clave primaria.





---

### 2. Relaciones Principales

* **Un usuario crea publicaciones:** Relación de 1 a N, donde un usuario puede hacer múltiples publicaciones, pero cada publicación pertenece a un único autor.


* **Interacciones en publicaciones:** Las publicaciones reciben múltiples comentarios y reacciones (relaciones de 1 a N con `COMENTARIO` y `REACCION`).


* **Red de contactos (Seguidores):** La tabla `SIGUE` conecta la entidad `USUARIO` consigo misma para permitir que un usuario siga a otros y a su vez tenga seguidores.
<img width="1326" height="817" alt="EJERCICIO 12-MR drawio" src="https://github.com/user-attachments/assets/014c0409-225f-420d-8aac-741a24f56282" />

Este diagrama muestra el **proceso completo de normalización de bases de datos** aplicado a una plataforma o red social, transformando una estructura inicial desnormalizada (Forma Normal 0) hasta llegar al diseño relacional optimizado en Tercera Forma Normal (3FN).

A continuación se detalla cada una de las fases representadas:

---

### 1. Fase Normal 0 (FN0) — Tabla No Normalizada

* **Qué se hace:** Se parte de una **única tabla plana y masiva** que agrupa toda la información de la red social en una sola estructura: datos del usuario, sus publicaciones anidadas, comentarios, reacciones, etiquetas y los usuarios a los que sigue.


* **Problema:** Contiene grupos repetitivos y colecciones de datos anidados dentro de una misma celda, lo que genera redundancia masiva y dificulta cualquier consulta o modificación estructurada.

---

### 2. Primera Forma Normal (1FN)

* **Qué se hace:** Se eliminan los grupos repetitivos y se asegura que **todos los atributos sean atómicos** (cada celda contiene un único valor). Cada fila representa una combinación independiente y se definen las claves primarias (`ID_USUARIO`, `ID_PUBLICACION`, `ID_COMENTARIO`).


* **Resultado:** Se obtiene una tabla plana (`TABLA RED_SOCIAL`) donde cada campo es indivisible.



---

### 3. Segunda Forma Normal (2FN)

* **Qué se hace:** Se parte de la 1FN y se eliminan las **dependencias parciales**. Se separan los datos de acuerdo con su clave principal correspondiente, dividiendo la información en dos tablas independientes:
* **`TABLA USUARIO`**: Almacena de forma centralizada la información personal y credenciales de cada miembro (`ID_USUARIO`, nombre, correo, contraseña, fecha de alta, biografía).


* **`TABLA PUBLICACION`**: Contiene el detalle y contenido multimedia de los posts, vinculados mediante una clave foránea al usuario creador (`ID_USUARIO`).




* **Resultado:** Se evita duplicar los datos del perfil de un usuario cada vez que realiza una publicación.

---

### 4. Tercera Forma Normal (3FN)

* **Qué se hace:** Se eliminan las **dependencias transitivas**, aislando todos aquellos atributos que dependen de otros campos no clave. El modelo se desglosa en múltiples tablas especializadas conectadas por claves foráneas (FK), garantizando la integridad referencial y una escalabilidad óptima:
* **`TABLA USUARIO`**: Mantiene los datos generales de perfil de cada miembro.


* **`TABLA PUBLICACION`**: Gestiona las publicaciones realizadas por los usuarios.


* **`TABLA COMENTARIO`**: Almacena las opiniones o respuestas hechas en las publicaciones, vinculando tanto al autor del comentario como al post correspondiente.


* **`TABLA REACCION`**: Registra los "Me gusta" o reacciones emitidas en los posts.


* **`TABLA ETIQUETA`**: Define las categorías o *tags* temáticos disponibles.


* **`TABLA SIGUE`**: Modela una relación de muchos a muchos (N:M) autorreferencial para gestionar la red de seguidores entre los propios usuarios.
<img width="3712" height="2734" alt="EJERCICIO 12-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/63ec2919-b5d6-4f9d-8e61-185dbccb2795" />
