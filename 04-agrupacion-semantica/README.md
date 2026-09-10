# Lección 4: Agrupación semántica y estructura de página

Esta lección continúa el trabajo de [Enlaces y listas](../03-enlaces-y-listas/README.md). Ya sabes cómo dar formato al texto, enlazar contenidos y estructurar datos en listas; ahora aprenderás a construir el esqueleto semántico completo de una página web (*Layout*) utilizando las etiquetas estructurales de HTML5.

---

## 1. Modelo mental: Anatomía semántica y Puntos de Referencia (*Landmarks*)

Antes de HTML5, las páginas se construían apilando cajas genéricas sin significado (`<div class="header">`, `<div class="menu">`, `<div class="footer">`). HTML5 introdujo **etiquetas estructurales semánticas** (*landmarks*) que le explican al navegador, a Google y a las tecnologías de asistencia la función exacta de cada bloque:

```text
+-------------------------------------------------------------+
|                      <header>                               |
|   - Logotipo / Nombre del sitio                             |
|   - <nav> (Menú de navegación principal)                    |
+-------------------------------------------------------------+
|                                                             |
|                          <main>                             |
|  +-------------------------------------+  +---------------+ |
|  |             <section>               |  |    <aside>    | |
|  |  +-------------+  +---------------+ |  |               | |
|  |  |  <article>  |  |   <article>   | |  |  - Barra      | |
|  |  |  (Entrada/  |  |   (Entrada/   | |  |    lateral    | |
|  |  |   Producto) |  |    Producto)  | |  |  - Biografía  | |
|  |  +-------------+  +---------------+ |  |  - Enlaces    | |
|  +-------------------------------------+  |    relevantes | |
|                                           +---------------+ |
+-------------------------------------------------------------+
|                      <footer>                               |
|   - Derechos de autor (Copyright), enlaces legales, etc.    |
+-------------------------------------------------------------+
```

### Qué observar en la anatomía semántica

- **Puntos de Referencia (*Landmarks*) en DevTools:** Los lectores de pantalla reconocen etiquetas como `<header>`, `<nav>`, `<main>`, `<aside>` y `<footer>` como zonas clave de navegación. Los usuarios ciegos pueden presionar un atajo de teclado para saltar directamente al `<main>` sin tener que escuchar todo el menú.
- Puedes verificar estos landmarks abriendo las **Herramientas de Desarrollador (F12)** $\rightarrow$ pestaña **Elementos** $\rightarrow$ pestaña lateral **Accesibilidad**.

### Práctica 1: La trinidad estructural base (en `index.html`)

1. Crea tu archivo `index.html` con la estructura base de HTML5 (`<!DOCTYPE html>`, `<html>`, `<head>` y `<body>`).
2. Dentro de `<body>`, escribe los tres bloques fundamentales: `<header>`, `<main>` y `<footer>`.
3. Abre DevTools (`F12`), ve al panel de Accesibilidad y comprueba cómo el navegador identifica automáticamente las regiones estructurales de tu documento.

---

## 2. Las etiquetas estructurales principales

| Etiqueta | Propósito Semántico | Regla de Oro |
| --- | --- | --- |
| `<header>` | Cabecera o bloque introductorio de la página o de un artículo. | Puede contener el logotipo, el título principal y la barra `<nav>`. |
| `<nav>` | Contenedor exclusivo de los **enlaces de navegación principales**. | No todo enlace va en `nav`; resérvalo para menús importantes del sitio. |
| `<main>` | Contenedor del **contenido central y único** del documento. | **Solo debe haber uno por página** y nunca debe anidarse dentro de header ni footer. |
| `<section>` | Agrupación temática genérica que trata un asunto específico. | Debe tener **su propio encabezado** (`h2`-`h6`) para titular la sección. |
| `<article>` | Unidad de contenido **independiente y reutilizable**. | Debe tener sentido por sí sola si la extraes y publicas en otro sitio (feed RSS). |
| `<aside>` | Contenido indirectamente relacionado o complementario. | Barras laterales (*sidebars*), biografías cortas, glosarios o publicidad. |
| `<footer>` | Pie de página o bloque de cierre. | Avisos legales, autoría, copyright, enlaces de privacidad y contacto. |

### Código de ejemplo: Cabecera y Pie global

```html
<!-- Encabezado general del sitio -->
<header>
  <h1>Mundo Tecnológico</h1>
  <nav aria-label="Navegación principal">
    <ul>
      <li><a href="#inicio">Inicio</a></li>
      <li><a href="#articulos">Artículos</a></li>
      <li><a href="#contacto">Contacto</a></li>
    </ul>
  </nav>
</header>

<!-- Pie de página general -->
<footer>
  <p>&copy; 2026 Mundo Tecnológico. Todos los derechos reservados.</p>
  <p><a href="#privacidad">Políticas de Privacidad</a></p>
</footer>
```

### Qué observar en los elementos estructurales

- **`<nav>` etiquetado:** Añadir `aria-label="Navegación principal"` ayuda a distinguir este menú si más adelante incluyes un segundo menú secundario en el pie de página.
- **Un único `<main>`:** El navegador espera que `<main>` represente lo exclusivo de esa página. Lo que se repite en todo el sitio (logo, menú global, copyright) queda fuera de `<main>`.

> [!IMPORTANT]
> Nunca coloques `<main>` dentro de `<header>`, `<footer>` ni dentro de un `<article>`. Debe ser un hijo directo del `<body>`.

### Práctica 2: Menú de navegación y pie (en `index.html`)

1. En tu archivo `index.html`, completa el `<header>` con un `<h1>` para tu blog y un menú `<nav>` con 3 enlaces.
2. Añade un `<footer>` con una nota de derechos de autor usando la entidad `&copy;` (©).
3. Comprueba en el navegador que el encabezado y el pie delimiten correctamente el espacio donde irá el contenido principal.

---

## 3. El dilema clásico: `section` vs. `article` vs. `div`

Uno de los mayores desafíos al comenzar con HTML5 es saber qué caja usar para agrupar contenido. Sigue este árbol de decisión mental:

```text
¿El contenido tiene sentido y se entiende por completo si lo extraes y publicas solo en otra web o en redes sociales?
 ├── SÍ  ──> Usa <article> (ej. Una noticia, un post de blog, una tarjeta de producto, una reseña).
 └── NO
      └── ¿El contenido representa un bloque temático claro que necesita su propio título?
           ├── SÍ  ──> Usa <section> (ej. Sección "Nuestros Servicios", "Testimonios", "Galería").
           └── NO  ──> Usa <div> (Solo para aplicar estilos CSS, flexbox o cuadrículas visuales).
```

### Código de ejemplo: Artículos dentro de una sección temática

```html
<main>
  <!-- Sección temática que agrupa todas las publicaciones -->
  <section id="articulos">
    <h2>Últimas Publicaciones</h2>

    <!-- Artículo 1: Unidad independiente de contenido -->
    <article>
      <h3>¿Qué es HTML5 semántico?</h3>
      <p>El HTML semántico dota de significado a la estructura web, facilitando que humanos y motores de búsqueda la comprendan.</p>
      <p><a href="#leer-mas">Leer artículo completo...</a></p>
    </article>

    <!-- Artículo 2: Otra unidad independiente -->
    <article>
      <h3>Guía rápida de Flexbox</h3>
      <p>Aprende a distribuir el espacio entre elementos de interfaz de forma dinámica y responsiva.</p>
      <p><a href="#leer-mas">Leer artículo completo...</a></p>
    </article>
  </section>
</main>
```

### Qué observar en `section` y `article`

- **La regla del encabezado:** Toda `<section>` debe tener un encabezado (`<h2>`, `<h3>`, etc.) que anuncie de qué trata ese bloque. Si una caja no necesita título, probablemente no sea una sección semántica sino un simple `<div>`.
- **Anidamiento bidireccional:** Un `<section>` puede contener múltiples `<article>` (como una sección de blog con varias entradas), pero un `<article>` extenso también puede dividirse internamente en varios `<section>` (por ejemplo, un reportaje largo dividido en "Introducción", "Metodología" y "Conclusiones").

> [!NOTE]
> La prueba de fuego para `<article>`: Si puedes enviarlo en un correo electrónico o mostrarlo en un lector de noticias RSS sin que pierda sentido, es un `<article>`.

### Práctica 3: Publicaciones del blog (en `index.html`)

1. Dentro del elemento `<main>` de tu `index.html`, crea una `<section id="articulos">` con su respectivo encabezado `<h2>`.
2. Dentro de esa sección, inserta dos elementos `<article>`, cada uno con su propio título `<h3>`, un párrafo descriptivo y un enlace de lectura.

---

## 4. Contenido complementario con `aside` y fechas legibles con `<time>`

### La barra lateral o apéndice con `<aside>`

`<aside>` representa información tangencialmente relacionada con el contenido principal. Si se eliminara de la página, el contenido central seguiría entendiéndose a la perfección:

```html
<!-- Barra lateral dentro de main -->
<aside>
  <h2>Sobre el autor</h2>
  <p>Alex Dev es educador web y apasionado por los estándares de código limpio y accesibilidad.</p>
  <ul>
    <li><a href="https://github.com">GitHub</a></li>
    <li><a href="https://linkedin.com">LinkedIn</a></li>
  </ul>
</aside>
```

### Fechas legibles por máquinas con `<time>`

El texto "hace 2 días" o "27 de agosto" es fácil de entender para un humano, pero confuso para un rastreador de Google. La etiqueta `<time>` resuelve esto con su atributo obligatorio `datetime`:

```html
<article>
  <header>
    <h3>Novedades de la Web en 2026</h3>
    <!-- El texto visible es para humanos; el atributo datetime es para las máquinas -->
    <p><small>Publicado el <time datetime="2026-08-27">27 de agosto de 2026</time></small></p>
  </header>
  <p>Resumen de las nuevas APIs nativas de los navegadores modernos...</p>
</article>
```

### Formatos estándar del atributo `datetime`

| Formato | Ejemplo en `datetime` | Uso común |
| --- | --- | --- |
| **Fecha simple** | `datetime="2026-08-27"` | Publicaciones de blog, cumpleaños, efemérides. |
| **Fecha y hora** | `datetime="2026-08-27T18:30"` | Horarios de vuelos, inicio de conferencias en vivo. |
| **Año y mes** | `datetime="2026-08"` | Periodos de estudio o historial laboral en un CV. |

### Qué observar en `aside` y `time`

- **Ámbito de `<aside>`:** Si `<aside>` se coloca dentro de un `<article>`, se considera complementario exclusivamente a ese artículo (como un glosario o notas al pie). Si se coloca dentro de `<main>`, se considera complementario a toda la página (como una barra lateral del sitio).
- **Impacto SEO de `<time>`:** Google utiliza las fechas de `<time datetime="...">` para mostrar la antigüedad de los artículos en la lista de resultados de búsqueda.

### Práctica 4: Barra lateral y fechas estructuradas (en `index.html`)

1. Agrega una etiqueta `<time datetime="YYYY-MM-DD">` dentro del primer `<article>` de tu `index.html` para indicar su fecha de publicación.
2. Agrega un `<aside>` dentro de `<main>` con una biografía corta del autor y enlaces a sus perfiles.

---

## 5. El contenedor neutro: `div` y cómo evitar la "Divitis"

La etiqueta `<div>` (*division*) es un elemento en bloque **completamente carente de valor semántico**. No le dice absolutamente nada al navegador sobre su contenido.

```html
<!-- ✅ USO CORRECTO: div solo como contenedor visual para aplicar CSS Flexbox o Grid -->
<div class="contenedor-columnas">
  <section id="articulos">...</section>
  <aside>...</aside>
</div>
```

```html
<!-- ❌ USO INCORRECTO: "Divitis" (destruye la semántica y la accesibilidad) -->
<div class="header">
  <div class="titulo">Mi Blog</div>
  <div class="nav">
    <div class="link"><a href="/">Inicio</a></div>
  </div>
</div>
```

### Qué observar en el uso de `div`

- Los lectores de pantalla ignoran los elementos `<div>` en el Árbol de Accesibilidad y pasan directamente a su contenido interno.
- Úsalo sin miedo cuando necesites una caja para centrar con CSS, crear fondos de pantalla o acomodar elementos en cuadrícula, pero **nunca como sustituto de una etiqueta semántica**.

> [!WARNING]
> **Evita la "Divitis":** Si el bloque es una cabecera usa `<header>`, si es un menú usa `<nav>`, si es un artículo usa `<article>`, y si es un pie de página usa `<footer>`. Si sustituyes todo por `<div>`, destruyes la estructura que permite a los buscadores y lectores de pantalla entender tu web.

### Práctica 5: Envoltorio visual para diseño (en `index.html`)

1. Envuelve tu `<section id="articulos">` y tu `<aside>` dentro de un `<div class="contenido-con-sidebar">`.
2. Inspecciona el código en DevTools (F12) y observa cómo el `div` actúa como caja contenedora sin alterar los roles accesibles de la sección ni de la barra lateral.

---

## Reto final de la lección: Maquetación Semántica para un Restaurante Local

Ahora que probaste cada etiqueta estructural en tu laboratorio (`index.html`), demostrarás tu autonomía maquetando la estructura completa de un sitio web desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `04-agrupacion-semantica`. Construirás la maqueta semántica del sitio web de un **Restaurante Tradicional** que cumpla estrictamente con la siguiente lista de control:

- [x] Estructura base completa de HTML5 (`<!DOCTYPE html>`, `<html lang="es">`, `<head>` con metadatos y `<body>`).
- [x] **Cabecera global (`<header>`):**
  - Un encabezado principal `<h1>` con el nombre del restaurante.
  - Una barra `<nav aria-label="Navegación principal">` con al menos 3 enlaces relativos (`#menu`, `#horarios`, `#chef`).
- [x] **Contenido principal (`<main>`):**
  - Un único elemento `<main>` que envuelva todo el cuerpo central de la página.
- [x] **Sección de Menú (`<section id="menu">`):**
  - Encabezado `<h2>` que titule la sección.
  - Al menos dos platos estructurados como elementos `<article>` independientes.
  - Cada plato debe incluir su nombre en un `<h3>`, descripción, precio y una etiqueta `<time>` que indique el tiempo estimado de preparación o temporada.
- [x] **Sección de Horarios y Ubicación (`<section id="horarios">`):**
  - Encabezado `<h2>`.
  - Párrafos estructurados con la dirección física y días de apertura.
- [x] **Barra lateral o apéndice (`<aside id="chef">`):**
  - Un mensaje especial del Chef con su filosofía culinaria o la promoción destacada de la semana.
- [x] **Pie de página (`<footer>`):**
  - Copyright formal usando la entidad `&copy;`.
  - Enlaces de contacto o redes sociales.
- [x] **Calidad estructural:** Jerarquía de encabezados ordenada (`h1` $\rightarrow$ `h2` $\rightarrow$ `h3`) sin saltos de nivel y ausencia de "divitis" injustificada.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Cuál es la diferencia conceptual y funcional entre un elemento `<section>` y un elemento `<article>`?
2. ¿Por qué el estándar de HTML5 exige que solo exista un elemento `<main>` visible por documento?
3. ¿En qué escenario técnico está plenamente justificado utilizar una etiqueta `<div>`?
4. ¿Qué ventaja aporta el atributo `datetime` en la etiqueta `<time>` en comparación con escribir la fecha como texto simple en un `<p>`?
5. ¿Qué es un *Landmark* (punto de referencia) de accesibilidad y cómo beneficia a una persona que utiliza un lector de pantalla?

---

## 📚 Recursos y documentación oficial

Para profundizar en la arquitectura y semántica estructural de páginas web, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Estructura del documento y del sitio web - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Document_and_website_structure)
- 📖 [Elementos de sección en HTML5 - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element#elementos_de_sección)
- 📖 [Referencia del elemento `<main>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/main)
- 📖 [Elemento `<time>` y formato de fechas - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/time)
- 📖 [Guía de Puntos de Referencia ARIA (Landmarks) - W3C WAI](https://www.w3.org/WAI/ARIA/apg/practices/landmark-regions/)
