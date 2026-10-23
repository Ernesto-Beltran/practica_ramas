# Práctica en directo: ramas en Git

Practicamos con comandos de Git lo visto en clase: clonar, remotos, preparar, confirmar, subir, ramas, fusiones y un conflicto. Seguimos este guion paso a paso, sin saltarnos ninguno. Las partes 1 a 6 duran unos 40 minutos. La parte 0 la hace solo el profesor, antes de clase.

## ⚠️ Antes de empezar

- 💻 Todo lo de Git se hace con **comandos de Git** en la terminal de VS Code, con **Git Bash** (lo explica el apartado siguiente). En la terminal solo se escriben comandos de Git: las carpetas y los archivos se crean, se abren y se editan desde VS Code.
- 🧩 El profesor usa **VS Codium** en LliureX y vosotros, **VS Code** en el portátil. VS Codium es VS Code sin la marca de Microsoft: tiene los mismos menús y botones.
- 🔢 Cada paso tiene **como mucho un comando**. Escríbelo o cópialo, pulsa **Intro** y no pases al siguiente hasta ver el resultado. Debajo de cada comando tienes:
  - 📝 qué hace el comando y cada una de sus partes;
  - 👀 qué verás al ejecutarlo;
  - 💡 la idea importante, cuando la hay;
  - 🖱️ cómo se hace lo mismo con los botones de VS Codium o VS Code, la primera vez que sale cada comando (si hay forma de hacerlo).
- 👀 El panel de **control de código fuente** (*Source Control*, **Ctrl + Mayús + G**) se mira para ver qué va pasando. Hoy usamos los comandos: no pulses sus botones (**Confirmar** (*Commit*), **Publicar Branch** (*Publish Branch*), **Sincronizar cambios** (*Sync Changes*), **+**…), aunque el guion te diga para qué sirven (🖱️). La única excepción es el paso 40.
- 🗂️ Los archivos se abren y se editan desde el **Explorador** (*Explorer*, **Ctrl + Mayús + E**). Puedes pasar del Explorador al control de código fuente y volver cuando quieras.
- 📋 Para pegar en la terminal: **Ctrl + V** en Windows; **Ctrl + Mayús + V** en LliureX.
- 💾 Guarda siempre con **Ctrl + S** antes de usar Git: si no guardas, Git no ve los cambios.
- 📄 No edites este `README.md`: solo se cambia `index.html`.
- ✍️ Escribe los mensajes de commit tal como vienen en cada paso.
- 🔢 Los códigos de commit (*hashes*, como `191f2e0`) de los ejemplos no coincidirán con los tuyos.
- 🌐 Git puede mostrar sus mensajes en inglés, en español o en valenciano, según el ordenador. El guion da el inglés y, en los mensajes importantes, el español: lo que importa es lo que dicen.
- 📖 Si al final de la terminal aparece `:`, Git te está mostrando la salida por páginas: pulsa **q** para salir.

## 💻 La terminal: usamos Git Bash

La **terminal** es el panel de VS Code donde se escriben comandos. El programa que los lee y los ejecuta se llama ***shell***, y hay varios:

| Shell | Dónde está |
|---|---|
| **CMD** (*Símbolo del sistema*) | Windows. Es el más antiguo. |
| **PowerShell** | Windows. Es el actual, y el que abre VS Code en Windows si no se cambia. |
| **bash** | Linux, y por tanto LliureX. |
| **Git Bash** | Windows. Es bash, y se instala junto con Git (*Git for Windows*). |

- 🐧 En esta práctica usamos **Git Bash**: es bash, la misma terminal que tiene el ordenador del profesor con LliureX, así que en tu pantalla verás lo mismo que en la suya.
- ✅ Los comandos de Git se escriben igual en todas: `git` es un programa aparte y la terminal solo lo pone en marcha. En PowerShell o en CMD, la práctica sale igual.
- ⚠️ Lo que cambia de una terminal a otra son sus propios comandos. Por ejemplo, para ver los archivos de una carpeta se usa `ls` en Git Bash, en LliureX y en PowerShell, pero `dir` en CMD. Por eso hoy solo escribimos comandos de Git.
- 🌿 Git Bash muestra al final de su línea, entre paréntesis, la rama en la que estás: por ejemplo, `(master)`. En cualquier terminal, la rama también se ve en VS Code abajo a la izquierda, en la barra de estado.

Para abrir Git Bash en el portátil: **Terminal > Nuevo terminal** (*Terminal > New Terminal*); después, a la derecha del panel de la terminal, pulsa la flecha **∨** que hay junto al **+** y elige **Git Bash**. Para que se abra siempre Git Bash, en ese mismo menú elige **Seleccionar perfil predeterminado** (*Select Default Profile*) > **Git Bash**. En LliureX no hay que elegir nada: la terminal ya es bash.

La línea de Git Bash es así, con tu usuario, tu ordenador y tu carpeta:

```
laura@portatil MINGW64 ~/Documents/vs_projects/practica_ramas (master)
$
```

- `laura@portatil`: tu usuario y tu ordenador.
- `MINGW64`: el sistema con el que Git Bash funciona en Windows. Ignóralo.
- `~/Documents/vs_projects/practica_ramas`: la carpeta en la que estás. `~` es tu carpeta de usuario.
- `(master)`: la rama en la que estás. Solo sale dentro de un repositorio de Git.
- `$`: la terminal espera un comando. Escríbelo a continuación.

En LliureX la línea es parecida (`usuario@equipo:~/…$`) y puede que no muestre la rama: mírala en la barra de estado.

---

## 0️⃣ Parte 0. Solo el profesor, antes de clase: crear el repositorio base

> Si eres alumno, salta a la Parte 1: este repositorio ya está creado y vas a clonarlo.

Se hace una sola vez, en Windows con VS Code.

**0.1.** Dentro de `vs_projects`, crea una carpeta `practica_ramas_base` y copia en ella `index.html` y este `README.md`. Ábrela con **Archivo > Abrir carpeta** y abre una terminal de **Git Bash** (apartado «💻 La terminal»).

**0.2.** Convierte la carpeta en un repositorio de Git:

```
git init -b master
```

📝 `git init` crea un repositorio vacío en la carpeta en la que estás: crea dentro una carpeta oculta, `.git`, donde Git guardará todo el historial. `-b master` pone a la primera rama el nombre `master`. Sin `-b`, Git usaría el nombre que tenga configurado ese ordenador, que puede ser `master` o `main`.

👀 `Initialized empty Git repository in …/practica_ramas_base/.git/` (en español, `Inicializado repositorio Git vacío en…`). En Git Bash, la línea de la terminal termina ahora en `(master)`: la carpeta ya es un repositorio.

🖱️ En VS Code y en VS Codium, con una carpeta que todavía no es un repositorio, el panel de control de código fuente muestra el botón **Inicializar repositorio** (*Initialize Repository*). Ese botón crea la rama `main`, no `master` (lo decide el ajuste `git.defaultBranchName` del editor): por eso usamos el comando.

💡 ¿Por qué `master` y no `main`? Es el nombre que usan el libro Pro Git, las diapositivas y las tareas anteriores, y el que crea `git init` en vuestros portátiles. Como toda la clase va a clonar este repositorio, todos tendréis la rama que se elija aquí, sea cual sea la configuración de cada portátil. GitHub usa `main` para los repositorios que crea con contenido, pero los dos nombres funcionan igual.

**0.3.** Prepara los dos archivos para el primer commit:

```
git add .
```

📝 `git add` lleva cambios al área de preparación: lo que irá en el próximo commit. El punto `.` significa «todo lo que hay en esta carpeta», aquí `index.html` y `README.md`.

👀 Normalmente no muestra nada. En Windows puede salir el aviso `LF will be replaced by CRLF`: es normal (Windows marca el final de las líneas de otra forma) y no hay que hacer nada.

**0.4.** Guarda el primer commit:

```
git commit -m "Punto de partida"
```

📝 `git commit` guarda en el historial una instantánea de lo que está preparado. `-m` permite escribir el mensaje del commit en el mismo comando, entre comillas. Sin `-m`, Git abriría un editor de texto para escribirlo (Vim en Windows, nano en LliureX).

👀 `[master (root-commit) 4260e2a] Punto de partida` y `2 files changed`. *root-commit* (`commit-raíz`) indica que es el primer commit del repositorio.

**0.5.** En [github.com](https://github.com) crea el repositorio **vacío** `practica_ramas_base`: **+ > New repository**, **Public**, **Add README** desactivado, sin `.gitignore` ni licencia, y **Create repository**. Copia la dirección **HTTPS**.

**0.6.** Guarda en tu repositorio local la dirección del de GitHub:

```
git remote add origin https://github.com/victorrpf/practica_ramas_base.git
```

📝 `git remote add` guarda la dirección de un repositorio remoto con un nombre corto. `origin` es ese nombre, el que se usa por costumbre para el remoto principal. No envía nada todavía.

👀 No muestra nada.

**0.7.** Sube la rama `master` a GitHub:

```
git push origin master
```

📝 `git push` envía tus commits a un remoto. `origin` dice a qué remoto y `master`, qué rama.

👀 Al final, `* [new branch]      master -> master`. Recarga la página del repositorio en GitHub: se ven `index.html` y este `README.md`, que GitHub muestra debajo de la lista de archivos.

**0.8.** Protege el repositorio base: en GitHub, entra en **Settings** y, abajo del todo (**Danger Zone**), pulsa **Archive this repository** y confírmalo. Un repositorio archivado se puede clonar, pero nadie puede subir nada, ni siquiera tú: si en clase te saltas los pasos 10 y 11, el `git push` fallará en lugar de cambiar el repositorio base.

**0.9.** Antes de clase, en el ordenador de LliureX, comprueba que puedes hacer `git push` desde la terminal de VS Codium con un repositorio de prueba. Si pide usuario y contraseña, GitHub no acepta la contraseña de la cuenta: hace falta un token. Si has ensayado la práctica, borra de GitHub tu repositorio `practica_ramas` y la carpeta local, para empezar de cero.

**0.10.** En clase, en LliureX con VS Codium, el profesor hace desde la Parte 1 lo mismo que los alumnos, con su propio repositorio `practica_ramas`.

---

## 1️⃣ Parte 1. Clona el repositorio base (5 min)

**1.** Abre VS Code. Entra en **Archivo > Abrir carpeta** (*File > Open Folder*) y abre tu carpeta de proyectos (en el portátil, `vs_projects`). Abre una terminal de **Git Bash** como explica el apartado «💻 La terminal», al principio del guion.

**2.** Comprueba el nombre con el que Git firma tus commits:

```
git config user.name
```

📝 `git config` lee o cambia la configuración de Git. Con solo el nombre de un ajuste, `user.name`, muestra su valor: el nombre que aparecerá como autor de tus commits.

👀 Tu nombre.

🖱️ No hay botón: el nombre y el correo de Git solo se miran y se cambian con `git config`.

**3.** Comprueba tu correo:

```
git config user.email
```

📝 Igual que el anterior, con el correo que acompaña a tu nombre en cada commit.

👀 Tu correo.

> 🆕 Si alguno de los dos no muestra nada, configúralo con tus datos, como explica el apartado [1.6 Configurando Git por primera vez](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez). Sin nombre ni correo, Git no te deja hacer commits. Primero el nombre:
>
> ```
> git config --global user.name "Tu Nombre"
> ```
>
> Después el correo:
>
> ```
> git config --global user.email "tu@correo.com"
> ```
>
> `--global` guarda el ajuste para todos tus repositorios. Ninguno de los dos muestra nada; repite los pasos 2 y 3 para comprobarlo.

**4.** Clona el repositorio del profesor en una carpeta nueva llamada `practica_ramas`:

```
git clone https://github.com/victorrpf/practica_ramas_base.git practica_ramas
```

📝 `git clone` descarga una copia completa de un repositorio: los archivos y todo su historial de commits. La dirección dice qué repositorio se copia, y la última palabra, `practica_ramas`, es el nombre de la carpeta que se crea. Además, Git guarda esa dirección como remoto, con el nombre `origin`.

👀 `Cloning into 'practica_ramas'...` (en español, `Clonando en 'practica_ramas'...`).

🖱️ **Ctrl + Mayús + P** y escribe **Git: Clonar** (*Git: Clone*): pide la dirección y la carpeta donde guardarlo, pero la carpeta nueva se llama siempre como el repositorio (`practica_ramas_base`). Con el comando eliges el nombre.

**5.** Abre la carpeta clonada: **Archivo > Abrir carpeta**, entra en `practica_ramas` y pulsa **Seleccionar carpeta** (*Select Folder*). Si VS Code te pregunta si confías en los autores, pulsa **Sí, confío en los autores** (*Yes, I trust the authors*). Vuelve a abrir la terminal (**Terminal > Nuevo terminal**; si no sale Git Bash, elígelo en la flecha **∨**) y el panel de control de código fuente (**Ctrl + Mayús + G**).

> A partir de aquí también puedes leer este guion en VS Code: en el Explorador (**Ctrl + Mayús + E**), clic derecho en `README.md` > **Abrir vista previa** (*Open Preview*).

**6.** Mira en qué estado está tu repositorio:

```
git status
```

📝 `git status` dice en qué rama estás y si hay archivos cambiados, preparados o nuevos.

👀 Verás:

```
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

En español: `En la rama master`, `Tu rama está actualizada con 'origin/master'.` y `nada para hacer commit, el árbol de trabajo está limpio`. Estás en la rama `master`, igual que la copia de GitHub, y no has cambiado nada.

🖱️ El panel de control de código fuente es un `git status` siempre a la vista: lista los archivos cambiados (**Cambios**, *Changes*) y los preparados (**Cambios "staged"**, *Staged Changes*). Ahora está vacío.

**7.** Mira el historial:

```
git log --oneline
```

📝 `git log` muestra los commits, del más nuevo al más antiguo. `--oneline` pone cada commit en una sola línea: su código corto y su mensaje.

👀 Un solo commit: `4260e2a (HEAD -> master, origin/master, origin/HEAD) Punto de partida`.

💡 `HEAD -> master` significa que estás en la rama `master`. `origin/master` es dónde estaba `master` en GitHub cuando clonaste. El código de ese commit es el mismo para toda la clase (el que se ve en la pantalla del profesor, no el del ejemplo): es el mismo commit, copiado.

🖱️ En el panel de control de código fuente, la sección **Graph** muestra el historial (en versiones antiguas del editor no existe).

---

## 2️⃣ Parte 2. Tu propio repositorio en GitHub (7 min)

**8.** Mira a qué remoto apunta tu copia:

```
git remote -v
```

📝 `git remote` lista los remotos guardados. `-v` (de *verbose*, «detallado») añade la dirección de cada uno: una línea para traer cambios (`fetch`) y otra para enviarlos (`push`).

👀 Dos líneas con `origin` y la dirección del repositorio del profesor (`victorrpf/practica_ramas_base`).

💡 Ahí no puedes subir nada: no tienes permiso. Vamos a cambiarlo por un repositorio tuyo.

🖱️ No hay una vista de remotos: se miran con el comando.

**9.** En [github.com](https://github.com), con tu cuenta, crea un repositorio **vacío**:
- Pulsa **+** (arriba a la derecha) > **New repository**.
- **Repository name**: `practica_ramas`.
- Elige **Public**.
- Deja **Add README** desactivado, y sin `.gitignore` ni licencia.
- Pulsa **Create repository**.
- En la página que aparece (**Quick setup**) está la dirección **HTTPS** de tu repositorio. Deja esta página abierta: la copiarás en el paso 11. No hagas los comandos que sugiere GitHub.

**10.** Quita el remoto del profesor:

```
git remote rm origin
```

📝 `git remote rm` (de *remove*, «quitar») borra de tu copia local el remoto `origin`, es decir, la dirección guardada. No borra nada en GitHub.

👀 No muestra nada.

🖱️ Botón **···** (*Más acciones*) de arriba del panel de control de código fuente > **Remoto** (*Remote*) > **Quitar remoto** (*Remove Remote*), y elige `origin`.

**11.** Añade tu repositorio como remoto. Escribe en la terminal `git remote add origin `, con un espacio al final, y **no pulses Intro**. Vuelve a la página de GitHub del paso 9, pulsa el botón de copiar que hay junto a la dirección **HTTPS**, pégala en la terminal y pulsa **Intro**. Tiene que quedar así, con tu usuario de GitHub en lugar de `TU_USUARIO`:

```
git remote add origin https://github.com/TU_USUARIO/practica_ramas.git
```

📝 `git remote add` guarda una dirección con un nombre corto, `origin`. Ahora `origin` es tu repositorio.

👀 No muestra nada.

🖱️ **···** > **Remoto** > **Agregar remoto...** (*Add Remote...*): pega la dirección y escribe el nombre, `origin`.

**12.** Comprueba el cambio:

```
git remote -v
```

👀 Las dos líneas de `origin` muestran tu dirección.

**13.** Sube tu copia a tu repositorio:

```
git push origin master
```

📝 `git push` envía tus commits a un remoto: `origin` (tu repositorio) y la rama `master`.

Si te pide iniciar sesión en GitHub, hazlo. En Windows se abre la ventana **Connect to GitHub**: pulsa **Sign in with your browser** y autoriza en el navegador.

👀 Al final, `* [new branch]      master -> master` (en español, `[nueva rama]`). Recarga la página de tu repositorio en GitHub: ya están `index.html` y `README.md`, con el commit del profesor.

🖱️ **···** > **"Pull", "Push"** > **Insertar en...** (*Push to...*), y elige `origin`. VS Codium traduce *push* como «insertar».

⚠️ No pulses **Publicar Branch** (*Publish Branch*): ya está subido. Ese botón seguirá apareciendo hasta el final de la práctica: es normal, ignóralo.

---

## 3️⃣ Parte 3. Un cambio, paso a paso (6 min)

**14.** Abre el Explorador (**Ctrl + Mayús + E**) y haz clic en `index.html`. En la línea `<p>Autor: (tu nombre)</p>`, cambia `(tu nombre)` por tu nombre, sin apellidos ni paréntesis: por ejemplo, `<p>Autor: Laura</p>`. Guarda con **Ctrl + S** y vuelve al control de código fuente con **Ctrl + Mayús + G**.

**15.** Mira el estado:

```
git status
```

👀 `modified:   index.html` (en español, `modificados:`), en rojo, debajo de `Changes not staged for commit:` (en español, `Cambios no rastreados para el commit:`): cambiado, pero sin preparar. En el panel de control de código fuente, `index.html` sale con una **M** (modificado).

**16.** Mira qué has cambiado exactamente:

```
git diff
```

📝 `git diff` muestra, línea a línea, lo que has cambiado y todavía no has preparado. Las líneas que quitas salen en rojo con `-`, y las que pones, en verde con `+`.

👀 Entre otras líneas, verás estas dos:

```
-  <p>Autor: (tu nombre)</p>
+  <p>Autor: Laura</p>
```

Si tu nombre lleva tilde o ñ y en la terminal se ve con códigos raros (como `<C3><AD>`), es solo cómo lo muestra la terminal: el archivo está bien.

🖱️ En el panel de control de código fuente, haz clic en `index.html` (dentro de **Cambios**): se abre una comparación, con la versión que tiene Git a la izquierda y la tuya a la derecha.

**17.** Prepara el cambio:

```
git add index.html
```

📝 `git add` lleva el archivo al área de preparación: lo que irá en el próximo commit. Esta vez se indica el nombre del archivo en lugar del punto.

👀 No muestra nada. En el panel, `index.html` pasa al grupo **Cambios "staged"** (*Staged Changes*).

🖱️ El **+** que aparece junto al archivo, en **Cambios**, al pasar el ratón: **Almacenar cambios provisionalmente** (*Stage Changes*). El **+** de la cabecera **Cambios** prepara todos los archivos, como `git add .`.

**18.** Mira el estado otra vez:

```
git status
```

👀 Ahora `index.html` sale en verde, en `Changes to be committed:` (en español, `Cambios a ser confirmados:`).

**19.** Guarda el cambio en un commit:

```
git commit -m "Escribe mi nombre"
```

📝 `git commit` guarda la instantánea de lo preparado en el historial, con el mensaje que va detrás de `-m`.

👀 `[master 191f2e0] Escribe mi nombre` y `1 file changed, 1 insertion(+), 1 deletion(-)`: una línea quitada y otra puesta.

🖱️ Escribe el mensaje en el cuadro **Mensaje** (*Message*) de arriba del panel y pulsa **✓ Confirmar** (*Commit*).

**20.** Súbelo a tu repositorio:

```
git push origin master
```

👀 Esta vez no sale `[new branch]`: la última línea es `4260e2a..191f2e0  master -> master`, del commit que ya estaba en GitHub al nuevo. En GitHub, tu repositorio ya tiene 2 commits.

---

## 4️⃣ Parte 4. Una rama nueva (8 min)

**21.** Crea una rama llamada `libros` y salta a ella:

```
git checkout -b libros
```

📝 `git checkout` salta a otra rama. `-b` hace que antes la cree: es lo mismo que `git branch libros` (crear la rama) seguido de `git checkout libros` (saltar a ella).

👀 `Switched to a new branch 'libros'` (en español, `Cambiado a nueva rama 'libros'`). En la barra de estado de VS Code, abajo a la izquierda, pone `libros`, y la línea de Git Bash termina en `(libros)`.

🖱️ Clic en el nombre de la rama, abajo a la izquierda en la barra de estado > **+ Crear nueva rama...** (*Create new branch...*), y escribe el nombre.

**22.** Mira tus ramas:

```
git branch
```

📝 `git branch`, sin nada más, lista las ramas de tu repositorio.

👀 Verás:

```
* libros
  master
```

💡 Una rama es un apuntador a un commit. El `*` marca la rama en la que estás, la que señala `HEAD`. Crear una rama es instantáneo: no copia ningún archivo.

🖱️ El mismo clic en la rama de la barra de estado muestra la lista de ramas.

**23.** En `index.html`, haz clic al final de la línea `<li>El principito</li>` y pulsa **Intro**: VS Code pone la sangría. Escribe `<li>` y verás que VS Code añade solo `</li>`. Entre las dos etiquetas, escribe `Harry Potter`. La línea nueva debe quedar así:

```
    <li>Harry Potter</li>
```

Guarda con **Ctrl + S**.

**24.** Prepara el cambio:

```
git add index.html
```

👀 No muestra nada.

**25.** Guárdalo en un commit:

```
git commit -m "Nuevo libro"
```

👀 `[libros a17a490] Nuevo libro`: el commit se ha guardado en la rama `libros`.

**26.** Mira el historial:

```
git log --oneline
```

👀 Verás:

```
a17a490 (HEAD -> libros) Nuevo libro
191f2e0 (origin/master, master) Escribe mi nombre
4260e2a Punto de partida
```

💡 `libros` ha avanzado con el commit nuevo; `master` se ha quedado donde estaba.

**27.** Vuelve a `master` y mira `index.html` en el editor:

```
git checkout master
```

📝 `git checkout master` salta a la rama `master`: Git cambia los archivos de tu carpeta por los del último commit de esa rama.

👀 `Switched to branch 'master'` (en español, `Cambiado a rama 'master'`) y la línea de Git Bash vuelve a `(master)`. **¡El libro ha desaparecido de `index.html`!**

💡 El libro no se ha perdido: está en el commit de la rama `libros`.

🖱️ Clic en la rama de la barra de estado y elige `master`. VS Codium traduce *checkout* de varias formas («extraer», «desproteger»): es lo mismo.

⚠️ Si antes de `Switched to branch 'master'` sale una línea `M	index.html` y el libro sigue ahí, no hiciste el commit del paso 25: mira la tabla del final.

**28.** Trae a `master` el trabajo de `libros`:

```
git merge libros
```

📝 `git merge` fusiona: trae a la rama en la que estás (`master`) los commits de la rama que escribes (`libros`).

👀 Verás `Updating 191f2e0..a17a490` (en español, `Actualizando…`) y `Fast-forward`, que sale en inglés en los dos idiomas. El libro vuelve a aparecer en `index.html`.

💡 Es una fusión de **avance rápido** (*fast-forward*): `master` no tenía commits nuevos, así que Git solo mueve el apuntador `master` hasta el commit de `libros`. No se crea ningún commit nuevo.

🖱️ **···** > **Rama** (*Branch*) > **Combinar...** (*Merge...*), y elige `libros`. VS Codium traduce *merge* como «combinar».

**29.** La rama ya no hace falta. Bórrala:

```
git branch -d libros
```

📝 `git branch -d` (de *delete*, «borrar») borra una rama. Solo la borra si ya está fusionada, para que no se pierda trabajo.

👀 `Deleted branch libros (was a17a490).` (en español, `Eliminada la rama libros (era a17a490).`).

💡 Se borra el apuntador, no los commits: el commit «Nuevo libro» ya está en `master`.

🖱️ **···** > **Rama** > **Borrar rama...** (*Delete Branch...*), y elige `libros`.

---

## 5️⃣ Parte 5. Un conflicto (10 min)

Ahora dos ramas van a cambiar **la misma línea** de formas distintas.

**30.** Crea la rama `titulo` y salta a ella:

```
git checkout -b titulo
```

👀 `Switched to a new branch 'titulo'`.

**31.** En `index.html`, en la línea `<h1>Mis libros</h1>`, haz clic justo antes de `</h1>` y escribe un espacio y `favoritos`. Debe quedar así; después guarda con **Ctrl + S**:

```
  <h1>Mis libros favoritos</h1>
```

**32.** Prepara el cambio:

```
git add index.html
```

👀 No muestra nada.

**33.** Guárdalo en un commit de la rama `titulo`:

```
git commit -m "Cambia el h1 en la rama titulo"
```

👀 `[titulo 9874f56] Cambia el h1 en la rama titulo`.

**34.** Vuelve a `master`:

```
git checkout master
```

👀 En `index.html`, el título vuelve a ser `Mis libros`.

**35.** Ahora, en la línea `<h1>Mis libros</h1>`, selecciona con el ratón solo el texto `Mis libros` (lo que hay entre `<h1>` y `</h1>`) y escribe `Libros que recomiendo`. Debe quedar así; después guarda con **Ctrl + S**:

```
  <h1>Libros que recomiendo</h1>
```

**36.** Prepara el cambio:

```
git add index.html
```

👀 No muestra nada.

**37.** Guárdalo en un commit de la rama `master`:

```
git commit -m "Cambia el h1 en master"
```

👀 `[master 2a3a52b] Cambia el h1 en master`.

💡 Ahora cada rama tiene un commit que la otra no tiene: el historial se ha bifurcado, y los dos commits cambian la misma línea.

**38.** Intenta fusionar `titulo` en `master`:

```
git merge titulo
```

👀 Verás:

```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

(en español: `Auto-fusionando index.html`, `CONFLICTO (contenido): Conflicto de fusión en index.html` y `Fusión automática falló; arregle los conflictos y luego realice un commit con el resultado.`). La línea de Git Bash termina en `(master|MERGING)`: estás en mitad de una fusión (*merging*, «fusionando»).

💡 Git no sabe cuál de los dos títulos quieres, así que detiene la fusión a medias y te lo pregunta a ti.

**39.** Mira el estado:

```
git status
```

👀 `You have unmerged paths.` y `both modified:   index.html` (en español, `Tienes rutas no fusionadas` y `modificados por ambos:`). En el panel de control de código fuente, `index.html` aparece en la sección **Fusionar cambios mediante combinación** (*Merge Changes*) con un **!**.

**40.** Abre `index.html`. Git ha escrito las dos versiones, separadas por marcas:

```
<<<<<<< HEAD
  <h1>Libros que recomiendo</h1>
=======
  <h1>Mis libros favoritos</h1>
>>>>>>> titulo
```

💡 Arriba, entre `<<<<<<< HEAD` y `=======`, está la versión de la rama en la que estás (`master`): VS Code la llama **Cambio actual**. Abajo, hasta `>>>>>>> titulo`, está la de la rama que traes: **Cambio entrante**.

Resuélvelo: justo encima de `<<<<<<< HEAD` hay una línea de texto pequeño, en gris: **Aceptar cambio actual | Aceptar cambio entrante | Aceptar ambos cambios | Comparar cambios**. Haz clic en **Aceptar cambio entrante** (*Accept Incoming Change*). Si lo prefieres, edítalo a mano: deja solo el `<h1>` que quieras y borra las tres líneas de marcas. No uses el botón **Resolver en el Editor de combinación** (*Resolve in Merge Editor*).

Comprueba que no queda ninguna marca (`<<<<<<<`, `=======`, `>>>>>>>`) y guarda con **Ctrl + S**.

**41.** Marca el conflicto como resuelto:

```
git add index.html
```

📝 Durante un conflicto, `git add` también le dice a Git que ese archivo ya está resuelto.

**42.** Mira el estado:

```
git status
```

👀 `All conflicts fixed but you are still merging.` (en español, `Todos los conflictos resueltos pero sigues fusionando.`).

**43.** Termina la fusión con un commit:

```
git commit -m "Fusiona la rama titulo"
```

👀 `[master 0910037] Fusiona la rama titulo`. La línea de Git Bash vuelve a `(master)`: la fusión ha terminado.

💡 Este es el **commit de fusión**. Es especial: tiene **dos padres**, el último commit de `master` y el de `titulo`.

**44.** Mira el historial como un dibujo:

```
git log --oneline --graph
```

📝 `--graph` dibuja con líneas a la izquierda cómo se separan y se vuelven a juntar las ramas.

👀 Verás algo así:

```
*   0910037 (HEAD -> master) Fusiona la rama titulo
|\
| * 9874f56 (titulo) Cambia el h1 en la rama titulo
* | 2a3a52b Cambia el h1 en master
|/
* a17a490 Nuevo libro
* 191f2e0 (origin/master) Escribe mi nombre
* 4260e2a Punto de partida
```

💡 El historial se separó en dos caminos y el commit de fusión los vuelve a unir.

🖱️ La sección **Graph** del panel de control de código fuente dibuja este mismo gráfico.

**45.** Borra la rama `titulo`, que ya está fusionada:

```
git branch -d titulo
```

👀 `Deleted branch titulo (was 9874f56).` (en español, `Eliminada la rama titulo (era 9874f56).`)

---

## 6️⃣ Parte 6. Sube tu trabajo y entrega (3 min)

**46.** Sube `master` a tu repositorio:

```
git push origin master
```

👀 La última línea es `191f2e0..0910037  master -> master`.

**47.** En GitHub, recarga tu repositorio y pulsa **Commits**: deben salir 6, el del profesor y tus 5 (el último, «Fusiona la rama titulo»). Las ramas `libros` y `titulo` no están en GitHub: solo has subido `master`.

**48.** Entrega en Aules el enlace de tu repositorio: `https://github.com/TU_USUARIO/practica_ramas`.

---

## 🆘 Si algo sale mal

| Mensaje o síntoma | Qué ha pasado y qué hacer |
|---|---|
| `fatal: destination path 'practica_ramas' already exists` (`la ruta de destino 'practica_ramas' ya existe…`) al clonar | Ya tienes una carpeta con ese nombre. Si es de esta práctica, ábrela (paso 5) y sigue por el paso en el que te quedaste; si no, bórrala desde el explorador de archivos y repite el paso 4. |
| En el menú de la flecha **∨** de la terminal no aparece **Git Bash** | Cierra VS Code y vuelve a abrirlo. Si sigue sin aparecer, haz la práctica en PowerShell (los comandos de Git son los mismos) y avisa al profesor. |
| `fatal: not a git repository` (`no es un repositorio git`) | La terminal no está en la carpeta `practica_ramas`. Repite el paso 5: abre esa carpeta y una terminal nueva. |
| `Permission to victorrpf/practica_ramas_base.git denied`, `This repository was archived` o error 403 al hacer `git push` | No has cambiado el remoto: vuelve a los pasos 10 y 11. Si dice *denied to* con otro nombre de usuario, Git está usando otra cuenta de GitHub guardada en ese ordenador: avisa al profesor. |
| `remote: Repository not found.` | La dirección de tu repositorio está mal copiada: repite los pasos 10 y 11 con la dirección correcta. |
| `error: remote origin already exists.` (`remoto origin ya existe.`) | Ya habías añadido `origin`. Mira cuál es con `git remote -v`; si no es el tuyo, repite los pasos 10 y 11. |
| En GitHub tu repositorio solo muestra un `README.md`, o el selector de rama dice `main` | Creaste el repositorio con README. En GitHub, entra en **Settings** y, abajo del todo (**Danger Zone**), pulsa **Delete this repository** y sigue las confirmaciones. Después créalo otra vez vacío con el mismo nombre (paso 9) y repite el paso 13. |
| `git status` dice `nothing to commit` (`nada para hacer commit`) justo después de editar | No has guardado: pulsa **Ctrl + S**. |
| `error: Your local changes to the following files would be overwritten by checkout` (o `by merge`, en el paso 38) | Has cambiado `index.html` y no has hecho el commit antes de cambiar de rama. Haz el `git add` y el `git commit` del paso en el que estabas y repite el comando que ha fallado (`git checkout` o `git merge`). |
| Después del commit de fusión todavía hay marcas `<<<<<<<` en `index.html` | Bórralas, deja el título que quieras, guarda y haz `git add index.html` y `git commit -m "Corrige el conflicto"`. |
| `git push` pide usuario y contraseña en la terminal | Tu ordenador no tiene configurado el inicio de sesión de GitHub, y GitHub no acepta la contraseña. Sigue con los pasos siguientes: las partes 3, 4 y 5 no necesitan GitHub. Salta los `git push` y, cuando puedas iniciar sesión (por ejemplo, en casa), haz solo el del paso 46: sube todo de una vez. |
| Al cambiar de rama sale una línea `M	index.html` y el archivo no cambia como dice el guion (en el paso 27 el libro no desaparece, o en el 34 el título no vuelve a `Mis libros`; después, `git merge` dice `Already up to date.`) | No hiciste el commit antes del `git checkout`, y el cambio sin confirmar se ha venido contigo a la otra rama. Vuelve a la rama anterior (`git checkout libros` o `git checkout titulo`), haz el `git add` y el `git commit` que faltaban, y repite el `git checkout master`. |
| `fatal: a branch named 'libros' already exists` (o `'titulo'`) | La rama ya está creada. Salta a ella sin `-b`: `git checkout libros`. |
| Después de `git commit` la terminal se convierte en un editor de texto | Te has dejado el `-m "mensaje"`. En Windows (Vim): pulsa **Esc**, escribe `:q!` y pulsa **Intro**. En LliureX (nano): pulsa **Ctrl + X**. Después repite el commit con `-m`. |
| La terminal termina en `:` | Pulsa **q**. |
