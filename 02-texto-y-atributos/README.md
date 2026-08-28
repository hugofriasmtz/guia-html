# Lección 2: texto, jerarquía y atributos

Esta lección continúa el documento que preparaste en [Estructura HTML5](../01-estructura-html/README.md). Ya comprendes el esqueleto base (`html`, `head`, `body`); ahora aprenderás a estructurar y dar significado real a todo el texto que vivirá dentro de `<body>`.

> [!TIP]
> Trabaja sobre el archivo `index.html` de la lección anterior. Agrega cada nuevo ejemplo dentro de la etiqueta `<body>`, guarda los cambios y refresca tu navegador para ver los resultados.

---

## 1. Modelo mental: Elementos en Bloque vs. Elementos en Línea

Antes de escribir texto, debes conocer los dos comportamientos naturales de las etiquetas en HTML:

```text
ELEMENTO EN BLOQUE (ej. <h1>, <p>, <hr>):
+-------------------------------------------------------------------+
| Ocupa todo el ancho disponible y fuerza un salto de línea antes y |
| después de él. Empieza siempre en un renglón nuevo.               |
+-------------------------------------------------------------------+

ELEMENTO EN LÍNEA (ej. <strong>, <em>, <span>, <code>):
Texto normal con un [elemento en línea] que solo ocupa el ancho de su contenido.
```

- **Elementos en Bloque (*Block*):** Crean estructuras grandes y párrafos independientes.
- **Elementos en Línea (*Inline*):** Viven **dentro** de un bloque de texto y no rompen el flujo de la lectura.

---

## 2. Encabezados: de `h1` a `h6`

Los encabezados organizan la jerarquía de la información, de mayor a menor importancia:

| Etiqueta | Nivel | ¿Cuándo utilizarla? |
| --- | --- | --- |
| `h1` | Primario | **Título principal de toda la página.** Solo debe haber **uno** por documento. |
| `h2` | Secundario | Título de una sección principal de contenido. |
| `h3` | Terciario | Subtema dentro de un `h2`. |
| `h4` | Nivel 4 | Subtema dentro de un `h3`. |
| `h5` | Nivel 5 | Subtema muy específico dentro de un `h4`. |
| `h6` | Nivel 6 | El nivel más específico y profundo disponible. |

### Ejemplo de jerarquía correcta

```html
<h1>Manual de Desarrollo Web</h1>

<h2>1. Fundamentos de HTML</h2>
<h3>1.1. Estructura básica</h3>
<h3>1.2. Encabezados y párrafos</h3>

<h2>2. Estilos con CSS</h2>
<h3>2.1. Selectores</h3>
<h4>2.1.1. Selectores de clase</h4>
```

### Las 2 Reglas de Oro de los encabezados

1. **Nunca te saltes niveles:** No pases de un `<h2>` directo a un `<h4>`. La jerarquía debe ser siempre escalonada.
2. **No elijas la etiqueta por su tamaño visual:** Si quieres un texto más grande o más pequeño, eso lo resolverás después con CSS. Elige la etiqueta únicamente por la relación jerárquica del tema.

> [!IMPORTANT]
> Los lectores de pantalla para personas con discapacidad visual y los motores de búsqueda como Google usan los encabezados como un índice para navegar por tu página. Una jerarquía rota arruina la accesibilidad y el SEO.

---

## 3. Párrafos (`p`), saltos de línea (`br`) y separadores (`hr`)

### Párrafos con `p`

Representan bloques normales de texto con una idea completa:

```html
<p>HTML estructura el contenido de una página mediante etiquetas semánticas.</p>
<p>El navegador se encarga de separar cada párrafo con un margen vertical automático.</p>
```

### Saltos de línea con `br` y divisiones temáticas con `hr`

Ambas son **etiquetas vacías** (no tienen etiqueta de cierre):

```html
<!-- br: Salto de línea donde el corte es parte del contenido -->
<p>
  Av. Juárez 100<br>
  Código Postal 06000<br>
  Ciudad de México
</p>

<!-- hr: Cambio temático de contenido (línea separadora) -->
<hr>

<p>Aquí comienza un tema completamente diferente al anterior.</p>
```

> [!WARNING]
> Nunca uses `<br><br><br>` para crear espacios en blanco o empujar elementos hacia abajo. Los espacios y separaciones visuales son responsabilidad exclusiva de CSS.

---

## 4. Dar significado al texto: Semántica vs. Presentación

HTML moderno no busca simplemente cambiar cómo se ve el texto, sino **comunicar qué significa**.

| Etiqueta Semántica | Significado real | Etiqueta Visual Antigua | Diferencia clave |
| --- | --- | --- | --- |
| `<strong>` | **Importancia o urgencia grave.** | `<b>` (Bold) | `strong` altera el tono en lectores de pantalla; `b` solo pone negrita sin importancia. |
| `<em>` | **Énfasis o acento verbal.** | `<i>` (Italic) | `em` cambia el sentido de la frase; `i` es solo texto cursivo (términos técnicos, nombres científicos). |
| `<del>` | Contenido **eliminado o tachado**. | `<s>` (Strikethrough) | `del` indica historial de cambio; `s` solo marca algo que ya no es vigente. |
| `<ins>` | Contenido **agregado o nuevo**. | `<u>` (Underline) | `ins` complementa a `del`; `u` solo subraya (evita `u` porque parece un enlace). |

### Ejemplo práctico de formato semántico

```html
<p><strong>Aviso urgente:</strong> La reunión cambió de horario.</p>
<p>Este curso es <em>realmente</em> práctico.</p>
<p>El precio anterior era <del>$100 USD</del> y el nuevo precio es <ins>$75 USD</ins>.</p>
<p>Para revisar: <mark>entregar antes del viernes</mark>.</p>
<p><small>Términos y condiciones sujetos a cambios sin previo aviso.</small></p>
```

---

## 5. Expresiones matemáticas y referencias: `sup` y `sub`

- `sup` (*superscript*): Texto en posición **superior** (exponentes matemáticos, notas al pie de página).
- `sub` (*subscript*): Texto en posición **inferior** (fórmulas químicas, índices numéricos).

```html
<p>La fórmula química del agua es H<sub>2</sub>O.</p>
<p>El teorema de Pitágoras se expresa como a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup>.</p>
<p>Este dato fue extraído de un estudio oficial<sup>[1]</sup>.</p>
```

> [!NOTE]
> `sup` y `sub` tienen valor semántico real en fórmulas y citas bibliográficas. No los uses solo para mover letras hacia arriba o abajo por razones decorativas.

---

## 6. Abreviaturas, citas y código

Para textos con naturaleza técnica o literaria, HTML dispone de etiquetas específicas:

```html
<!-- Abreviaturas con explicación al pasar el ratón -->
<p>Estamos aprendiendo <abbr title="HyperText Markup Language">HTML</abbr>.</p>

<!-- Cita corta dentro de un párrafo -->
<p>Como decía Steve Jobs: <q cite="https://ejemplo.com">Sigue hambriento, sigue alocado.</q></p>

<!-- Cita en bloque extensa -->
<blockquote cite="https://w3.org">
  <p>El poder de la Web está en su universalidad. El acceso de todos, independientemente de la discapacidad, es un aspecto esencial.</p>
  <cite>— Tim Berners-Lee, creador de la Web</cite>
</blockquote>

<!-- Fragmentos de código -->
<p>Para crear un párrafo en HTML se utiliza la etiqueta <code>&lt;p&gt;</code>.</p>

<!-- Bloque de código con espacios y saltos respetados -->
<pre><code>function saludar() {
  console.log("¡Hola, mundo!");
}</code></pre>
```

- `q`: Agrega automáticamente las comillas tipográficas según el idioma configurado en `<html lang="...">`.
- `blockquote`: Bloque para citas largas que se destaca del resto del texto.
- `code` y `pre`: `code` indica que el texto es código de programación; `pre` le ordena al navegador que mantenga los espacios en blanco e indentaciones exactas tal como fueron escritos.

---

## 7. Agrupación genérica en línea con `span`

La etiqueta `span` es un contenedor en línea **neutro**. No tiene ningún significado semántico por sí misma.

```html
<p>El estado del servidor es <span class="servidor-activo">Operativo</span>.</p>
```

### ¿Para qué sirve `span`?

Se utiliza para envolver una palabra o frase corta cuando después quieres aplicarle un estilo visual con CSS (como cambiarle el color) o manipularla con JavaScript, sin alterar el significado semántico del párrafo.

---

## 8. Atributos Globales indispensables

Los atributos son modificadores que se agregan a la etiqueta de apertura para aportar datos extra o identificar el elemento:

```html
<p id="parrafo-destacado" class="alerta texto-grande" lang="en" title="Información extra">
  This is an important warning message.
</p>
```

| Atributo | Propósito | Regla de Oro |
| --- | --- | --- |
| `id` | Identificador **único** para un solo elemento en toda la página. | **No se puede repetir.** Solo puede existir un elemento con ese mismo `id` en todo el documento. |
| `class` | Clasificador o etiqueta grupal para uno o varios elementos. | **Se puede repetir** en múltiples elementos que compartirán estilos. Un elemento puede tener varias clases separadas por espacios. |
| `title` | Muestra un texto emergente (*tooltip*) al pasar el cursor por encima. | Útil como ayuda visual secundaria, pero no pongas información crítica ahí. |
| `lang` | Cambia el idioma de ese fragmento específico de texto. | Ideal si estás escribiendo en español pero citas una frase en inglés o francés. |

---

## Reto final de la lección

Crea un artículo de blog estructurado en tu archivo `index.html` que cumpla con toda la siguiente lista de verificación:

- [ ] Un único `h1` con el título del artículo y un `id="titulo-articulo"`.
- [ ] Al menos dos secciones divididas con `h2`, y una de ellas subdividida con un `h3`.
- [ ] Al menos tres párrafos `<p>` que incluyan:
  - Una palabra importante con `<strong>`.
  - Una palabra con énfasis con `<em>`.
  - Un fragmento de texto marcado con `<mark>`.
  - Una corrección histórica con `<del>` e `<ins>`.
- [ ] Una dirección o poema que utilice correctamente `<br>` para saltos de línea justificados.
- [ ] Una fórmula química o matemática con `<sup>` o `<sub>`.
- [ ] Una abreviatura con `<abbr title="...">`.
- [ ] Una cita textual con `<blockquote>` y su respectiva etiqueta `<cite>`.
- [ ] Un bloque de código con `<pre><code>`.
- [ ] Al menos dos párrafos que compartan la misma `class="parrafo-resumen"`.

### Preguntas de autoevaluación

1. ¿Por qué es una mala práctica saltar de un `<h2>` directamente a un `<h5>`?
2. ¿Cuál es la diferencia entre un elemento en bloque (`block`) y uno en línea (`inline`)?
3. Si solo quieres poner una palabra en negrita sin que signifique "urgencia o importancia", ¿qué etiqueta debes usar y por qué?
4. ¿Por qué el atributo `id` no debe repetirse en una misma página web?

---

## 📚 Recursos y documentación oficial

Para profundizar en el formateo semántico y jerarquía de textos, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Fundamentos de texto en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/HTML_text_fundamentals)
- 📖 [Elementos de bloque vs. elementos en línea - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Block-level_elements)
- 📖 [Atributos globales en HTML - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Global_attributes)
