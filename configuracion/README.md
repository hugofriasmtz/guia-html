# Configuración del entorno de desarrollo

HTML puede aprenderse y escribirse en cualquier programa que permita editar texto plano, incluso en herramientas básicas como el Bloc de notas. También puedes usar editores como [Sublime Text](https://www.sublimetext.com/), [Notepad++](https://notepad-plus-plus.org/) o [Vim](https://www.vim.org/).

Sin embargo, en este curso utilizaremos **[Visual Studio Code](https://code.visualstudio.com/)** porque ofrece autocompletado inteligente, motor de atajos Emmet y extensiones que facilitan el aprendizaje profesional sin ocultar el funcionamiento real de la web.

Esta configuración se realiza **una sola vez** al inicio del curso.

> [!TIP]
> No estás obligado a usar herramientas complejas para escribir HTML. Seguiremos los ejercicios con Visual Studio Code y la extensión **Live Preview**, pero todos los conceptos y etiquetas funcionan exactamente igual en cualquier editor y navegador del mundo.

---

## 1. Elige tu herramienta de trabajo

Para seguir el curso necesitarás:

1. **Un editor de código:** Recomendamos descargar e instalar **[Visual Studio Code](https://code.visualstudio.com/)** (gratuito y disponible para Windows, macOS y Linux).
2. **Un navegador web moderno:** Como Firefox, Google Chrome, Brave o Edge (donde probaremos nuestras páginas y utilizaremos las Herramientas de Desarrollador con la tecla `F12`).
3. **La carpeta del curso:** El directorio donde guardarás tus archivos y lecciones.

Si decides utilizar otro editor, conserva exactamente los mismos nombres de archivos y estructura de código que explicamos en las guías.

---

## 2. Abre la carpeta del curso en Visual Studio Code

Para que las rutas de los archivos y los enlaces relativos funcionen correctamente, debemos abrir la carpeta completa del proyecto como espacio de trabajo:

1. Abre Visual Studio Code.
2. En el menú superior, selecciona **File > Open Folder...** (Archivo > Abrir carpeta...).
3. Selecciona la carpeta raíz del curso (`guia-html`).
4. Comprueba que las carpetas de las lecciones aparezcan ordenadas en el explorador lateral izquierdo.

> [!IMPORTANT]
> **Abre siempre la carpeta completa del curso**, no archivos sueltos individuales. Al abrir la carpeta raíz, VS Code entiende la jerarquía del proyecto y las rutas relativas funcionarán de forma predecible.

---

## 3. Dinámica de trabajo: Los dos archivos por lección

Para garantizar que aprendas experimentando sin miedo a romper tu trabajo final, en casi todas las lecciones trabajarás con **dos archivos** dentro de cada carpeta:

```text
guia-html/
├── README.md
├── configuracion/
│   └── README.md
├── 01-estructura-html/
│   ├── README.md                <-- Guía de estudio de la lección
│   ├── index.html               <-- Tu LABORATORIO (para probar las micro-prácticas)
│   └── reto.html                <-- Tu RETO FINAL (proyecto autónomo desde cero)
├── 02-texto-y-atributos/
│   ├── README.md
│   ├── index.html
│   └── reto.html
├── 03-enlaces-y-listas/
├── ...
├── 12-proyecto-guiado-landing/  <-- Taller integrador guiado
└── 13-desafio-tecnico-final/    <-- Examen técnico final autónomo
```

- **`index.html` (El Laboratorio):** Es tu mesa de experimentos. Aquí seguirás las micro-prácticas paso a paso, probarás etiquetas, provocarás errores intencionales y auditarás el código en el navegador.
- **`reto.html` (El Proyecto Autónomo):** Es el desafío técnico final de cada lección. Una hoja en blanco con una lista de requisitos del mundo real que resolverás por tu cuenta para consolidar lo aprendido.

---

## 4. Cómo reconocer y nombrar un archivo HTML

Un archivo web siempre debe terminar con la extensión **`.html`**:

```text
index.html
reto.html
```

- **Regla de oro:** Escribe los nombres siempre en **minúsculas, sin espacios, sin tildes y sin eñes**. Si el nombre tiene varias palabras, sepáralas con guiones medios (ej. `sobre-mi.html`).
- Evita que tu sistema operativo guarde archivos con doble extensión accidental como `index.html.txt`.
- Si Visual Studio Code reconoce el archivo correctamente, mostrará la palabra **HTML** en la esquina inferior derecha de la barra de estado.

---

## 5. El motor de atajos: Emmet en VS Code

Emmet es una herramienta de productividad integrada nativamente en Visual Studio Code que permite escribir esqueletos y etiquetas HTML en milisegundos.

Para comprobar que está activo:

1. Crea o abre un archivo que termine en `.html`.
2. Escribe un único signo de admiración: `!`
3. Presiona la tecla **`Enter`** (o **`Tab`**).
4. Comprueba que aparece de inmediato la plantilla base estándar de HTML5.

> [!WARNING]
> Si `!` + `Enter` no genera la plantilla, verifica en la esquina inferior derecha que el modo de lenguaje del archivo diga **HTML**. Si dice "Plain Text", haz clic sobre él y selecciona HTML en la lista.

---

## 6. Instala y configura Live Preview

**[Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)** es una extensión oficial desarrollada por **Microsoft** para Visual Studio Code. Permite visualizar tu página web en tiempo real dentro de una pestaña interna del editor, actualizando los cambios automáticamente cada vez que guardas el archivo.

### Pasos para instalarla

1. Haz clic en el icono de **Extensiones** en la barra lateral izquierda de VS Code (o presiona `Ctrl + Shift + X` / `Cmd + Shift + X`).
2. En la barra de búsqueda, escribe `Live Preview`.
3. Localiza la extensión publicada por **Microsoft** y haz clic en **Install**.

### Cómo usarla en tus ejercicios

1. Abre cualquier archivo `.html` (por ejemplo, tu `index.html`).
2. Haz clic derecho en cualquier parte del editor de código.
3. Selecciona la opción **Live Preview: Show Preview**.
4. Se abrirá una pestaña al lado de tu código mostrando el resultado visual en vivo.

> [!NOTE]
> Live Preview también levanta un **servidor local de pruebas**. Si prefieres ver tu página en una ventana completa de tu navegador habitual (Chrome, Firefox, Brave), puedes hacer clic en el botón con forma de flecha saliente en la esquina superior de la pestaña de vista previa.

---

## 7. Extensiones opcionales recomendadas

Puedes instalar estas extensiones complementarias para mejorar tu flujo de trabajo, aunque no son obligatorias:

- **[Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode):** Formatea e indenta automáticamente tu código con espacios limpios cada vez que guardas (`Ctrl + S`).
- **[Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag):** Si cambias el nombre de una etiqueta de apertura (ej. de `<h2>` a `<h3>`), renombra automáticamente la etiqueta de cierre correspondiente.

> [!TIP]
> Instala extensiones solo cuando comprendas qué problema resuelven. La herramienta debe ayudarte a escribir más cómodo, no ocultar lo que ocurre detrás del lenguaje.

---

## 8. Flujo de trabajo con Git y GitHub (Opcional)

Si ya tienes conocimientos básicos de Git, te recomendamos trabajar con un sistema de ramas para mantener intactas las guías teóricas y guardar tus ejercicios personales:

- `main`: Contiene las lecciones y guías originales del curso.
- `ejercicios-<tu-nombre>`: Tu rama personal de trabajo donde resolverás las prácticas y retos.

### 1. Abre la terminal integrada de VS Code

Presiona el atajo ``Ctrl + ` `` (o `Ctrl + ñ` según tu teclado) o ve al menú superior **Terminal > New Terminal**.

### 2. Clona el repositorio

```bash
# Vía HTTPS
git clone https://github.com/hugofriasmtz/guia-html.git
cd guia-html

# O vía SSH (si tienes llaves configuradas)
git clone git@github.com:hugofriasmtz/guia-html.git
cd guia-html
```

### 3. Crea tu rama personal antes de empezar

```bash
git switch -c ejercicios-mi-nombre
```

Confirma que estás en tu rama ejecutando:

```bash
git branch --show-current
```

### 4. Guarda tus avances

Cada vez que concluyas una lección o reto:

```bash
git add .
git commit -m "Completa Lección 01: Estructura HTML y reto final"
git push -u origin ejercicios-mi-nombre
```

> [!CAUTION]
> Antes de hacer `git add .`, revisa qué archivos estás guardando. Nunca subas archivos temporales, contraseñas ni datos sensibles a un repositorio público. Si aún no sabes usar Git, no te preocupes: puedes crear y guardar tus archivos directamente en VS Code sin tocar la terminal.

---

## 9. Lista de comprobación previa al curso

Antes de abrir la primera lección, verifica que tu entorno esté a punto:

- [ ] Visual Studio Code está instalado y abre correctamente.
- [ ] Tu navegador web habitual abre y visualiza páginas web.
- [ ] La carpeta raíz `guia-html` está abierta en el explorador de VS Code.
- [ ] La extensión **Live Preview de Microsoft** está instalada.
- [ ] Al escribir `!` y presionar `Enter` en un archivo `.html`, se genera la plantilla base de HTML5.
- [ ] Sabes abrir la vista previa con clic derecho $\rightarrow$ **Show Preview**.
- [ ] Tienes claro que usarás `index.html` para experimentar y `reto.html` para resolver los desafíos.

¡Todo listo! Continúa con la **[Lección 1: Estructura de un documento HTML5](../01-estructura-html/README.md)**.
