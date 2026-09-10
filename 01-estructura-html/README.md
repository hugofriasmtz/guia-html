# Lección 1: Estructura de un documento HTML5

Esta lección explica cómo nace un documento web y cómo se organizan sus partes fundamentales. Antes de escribir textos, enlaces o botones, necesitas preparar el esqueleto estándar que todo navegador web espera recibir.

---

## 1. El punto de partida: ¿Por qué `index.html`?

En desarrollo web, el archivo principal de una carpeta siempre debe llamarse **`index.html`** (completamente en minúsculas y sin espacios).

Los servidores web están configurados para buscar y abrir de forma automática este archivo cuando alguien ingresa a la dirección de un sitio web.

Trabajaremos con la siguiente estructura limpia directamente en tu carpeta:

```text
01-estructura-html/
├── README.md                    # Esta guía de aprendizaje
├── index.html                   # Tu laboratorio de pruebas
└── reto.html                    # Tu reto final escrito a mano
```

### Qué observar en el archivo inicial

- **Convención universal de nombres:** Los nombres de archivos y carpetas en la web deben escribirse siempre en **minúsculas, sin espacios, sin tildes y sin eñes**. Si el nombre tiene varias palabras, sepáralas con guiones medios (ej. `mi-pagina.html`).
- **Extensión `.html`:** Le indica a VS Code y al sistema operativo que el archivo contiene código de hipertexto estructurado (no debe terminar en `.html.txt`).

### Práctica 1: Creando tu primer archivo web (en `index.html`)

1. Abre la carpeta del curso en Visual Studio Code (**File > Open Folder...**).
2. Dentro de `01-estructura-html`, crea un archivo nuevo y nómbralo exactamente `index.html`.
3. Déjalo abierto en el editor para comenzar con la siguiente sección.

---

## 2. Anatomía de una etiqueta y un elemento

Antes de escribir el esqueleto completo, debes comprender los bloques básicos de construcción de HTML:

```html
<p class="destacado">Hola, mundo</p>
```

```text
|<------------- Elemento completo ------------->|
 <p class="destacado">  Hola, mundo  </p>
 ^   ^       ^               ^        ^
 |   |       |               |        +-- Etiqueta de cierre (lleva /)
 |   |       |               +----------- Contenido
 |   |       +--------------------------- Valor del atributo (entre comillas)
 |   +----------------------------------- Nombre del atributo
 +--------------------------------------- Etiqueta de apertura
```

- **Etiqueta (*Tag*):** Las instrucciones encerradas entre `<` y `>`, como `<p>` (apertura) o `</p>` (cierre).
- **Elemento (*Element*):** El conjunto completo: etiqueta de apertura + atributos + contenido + etiqueta de cierre.
- **Atributo (*Attribute*):** Información adicional que modifica el comportamiento o apariencia del elemento (se escribe en formato `nombre="valor"`).
- **Etiquetas vacías (*Void elements*):** Etiquetas que no encierran texto y **no tienen etiqueta de cierre**, como `<meta>`, `<br>` o `<img>`.

> [!NOTE]
> **Estándar profesional:** Aunque HTML tolera escribir etiquetas en mayúsculas como `<P CLASS="TEST">`, en la industria profesional se escribe **estrictamente todo en minúsculas y los valores de los atributos siempre entre comillas dobles**.

### Qué observar en las etiquetas

- La etiqueta de cierre se diferencia de la de apertura únicamente por la barra diagonal inclinada hacia la derecha (`/`).
- Omitir una comilla de cierre en un atributo (ej. `class="destacado`) es un error común que puede romper la lectura de todo el código que escribas debajo.

### Práctica 2: Escribiendo tu primer elemento y usando Live Preview (en `index.html`)

1. En tu archivo `index.html`, escribe manualmente: `<p>Hola, mundo web</p>`.
2. Guarda el archivo con `Ctrl + S` (o `Cmd + S` en Mac).
3. Haz clic derecho sobre el editor y selecciona **Live Preview: Show Preview** (como [configuramos en el entorno](../configuracion/README.md)).
4. Comprueba que se abre la ventana lateral con tu texto en vivo.

---

## 3. Generar la estructura base con Emmet

Escribir toda la plantilla inicial línea por línea cada vez que inicias un proyecto es tedioso. VS Code incluye **Emmet**, un motor de atajos ultrarrápido:

1. Borra lo que tenías en `index.html`.
2. Escribe un único signo de admiración: `!`
3. Presiona de inmediato la tecla **`Enter`** (o **`Tab`**).

Emmet generará automáticamente la plantilla estándar oficial de HTML5:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>

</body>
</html>
```

> [!IMPORTANT]
> Emmet es una herramienta de productividad del editor, **no es parte del lenguaje HTML**. Para que funcione, asegúrate de que VS Code reconozca el archivo con el modo de lenguaje "HTML" (puedes verificarlo en la esquina inferior derecha de la barra de estado).

### Qué observar en Emmet

- Por defecto, Emmet suele generar `<html lang="en">`. Como desarrolladores en habla hispana, la primera buena práctica que debemos aplicar siempre es cambiarlo a `<html lang="es">`.

### Práctica 3: Generación rápida con Emmet (en `index.html`)

1. En tu `index.html`, borra todo el contenido y genera la plantilla usando el atajo `!` + `Enter`.
2. Cambia el atributo a `lang="es"`.
3. Cambia el contenido dentro de `<title>` por: `Mi Laboratorio HTML`.
4. Guarda los cambios (`Ctrl + S`) y observa cómo la pestaña de **Live Preview** se actualiza automáticamente.

---

## 4. Desglose de cada parte del esqueleto

Toda página web moderna en el mundo se apoya sobre estas 7 líneas esenciales:

| Elemento / Declaración | ¿Para qué sirve exactamente? | ¿Qué ocurre si falta? |
| --- | --- | --- |
| `<!DOCTYPE html>` | Le comunica al motor del navegador que utilice el estándar moderno **HTML5**. | El navegador entra en *Modo Quirks* (modo de compatibilidad retroactivo) y renderiza la web con errores visuales antiguos de los años 90. |
| `<html lang="es">` | El elemento raíz (*root*) que encapsula todo el documento. `lang="es"` define el idioma en español. | Los lectores de pantalla para personas con discapacidad visual y los traductores automáticos no sabrán cómo pronunciar el texto. |
| `<head>` | La sala de control del documento. Almacena **metadatos**, configuraciones y conexiones a recursos externos. | El navegador no sabrá qué título poner, qué fuentes cargar ni cómo decodificar caracteres especiales. |
| `<meta charset="UTF-8">` | Codificación universal de caracteres (soporte para tildes, eñes, símbolos y emojis). | Las palabras con caracteres especiales se mostrarán rotas en pantalla (ejemplo: `AÃ±o` en lugar de `Año`). |
| `<meta name="viewport"...>` | Controla el escalado y dimensionamiento en pantallas de teléfonos móviles. | En un celular, la página se verá como una versión de computadora diminuta e ilegible sin hacer zoom manual. |
| `<title>` | Título visible en la pestaña del navegador, en marcadores y en los resultados de búsqueda de Google. | La pestaña mostrará la dirección cruda del archivo o "Sin título". |
| `<body>` | El escenario visible. Contiene **todo lo que el usuario ve e interactúa** en la pantalla. | El lienzo de la página permanecerá completamente en blanco. |

> [!WARNING]
> **El peligro del Modo Quirks:**  
> La línea `<!DOCTYPE html>` no es una etiqueta HTML (no tiene cierre); es una declaración inicial obligatoria. Si la omites o colocas texto antes de ella, los navegadores emularán el comportamiento de Internet Explorer 5, rompiendo el cálculo de cajas y los estilos modernos.

### Qué observar en el esqueleto

- El documento tiene una separación tajante: lo que se coloca dentro de `<head>` es información para la máquina; lo que se coloca dentro de `<body>` es información para el ser humano.

### Práctica 4: Comprobando el título y el cuerpo (en `index.html`)

1. Dentro de la etiqueta `<body>` de tu `index.html`, escribe: `<h1>¡Hola desde el cuerpo del documento!</h1>`.
2. Guarda los cambios (`Ctrl + S`).
3. Observa en la vista previa de Live Preview cómo el `<h1>` aparece en grande en la pantalla blanca, mientras que el contenido de `<title>` vive exclusivamente en la barra superior.

---

## 5. El Árbol del documento (DOM) y DevTools desde el Día 1

HTML organiza la información en una estructura de árbol genealógico con relaciones de jerarquía:

```text
html (Elemento Raíz / Ancestro mayor)
├── head (Hijo de html, Hermano de body)
│   ├── meta (Hijo de head)
│   └── title (Hijo de head, Hermano de meta)
└── body (Hijo de html, Hermano de head)
    └── h1 (Hijo de body)
```

- **Elemento Padre:** El contenedor directo de otro elemento (`html` es padre de `head` y `body`).
- **Elemento Hijo:** El elemento que reside dentro de otro (`title` es hijo de `head`).
- **Elementos Hermanos (*Siblings*):** Elementos que comparten el mismo nivel dentro del mismo padre (`head` y `body` son hermanos).

### Tu primer contacto con las Herramientas de Desarrollador (*DevTools*)

Los programadores profesionales no "adivinan" cómo el navegador interpreta el código; lo auditan en vivo con las DevTools:

```text
CÓDIGO EN TU EDITOR (Texto plano guardado)
          |
          v (El navegador lo interpreta)
EL ÁRBOL VIVO EN DEVTOOLS (Panel Elementos con F12)
```

### Qué observar en las DevTools

- **Diferencia entre "Ver código fuente" e "Inspeccionar":**
  - Si abres la página en tu navegador habitual y presionas `Ctrl + U` (Ver código fuente), verás el archivo de texto estático tal como lo guardaste en VS Code.
  - Si presionas **F12** (o clic derecho $\rightarrow$ **Inspeccionar**), se abrirá el panel interactivo de DevTools: aquí ves el **Árbol DOM vivo**, donde puedes desplegar y colapsar las flechas de `head` y `body` para explorar la jerarquía de padres e hijos en tiempo real.

### Práctica 5: Tu primera inspección profesional (en `index.html`)

1. En la pestaña de Live Preview, haz clic en el botón superior con forma de flecha saliente para abrir tu página en tu navegador habitual (Chrome, Firefox, Brave o Edge).
2. Presiona la tecla **`F12`**.
3. En la pestaña **Elementos / Inspector**, haz clic sobre la flecha que está junto a `<body>` para desplegarla y contraerla.
4. Pasa el cursor sobre la etiqueta `<h1>` dentro del panel y observa cómo el navegador resalta visualmente el elemento en la página web.

---

## 6. Anidamiento correcto, Indentación y Comentarios

### Anidamiento correcto (La regla de las cajas)

Cuando colocas un elemento dentro de otro, debes cerrarlo **en orden inverso al que lo abriste**. La última etiqueta que se abre debe ser la primera en cerrarse:

```html
<!-- ❌ INCORRECTO: Etiquetas cruzadas (rompe la jerarquía) -->
<p>Este texto tiene <strong>palabras importantes</p></strong>

<!-- ✅ CORRECTO: 'strong' se abre al final y se cierra primero -->
<p>Este texto tiene <strong>palabras importantes</strong></p>
```

### Indentación (Sangría)

La indentación consiste en añadir dos espacios en blanco al inicio de cada línea para mostrar visualmente que un elemento es hijo de otro.

El navegador ignora estos espacios, pero para un programador son indispensables para no perderse en documentos extensos:

```html
<!-- Código limpio y legible con 2 espacios por nivel -->
<html>
  <head>
    <title>Estructura clara</title>
  </head>
  <body>
    <p>Texto indentado correctamente.</p>
  </body>
</html>
```

### Comentarios en HTML

Los comentarios te permiten dejar notas explicativas en el código que el navegador ignorará por completo al renderizar la página:

```html
<!-- Esto es un comentario: no se verá en la pantalla -->
<p>Texto visible para el usuario.</p>
```

> [!CAUTION]
> **Nunca guardes información confidencial en comentarios:**  
> Cualquier usuario en internet puede ver los comentarios de tu HTML simplemente presionando `Ctrl + U` (Ver código fuente). Jamás anotes contraseñas, claves privadas ni notas personales en comentarios de HTML.

### Qué observar en comentarios y anidamiento

- Los comentarios se abren con `<!--` y se cierran con `-->`.
- Si olvidas cerrar un comentario, todo el código HTML que escribas hacia abajo desaparecerá de la pantalla porque el navegador creerá que sigue siendo parte de la nota.

### Práctica 6: Comentarios y anidamiento limpio (en `index.html`)

1. En tu archivo `index.html`, agrega un comentario dentro de `<body>` que diga: `<!-- Sección principal del laboratorio -->`.
2. Debajo del comentario, añade un párrafo `<p>` que contenga una palabra dentro de `<strong>` asegurándote de cerrar `</strong>` antes de cerrar `</p>`.
3. Guarda (`Ctrl + S`) y verifica en Live Preview que el texto del párrafo se muestra en pantalla y que el comentario es 100% invisible para el usuario.

---

## Reto final de la lección: Tu primer esqueleto escrito a mano

Ahora que ya experimentaste con Emmet, abriste Live Preview, inspeccionaste el DOM con DevTools y comprendes la jerarquía de cada etiqueta, demostrarás tu autonomía escribiendo la plantilla base completa **a mano y desde cero, sin utilizar el atajo de autocompletado**.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `01-estructura-html`. Construirás la plantilla base oficial para el **Lanzamiento de tu Portafolio Personal** que cumpla estrictamente con la siguiente lista de verificación:

- [x] El archivo debe llamarse exactamente `reto.html` y estar ubicado directamente dentro de `01-estructura-html/`.
- [x] **Escrito a mano:** Escribe cada etiqueta carácter por carácter (no uses el atajo `!` de Emmet) para interiorizar la sintaxis.
- [x] La primera línea debe ser la declaración de estándar: `<!DOCTYPE html>`.
- [x] El elemento raíz `<html>` debe incluir el atributo de idioma en español: `lang="es"`.
- [x] **Configuración en `<head>`:**
  - [x] Codificación de caracteres universales con `<meta charset="UTF-8">`.
  - [x] Configuración responsiva con `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
  - [x] Título de pestaña personalizado con el formato: `<title>Mi Portafolio Profesional | Inicio</title>`.
- [x] **Contenido en `<body>`:**
  - [x] Un encabezado `<h1>` con tu nombre completo o nombre del proyecto.
  - [x] Un párrafo `<p>` que contenga una breve descripción de bienvenida y al menos una palabra dentro de `<strong>`.
  - [x] Al menos un comentario descriptivo `<!-- ... -->` que indique dónde colocarás tus proyectos en las siguientes lecciones.
- [x] **Calidad de código:**
  - [x] Cero cruces de etiquetas (anidamiento perfecto de cajas).
  - [x] Indentación limpia y uniforme de 2 espacios por cada nivel jerárquico.
- [x] **Comprobación:**
  - [x] Abre `reto.html` con **Live Preview: Show Preview** (o en el navegador con `F12`) y confirma que se visualice tu árbol DOM sin errores ni etiquetas fuera de lugar.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Por qué el archivo principal de una aplicación o sitio web siempre debe nombrarse `index.html`?
2. ¿Cuál es la diferencia técnica exacta entre una etiqueta (*tag*) y un elemento (*element*) en HTML?
3. ¿Qué problema visual ocurrirá en la pantalla si olvidas incluir la etiqueta `<meta charset="UTF-8">` al escribir en español?
4. ¿Por qué las etiquetas como `<meta>`, `<br>` o `<img>` no tienen una etiqueta de cierre correspondiente (como `</meta>`)?
5. ¿Qué ocurre internamente en el navegador si omites la declaración inicial `<!DOCTYPE html>`?

---

## 📚 Recursos y documentación oficial

Para profundizar en la estructura de documentos web y estándares iniciales, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Primeros pasos con HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Getting_started_with_HTML)
- 📖 [Qué hay en el head: Metadatos en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/The_head_metadata_in_HTML)
- 📖 [Referencia del elemento raíz `<html>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/html)
- 📖 [Glosario: Elementos vacíos (Void Elements) - MDN](https://developer.mozilla.org/es/docs/Glossary/Void_element)
- 📖 [El modo de compatibilidad (Quirks Mode) explicado - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)
