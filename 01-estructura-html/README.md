# Lección 1: Estructura de un documento HTML5

Esta lección explica cómo nace un documento web y cómo se organizan sus partes fundamentales. Antes de escribir textos, enlaces o botones, necesitas preparar el esqueleto estándar que todo navegador web espera recibir.

> [!TIP]
> Trabaja con calma y cambia una sola cosa a la vez. Guarda el archivo con `Ctrl + S` (o `Cmd + S` en Mac), recarga el navegador y observa el resultado.

---

## 1. El punto de partida: ¿Por qué `index.html`?

En desarrollo web, el archivo principal siempre debe llamarse `index.html` (en minúsculas y sin espacios). Los servidores web de todo el mundo están configurados para buscar y abrir automáticamente este archivo cuando alguien visita la dirección de un sitio.

Crea la siguiente estructura de carpetas en tu computadora:

```text
01-estructura-html/
├── README.md
└── mi-primera-pagina/
    └── index.html
```

---

## 2. Anatomía de una etiqueta y un elemento

Antes de escribir la plantilla completa, es fundamental entender cómo se compone el código HTML:

```html
<p class="destacado">Hola, mundo</p>
```

```html
|<------------- Elemento completo ------------->|
 <p class="destacado">  Hola, mundo  </p>
 ^   ^       ^               ^        ^
 |   |       |               |        +-- Etiqueta de cierre (lleva /)
 |   |       |               +----------- Contenido
 |   |       +--------------------------- Valor del atributo (entre comillas)
 |   +----------------------------------- Nombre del atributo
 +--------------------------------------- Etiqueta de apertura
```

* **Etiqueta (*Tag*):** Las instrucciones entre `<` y `>`, como `<p>` o `</p>`.
* **Elemento (*Element*):** Todo el conjunto desde la etiqueta de apertura hasta la etiqueta de cierre, incluyendo su contenido.
* **Atributo (*Attribute*):** Información adicional que modifica el comportamiento del elemento (se escribe en formato `nombre="valor"`).
* **Etiquetas vacías (*Void elements*):** Etiquetas que no encierran texto y **no tienen etiqueta de cierre**, como `<meta>`, `<br>` o `<img>`.

---

## 3. Generar la estructura base con Emmet

Abre `index.html` en Visual Studio Code, escribe un único signo de admiración `!` y presiona la tecla `Tab` (o `Enter`).

Emmet generará la plantilla estándar de HTML5:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi primera página</title>
  </head>
  <body>
    <!-- El contenido visible irá aquí en las siguientes lecciones -->
  </body>
</html>
```

> [!IMPORTANT]
> Emmet es un asistente de autocompletado integrado en el editor, no es parte del lenguaje HTML. Para que funcione, asegúrate de que el editor reconozca el archivo como HTML (puedes verificarlo en la esquina inferior derecha de VS Code).

---

## 4. Desglose de cada parte del esqueleto

| Elemento / Declaración | ¿Para qué sirve exactamente? | ¿Qué pasa si falta? |
| --- | --- | --- |
| `<!DOCTYPE html>` | Le dice al navegador que use el estándar moderno **HTML5**. | El navegador entra en *modo compatibilidad* (Quirks Mode) y puede mostrar estilos rotos. |
| `<html lang="es">` | El contenedor raíz de todo el documento. `lang="es"` define el idioma en español. | Los lectores de pantalla para personas ciegas o los traductores automáticos no sabrán cómo pronunciar el texto. |
| `<head>` | Contenedor de **metadatos** (información para el navegador y buscadores). No se muestra directamente en la página. | El navegador no sabrá qué título poner, qué fuentes cargar ni cómo procesar los caracteres. |
| `<meta charset="UTF-8">` | Codificación de caracteres universales (tildes, eñes, emojis, caracteres especiales). | Palabras como "Canción" o "Año" se mostrarán rotas como `CanciÃ³n` o `AÃ±o`. |
| `<meta name="viewport"...>` | Controla cómo se adapta la página en dispositivos móviles (pantallas pequeñas). | En un celular, la página se verá como una versión de escritorio diminuta e ilegible sin zoom. |
| `<title>` | El título visible en la pestaña del navegador y en los resultados de Google. | La pestaña mostrará la ruta del archivo o "Sin título". |
| `<body>` | Contiene **todo lo que el usuario puede ver e interactuar** en pantalla. | No podrás mostrar textos, imágenes, videos ni botones. |

---

## 5. El Árbol del documento: Padres, Hijos y Hermanos

HTML organiza la información en una estructura de árbol genealógico (llamada jerarquía del DOM). Comprender esta relación es clave:

```text
html (Elemento Raíz / Abuelo)
├── head (Hijo de html, Hermano de body)
│   ├── meta (Hijo de head)
│   └── title (Hijo de head, Hermano de meta)
└── body (Hijo de html, Hermano de head)
```

* **Elemento Padre:** El elemento contenedor directo (por ejemplo, `html` es padre de `head` y `body`).
* **Elemento Hijo:** El elemento que está dentro de otro (por ejemplo, `title` es hijo de `head`).
* **Elementos Hermanos (*Siblings*):** Elementos que están en el mismo nivel dentro del mismo padre (`head` y `body` son hermanos).

---

## 6. Anidamiento, Indentación y Comentarios

### Anidamiento correcto

Cuando colocas un elemento dentro de otro, debes cerrarlo **en orden inverso** al que lo abriste (como una caja dentro de otra caja):

```html
<!-- Correcto: head se abre primero y se cierra al final -->
<head>
  <title>Mi página</title>
</head>

<!-- Incorrecto: cruce de etiquetas -->
<head>
  <title>Mi página</head>
</title>
```

### Indentación (Sangría)

La indentación consiste en dejar 2 espacios al inicio de una línea para mostrar que un elemento está dentro de otro. El navegador ignora estos espacios, pero para ti como programador son vitales para leer el código sin confundirte.

### Comentarios en HTML

Los comentarios te permiten dejar notas explicativas en el código que el navegador ignorará por completo:

```html
<!-- Esto es un comentario: no se verá en la pantalla -->
```

> [!WARNING]
> Nunca uses comentarios para guardar contraseñas, claves secretas o datos confidenciales. Cualquier persona puede ver el código fuente de tu página haciendo clic derecho y seleccionando "Ver código fuente".

---

## Reto de estructura HTML5

Crea y comprueba tu propio archivo `index.html` cumpliendo los siguientes requisitos:

1. [ ] El archivo debe llamarse exactamente `index.html` y estar guardado dentro de su propia carpeta.
2. [ ] Debe iniciar con la declaración `<!DOCTYPE html>`.
3. [ ] El elemento `<html>` debe tener el atributo `lang="es"`.
4. [ ] El `<head>` debe contener el `charset="UTF-8"`, el `viewport` y un `<title>` descriptivo (por ejemplo: `Mi Portafolio - Inicio`).
5. [ ] Debe incluir al menos un comentario dentro de `<body>` explicando qué contendrá esa sección más adelante.
6. [ ] Todo el código debe tener una indentación limpia y sin cruce de etiquetas.
7. [ ] Abre el archivo en tu navegador haciendo doble clic sobre él o usando la extensión *Live Server* de VS Code y verifica que el título de la pestaña sea el correcto.

### Preguntas de autoevaluación

Antes de pasar a la Lección 2, responde con tus propias palabras:

* ¿Por qué el archivo principal de una web se llama `index.html`?
* ¿Cuál es la diferencia exacta entre una etiqueta (`tag`) y un elemento (`element`)?
* ¿Qué problema visual ocurre si olvidas la línea `<meta charset="UTF-8">`?
* ¿Por qué la etiqueta `<meta>` no necesita una etiqueta de cierre `</meta>`?
* ¿Qué diferencia de propósito existe entre `<head>` y `<body>`?

## 📚 Recursos y documentación oficial

Para profundizar en la estructura de documentos web y estándares, consulta la documentación oficial de **MDN Web Docs**:

* 📖 [Primeros pasos con HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Getting_started_with_HTML)
* 📖 [Qué hay en el head: Metadatos en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/The_head_metadata_in_HTML)
* 📖 [Referencia del elemento raíz `<html>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/html)
