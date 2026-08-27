# Estructura HTML5

Esta lección explica cómo nace un documento HTML5 y cómo se organizan sus partes principales. Todavía no estudiaremos títulos, párrafos, enlaces, imágenes ni formularios. Esos elementos aparecerán en las siguientes lecciones, cuando empecemos a agregar contenido.

> [!TIP]
> Cambia una sola cosa cada vez. Guarda el archivo, observa el resultado y explica qué cambió.

## La idea principal

Una página HTML se construye dentro de un archivo de texto que el navegador puede interpretar. Antes de agregar contenido, necesitas una estructura base.

Puedes imaginarla como un edificio:

- `html` es el edificio completo.
- `head` contiene información sobre el documento.
- `body` será el espacio donde después colocarás el contenido visible.

## 1. Crea el archivo `index.html`

Dentro de la carpeta de esta lección, crea una carpeta llamada `mi-primera-pagina`. Dentro de ella crea un archivo llamado `index.html`.

La estructura inicial será:

```text
01-estructura-html/
|-- README.md
|-- mi-primera-pagina/
|   |-- index.html
```

Por ahora, `index.html` puede estar vacío. En el siguiente paso generaremos su estructura.

## 2. Genera la plantilla con Emmet

Abre `index.html` en Visual Studio Code y escribe un signo de admiración: `!`. Después presiona `Tab`.

Visual Studio Code generará una plantilla parecida a esta:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
  </body>
</html>
```

Emmet es una herramienta que genera estructuras repetitivas rápidamente. No es una etiqueta HTML.

> [!IMPORTANT]
> El atajo `!` + `Tab` funciona cuando VS Code reconoce el archivo como HTML. Si no aparece la plantilla, revisa el lenguaje seleccionado en la esquina inferior derecha.

Después de generar la plantilla, ya no crearás otro archivo para cada etiqueta. Irás agregando cada elemento dentro de la estructura que ya existe.

## 3. Cambia los datos iniciales

Primero cambia el idioma del documento:

```html
<html lang="es">
```

Después cambia el título de la pestaña:

```html
<title>Mi primera página</title>
```

La plantilla debe quedar así por ahora:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi primera página</title>
  </head>
  <body>
  </body>
</html>
```

Guarda el archivo y ábrelo en el navegador. La página estará vacía, pero la pestaña debe mostrar `Mi primera página`.

> [!NOTE]
> El texto de la pestaña se controla con `title`. El contenido que la persona verá dentro de la página se agregará después en `body`.

## 4. Comprende cada parte

| Elemento | ¿Qué es y para qué sirve? |
| --- | --- |
| `<!DOCTYPE html>` | Declaración que indica al navegador que el documento utiliza HTML5. |
| `<html lang="es">` | Elemento raíz que contiene todo el documento HTML. `lang="es"` indica que el idioma principal es español. |
| `<head>` | Contiene información sobre el documento, como metadatos, el título y archivos relacionados. Normalmente no muestra contenido en la página. |
| `<meta charset="UTF-8">` | Metadato que indica cómo interpretar los caracteres. Permite mostrar correctamente tildes, eñes y otros símbolos. |
| `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | Metadato que ayuda a adaptar el ancho y la escala de la página a la pantalla del dispositivo. |
| `<title>` | Define el título que aparece en la pestaña del navegador, en favoritos y en otros lugares. |
| `<body>` | Contiene todo el contenido que la persona podrá ver e interactuar en la página. |

La relación entre las partes es:

```text
html
|-- head
|   |-- meta
|   |-- title
|-- body
```

`html` contiene dos grandes zonas: `head` y `body`. No debes colocar contenido visible directamente fuera de ellas.

## 5. Entiende la apertura y el cierre

La mayoría de las etiquetas tienen una apertura y un cierre:

```html
<etiqueta>Contenido</etiqueta>
```

La barra `/` indica el cierre. En este ejemplo, el elemento completo es todo lo que va desde `<etiqueta>` hasta `</etiqueta>`.

La estructura también puede contener elementos dentro de otros. Esto se llama anidamiento:

```html
<elemento-exterior>
  <elemento-interior>
  </elemento-interior>
</elemento-exterior>
```

Primero se cierra el elemento interior y después el exterior.

> [!WARNING]
> Si abres una etiqueta dentro de otra, respeta el orden de cierre. Un anidamiento desordenado puede provocar resultados inesperados y dificultar la lectura del documento.

## 6. La indentación ayuda a leer

La indentación son los espacios que colocas antes de una línea para mostrar su nivel dentro de la estructura:

```html
<html>
  <head>
    <title>Mi página</title>
  </head>
  <body>
  </body>
</html>
```

El navegador puede mostrar la página aunque falten esos espacios, pero tú tendrás más dificultad para entender qué elemento contiene a otro.

## Reto de estructura HTML5

Crea y revisa tu propio archivo `index.html` siguiendo estos requisitos:

- Debe comenzar con `<!DOCTYPE html>`.
- Debe tener un elemento `html` con `lang="es"`.
- Debe contener `head` y `body`.
- Debe incluir `meta charset="UTF-8"`.
- Debe incluir `meta viewport`.
- Debe tener un `title` personalizado.
- `head` y `body` deben estar correctamente anidados.
- La página debe abrirse en el navegador aunque `body` todavía esté vacío.

### Comprueba tu trabajo

Explica con tus palabras:

1. Qué función cumple `DOCTYPE`.
2. Qué contiene `html`.
3. Qué diferencia hay entre `head` y `body`.
4. Qué hace `meta charset`.
5. Para qué sirve `title`.
6. Por qué la indentación ayuda a leer el código.

Cuando puedas responder estas preguntas, continúa con la siguiente lección para agregar texto mediante `h1`, `h2` y `p`.
