# Lección 4: Agrupación semántica y estructura de página

Esta lección continúa el trabajo de [Enlaces y listas](../03-enlaces-y-listas/README.md). Ya sabes cómo dar formato al texto, crear listas y enlazar contenidos; ahora aprenderás a estructurar el esqueleto semántico completo de una página web (*Layout*) utilizando las etiquetas de estructura de HTML5.

> [!TIP]
> Antes de escribir una sola línea de código en un proyecto real, dibuja en una libreta o imagina las cajas principales que compondrán tu página web.

---

## 1. Modelo mental: Anatomía semántica de una web

Antes de HTML5, los desarrolladores usaban `<div class="header">`, `<div class="footer">`, etc. HTML5 introdujo **etiquetas semánticas estructurales** (*landmarks*) que le explican al navegador, a Google y a los lectores de pantalla qué función cumple cada sección:

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
|  |  |  (Noticia/  |  |   (Noticia/   | |  |    lateral    | |
|  |  |   Producto) |  |    Producto)  | |  |  - Enlaces    | |
|  |  +-------------+  +---------------+ |  |    relacionados|
|  +-------------------------------------+  |  - Publicidad | |
|                                           +---------------+ |
+-------------------------------------------------------------+
|                      <footer>                               |
|   - Derechos de autor (Copyright), enlaces legales, etc.    |
+-------------------------------------------------------------+
```

---

## 2. Las etiquetas estructurales principales

| Etiqueta | Propósito Semántico | Regla de Oro |
| --- | --- | --- |
| `<header>` | Cabecera o bloque introductorio de la página o de un artículo. | Puede contener el logo, el lema y el menú `<nav>`. |
| `<nav>` | Contenedor de los **enlaces de navegación principales** del sitio. | No todo enlace va en `nav`; resérvalo para menús importantes. |
| `<main>` | Contiene el **contenido único y principal** del documento. | **Solo debe haber uno por página** y no debe ir dentro de header ni footer. |
| `<section>` | Agrupación temática genérica de contenido que suele tener su propio encabezado (`h2`-`h6`). | Úsalo para dividir temas: "Quiénes somos", "Servicios", "Contacto". |
| `<article>` | Contenido **independiente y reutilizable** (tiene sentido por sí solo fuera de la web). | Entradas de blog, noticias, tarjetas de producto, reseñas. |
| `<aside>` | Contenido indirectamente relacionado o complementario. | Barras laterales (*sidebars*), glosarios, publicidad o biografías cortas. |
| `<footer>` | Pie de página o cierre de la página o de un artículo. | Información legal, autor, copyright, enlaces de privacidad. |

---

## 3. `section` vs. `article` vs. `div` (El dilema más común)

Para decidir qué etiqueta usar, sigue este diagrama de decisión:

```text
¿El contenido tiene sentido si lo extraes y publicas solo en otra web o en un lector RSS?
 ├── SÍ  ──> Usa <article> (ej. Una noticia, un post de blog, una reseña de producto).
 └── NO
      └── ¿El contenido representa un bloque temático claro con su propio título?
           ├── SÍ  ──> Usa <section> (ej. Sección "Nuestros Servicios" o "Testimonios").
           └── NO  ──> Usa <div> (Solo para aplicar estilos con CSS o crear envoltorios visuales).
```

---

## 4. Ejemplo de código estructurado

Crea un archivo `index.html` dentro de tu carpeta `04-agrupacion-semantica/` y prueba esta estructura:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog de Tecnología</title>
</head>
<body>

  <!-- Encabezado general del sitio -->
  <header>
    <h1>Mundo Tecnológico</h1>
    <nav>
      <ul>
        <li><a href="#inicio">Inicio</a></li>
        <li><a href="#articulos">Artículos</a></li>
        <li><a href="#contacto">Contacto</a></li>
      </ul>
    </nav>
  </header>

  <!-- Contenido principal de la página -->
  <main>
    <section id="articulos">
      <h2>Últimas Publicaciones</h2>
      
      <!-- Cada artículo es independiente -->
      <article>
        <header>
          <h3>¿Qué es HTML5 semántico?</h3>
          <p><small>Publicado el <time datetime="2026-08-27">27 de agosto de 2026</time></small></p>
        </header>
        <p>El HTML semántico dota de significado y accesibilidad a la estructura de la web, facilitando que máquinas y humanos la comprendan.</p>
        <footer>
          <p><small>Autor: Alex Dev</small></p>
        </footer>
      </article>
    </section>

    <!-- Barra lateral con contenido complementario -->
    <aside>
      <h2>Sobre el autor</h2>
      <p>Desarrollador web apasionado por los estándares web y el código limpio.</p>
    </aside>
  </main>

  <!-- Pie de página general -->
  <footer>
    <p>&copy; 2026 Mundo Tecnológico. Todos los derechos reservados.</p>
  </footer>

</body>
</html>
```

### Qué observar en la estructura

- Tanto la página completa como un `<article>` individual pueden tener su propio `<header>` y `<footer>` interno.
- La etiqueta `<time datetime="YYYY-MM-DD">` permite a los motores de búsqueda leer fechas exactas en formato legible por máquinas.
- Cada `<section>` y `<article>` tiene su propio encabezado (`h2`, `h3`) para mantener la jerarquía ordenada.

> [!IMPORTANT]
> Un documento **solo puede tener un elemento `<main>` visible**. Nunca coloques `<main>` dentro de `<header>`, `<footer>` ni dentro de un `<article>`.

---

## 5. El contenedor neutro: `div`

La etiqueta `<div>` (*division*) es un contenedor en bloque **sin ningún valor semántico**.

```html
<!-- div usado correctamente: solo como caja para aplicar diseño CSS en cuadrícula -->
<div class="tarjetas-contenedor">
  <article>...</article>
  <article>...</article>
</div>
```

> [!WARNING]
> **Evita la "Divitis":** No uses `<div>` para todo. Si el bloque es un menú usa `<nav>`, si es un pie de página usa `<footer>`, y si es un artículo usa `<article>`. Reserva `<div>` únicamente cuando necesites una caja para acomodar el diseño con CSS.

---

## Reto final de la lección

Crea una maqueta semántica completa para el sitio web de un **Restaurante local** en tu archivo `index.html`:

- [x] Un `<header>` con el nombre del restaurante (`h1`) y un menú de navegación `<nav>`.
- [x] Un único elemento `<main>` que envuelva todo el cuerpo central de la página.
- [x] Una `<section>` de "Especialidades del Día" con al menos 2 `<article>` (cada plato con su nombre `h3`, descripción y precio).
- [x] Una `<section>` de "Horarios y Ubicación" con los datos del local.
- [x] Un `<aside>` con una promoción especial o el mensaje del chef del mes.
- [x] Un `<footer>` con el copyright y enlaces de contacto o redes sociales.
- [x] Verifica que no existan errores de anidamiento y que la jerarquía de títulos (`h1`, `h2`, `h3`) sea coherente.

### Preguntas de autoevaluación

1. ¿Cuál es la diferencia fundamental entre `<section>` y `<article>`?
2. ¿Por qué solo debe existir un elemento `<main>` por página?
3. ¿En qué situaciones específicas está justificado el uso de un `<div>`?

---

## 📚 Recursos y documentación oficial

Para profundizar en la arquitectura y semántica estructural de páginas web, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Estructura del documento y del sitio web - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Document_and_website_structure)
- 📖 [Elementos de sección en HTML5 - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element#elementos_de_sección)
- 📖 [Referencia del elemento `<main>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/main)
