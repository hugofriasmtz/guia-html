# Lección 2: Texto, jerarquía y atributos

Esta lección continúa el trabajo tras dominar la [Estructura base de HTML5](../01-estructura-html/README.md). Ya comprendes el propósito de `<html>`, `<head>` y `<body>`; ahora aprenderás a estructurar, clasificar y dar significado real a todo el texto que vive dentro del lienzo de la página.

---

## 1. Modelo mental: Elementos en Bloque (*Block*) vs. Elementos en Línea (*Inline*)

Antes de escribir cualquier párrafo, debes comprender los dos comportamientos visuales y estructurales básicos de las etiquetas en HTML:

```text
ELEMENTO EN BLOQUE (ej. <h1>, <p>, <div>, <hr>):
+-------------------------------------------------------------------+
| Ocupa el 100% del ancho disponible de la pantalla y fuerza un     |
| salto de línea antes y después. Siempre empieza en renglón nuevo. |
+-------------------------------------------------------------------+

ELEMENTO EN LÍNEA (ej. <strong>, <em>, <span>, <code>):
Texto normal con un [elemento en línea] que solo ocupa el ancho
estricto de su contenido y no rompe el flujo del renglón.
```

### Código de ejemplo

```html
<!-- Elementos en bloque: cada uno se posiciona en una línea nueva -->
<p>Este es el primer párrafo completo.</p>
<p>Este es el segundo párrafo (aparece abajo automáticamente).</p>

<!-- Elementos en línea: conviven dentro del mismo renglón -->
<p>
  En esta frase hay una palabra <strong>muy importante</strong> y 
  otra palabra con <em>énfasis especial</em> sin romper la línea.
</p>
```

### Qué observar en bloques y líneas

- **Inspección en DevTools:** Abre tu navegador, pulsa `F12` y pasa el cursor sobre un `<p>` en la pestaña *Elementos*: verás que la caja sombreada en azul se extiende de borde a borde de la ventana (100% de ancho).
- Si pasas el cursor sobre un `<strong>`, verás que la caja azul se ajusta únicamente al ancho milimétrico de las palabras que contiene.

### Práctica 1: Inspeccionando la caja en DevTools (en `index.html`)

1. Crea tu archivo `index.html` con la estructura base de HTML5.
2. Agrega dentro de `<body>` los dos párrafos del ejemplo anterior.
3. Abre la página en tu navegador, presiona `F12` y usa la herramienta de inspección (icono de flecha o `Ctrl + Shift + C`) para tocar el `<p>` y luego el `<strong>`. Comprueba visualmente cómo el párrafo ocupa todo el renglón y el elemento en línea solo su texto.

---

## 2. Encabezados: de `h1` a `h6` y la jerarquía del documento

Los encabezados organizan el contenido en un árbol jerárquico de temas y subtemas, de mayor a menor relevancia:

| Etiqueta | Jerarquía | Función estructural |
| --- | --- | --- |
| `<h1>` | Nivel 1 (Principal) | **Título principal de toda la página.** Solo debe existir **uno** por documento. |
| `<h2>` | Nivel 2 (Sección) | Títulos de las secciones temáticas principales. |
| `<h3>` | Nivel 3 (Subtema) | Subtemas o apartados que pertenecen a un `<h2>`. |
| `<h4>` | Nivel 4 (Detalle) | Subdivisiones de un `<h3>`. |
| `<h5>` | Nivel 5 (Puntual) | Subtemas específicos dentro de un `<h4>`. |
| `<h6>` | Nivel 6 (Mínimo) | El nivel jerárquico más profundo disponible en HTML. |

### Código de ejemplo: Esquema jerárquico estricto

```html
<!-- Título global de la página -->
<h1>Manual de Desarrollo Web Profesional</h1>

<!-- Primera sección principal -->
<h2>1. Fundamentos de HTML5</h2>
<h3>1.1. Estructura básica del documento</h3>
<h3>1.2. Jerarquía de texto y encabezados</h3>

<!-- Segunda sección principal -->
<h2>2. Estilos y Presentación con CSS</h2>
<h3>2.1. Selectores básicos</h3>
<h4>2.1.1. Selectores de clase y atributo</h4>
```

### Las 2 Reglas de Oro de los encabezados

1. **Nunca te saltes niveles hacia abajo:** No pases de un `<h2>` directo a un `<h4>`. El esquema debe descender de forma escalonada (`h1` $\rightarrow$ `h2` $\rightarrow$ `h3`). Sí puedes volver a subir de golpe (de un `<h3>` a un nuevo `<h2>` para iniciar otra sección).
2. **Nunca elijas la etiqueta por su tamaño visual:** Si necesitas que un título se vea más grande o más pequeño, eso se resuelve exclusivamente con CSS. La etiqueta HTML se elige **únicamente por la jerarquía semántica de la información**.

> [!IMPORTANT]
> Los motores de búsqueda (Google) y las personas que navegan con lectores de pantalla utilizan los encabezados para construir un **índice de contenidos navegable**. Si tienes múltiples `<h1>` o te saltas niveles, la página se vuelve confusa e inaccesible.

### Práctica 2: Construyendo un esquema jerárquico (en `index.html`)

En tu archivo `index.html`, escribe un esquema jerárquico con un único `<h1>` sobre tu tema de estudio favorito, dos secciones principales con `<h2>` y al menos dos subtemas en cada sección usando `<h3>`.

---

## 3. Párrafos (`p`), saltos de línea (`br`) y separadores (`hr`)

### Párrafos con `p`

Representan unidades de pensamiento o bloques de texto con una idea completa:

```html
<p>HTML estructura la información mediante elementos semánticos que aportan significado.</p>
<p>El navegador separa automáticamente los párrafos mediante un margen vertical predeterminado.</p>
```

### Saltos de línea justificados con `br`

`<br>` (*break*) es una **etiqueta vacía** (no tiene cierre `</br>`) que introduce un salto de línea dentro de un párrafo **únicamente cuando el corte es parte natural del contenido** (como en una dirección postal o un poema):

```html
<p>
  Av. Reforma 222, Piso 8<br>
  Colonia Juárez, CP 06600<br>
  Ciudad de México, México
</p>
```

### Cambio temático con `hr`

`<hr>` (*horizontal rule*) representa una **ruptura o cambio temático** entre dos bloques de texto. Aunque el navegador dibuja una línea gris horizontal por defecto, su valor real es semántico:

```html
<p>En este bloque analizamos la teoría del diseño responsivo.</p>

<!-- Ruptura temática: el tema cambia radicalmente a continuación -->
<hr>

<p>En este nuevo apartado revisaremos las tarifas y costos de los servidores.</p>
```

> [!WARNING]
> **Prohibido usar `<br><br><br>` para separar cosas:**  
> Nunca utilices etiquetas `<br>` sucesivas para generar espacios en blanco o empujar elementos hacia abajo. Los márgenes, separaciones y espacios visuales son responsabilidad exclusiva de CSS.

### Qué observar en párrafos y saltos

- Si dejas 10 saltos de línea con la tecla Enter dentro de un `<p>` en tu editor de código, el navegador los colapsará en **un único espacio en blanco**. Para saltar renglón sin abrir otro párrafo, la única herramienta válida es `<br>`.

### Práctica 3: Separación temática y saltos justificados (en `index.html`)

1. Agrega a tu `index.html` un párrafo con la dirección de tu oficina o centro de estudio utilizando `<br>` para cada renglón.
2. Coloca una etiqueta `<hr>` debajo.
3. Añade un nuevo párrafo para iniciar un tema diferente y observa cómo el navegador dibuja la división semántica.

---

## 4. Dar significado al texto: Semántica vs. Presentación

En los inicios de la web existían etiquetas puramente visuales (`<b>` para negrita, `<i>` para cursiva). HTML5 introdujo etiquetas que no solo cambian la apariencia, sino que **comunican qué significa ese texto**:

| Etiqueta Semántica | Significado Real | Etiqueta Visual Antigua | Diferencia Técnica Clave |
| --- | --- | --- | --- |
| `<strong>` | **Importancia seria o advertencia.** | `<b>` (Bold / Negrita) | `strong` altera el tono de voz en lectores de pantalla; `b` solo pone negrita visual sin valor semántico. |
| `<em>` | **Énfasis o acento verbal.** | `<i>` (Italic / Cursiva) | `em` cambia el sentido literal de la oración; `i` es solo cursiva para términos técnicos o nombres científicos. |
| `<del>` | Contenido **eliminado o tachado**. | `<s>` (Strikethrough) | `del` registra un historial de cambios o precios anteriores; `s` solo marca algo que ya no es vigente. |
| `<ins>` | Contenido **agregado o nuevo**. | `<u>` (Underline) | `ins` complementa a `del` (se muestra subrayado); evita usar `u` porque los usuarios lo confunden con un enlace. |
| `<mark>` | Texto **resaltado o relevante**. | N/A | Simula un marcador fluorescente amarillo para destacar coincidencias de búsqueda o notas. |
| `<small>` | Texto secundario o letra chica. | N/A | Representa notas al pie, avisos de copyright o términos y condiciones legales. |

### Código de ejemplo: Oferta comercial semántica

```html
<p><strong>Aviso importante:</strong> La promoción vence esta noche.</p>

<p>Este curso es <em>verdaderamente</em> práctico.</p>

<!-- Registro de actualización de precios -->
<p>Precio de lanzamiento: <del>$100 USD</del> <ins>$60 USD</ins>.</p>

<!-- Resaltado de búsqueda -->
<p>Resultados encontrados: términos de <mark>accesibilidad web</mark> en el documento.</p>

<!-- Letra chica legal -->
<p><small>© 2026 Empresa. Precios sujetos a cambio sin previo aviso.</small></p>
```

### Qué observar en el formato semántico

- Si una persona ciega navega por un sitio con lector de pantalla, `<strong>` y `<em>` se anuncian con una entonación diferente o indicando verbalmente la importancia, mientras que `<b>` e `<i>` suelen ser leídos con voz plana sin alertar al usuario.

> [!TIP]
> **Regla sencilla:** Si solo necesitas que una palabra se vea en negrita por diseño cosmético (como la primera palabra de una lista), usa CSS (`font-weight: bold`). Reserva `<strong>` únicamente cuando la palabra realmente implique advertencia, urgencia o jerarquía de lectura.

### Práctica 4: Formato semántico de oferta comercial (en `index.html`)

Escribe en tu `index.html` un párrafo de producto que contenga: una advertencia con `<strong>`, una palabra enfatizada con `<em>`, un precio tachado con `<del>` acompañado de su nuevo precio con `<ins>`, y un aviso legal final con `<small>`.

---

## 5. Expresiones matemáticas, fórmulas y referencias: `sup` y `sub`

- `<sup>` (*superscript*): Eleva el texto a una posición **superior** con tamaño reducido (exponentes matemáticos, notas al pie de página).
- `<sub>` (*subscript*): Desciende el texto a una posición **inferior** con tamaño reducido (fórmulas químicas, índices matemáticos).

```html
<!-- Fórmulas químicas -->
<p>El agua se compone de dos moléculas de hidrógeno y una de oxígeno: H<sub>2</sub>O.</p>

<!-- Exponentes matemáticos -->
<p>El teorema de Pitágoras establece que a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup>.</p>

<!-- Notas al pie de página / Referencias bibliográficas -->
<p>El estándar de accesibilidad fue actualizado recientemente<sup>[1]</sup>.</p>
```

### Qué observar en `sup` y `sub`

- Estas etiquetas tienen un valor semántico específico en ciencias y literatura técnica. No las utilices para mover letras arriba o abajo por razones puramente estéticas; para diseño tipográfico se utiliza CSS (`vertical-align`).

### Práctica 5: Fórmulas científicas y notas al pie (en `index.html`)

Agrega a tu `index.html` dos oraciones: una que describa la fórmula de la fotosíntesis o de un elemento químico con `<sub>`, y otra con una ecuación cuadrática o referencia bibliográfica con `<sup>`.

---

## 6. Abreviaturas, citas y fragmentos de código

Para contenidos de naturaleza técnica o académica, HTML dispone de elementos enriquecidos:

### Ejemplos de abreviaturas, citas y código

```html
<!-- 1. Abreviatura con título explicativo (muestra un tooltip al pasar el cursor) -->
<p>Estamos aprendiendo los estándares de <abbr title="HyperText Markup Language">HTML</abbr>.</p>

<!-- 2. Cita corta en línea (el navegador añade las comillas automáticamente) -->
<p>Como decía Sócrates: <q cite="https://es.wikipedia.org/wiki/S%C3%B3crates">Solo sé que no sé nada.</q></p>

<!-- 3. Cita en bloque extensa con su respectiva fuente -->
<blockquote cite="https://w3.org">
  <p>El poder de la Web está en su universalidad. El acceso de todos, independientemente de la discapacidad, es un aspecto esencial.</p>
  <cite>— Tim Berners-Lee, creador de la Web</cite>
</blockquote>

<!-- 4. Fragmento de código en línea -->
<p>Para definir un encabezado principal se utiliza la etiqueta <code>&lt;h1&gt;</code>.</p>

<!-- 5. Bloque de código con espacios y saltos respetados exactamente -->
<pre><code>function saludar(nombre) {
  return "Hola, " + nombre;
}</code></pre>
```

### ¿Por qué escribimos `&lt;h1&gt;` en lugar de `<h1>`? (Entidades HTML)

> [!IMPORTANT]
> **La regla del escape de caracteres:**  
> Si dentro de un párrafo escribes literalmente `<code><h1></code>`, el navegador **pensará que estás abriendo un encabezado real** e intentará renderizarlo como título en lugar de mostrar el texto.  
> Cuando necesitas mostrar los símbolos de menor que (`<`) y mayor que (`>`) como texto visible, debes usar sus **entidades HTML**:
>
> - `<` se escribe como `&lt;` (*less than*)
> - `>` se escribe como `&gt;` (*greater than*)
> - `&` se escribe como `&amp;` (*ampersand*)

### Qué observar en citas y bloques de código

- **`<q>` vs. comillas manuales:** La etiqueta `<q>` inserta las comillas tipográficas correctas según el idioma configurado en `<html lang="...">` (comillas latinas `« »` en español formal o comillas inglesas `" "` en inglés).
- **El superpoder de `<pre>`:** A diferencia de las demás etiquetas donde el navegador colapsa múltiples espacios en blanco, `<pre>` respeta cada tabulación, espacio y salto de línea exactamente como lo escribiste en tu editor.

### Práctica 6: Citas estructuradas y código escapado (en `index.html`)

1. Agrega a tu `index.html` una cita en bloque `<blockquote>` con su autor dentro de `<cite>`.
2. Añade debajo un bloque `<pre><code>` que contenga tres líneas de código de programación con sangría/indentación.
3. Explica dentro de un párrafo cómo se escribe una etiqueta HTML usando las entidades `&lt;` y `&gt;`.

---

## 7. Contenedores genéricos en línea y atributos globales

### Agrupación neutra con `span`

La etiqueta `<span>` es un contenedor en línea **completamente carente de significado semántico**. Se utiliza para envolver una palabra o frase cuando necesitas aplicarle un estilo con CSS o manipularla con JavaScript sin alterar el valor semántico del texto:

```html
<p>El estado actual del servidor es <span class="badge-activo">Operativo</span>.</p>
```

### Atributos Globales indispensables

Los atributos son directivas que se colocan dentro de la etiqueta de apertura para configurar propiedades o identificar el elemento:

```html
<!-- Ejemplo con múltiples atributos globales combinados -->
<p id="parrafo-principal" class="alerta texto-grande" lang="en" title="Información adicional">
  This sentence is in English.
</p>
```

| Atributo Global | Propósito | Regla de Oro |
| --- | --- | --- |
| `id` | Identificador **único** e irrepetible para un solo elemento en toda la página. | **Nunca se puede duplicar.** No puede haber dos elementos con el mismo `id` en el mismo archivo. |
| `class` | Clasificador grupal para uno o varios elementos que compartirán estilos o lógica. | **Se puede repetir** en tantos elementos como quieras. Un elemento puede tener múltiples clases separadas por espacios. |
| `title` | Muestra un texto flotante de ayuda (*tooltip*) al colocar el ratón encima. | Útil para pistas secundarias; nunca pongas información crítica aquí porque no funciona en móviles. |
| `lang` | Declara el idioma específico de ese fragmento de texto si difiere del resto de la página. | Ayuda a los lectores de pantalla a pronunciar correctamente frases en idiomas extranjeros. |

> [!WARNING]
> **Cuidado con duplicar IDs:** Si repites un `id="destacado"` en dos elementos diferentes, romperás la validación del W3C, arruinarás los enlaces de ancla interna y provocarás fallos silenciosos en scripts de JavaScript.

### Práctica 7: Identificadores y clases grupales (en `index.html`)

1. En tu `index.html`, crea dos párrafos que compartan la misma `class="resumen-modulo"`.
2. Asigna un `id="contacto-oficial"` a uno solo de ellos.
3. Añade una frase en otro idioma (inglés, francés, etc.) dentro de un párrafo envolviéndola en un `<span lang="en">`.

---

## Reto final de la lección: Artículo de Divulgación Científica

Ahora que dominas la jerarquía de encabezados, el formato semántico, las citas y los atributos en tu laboratorio (`index.html`), demostrarás tu autonomía maquetando un documento estructurado completo desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `02-texto-y-atributos`. Construirás un **Artículo de Divulgación Científica sobre la Exploración Espacial** que cumpla estrictamente con la siguiente lista de control:

- [x] Estructura base completa de HTML5 (`<!DOCTYPE html>`, `<html lang="es">`, `<head>` con metadatos y `<body>`).
- [x] **Jerarquía impecable:**
  - Un único encabezado principal `<h1>` con el título del artículo y su respectivo `id="titulo-articulo"`.
  - Al menos dos secciones temáticas divididas con `<h2>`.
  - Al menos una de las secciones debe subdividirse con un `<h3>` sin saltarse ningún nivel intermedio.
- [x] **Formatos semánticos en el contenido:**
  - Al menos tres párrafos `<p>` bien redactados.
  - Una advertencia o dato crítico enfatizado con `<strong>`.
  - Un concepto clave con acento verbal usando `<em>`.
  - Un fragmento de texto resaltado con `<mark>`.
  - Un registro de actualización de datos utilizando `<del>` para el dato anterior e `<ins>` para el dato corregido.
  - Una nota legal o de aclaración secundaria con `<small>`.
- [x] **Ciencia y fórmulas:**
  - Al menos una fórmula química (ej. combustible de cohetes o agua) o expresión física/matemática utilizando correctamente `<sub>` o `<sup>`.
- [x] **Abreviaturas y citas:**
  - Una abreviatura técnica explicada mediante `<abbr title="...">` (ej. NASA, ESA, CO₂).
  - Una cita textual extensa en bloque mediante `<blockquote>` con su atributo `cite` y la mención de su autor con `<cite>`.
- [x] **Código y datos técnicos:**
  - Un bloque de código de programación formateado con `<pre><code>` con indentación respetada.
  - La explicación en texto de una etiqueta HTML utilizando las entidades de escape obligatorias `&lt;` y `&gt;`.
- [x] **Atributos globales:**
  - Al menos dos párrafos deben compartir la misma `class="parrafo-destacado"`.
  - Un fragmento de texto en otro idioma envuelto en `<span lang="...">`.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Por qué es un error grave de accesibilidad y SEO saltar de un `<h2>` directamente a un `<h5>` para que el texto se vea más pequeño?
2. ¿Cuál es la diferencia de comportamiento visual y espacial entre un elemento en bloque (`block`) y un elemento en línea (`inline`)?
3. Si solo necesitas poner una palabra en negrita por razones visuales de diseño, ¿por qué deberías evitar la etiqueta `<strong>`?
4. ¿Por qué el atributo `id` debe ser estrictamente único en todo el documento, mientras que el atributo `class` puede repetirse?
5. ¿Qué ocurre en el navegador si escribes `<code><p></code>` directamente sin usar las entidades `&lt;` y `&gt;`?

---

## 📚 Recursos y documentación oficial

Para profundizar en el formateo semántico y jerarquía de textos, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Fundamentos de texto en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/HTML_text_fundamentals)
- 📖 [Elementos de bloque vs. elementos en línea - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Block-level_elements)
- 📖 [Referencia de encabezados (`<h1>` a `<h6>`) - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/Heading_Elements)
- 📖 [Atributos globales en HTML - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Global_attributes)
- 📖 [Entidades y caracteres especiales en HTML - MDN](https://developer.mozilla.org/es/docs/Glossary/Entity)
