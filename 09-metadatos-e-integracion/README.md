# Lección 9: Metadatos, integración externa y SEO técnico

Esta lección continúa la ruta tras aprender los componentes nativos en [Elementos Interactivos](../08-elementos-interactivos/README.md). Hasta ahora nos hemos enfocado casi exclusivamente en lo que ocurre dentro de `<body>` (lo visible para el usuario). En este capítulo nos trasladamos a la "sala de máquinas" del documento: la etiqueta `<head>`.

Aprenderás a configurar metadatos para buscadores (SEO), previsualizaciones atractivas en redes sociales (Open Graph), favicons modernos y la integración optimizada de hojas de estilo (CSS) y scripts (JavaScript).

> [!TIP]
> Crea tu archivo `index.html` dentro de `09-metadatos-e-integracion`. Aunque la mayoría de estas etiquetas no pintan texto en la pantalla, podrás comprobar sus efectos inspeccionando la pestaña del navegador, probando cómo se comparte en redes y revisando el tráfico de red en las herramientas de desarrollo (*DevTools*).

---

## 1. Modelo mental: La sala de control (`<head>`) vs. El escenario (`<body>`)

```text
+-----------------------------------------------------------------------+
|  <head> : LA SALA DE CONTROL (Invisible para el usuario directo)      |
|  - ¿Cómo se codifica el texto? (UTF-8)                               |
|  - ¿Cómo debe escalar en pantallas móviles? (Viewport)               |
|  - ¿Cómo nos indexa Google? (SEO y Canónicas)                        |
|  - ¿Cómo se ve al compartir en WhatsApp/Twitter? (Open Graph)        |
|  - Recursos externos: Tipografías, Estilos CSS, Iconos, Scripts.     |
+-----------------------------------------------------------------------+
|  <body> : EL ESCENARIO (Lo que el usuario ve e interactúa)           |
|  - Encabezados, párrafos, formularios, tablas, botones, etc.         |
+-----------------------------------------------------------------------+
```

---

## 2. Metadatos esenciales para renderizado y SEO básico

Toda página web profesional en producción debe contar como mínimo con las siguientes etiquetas dentro de `<head>`:

```html
<head>
  <!-- 1. Juego de caracteres universal -->
  <meta charset="UTF-8">

  <!-- 2. Adaptabilidad en dispositivos móviles (Responsive Design) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Título único de la pestaña y del resultado en Google (máx. 60 caracteres) -->
  <title>Aprende Desarrollo Web Moderno | MiPlataforma</title>

  <!-- 4. Descripción para el resumen de Google (Snippet SEO, 150-160 caracteres) -->
  <meta name="description" content="Aprende HTML5 semántico, CSS moderno y accesibilidad web paso a paso con proyectos prácticos desde cero.">

  <!-- 5. Autor y control de rastreadores (Googlebot) -->
  <meta name="author" content="Tu Nombre o Empresa">
  <meta name="robots" content="index, follow">

  <!-- 6. Color de la barra de navegación del navegador en móviles (Android/Safari) -->
  <meta name="theme-color" content="#0f172a">
</head>
```

### Explicación de etiquetas clave

| Etiqueta / Atributo | ¿Para qué sirve? | Impacto si se omite |
| --- | --- | --- |
| `charset="UTF-8"` | Soporte para tildes, eñes, caracteres especiales y emojis. | Caracteres rotos tipo `Ã±` o ``. |
| `viewport` | Le indica al móvil que ajuste el ancho de la página al ancho de su pantalla. | En móviles la web se verá minúscula y con zoom alejado. |
| `<title>` | Título de la pestaña, marcador del navegador y encabezado en Google. | Pésimo SEO y pestaña con la URL cruda. |
| `name="description"` | Texto de vista previa que aparece debajo del título en búsquedas de Google. | Google elegirá texto al azar de tu página para mostrar. |
| `name="robots"` | Instrucciones a los motores de búsqueda (`index`/`noindex`, `follow`/`nofollow`). | Comportamiento por defecto del rastreador. |

---

## 3. Favicons e identidad de marca

El favicon es el icono identificativo que aparece en la pestaña del navegador, marcadores y accesos directos:

```html
<!-- Favicon clásico para navegadores antiguos -->
<link rel="icon" href="/favicon.ico" sizes="any">

<!-- Favicon vectorial moderno (escala perfecto y soporta modo oscuro) -->
<link rel="icon" href="/favicon.svg" type="image/svg+xml">

<!-- Icono para cuando el usuario guarda la web en la pantalla de inicio de iPhone/iPad -->
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

---

## 4. Integración de recursos externos y optimización de rendimiento

Para conectar fuentes y hojas de estilo utilizamos `<link>`:

```html
<!-- Conexión a hoja de estilos CSS externa -->
<link rel="stylesheet" href="css/estilos.css">

<!-- Optimización de tipografías externas (ej. Google Fonts) -->
<!-- 1. Abre la conexión DNS anticipadamente para acelerar la descarga -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- 2. Descarga la tipografía -->
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap">
```

> [!NOTE]
> `rel="preconnect"` y `rel="dns-prefetch"` son *Resource Hints* (pistas de recursos). Le ordenan al navegador resolver la conexión al servidor de fuentes antes de que empiece a procesar el CSS, reduciendo el tiempo de carga notablemente.

---

## 5. Carga de scripts JavaScript: `defer` vs. `async`

Por defecto, cuando el navegador encuentra un `<script>`, detiene la lectura del HTML hasta descargar y ejecutar el script. Para evitar que la página se quede congelada en blanco, usamos atributos de carga asíncrona:

```text
SÍNCRONO (Sin atributos - BLOQUEA EL PARSING):
HTML Parsing ----> [ PAUSA / Descarga JS + Ejecuta ] ----> Sigue HTML Parsing

ASYNC (Se ejecuta apenas descarga, sin respetar orden):
HTML Parsing -------------------------> [ PAUSA / Ejecuta JS ] ---> Sigue HTML
           \-- Descarga JS (Paralelo) --/

DEFER (Descarga en paralelo y ejecuta AL FINAL en orden exacto - RECOMENDADO):
HTML Parsing -----------------------------------------------------> [ Fin del HTML ]
           \-- Descarga JS (Paralelo) --/                           [ Ejecuta JS ]
```

### Comparativa de inclusión de scripts

```html
<!-- 1. DEFER (La opción recomendada para la gran mayoría de casos) -->
<!-- Descarga en paralelo y se ejecuta solo cuando todo el HTML ha sido leído -->
<script src="app.js" defer></script>

<!-- 2. ASYNC (Ideal para scripts independientes como Google Analytics o publicidad) -->
<!-- Se ejecuta de inmediato en cuanto termina de descargar, interrumpiendo el HTML -->
<script src="analiticas.js" async></script>

<!-- 3. MÓDULOS MODERNOS (Tienen comportamiento defer automático) -->
<script type="module" src="main.js"></script>
```

> [!WARNING]
> Nunca uses `async` para scripts que dependan unos de otros o que necesiten manipular elementos del HTML antes de que existan en el DOM. Para esos casos, usa siempre `defer`.

---

## 6. Social Cards: Open Graph (WhatsApp, Facebook, LinkedIn) y Twitter

Cuando compartes un enlace por WhatsApp, Telegram, Slack, LinkedIn o X (Twitter), las aplicaciones leen metadatos especiales para generar una tarjeta enriquecida con imagen, título y descripción:

```html
<!-- OPEN GRAPH (Estándar adoptado por WhatsApp, Facebook, LinkedIn, Discord, etc.) -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://misitio.com/cursos/html5">
<meta property="og:title" content="Aprende HTML5 Profesional desde Cero">
<meta property="og:description" content="Domina la estructura web moderna, semántica, accesibilidad y metadatos con proyectos reales.">
<!-- La imagen debe ser una URL absoluta y se recomienda un tamaño de 1200x630 píxeles -->
<meta property="og:image" content="https://misitio.com/assets/og-portada.jpg">

<!-- TWITTER CARDS (Específico para X / Twitter) -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@usuario_empresa">
<meta name="twitter:title" content="Aprende HTML5 Profesional desde Cero">
<meta name="twitter:description" content="Domina la estructura web moderna, semántica y accesibilidad.">
<meta name="twitter:image" content="https://misitio.com/assets/og-portada.jpg">
```

---

## 7. SEO Técnico y Enlaces Canónicos

Si una misma página puede ser accedida desde múltiples URLs (por ejemplo `https://ejemplo.com/producto`, `https://ejemplo.com/producto?color=azul` o `http://www.ejemplo.com/producto`), los buscadores podrían penalizar tu web por **contenido duplicado**.

Para indicarle a Google cuál es la URL oficial y definitiva, se utiliza la etiqueta canónica:

```html
<link rel="canonical" href="https://misitio.com/cursos/html5">
```

---

## Reto final de la lección

Construye un archivo `index.html` completamente configurado para una **Landing Page de Lanzamiento de un Producto Digital / Startup** que incluya un `<head>` de nivel profesional con la siguiente lista de verificación:

- [ ] Declaración de `<!DOCTYPE html>` e `<html lang="es">`.
- [ ] Configuración esencial de renderizado:
  - Codificación con `charset="UTF-8"`.
  - `viewport` configurado para diseño responsivo.
  - `theme-color` con un color hexadecimal acorde a la marca.
- [ ] SEO básico:
  - `<title>` descriptivo que incluya el nombre de la marca y la propuesta de valor.
  - `<meta name="description">` optimizada de entre 140 y 160 caracteres.
  - `<meta name="robots" content="index, follow">`.
  - Enlace canónico `<link rel="canonical" href="...">`.
- [ ] Iconos de identidad:
  - Un favicon clásico `.ico` o `.svg`.
  - Un enlace `apple-touch-icon`.
- [ ] Optimización de recursos externos:
  - Al menos una conexión optimizada con `<link rel="preconnect">` a Google Fonts y la importación de su CSS.
  - Un archivo CSS local vinculado con `<link rel="stylesheet">`.
  - Un script local vinculado de forma no bloqueante usando el atributo `defer`.
- [ ] Tarjetas completas para redes sociales:
  - Todas las etiquetas Open Graph indispensables (`og:title`, `og:description`, `og:image`, `og:url`, `og:type`).
  - Tarjeta de Twitter configurada con `summary_large_image`.
- [ ] Un `<body>` mínimo pero semántico (`<header>`, `<main>`, `<footer>`) para comprobar que el documento es válido.

### Preguntas de autoevaluación

1. ¿Qué problema visual crítico ocurrirá en un teléfono móvil inteligente si olvidas incluir la etiqueta `<meta name="viewport" ...>`?
2. ¿Cuál es la diferencia fundamental en la descarga y ejecución de un script con el atributo `defer` frente a uno con `async`?
3. ¿Por qué las URLs de las imágenes en las etiquetas `og:image` deben ser rutas absolutas (con `https://`) en lugar de relativas?
4. ¿Para qué sirve la etiqueta `<link rel="canonical">` y qué problema evita en los motores de búsqueda?

---

## 📚 Recursos y documentación oficial

Para profundizar en la configuración avanzada del documento y las etiquetas del `<head>`, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Qué hay en el `<head>`: Metadatos en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/What_is_in_the_head)
- 📖 [Referencia del elemento `<meta>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/meta)
- 📖 [Referencia del elemento `<script>` y atributos de carga - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/script)
- 📖 [El protocolo Open Graph - Documentación oficial](https://ogp.me/)
