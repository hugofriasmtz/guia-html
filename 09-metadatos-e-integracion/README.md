# Lección 9: Metadatos, integración externa y SEO técnico

Esta lección continúa la ruta tras aprender los componentes nativos en [Elementos Interactivos](../08-elementos-interactivos/README.md). Hasta ahora nos hemos enfocado casi exclusivamente en lo que ocurre dentro de `<body>` (lo visible para el usuario). En este capítulo nos trasladamos a la "sala de máquinas" del documento: la etiqueta `<head>`.

Aprenderás a configurar metadatos para motores de búsqueda (SEO), tarjetas de previsualización para redes sociales y mensajería (Open Graph), favicons modernos de alta resolución y la integración optimizada de hojas de estilo (CSS) y scripts (JavaScript) sin bloquear la pantalla.

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

El navegador procesa el documento HTML de arriba hacia abajo. Todo lo que coloques en el `<head>` le enseña al motor de renderizado **cómo interpretar, conectar y dimensionar** la página antes de dibujar el primer píxel del `<body>`.

### Qué observar en la separación entre `<head>` y `<body>`

- Nada de lo que esté dentro de `<head>` (excepto el título de la pestaña) se mostrará visualmente en el lienzo de la página.
- Si colocas por error etiquetas de contenido como `<h1>` o `<p>` dentro del `<head>`, los navegadores modernos forzarán el cierre automático del `<head>` y empujarán ese contenido hacia el `<body>`, rompiendo la arquitectura del documento.

### Práctica 1: Inspeccionando la sala de máquinas (en `index.html`)

1. Crea tu archivo `index.html` con una estructura mínima de HTML5.
2. Abre la página en tu navegador y presiona la tecla `F12` (o clic derecho $\rightarrow$ *Inspeccionar*).
3. En la pestaña **Elementos / Inspector**, despliega la etiqueta `<head>` y comprueba cómo el navegador mantiene organizadas las directivas internas separadas del `<body>`.

---

## 2. Metadatos esenciales para renderizado y SEO básico

Toda página web moderna en producción debe contar como mínimo con las siguientes etiquetas base dentro de su `<head>`:

```html
<head>
  <!-- 1. Juego de caracteres universal (debe ser la primera etiqueta) -->
  <meta charset="UTF-8">

  <!-- 2. Adaptabilidad en dispositivos móviles (Responsive Design) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Título único de la pestaña y del resultado en Google (máx. 60 caracteres) -->
  <title>Aprende Desarrollo Web Moderno | MiPlataforma</title>

  <!-- 4. Descripción para el resumen de Google (Snippet SEO, 140-160 caracteres) -->
  <meta name="description" content="Aprende HTML5 semántico, CSS moderno y accesibilidad web paso a paso con proyectos prácticos desde cero.">

  <!-- 5. Control de indexación para rastreadores (Googlebot) -->
  <meta name="robots" content="index, follow">

  <!-- 6. Color de la barra de navegación del navegador en móviles (Android/Safari) -->
  <meta name="theme-color" content="#0f172a">
</head>
```

### Explicación de etiquetas clave

| Etiqueta / Atributo | ¿Para qué sirve? | Impacto si se omite |
| --- | --- | --- |
| `charset="UTF-8"` | Soporte universal para tildes, eñes, símbolos matemáticos y emojis. | Caracteres rotos en pantalla (ej. `Ã±` en lugar de `ñ`). |
| `viewport` | Ajusta el ancho virtual de la página al ancho físico de la pantalla del móvil. | En móviles la web se verá minúscula, con zoom alejado y letras ilegibles. |
| `<title>` | Título de la pestaña, marcador del navegador y encabezado azul en Google. | Pésimo posicionamiento SEO; el navegador mostrará la URL cruda. |
| `name="description"` | Texto de vista previa que aparece debajo del título en los resultados de Google. | Google elegirá texto al azar de tu página para rellenar el fragmento. |
| `name="robots"` | Instrucciones al rastreador (`index`/`noindex`, `follow`/`nofollow`). | El buscador aplicará su criterio predeterminado sin control tuyo. |
| `name="theme-color"` | Tinta la barra de estado superior del navegador móvil con el color de tu marca. | La barra móvil permanecerá en el color gris o blanco genérico del sistema. |

> [!IMPORTANT]
> **La regla de los 1024 bytes:**  
> La etiqueta `<meta charset="UTF-8">` debe colocarse **dentro de los primeros 1024 bytes del documento** (es decir, en las primeras líneas del `<head>`). Si la colocas muy abajo, el navegador podría empezar a leer el archivo con una codificación incorrecta antes de enterarse de que debía usar UTF-8.

### Qué observar en los metadatos esenciales

- **Longitudes recomendadas por Google:**
  - `<title>`: Entre **50 y 60 caracteres**. Si te pasas, los buscadores cortarán el final con puntos suspensivos (`...`).
  - `<meta name="description">`: Entre **140 y 160 caracteres**. Debe ser un resumen persuasivo que invite al usuario a hacer clic.
- **La magia del Viewport:** `width=device-width` sincroniza los píxeles CSS con los píxeles lógicos del móvil, e `initial-scale=1.0` establece una escala directa 1:1 sin zoom artificial.

### Práctica 2: Provocando el error móvil y de codificación (en `index.html`)

1. En tu `index.html`, escribe dentro del `<body>` un párrafo con tildes, eñes y emojis.
2. Agrega la etiqueta `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
3. Abre DevTools (`F12`), activa el modo de dispositivo móvil (**Ctrl + Shift + M** o Cmd + Shift + M) y observa cómo el texto se lee en tamaño natural.
4. Ahora **borra o comenta la etiqueta viewport**, recarga la vista móvil y comprueba el desastre visual: el navegador renderiza la web como si fuera una pantalla gigante de computadora de 980px, haciendo el texto diminuto. Vuelve a activarla.

---

## 3. Favicons e identidad de marca

El favicon es el icono identificativo que aparece en la pestaña del navegador, en la barra de marcadores, en el historial y en los accesos directos de teléfonos móviles.

En la web moderna se utiliza una combinación de formatos para cubrir navegadores clásicos, pantallas de alta densidad y dispositivos Apple:

```html
<!-- 1. Favicon clásico para máxima compatibilidad con navegadores antiguos -->
<link rel="icon" href="favicon.ico" sizes="32x32">

<!-- 2. Favicon vectorial SVG moderno (escalado perfecto y soporte de modo oscuro) -->
<link rel="icon" href="favicon.svg" type="image/svg+xml">

<!-- 3. Icono para cuando el usuario guarda la web en la pantalla de inicio de iPhone/iPad -->
<link rel="apple-touch-icon" href="apple-touch-icon.png">
```

### Qué observar en los favicons

- **Prioridad del SVG:** Si un navegador moderno detecta el archivo `.svg`, lo preferirá sobre el `.ico`. La gran ventaja del formato SVG es que pesa menos de 2 KB, nunca se ve pixelado y puede incluir código CSS interno para cambiar de color automáticamente si el usuario tiene su computadora en **Modo Oscuro** (`@media (prefers-color-scheme: dark)`).
- **Caché agresiva:** Los navegadores guardan los favicons en memoria de forma muy agresiva. Si cambias el icono de tu web y no se actualiza en la pestaña, prueba abrir la web en una ventana de incógnito o borrar la caché del navegador.

> [!TIP]
> Si no tienes un archivo `.ico` o `.svg` a la mano durante tus pruebas locales, puedes usar un emoji como favicon temporal directo en HTML con esta línea:  
> `<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🚀</text></svg>">`

### Práctica 3: Identidad visual en la pestaña (en `index.html`)

1. En el `<head>` de tu `index.html`, agrega el favicon temporal con emoji del tip anterior (puedes cambiar el emoji `🚀` por el que prefieras).
2. Guarda el archivo, recarga la página y observa cómo la pestaña de tu navegador muestra inmediatamente el icono personalizado junto a tu `<title>`.

---

## 4. Integración de recursos externos y optimización de rendimiento

Para conectar tipografías externas y hojas de estilo utilizamos la etiqueta `<link>`. El navegador debe descargar estos recursos rápidamente para evitar retrasar el dibujo de la pantalla.

```html
<!-- Conexión obligatoria a tu hoja de estilos local -->
<link rel="stylesheet" href="css/estilos.css">

<!-- OPTIMIZACIÓN DE FUENTES EXTERNAS (Google Fonts) -->
<!-- 1. Abre la conexión DNS y protocolo TLS anticipadamente (Resource Hints) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- 2. Descarga la hoja de estilos con la tipografía solicitada -->
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap">
```

### Qué observar en la precarga y conexión de recursos

- **`rel="preconnect"` (Pista de recurso / Resource Hint):** Le ordena al navegador conectarse con el servidor de Google Fonts en segundo plano mientras sigue leyendo el resto del HTML. Cuando el documento llega a la línea que pide la fuente `Inter`, el "apretón de manos" de red ya está resuelto, ahorrando hasta 300 milisegundos de tiempo de carga.
- **`crossorigin`:** Es obligatorio al conectarse con `fonts.gstatic.com` porque las tipografías web se descargan mediante solicitudes de origen cruzado (CORS). Si omites este atributo, la preconexión será descartada por el navegador.

### Práctica 4: Auditoría de red en DevTools (en `index.html`)

1. Agrega los enlaces de Google Fonts del ejemplo en el `<head>` de tu `index.html`.
2. Abre las herramientas de desarrollo (`F12`) y ve a la pestaña **Red (Network)**.
3. Filtra por **Fuentes (Fonts)** o **CSS** y recarga la página (Ctrl + R).
4. Comprueba cómo el navegador registra la descarga de la hoja de estilos de Google y del archivo binario de la fuente sin errores de conexión.

---

## 5. Carga de scripts JavaScript: `defer` vs. `async`

Por defecto, cuando el navegador encuentra una etiqueta `<script src="...">`, **detiene por completo la lectura y construcción del HTML** hasta que el script se descarga y se ejecuta. Esto se conoce como *bloqueo del renderizado* y deja al usuario frente a una pantalla en blanco.

Para evitarlo, HTML5 ofrece dos atributos de ejecución asíncrona:

```text
SÍNCRONO TRADICIONAL (Sin atributos - BLOQUEA EL DOCUMENTO):
HTML Parsing ----> [ PAUSA: Descarga JS + Ejecuta ] ----> Continúa HTML Parsing

ASYNC (Descarga paralela, pero interrumpe el HTML apenas termina de bajar):
HTML Parsing -------------------------> [ PAUSA: Ejecuta JS ] ---> Continúa HTML
           \-- Descarga JS (Paralelo) --/

DEFER (Descarga paralela y se ejecuta AL FINAL respetando el orden - RECOMENDADO):
HTML Parsing -----------------------------------------------------> [ Fin del HTML ]
           \-- Descarga JS (Paralelo) --/                           [ Ejecuta JS ]
```

### Comparativa de inclusión de scripts

```html
<!-- 1. DEFER (La opción estándar para tus scripts de interfaz) -->
<!-- Descarga en segundo plano y se ejecuta solo cuando todo el HTML ha sido procesado -->
<script src="js/app.js" defer></script>

<!-- 2. ASYNC (Para scripts independientes que no tocan el DOM) -->
<!-- Se ejecuta de inmediato en cuanto termina de descargar, sin importar en qué punto va el HTML -->
<script src="https://www.googletagmanager.com/gtag/js" async></script>

<!-- 3. MÓDULOS MODERNOS -->
<!-- Tienen comportamiento 'defer' automático por especificación -->
<script type="module" src="js/main.js"></script>
```

### Qué observar en la carga de scripts

- **Ubicación en el `<head>`:** Gracias al atributo `defer`, hoy en día podemos colocar todos los scripts organizados limpiamente dentro del `<head>`. Ya no es necesario enviarlos al final del `<body>` como se hacía antiguamente.
- **Garantía de orden:** Si tienes tres scripts con `defer` (`a.js`, `b.js`, `c.js`), el navegador garantiza que se ejecutarán en ese orden exacto al finalizar la lectura del HTML. Con `async`, se ejecutará primero el que pese menos y termine de descargar antes, lo que puede provocar fallos si un script depende de variables del otro.

> [!WARNING]
> Nunca uses `async` para scripts que necesiten seleccionar o manipular elementos del HTML (como un botón o un formulario). Si el script descarga rápido y se ejecuta antes de que el navegador llegue a pintar ese botón, tu código fallará con el clásico error: `Cannot read properties of null`. Para scripts de interfaz, usa siempre `defer`.

### Práctica 5: Verificando el orden de ejecución con la consola (en `index.html`)

1. En tu carpeta, crea un archivo rápido llamado `prueba.js` con una sola línea:  
   `console.log("El DOM está listo y el script cargó con defer:", document.body);`
2. Enlázalo en el `<head>` de tu `index.html` usando `<script src="prueba.js" defer></script>`.
3. Abre tu navegador, abre la **Consola de DevTools** (`F12`) y recarga la página. Comprueba que el script se ejecuta correctamente sin que `document.body` sea nulo.

---

## 6. Social Cards: Open Graph (WhatsApp, LinkedIn, Discord) y Twitter

Cuando compartes un enlace de tu web a través de WhatsApp, Telegram, Slack, Facebook o LinkedIn, estas aplicaciones no leen tu diseño visible: envían un bot que lee exclusivamente los metadatos del protocolo **Open Graph (`og:`)** para armar una tarjeta enriquecida con imagen, título y resumen.

```html
<!-- PROTOCOLO OPEN GRAPH (Estándar para WhatsApp, Facebook, LinkedIn, Discord) -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://misitio.com/cursos/html5">
<meta property="og:title" content="Aprende HTML5 Profesional desde Cero">
<meta property="og:description" content="Domina la arquitectura web moderna, semántica, accesibilidad y metadatos con proyectos reales.">

<!-- LA IMAGEN DEBE SER OBLIGATORIAMENTE UNA URL ABSOLUTA -->
<meta property="og:image" content="https://misitio.com/assets/portada-og.jpg">
<meta property="og:image:alt" content="Banner promocional del curso de desarrollo web con logotipo oficial">
<meta property="og:locale" content="es_ES">

<!-- TARJETAS DE X / TWITTER (Específico para la plataforma X) -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@tu_usuario">
<meta name="twitter:title" content="Aprende HTML5 Profesional desde Cero">
<meta name="twitter:description" content="Domina la arquitectura web moderna, semántica y accesibilidad.">
<meta name="twitter:image" content="https://misitio.com/assets/portada-og.jpg">
```

### Qué observar en las tarjetas sociales

- **La trampa de la URL relativa en `og:image`:**  
  Un error clásico de principiante es escribir `content="assets/foto.jpg"`. WhatsApp o LinkedIn **no saben cuál es tu dominio** si pones una ruta relativa; el rastreador fallará en silencio y la tarjeta saldrá vacía o con un recuadro gris. La URL de la imagen debe ser **estrictamente absoluta** (`https://...`).
- **Dimensiones ideales de la imagen:**  
  La medida estándar recomendada para que la imagen no salga recortada ni borrosa es de **1200 x 630 píxeles** (proporción 1.91:1), con un peso menor a 1 MB.

> [!CAUTION]
> WhatsApp y Facebook cachean las tarjetas sociales por semanas. Si subes cambios a tu web y al compartir el link en WhatsApp sigue saliendo la imagen vieja, debes forzar la actualización usando la herramienta oficial [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/).

### Práctica 6: Configurando y previsualizando tarjetas sociales (en `index.html`)

1. Agrega el bloque de etiquetas Open Graph y Twitter Cards dentro del `<head>` de tu `index.html`.
2. Para verificar cómo se verían tus tarjetas en la vida real sin tener que publicar la web a un servidor, visita el sitio gratuito [metatags.io](https://metatags.io/) o [opengraph.xyz](https://www.opengraph.xyz/).
3. Experimenta en esas plataformas cambiando el título y la imagen para familiarizarte con las proporciones visuales de cada red social.

---

## 7. SEO Técnico y Enlaces Canónicos

En internet es muy común que una misma página sea accesible desde múltiples direcciones URL debido a parámetros de campaña, certificados o subdominios:

- `https://mitienda.com/producto`
- `https://mitienda.com/producto?campana=facebook`
- `https://mitienda.com/producto?color=azul`
- `http://mitienda.com/producto` (sin SSL)

Para Google, estas son cuatro páginas distintas con exactamente el mismo texto, lo que genera una penalización por **contenido duplicado**.

Para indicarle a los buscadores cuál es la URL oficial y principal que debe indexarse, se utiliza la etiqueta canónica:

```html
<!-- Le dice a Google: 'Ignora los parámetros de la URL; esta es la dirección original' -->
<link rel="canonical" href="https://mitienda.com/producto">
```

### Qué observar en las etiquetas canónicas

- Debe ser una URL absoluta y apuntar siempre a la versión segura con protocolo `https://`.
- Cada página de tu sitio debe tener su propia etiqueta canónica apuntando a su URL representativa.

### Práctica 7: Blindando la URL canónica (en `index.html`)

Agrega a tu `index.html` una etiqueta `<link rel="canonical">` que apunte al dominio ficticio oficial de tu proyecto (ej. `https://mi-proyecto-web.com/`).

---

## Reto final de la lección: Configuración de Producción para una Startup

Ahora que experimentaste con cada metadato en tu laboratorio (`index.html`) y comprendes cómo validarlos con DevTools, demostrarás tu autonomía construyendo la cabecera completa para un proyecto real desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `09-metadatos-e-integracion`. Construirás la estructura completa para la **Página de Lanzamiento de una Startup Tecnológica (SaaS)** que cumpla con todos los puntos de la siguiente lista de control:

- [ ] Declaración de `<!DOCTYPE html>` e `<html lang="es">`.
- [ ] **Configuración esencial de renderizado:**
  - [ ] `<meta charset="UTF-8">` ubicado dentro de las primeras líneas del `<head>`.
  - [ ] `<meta name="viewport">` configurado correctamente para diseño responsivo.
  - [ ] `<meta name="theme-color">` con un color de identidad de marca en formato hexadecimal.
- [ ] **Optimización SEO:**
  - [ ] `<title>` profesional estructurado: *Nombre del Producto | Propuesta de Valor* (entre 50 y 60 caracteres).
  - [ ] `<meta name="description">` persuasiva y concisa (entre 140 y 160 caracteres).
  - [ ] Directiva `<meta name="robots" content="index, follow">`.
  - [ ] Enlace canónico `<link rel="canonical">` con URL absoluta.
- [ ] **Identidad de marca:**
  - [ ] Enlace a favicon vectorial SVG o clásico `.ico`.
  - [ ] Enlace a icono táctil para dispositivos Apple (`apple-touch-icon`).
- [ ] **Rendimiento e integración:**
  - [ ] Al menos una directiva de preconexión (`<link rel="preconnect">`) hacia un servicio de fuentes externas como Google Fonts.
  - [ ] Conexión a hoja de estilos local mediante `<link rel="stylesheet">`.
  - [ ] Conexión a script local utilizando el atributo no bloqueante `defer`.
- [ ] **Social Media Cards (Open Graph y Twitter):**
  - [ ] Metadatos Open Graph completos (`og:title`, `og:description`, `og:image`, `og:url`, `og:type`, `og:locale`).
  - [ ] La etiqueta `og:image` debe utilizar obligatoriamente una URL absoluta.
  - [ ] Tarjeta de Twitter configurada con formato visual grande (`summary_large_image`).
- [ ] **Validación en el navegador:**
  - [ ] Un `<body>` mínimo con `<header>`, `<main>` y `<footer>` que demuestre que el documento carga limpiamente sin errores en la consola de DevTools.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Qué problema visual crítico ocurrirá en un teléfono móvil inteligente si olvidas incluir la etiqueta `<meta name="viewport" ...>`?
2. ¿Por qué la etiqueta `<meta charset="UTF-8">` debe ubicarse en las primeras líneas del `<head>`, dentro de los primeros 1024 bytes del documento?
3. ¿Cuál es la diferencia técnica fundamental entre un script cargado con `defer` versus uno con `async` respecto al orden de ejecución y la manipulación del DOM?
4. ¿Por qué las aplicaciones de mensajería como WhatsApp no muestran la imagen de vista previa si colocas una ruta relativa (ej. `content="assets/img.jpg"`) en la etiqueta `og:image`?
5. ¿Para qué sirve la etiqueta `<link rel="canonical">` y qué penalización evita en los motores de búsqueda como Google?

---

## 📚 Recursos y documentación oficial

Para profundizar en la configuración avanzada del documento y las etiquetas del `<head>`, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Qué hay en el `<head>`: Metadatos en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/What_is_in_the_head)
- 📖 [Referencia del elemento `<meta>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/meta)
- 📖 [Referencia del elemento `<script>` y atributos de carga - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/script)
- 📖 [Estrategias de precarga con Resource Hints (`preconnect`, `dns-prefetch`) - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Attributes/rel/preconnect)
- 📖 [Documentación y especificación oficial de Open Graph](https://ogp.me/)
