# Lección 2: texto, etiquetas y atributos

Esta lección continúa el documento que preparaste en [Estructura HTML5](../01-estructura-html/README.md). Ya tienes `html`, `head` y `body`; ahora aprenderás a escribir y organizar texto dentro de `body`.

> [!TIP]
> Trabaja sobre el mismo `index.html` de la lección anterior. Agrega cada ejemplo dentro de `body`, guarda el archivo y revisa el resultado en el navegador.

## 1. Encabezados: de `h1` a `h6`

Los encabezados organizan los temas de una página. HTML tiene seis niveles:

| Etiqueta | ¿Para qué sirve? |
| --- | --- |
| `h1` | Título principal de toda la página. |
| `h2` | Título de una sección principal. |
| `h3` | Subtema dentro de una sección `h2`. |
| `h4` | Subtema dentro de una sección `h3`. |
| `h5` | Subtema dentro de una sección `h4`. |
| `h6` | Nivel más específico de encabezado. |

### Ejemplo de jerarquía

Agrega este contenido dentro de `body`:

```html
<h1>Guía para crear una página web</h1>

<h2>Planear la página</h2>
<h3>Definir el objetivo</h3>
<h3>Conocer al público</h3>

<h2>Construir la página</h2>
<h3>Crear el contenido</h3>
<h4>Escribir los textos</h4>
<h5>Revisar los títulos</h5>
<h6>Comprobar los detalles</h6>
```

El ejemplo se puede leer como el índice de un libro: `h1` presenta el tema general, `h2` divide los temas principales y los niveles siguientes crean subdivisiones.

> [!IMPORTANT]
> No elijas `h3`, `h4`, `h5` o `h6` porque su texto se vea más pequeño. El nivel representa la relación del contenido. Más adelante CSS cambiará el tamaño visual.

### Práctica de encabezados

Crea la estructura de un artículo sobre una ciudad usando:

- Un `h1` para el nombre del artículo.
- Tres `h2` para los temas principales.
- Al menos un `h3` dentro de cada `h2`.
- Un `h4` dentro de uno de tus `h3`.

Después lee únicamente tus encabezados. Si parecen el índice ordenado de un artículo, la jerarquía está bien encaminada.

> [!NOTE]
> En HTML, el nivel del encabezado depende de la importancia y relación del tema. Su tamaño visual se puede cambiar más adelante con CSS.

## 2. Párrafos con `p`

La etiqueta `p` representa un párrafo: un bloque normal de texto.

```html
<h1>Mi portafolio</h1>
<p>Estoy aprendiendo a crear páginas web.</p>
<p>Mi objetivo es construir sitios claros, útiles y fáciles de navegar.</p>
```

El navegador coloca cada párrafo en una línea o bloque separado. No necesitas agregar etiquetas especiales para que el texto pase al siguiente renglón.

### Qué observar en los párrafos

- Cada `p` contiene una idea o bloque de texto.
- Los párrafos aparecen en el orden en que los escribes.
- El espacio que ves entre ellos es un estilo predeterminado del navegador.

### Práctica de párrafos

Agrega tres párrafos sobre ti:

- Quién eres.
- Qué estás aprendiendo.
- Qué tipo de página quieres crear.

## 3. Saltos de línea y separadores

Usa `br` cuando un salto de línea forma parte del contenido, por ejemplo, en una dirección o una canción. No lo uses para crear espacios de diseño.

```html
<p>
  Reforma 25<br>
  Centro, Ciudad de México
</p>
```

Usa `hr` para separar un cambio de tema dentro del contenido:

```html
<p>Esta es la introducción del artículo.</p>
<hr>
<p>Ahora comienza una sección diferente.</p>
```

### Qué observar en `br` y `hr`

- `br` cambia de línea dentro del mismo contenido.
- `hr` marca una separación entre temas.
- Ninguna de las dos etiquetas sirve para construir el diseño completo de la página.

> [!WARNING]
> No uses muchos `br` para acomodar una página. Los espacios, columnas y posiciones se resolverán después con CSS.

### Reto de separación

Escribe una dirección usando `br` y crea un artículo con dos temas separados por `hr`. Explica por qué cada etiqueta está justificada.

## 4. Dar significado al texto

Estas etiquetas no solo cambian la apariencia: indican qué significa el texto.

```html
<p><strong>Importante:</strong> guarda tu trabajo con frecuencia.</p>
<p>Este término tiene <em>énfasis</em> dentro de la oración.</p>
<p><mark>Texto resaltado</mark> para revisar después.</p>
<p><small>Nota legal o información secundaria.</small></p>
<p><del>Texto eliminado</del> y <ins>texto agregado</ins>.</p>
<p>La palabra <u>revisar</u> está marcada para llamar la atención.</p>
```

- `strong` indica importancia.
- `em` indica énfasis.
- `mark` resalta una parte relacionada con el contexto.
- `small` representa texto secundario o de menor importancia.
- `del` representa contenido eliminado.
- `ins` representa contenido agregado.
- `u` marca un texto que necesita una atención especial, pero no debe usarse solo para decorar.

`b`, `i` y `s` también existen, pero tienen significados más específicos:

```html
<p><b>Palabra clave</b> dentro de una explicación.</p>
<p><i>Nombre científico</i> dentro de un texto.</p>
<p><s>Evento cancelado</s></p>
```

- `b` llama la atención sobre una palabra sin indicar importancia especial.
- `i` representa una voz, término o expresión diferenciada.
- `s` representa información que ya no es correcta o relevante.

### Qué observar en el formato del texto

`strong`, `em`, `del` e `ins` aportan significado. Aunque el navegador suele mostrar estos elementos con estilos distintos, su función principal es explicar qué representa cada fragmento.

> [!NOTE]
> No elijas una etiqueta porque haga el texto negrita o inclinado. Elige la que describa mejor el significado; CSS se encargará de la apariencia.

### Práctica de formato semántico

Escribe un aviso que incluya:

- Una parte importante.
- Una palabra con énfasis.
- Un texto resaltado.
- Un dato corregido con `del` e `ins`.

## 5. Texto superior e inferior: `sup` y `sub`

`sup` coloca texto en una posición superior y `sub` en una posición inferior. Son útiles para exponentes, fórmulas y referencias.

```html
<p>La fórmula del agua es H<sub>2</sub>O.</p>
<p>La expresión matemática es x<sup>2</sup> + y<sup>2</sup>.</p>
<p>Consulta la referencia<sup>1</sup>.</p>
```

El número no cambia el tamaño mediante CSS: `sup` y `sub` expresan que ese texto tiene una relación superior o inferior con el contenido principal.

### Qué observar en `sup` y `sub`

- `sup` puede representar un exponente o una referencia.
- `sub` puede representar parte de una fórmula.
- El número o símbolo sigue siendo parte del contenido del texto.

> [!CAUTION]
> No uses `sup` o `sub` únicamente para mover texto hacia arriba o abajo por diseño. Si necesitas cambiar la posición visual, ese trabajo corresponde a CSS.

### Reto de expresiones

Escribe en HTML:

- La fórmula del dióxido de carbono: CO₂.
- La fórmula del área de un cuadrado: A = l².
- Una nota al pie con un número superior.

## 6. Abreviaturas, citas y código

HTML tiene etiquetas para textos con significados particulares:

```html
<p><abbr title="HyperText Markup Language">HTML</abbr> estructura el contenido web.</p>
<p>Como dice el refrán: <q>La práctica hace al maestro.</q></p>
<blockquote>
  <p>Una estructura clara facilita el mantenimiento de una página.</p>
</blockquote>
<p>Para abrir una página, escribe <code>index.html</code>.</p>
<pre><code>h1 { color: red; }</code></pre>
```

- `abbr` muestra una abreviatura con su significado completo en `title`.
- `q` representa una cita breve dentro de un párrafo.
- `blockquote` representa una cita extensa.
- `code` representa una parte de código.
- `pre` conserva espacios y saltos de línea, útil para mostrar código con formato.

### Qué observar en estas etiquetas

Cada etiqueta comunica un tipo de texto distinto: una abreviatura, una cita breve, una cita extensa o código. El navegador puede aplicarles estilos predeterminados, pero el significado es lo más importante.

### Práctica de texto especializado

Crea una explicación breve sobre HTML que incluya:

- Una abreviatura.
- Una cita breve.
- Una cita extensa.
- Un fragmento de código.

## 7. Agrupar texto con `span`

`span` agrupa una parte pequeña de texto sin darle un significado especial. Es útil cuando después quieres aplicarle CSS o identificarlo para JavaScript.

```html
<p>Mi nivel actual es <span>principiante</span>.</p>
```

`span` no crea una sección ni un bloque nuevo. Solo marca una parte dentro de otro contenido.

### Qué observar en `span`

Si quitas `span`, el texto seguirá apareciendo. Su función es identificar un fragmento pequeño para trabajarlo después, no crear una sección ni cambiar por sí solo la apariencia.

> [!IMPORTANT]
> Usa `span` para fragmentos pequeños. Para agrupar temas completos utiliza etiquetas como `section`, `article` o `div` cuando corresponda.

### Reto de `span`

Escribe un párrafo sobre tu aprendizaje y marca con `span` una palabra que después quieras cambiar de color con CSS. Explica por qué `span` es adecuado para esa palabra.

## 8. Atributos relacionados con el texto

Los atributos agregan información o identifican elementos. Ahora que entiendes el contenido, puedes estudiarlos al final de la lección.

```html
<h1 id="inicio" class="titulo-principal" title="Título de la página">
  Mi portafolio
</h1>
<p lang="es" dir="ltr">Estoy aprendiendo HTML.</p>
```

- `id` identifica un elemento único. Después puede servir para enlazarlo.
- `class` agrupa elementos que compartirán características.
- `title` ofrece información adicional cuando la persona pasa el cursor, aunque no debe sustituir contenido importante.
- `lang` indica el idioma del contenido.
- `dir` indica la dirección del texto, por ejemplo `ltr` de izquierda a derecha.

### Qué observar en los atributos

Los atributos no son contenido independiente. Agregan información al elemento o lo identifican para que la página pueda enlazarlo, describirlo o aplicarle estilos más adelante.

### Práctica de atributos

Agrega a tu página:

- Un `id` a la sección inicial.
- Una `class` a dos párrafos relacionados.
- Un `title` que aporte información adicional a un elemento.
- `lang="es"` en el documento si todavía no lo agregaste en la lección anterior.

## Reto final de la lección

Crea una página de presentación que incluya:

- Un `h1` y por lo menos dos niveles adicionales de encabezado.
- Párrafos con `strong`, `em`, `mark` y `small`.
- Un ejemplo con `sup` y otro con `sub`.
- Una cita con `q` o `blockquote`.
- Un fragmento de código con `code`.
- Una palabra agrupada con `span`.
- Atributos `id`, `class`, `title` y `lang`.

Revisa el resultado sin CSS y explica qué función cumple cada etiqueta. No avances hasta distinguir entre una etiqueta que describe el significado del texto y un estilo que solo cambiará su apariencia.
