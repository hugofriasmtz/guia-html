# Lección 11: Arquitectura de sitios multipágina y navegación estructurada

Esta lección continúa la ruta tras dominar los estándares de [Accesibilidad y Validación](../10-accesibilidad-y-validacion/README.md). En el desarrollo profesional, rara vez trabajarás en un solo archivo aislado; los sitios web reales están compuestos por decenas o cientos de documentos interconectados.

En este capítulo aprenderás a diseñar **arquitecturas de carpetas escalables**, dominar la **resolución de rutas relativas**, mantener la **consistencia estructural** entre páginas y construir sistemas de navegación accesibles (como migas de pan o *breadcrumbs* y estados de página activa).

> [!TIP]
> En esta lección no trabajarás con un único archivo. Crearás una estructura con múltiples archivos `.html` y carpetas de recursos (*assets*) dentro de `11-sitio-multipagina` para poner a prueba la navegación real entre páginas.

---

## 1. Modelo mental: Árbol de directorios y resolución de rutas

Para que las páginas, imágenes y hojas de estilo se encuentren entre sí, debes comprender cómo moverte hacia arriba o hacia abajo en el árbol de carpetas del proyecto:

```text
MI-SITIO-WEB/
│
├── index.html                  <-- Página de inicio (Raíz)
├── nosotros.html               <-- Página al mismo nivel
│
├── servicios/
│   ├── index.html              <-- Subpágina de servicios
│   └── consultoria.html        <-- Subpágina anidada
│
└── assets/
    ├── css/
    │   └── estilos.css         <-- Hoja de estilos
    └── img/
        └── logo.svg            <-- Imagen compartida
```

### Reglas de navegación entre directorios

```text
MISMO NIVEL:
nosotros.html busca a index.html:           href="index.html" (o "./index.html")

BAJAR A UNA SUBCARPETA:
index.html busca a consultoria.html:        href="servicios/consultoria.html"

SUBIR UN NIVEL (..):
consultoria.html busca a nosotros.html:     href="../nosotros.html"

SUBIR Y VOLVER A BAJAR:
consultoria.html busca el logo:             src="../assets/img/logo.svg"
```

---

## 2. Rutas relativas vs. Rutas absolutas

| Tipo de Ruta | Ejemplo de sintaxis | ¿Cómo funciona? | ¿Cuándo utilizarla? |
| --- | --- | --- | --- |
| **Relativa simple** | `href="contacto.html"` | Busca el archivo en la misma carpeta donde está el documento actual. | Enlaces entre páginas que conviven en el mismo directorio. |
| **Relativa ascendente** | `href="../index.html"` | Sube un nivel en las carpetas con `../` para buscar el archivo. | Enlaces desde páginas dentro de subcarpetas hacia la raíz. |
| **Relativa a la raíz** | `href="/assets/img/logo.png"` | Inicia la búsqueda desde la raíz del servidor web (la barra `/` inicial). | Proyectos servidos mediante servidores locales (Live Server, Vite) o en producción. |
| **Absoluta externa** | `href="https://sitio.com/guia"` | URL completa con protocolo y dominio. | Enlaces hacia páginas externas ajenas a tu sitio. |

> [!WARNING]
> Ten cuidado con las rutas que inician con barra diagonal `/` (como `href="/contacto.html"`) si abres los archivos haciendo doble clic directo en el explorador (`file:///C:/...`). La barra `/` buscará la raíz de tu disco duro, no la de tu proyecto. Utiliza siempre extensiones de servidor local como *Live Server* en VS Code.

---

## 3. Navegación global consistente y estado activo (`aria-current`)

En un sitio multipágina, la cabecera (`<header>`) y el pie de página (`<footer>`) deben mantenerse estructuralmente idénticos en todas las vistas para ofrecer predictibilidad al usuario.

Para que los usuarios (y los lectores de pantalla) sepan exactamente en qué página se encuentran parados, se utiliza el atributo `aria-current="page"`:

### En el archivo `index.html` (Inicio)

```html
<header>
  <a href="index.html" class="logo">
    <img src="assets/img/logo.svg" alt="Inicio - MiEmpresa">
  </a>

  <nav aria-label="Navegación principal">
    <ul>
      <li><a href="index.html" aria-current="page" class="activo">Inicio</a></li>
      <li><a href="nosotros.html">Nosotros</a></li>
      <li><a href="servicios/index.html">Servicios</a></li>
      <li><a href="contacto.html">Contacto</a></li>
    </ul>
  </nav>
</header>
```

### En el archivo `nosotros.html`

```html
<header>
  <a href="index.html" class="logo">
    <img src="assets/img/logo.svg" alt="Inicio - MiEmpresa">
  </a>

  <nav aria-label="Navegación principal">
    <ul>
      <li><a href="index.html">Inicio</a></li>
      <li><a href="nosotros.html" aria-current="page" class="activo">Nosotros</a></li>
      <li><a href="servicios/index.html">Servicios</a></li>
      <li><a href="contacto.html">Contacto</a></li>
    </ul>
  </nav>
</header>
```

> [!NOTE]
> `aria-current="page"` comunica semánticamente a las tecnologías de asistencia que ese enlace corresponde a la página actual, mientras que la clase CSS `.activo` se usa para destacarlo visualmente.

---

## 4. Migas de pan semánticas (*Breadcrumbs*)

Las migas de pan indican la jerarquía de ubicación en páginas anidadas o profundas. La estructura semántica recomendada por los estándares es una lista ordenada `<ol>` dentro de un `<nav>` con su respectiva etiqueta accesible:

```html
<!-- Ubicación: servicios/consultoria.html -->
<nav aria-label="Migas de pan" class="breadcrumbs">
  <ol>
    <li><a href="../index.html">Inicio</a></li>
    <li><a href="index.html">Servicios</a></li>
    <li aria-current="page">Consultoría Estratégica</li>
  </ol>
</nav>
```

- La última posición de la lista representa la página actual: no lleva enlace `<a>` y se marca con `aria-current="page"`.

---

## 5. Arquitectura recomendada para proyectos web

Para mantener un proyecto ordenado a medida que crece, adopta una convención modular clara:

```text
proyecto-web/
│
├── index.html                   # Página de inicio principal
├── nosotros.html                # Vista de información institucional
├── contacto.html                # Formulario de contacto y soporte
│
├── blog/                        # Sección temática con subpáginas
│   ├── index.html               # Listado de todos los artículos
│   └── primer-articulo.html     # Vista individual de un artículo
│
└── assets/                      # Recursos estáticos
    ├── css/
    │   └── main.css             # Estilos globales
    ├── js/
    │   └── app.js               # Lógica interactiva
    └── img/
        ├── brand/               # Logos e isotipos
        └── content/             # Fotografías e ilustraciones de artículos
```

---

## Reto final de la lección

Construye un **Sitio Web Multipágina de 4 Vistas Interconectadas** dentro de tu carpeta `11-sitio-multipagina` respetando la arquitectura de archivos y cumpliendo todos los puntos de verificación:

- [ ] Estructura de carpetas y archivos organizada:

  ```text
  11-sitio-multipagina/
  ├── index.html
  ├── nosotros.html
  ├── contacto.html
  ├── servicios/
  │   └── index.html
  └── assets/
      └── img/
  ```

- [ ] Enlace global de navegación idéntico en las 4 páginas dentro de un `<nav aria-label="Navegación principal">`.
- [ ] Atributo `aria-current="page"` ubicado correctamente en el enlace correspondiente a la vista abierta en cada uno de los 4 archivos.
- [ ] Rutas relativas correctamente resueltas (ej. desde `servicios/index.html` para volver al inicio usando `../index.html`).
- [ ] Una barra de migas de pan (*Breadcrumbs*) semántica dentro de `servicios/index.html` que permita regresar a la página de Inicio.
- [ ] Metadatos `<title>` y `<meta name="description">` únicos y personalizados en cada uno de los 4 archivos `.html`.
- [ ] Un pie de página común (`<footer>`) en todas las vistas con información de derechos de autor y enlaces secundarios relativos.

### Preguntas de autoevaluación

1. Si estás editando el archivo `servicios/consultoria.html`, ¿qué ruta relativa debes escribir en un enlace para dirigir al usuario a `nosotros.html` situado en la raíz?
2. ¿Por qué es importante incluir el atributo `aria-current="page"` en el menú de navegación además de cambiar el color del enlace con una clase CSS?
3. ¿Cuál es la estructura HTML recomendada por el W3C para representar unas migas de pan (*breadcrumbs*) accesibles?
4. ¿Qué diferencia técnica existe entre una ruta que empieza por `./archivo.html` y otra que empieza por `../archivo.html`?

---

## 📚 Recursos y documentación oficial

Para profundizar en la navegación web, estructuración de URLs y buenas prácticas de enlazado, consulta **MDN Web Docs**:

- 📖 [Creando hipervínculos y rutas relativas en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Creating_hyperlinks)
- 📖 [Patrón accesible de Migas de Pan (Breadcrumb Pattern) - W3C WAI](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)
- 📖 [El atributo `aria-current` en la navegación - MDN](https://developer.mozilla.org/es/docs/Web/Accessibility/ARIA/Attributes/aria-current)
