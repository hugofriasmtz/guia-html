# Configuración del entorno

HTML puede aprenderse y escribirse en cualquier programa que permita crear archivos de texto, incluso en una herramienta sencilla como el Bloc de notas. También puedes usar [Sublime Text](https://www.sublimetext.com/), [Notepad++](https://notepad-plus-plus.org/), [Vim](https://www.vim.org/) u otra opción similar.

En este curso utilizaremos [Visual Studio Code](https://code.visualstudio.com/) porque ofrece autocompletado, Emmet y extensiones que hacen más cómodo el aprendizaje. Estas ayudas permiten trabajar más rápido, pero no son necesarias para que HTML funcione.

También necesitarás un navegador para abrir y revisar tus páginas. Además, usaremos la extensión Live Preview para ver los cambios con mayor comodidad. Esta configuración se realiza una sola vez para todo el curso.

> [!TIP]
> No necesitas una herramienta específica para aprender HTML. Seguiremos los ejemplos con Visual Studio Code y Live Preview, pero los conceptos funcionan igual en cualquier otra opción.

## 1. Elige tu herramienta

Puedes elegir una de estas opciones:

- **[Visual Studio Code](https://code.visualstudio.com/):** es la opción que usaremos en este curso.
- **Otra herramienta para escribir texto:** también funciona, aunque los atajos pueden cambiar.
- **Editor de texto sencillo:** permite escribir HTML, pero tendrás menos ayudas automáticas.

Si utilizarás otra opción, conserva el mismo nombre de archivo y escribe el HTML de la misma manera. Cuando la guía mencione un atajo específico de VS Code, busca la función equivalente en tu herramienta.

## 2. Comprueba las herramientas

Necesitas:

- Un programa para crear archivos de texto.
- Un navegador, como Firefox, Chrome, Brave.
- Una carpeta para guardar el curso.

Ábrelo y confirma que puedes crear y guardar archivos de texto.

## 3. Abre la carpeta del curso en Visual Studio Code

Como este curso utilizará Visual Studio Code, seguiremos estos pasos:

1. Selecciona **File > Open Folder**.
2. Abre la carpeta `<nombre-de-la-carpeta>`.
3. Comprueba que las carpetas de las lecciones aparecen en el explorador lateral.

La carpeta abierta será la raíz del proyecto. Las rutas de los archivos se interpretarán tomando esa carpeta como referencia.

> [!IMPORTANT]
> Abre la carpeta completa del curso, no solamente un archivo individual. Así podrás navegar entre las lecciones y mantener organizados tus ejercicios. Si usas otro editor, abre la carpeta completa con la opción equivalente.

## 4. Crea tu carpeta de práctica

Cada lección tendrá sus propios archivos de ejemplo y de reto. Para la primera lección, crearás la carpeta desde su README. No necesitas crear todas las carpetas de ejercicios ahora.

La estructura general del curso se verá así:

```text
html_5/
|-- README.md
|-- configuracion/
|   |-- README.md
|-- 01-estructura-html/
|   |-- README.md
|   |-- mi-primera-pagina/
|-- 02-texto-y-atributos/
|   |-- README.md
|-- ...
```

## 5. Cómo reconocer un archivo HTML

Un archivo HTML termina en `.html`. Por ejemplo:

```text
index.html
```

No debe terminar en `.html.txt`. Si Visual Studio Code reconoce correctamente el archivo, normalmente mostrará HTML como lenguaje en la esquina inferior derecha.

## 6. Activa Emmet en VS Code

Emmet es una herramienta incluida en Visual Studio Code que permite escribir estructuras HTML más rápido.

Para comprobarlo:

1. Crea o abre un archivo que termine en `.html`.
2. Escribe `!`.
3. Presiona `Tab`.
4. Comprueba que aparece una plantilla HTML.

> [!WARNING]
> Si `!` + `Tab` no funciona, revisa que el archivo termine en `.html` y que el lenguaje seleccionado sea HTML. Puedes cambiarlo desde la esquina inferior derecha del editor.

## 7. Instala y usa Live Preview

[Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) es una extensión de Visual Studio Code que muestra la página mientras trabajas y permite revisar los cambios con mayor comodidad.

Para instalarla:

1. Abre el panel de extensiones con el icono de pieza de rompe-cabeza de la barra lateral.
2. Busca `Live Preview`.
3. Instala la extensión publicada por **Microsoft**.
4. Abre un archivo `.html`.
5. Haz clic derecho dentro del archivo.
6. Selecciona **Show Preview**.
7. Comprueba que se abre una nueva ventana con tu página.

> [!IMPORTANT]
> En este curso usaremos Live Preview para revisar los ejercicios. No es obligatorio para que HTML funcione: también puedes abrir el archivo `.html` directamente en el navegador.

## 8. Abre un archivo directamente en el navegador

Para ver una página HTML:

1. Guarda el archivo con Ctrl+S.
2. Busca el archivo en el explorador de archivos.
3. Ábrelo con tu navegador.
4. Regresa a VS Code, cambia algo y guarda.
5. Actualiza la página del navegador.

Si no estás usando Visual Studio Code o Live Preview, guarda el archivo, ábrelo desde el explorador de archivos y actualiza el navegador después de cada cambio.

## 9. Extensiones opcionales de VS Code

Puedes usar estas extensiones, pero no son obligatorias:

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode): ayuda a dar formato consistente al código.
- [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag): cambia automáticamente una etiqueta de cierre cuando modificas la de apertura.

Instala una extensión solo cuando entiendas qué problema resuelve. La herramienta debe ayudarte a aprender, no ocultar lo que ocurre en el código.

## 10. Opción para trabajar con Git y GitHub

Si ya conoces Git y GitHub, puedes clonar el repositorio para obtener las guías y la estructura completa del curso.

La organización recomendada es:

- `main`: contiene las guías oficiales del curso.
- Tu rama personal: contiene tus ejercicios, cambios y avances.

De esta forma puedes consultar siempre la versión original de las guías y trabajar con libertad sin modificar `main`.

### Clonar el repositorio

En la página del repositorio, selecciona **Code**, copia la dirección HTTPS y ejecuta en la terminal:

```bash
git clone https://github.com/hugofriasmtz/html_5.git
cd html_5
```

si tienes una llave SSH configurada, puedes usar la dirección SSH en lugar de HTTPS.

```bash
git clone git@github.com:hugofriasmtz/html_5.git
cd html_5
```

Después abre esa carpeta en VS Code.

### Crear tu rama personal

Crea tu rama antes de comenzar los ejercicios:

```bash
git switch -c nombre-de-tu-rama
```

Usa un nombre que te identifique, por ejemplo `ejercicios-hugo`.

Comprueba en qué rama estás:

```bash
git branch --show-current
```

El resultado debe mostrar el nombre de tu rama personal.

### Guardar tus avances

Cuando termines un ejercicio, puedes guardar los cambios en tu rama:

```bash
git add .
git commit -m "Completa ejercicio de estructura HTML"
git push -u origin nombre-de-tu-rama
```

Reemplaza `nombre-de-tu-rama` por el nombre real de tu rama.

> [!IMPORTANT]
> Antes de crear o modificar ejercicios, confirma que no estás en `main`. Tus prácticas deben guardarse en tu rama personal.

Revisa los archivos incluidos antes de confirmar los cambios y mantén tus ejercicios dentro de la rama personal.

> [!CAUTION]
> No uses `git add .` sin revisar los archivos que vas a guardar. Evita subir contraseñas, datos personales, archivos innecesarios o imágenes con una licencia que no permita compartirlas.

Si todavía no conoces Git, puedes trabajar directamente con las carpetas y los archivos desde VS Code. Git es una forma de organizar versiones, no un requisito para aprender HTML.

## 11. Revisión final

Antes de comenzar la primera lección, comprueba:

- [ ] Elegí una herramienta para escribir HTML.
- [ ] Visual Studio Code está instalado y abre correctamente.
- [ ] El navegador abre páginas HTML.
- [ ] La carpeta `html_5_css` está abierta en VS Code.
- [ ] Puedes crear y guardar un archivo.
- [ ] VS Code reconoce los archivos `.html` como HTML.
- [ ] El atajo `!` + `Tab` genera una plantilla.
- [ ] Instalé Live Preview en VS Code.
- [ ] Sé abrir una página con **Show Preview**.
- [ ] Sabes actualizar la página en el navegador.

Cuando termines esta lista, continúa con [Estructura de un documento HTML](../01-estructura-html/README.md).
