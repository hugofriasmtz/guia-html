# Lección 5: Contenido embebido y multimedia

Esta lección continúa el trabajo de [Agrupación semántica](../04-agrupacion-semantica/README.md). Ahora aprenderás a enriquecer tu estructura web incorporando imágenes accesibles, leyendas formales, audio y video nativo, e incrustación de contenido externo con `iframe`.

> [!TIP]
> **Metodología de trabajo en esta lección:**  
> Crea una subcarpeta llamada `assets/` o `imagenes/` si prefieres guardar archivos locales en lugar de usar enlaces de prueba.

---

## 1. Imágenes con la etiqueta `img`

`<img>` es una **etiqueta vacía** (autocontenida, no tiene cierre `</img>`) que solicita al navegador descargar y renderizar un archivo gráfico mediante atributos.

```html
<img 
  src="https://picsum.photos/800/450" 
  alt="Cadena montañosa nevada durante el atardecer en los Alpes suizos" 
  width="800" 
  height="450" 
  loading="lazy"
>
```

### Atributos indispensables de `img`

| Atributo | Propósito | Regla de oro |
| --- | --- | --- |
| `src` (*source*) | Ruta relativa o absoluta del archivo. | Revisa que la ruta, el nombre y la extensión coincidan de forma exacta. |
| `alt` (*alternative text*) | Descripción textual para accesibilidad y SEO. | **Obligatorio siempre.** Se lee en lectores de pantalla y se muestra si la imagen no carga por fallas de red. |
| `width` / `height` | Dimensiones intrínsecas (solo números, sin `px`). | Ayuda al navegador a reservar el espacio exacto antes de descargar la imagen, evitando saltos de pantalla molestos (*Cumulative Layout Shift* o CLS). |
| `loading="lazy"` | Carga diferida (*Lazy Loading*). | Pospone la descarga de la imagen hasta que el usuario hace scroll cerca de ella, ahorrando datos móviles y acelerando la web. |

### Criterio profesional: ¿Qué formato de imagen elegir?

En la web moderna no usamos cualquier formato al azar; cada uno resuelve una necesidad técnica:

| Formato | Uso ideal en proyectos reales | Ventaja técnica |
| --- | --- | --- |
| **SVG** (`.svg`) | Logos, íconos, isotipos e ilustraciones simples. | Es código vectorial; **escalado infinito** sin perder nitidez y peso mínimo. |
| **WebP / AVIF** | Fotografías, banners y portadas principales. | El estándar moderno de la web; pesan hasta un **40% menos** que un JPG con la misma calidad. |
| **PNG** (`.png`) | Imágenes complejas que requieren **transparencia**. | Conserva transparencias nítidas, pero suele ser más pesado que WebP. |
| **JPG / JPEG** | Fotografías cuando se requiere soporte para sistemas muy antiguos. | Compatibilidad universal, pero superado hoy en día por WebP. |

> [!CAUTION]
> **Criterio para el atributo `alt`:**
>
> - **Informativa:** Describe brevemente la acción o información visual clave.
> - **Decorativa (fondos, líneas, separadores):** Escribe `alt=""` (cadena vacía). Si eliminas el atributo por completo, el lector de pantalla leerá la ruta del archivo en voz alta (`/assets/img/adorno_v2.svg`), arruinando la accesibilidad.
> - **Prohibido:** No escribas `alt="Foto de..."` o `alt="Imagen de..."`. El lector de pantalla ya anuncia automáticamente que se trata de un elemento gráfico.

### Qué observar en las imágenes

- **Reserva de espacio (CLS):** Al definir `width="800"` y `height="450"`, el navegador calcula la proporción (16:9) y reserva ese hueco exacto en la pantalla antes de que el archivo termine de bajar.
- **Comportamiento ante errores:** Si la ruta en `src` falla, el navegador muestra un icono de imagen rota junto con el texto del `alt`.

### Práctica 1: El laboratorio de imágenes (en `index.html`)

1. Crea tu archivo `index.html` con la estructura base de HTML5.
2. Agrega una imagen usando la URL pública de prueba: `https://picsum.photos/600/400`.
3. Asígnale un `alt` descriptivo, sus dimensiones fijas `width="600"`, `height="400"` y `loading="lazy"`.
4. Cambia a propósito una letra de la URL para romperla, guarda y observa cómo el navegador muestra tu texto alternativo en pantalla.

---

## 2. Figuras con `figure` y `figcaption`

Cuando una imagen, diagrama, infografía o fragmento de código forma parte del contenido principal y requiere un pie de foto explicativo, una numeración formal o créditos de autor, se utiliza el elemento semántico `<figure>`:

```html
<figure>
  <img 
    src="https://picsum.photos/id/1018/600/400" 
    alt="Valle rodeado de montañas al amanecer con cielo despejado"
    width="600" 
    height="400"
    loading="lazy"
  >
  <figcaption>Figura 1: Vista panorámica del Parque Nacional durante la expedición botánica de 2026. Fotografía de Elena Ramos.</figcaption>
</figure>
```

### Diferencia clave: `alt` vs. `figcaption`

| Elemento | ¿Para qué sirve? | ¿Quién lo lee? |
| --- | --- | --- |
| **`alt`** | Describe **qué se ve visualmente** en la imagen. | Lectores de pantalla y usuarios con fallas de conexión. |
| **`<figcaption>`** | Aporta **contexto, explicación, autoría o numeración**. | Visible para **todos** los usuarios en la pantalla. |

### Qué observar en `figure` y `figcaption`

- `<figure>` representa una unidad de contenido autocontenida que podría moverse a otra parte de la página sin alterar el significado del texto principal.
- `<figcaption>` solo puede colocarse como el **primer** o el **último** elemento hijo directo dentro de `<figure>`.
- Por defecto, los navegadores aplican un margen lateral sangrado a la etiqueta `<figure>`.

### Práctica 2: Publicación con figura formal (en `index.html`)

1. En tu `index.html`, envuelve una imagen dentro de un contenedor `<figure>`.
2. Añade un `<figcaption>` al pie que incluya el título de la obra, el año y el crédito del autor.
3. Comprueba en tu navegador cómo el pie de foto queda asociado visual y semánticamente a la imagen.

---

## 3. Imágenes adaptables con `picture` y `source`

La etiqueta `<picture>` es un contenedor inteligente que permite al navegador elegir la mejor versión de una imagen según dos necesidades:

1. **Formatos de última generación:** Servir formatos optimizados (`.webp` o `.avif`) a navegadores modernos, con respaldo `.jpg` para navegadores antiguos.
2. **Dirección de arte (*Art Direction*):** Servir una imagen recortada en vertical para celulares y una panorámica para pantallas de escritorio.

```html
<picture>
  <!-- 1. Si la pantalla mide 768px o más, evalúa servir imagen de escritorio -->
  <source media="(min-width: 768px)" srcset="https://picsum.photos/900/400" type="image/webp">
  
  <!-- 2. Para pantallas pequeñas (móviles), sirve una versión cuadrada -->
  <source srcset="https://picsum.photos/400/400" type="image/webp">
  
  <!-- 3. Imagen por defecto OBLIGATORIA (sirve de renderizador base y respaldo) -->
  <img 
    src="https://picsum.photos/600/400" 
    alt="Espacio de trabajo moderno con laptop y café" 
    width="600" 
    height="400"
  >
</picture>
```

### Qué observar en `picture` y `source`

- **Evaluación en cascada:** El navegador evalúa las etiquetas `<source>` de arriba hacia abajo y descargará **únicamente la primera opción que cumpla la condición**.
- **La etiqueta `<img>` sigue siendo obligatoria:** `<picture>` y `<source>` son solo reglas de decisión; el elemento que realmente dibuja la imagen en pantalla y aloja el atributo `alt` sigue siendo la etiqueta `<img>` interna.

> [!TIP]
> Si omites la etiqueta `<img>` dentro de `<picture>`, no se mostrará absolutamente nada en la pantalla. `<picture>` no dibuja nada por sí sola.

### Práctica 3: Dirección de arte adaptable (en `index.html`)

1. Copia el bloque `<picture>` del ejemplo en tu `index.html`.
2. Abre la página en tu navegador e inspecciona el elemento.
3. Cambia el ancho de la ventana del navegador (o activa la vista responsive con F12) y observa cómo la imagen conmuta automáticamente entre formato panorámico y cuadrado al cruzar los `768px`.

---

## 4. Audio y Video nativo con HTML5

HTML5 permite reproducir multimedia directamente en el navegador sin plugins externos.

### Video nativo con `<video>`

```html
<video 
  controls 
  width="640" 
  height="360" 
  poster="https://picsum.photos/640/360" 
  preload="metadata"
>
  <!-- Fuentes en múltiples formatos para compatibilidad universal -->
  <source src="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4" type="video/mp4">
  <source src="videos/trailer.webm" type="video/webm">
  
  <!-- Pistas de subtítulos o accesibilidad -->
  <track src="subtitulos/es.vtt" kind="subtitles" srclang="es" label="Español" default>
  
  <!-- Mensaje de respaldo si el navegador es incompatible -->
  <p>Tu navegador no soporta video HTML5 nativo.</p>
</video>
```

### Atributos clave de multimedia

- **`controls`**: Muestra la botonera nativa (play, pausa, volumen y pantalla completa). Sin este atributo, el reproductor no mostrará controles.
- **`poster`**: URL de una imagen de portada que se muestra antes de que el usuario pulse "Play".
- **`preload`**: Controla la estrategia de descarga previa:
  - `none`: No descarga nada hasta que el usuario pulsa play (ideal para ahorrar datos).
  - `metadata`: Solo descarga la duración, dimensiones y primer fotograma.
  - `auto`: Descarga el archivo de inmediato.
- **`<track>`**: Introduce subtítulos o transcripciones usando archivos en formato WebVTT (`.vtt`).

### Audio nativo con `<audio>`

```html
<audio controls preload="none">
  <source src="https://actions.google.com/sounds/v1/ambiences/rain_heavy.ogg" type="audio/ogg">
  <source src="audios/lluvia.mp3" type="audio/mpeg">
  <p>Tu navegador no soporta el reproductor de audio.</p>
</audio>
```

> [!WARNING]
> **La regla de `autoplay`:**  
> Los navegadores modernos **bloquean por defecto cualquier reproducción automática con sonido**. El atributo `autoplay` solo funcionará en videos si está acompañado de `muted`:  
> `<video controls autoplay muted playsinline>`.

### Qué observar en audio y video

- El texto que pongas antes de cerrar `</video>` o `</audio>` solo se muestra en navegadores muy antiguos que no entienden HTML5.
- Ofrecer formatos alternativos (`.mp4` y `.webm` para video; `.mp3` y `.ogg` para audio) garantiza reproducción en cualquier dispositivo.

### Práctica 4: Controles multimedia (en `index.html`)

1. Añade a tu `index.html` el reproductor de video de prueba del ejemplo.
2. Quita temporalmente el atributo `controls` y recarga la página para verificar cómo desaparece la botonera. Vuelve a agregarlo.
3. Agrega el reproductor de audio con `preload="none"` y comprueba la reproducción de sonido nativa.

---

## 5. Contenido incrustado externo con `iframe`

La etiqueta `<iframe>` (*inline frame*) permite incrustar un documento o servicio externo completo dentro de tu página, como mapas, videos de YouTube o listas de Spotify:

### Ejemplo con OpenStreetMap

```html
<iframe 
  src="https://www.openstreetmap.org/export/embed.html?bbox=-3.708%2C40.415%2C-3.701%2C40.420&amp;layer=mapnik" 
  width="600" 
  height="400" 
  title="Mapa interactivo con la ubicación de nuestra sede central" 
  loading="lazy" 
  allowfullscreen
></iframe>
```

### El caso real: Incrustar YouTube o Spotify

Cuando entras a YouTube o Spotify y pulsas **Compartir $\rightarrow$ Insertar (Embed)**, la plataforma te entrega un código con esta estructura:

```html
<iframe 
  width="560" 
  height="315" 
  src="https://www.youtube-nocookie.com/embed/dQw4w9WgXcQ" 
  title="Reproductor de video de YouTube" 
  loading="lazy"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
  allowfullscreen
></iframe>
```

- **`allow="..."`**: Es una lista de permisos explícitos (*Feature Policy*). Le autoriza al reproductor externo acceder al acelerómetro del móvil, permitir pantalla completa (`allowfullscreen`) o habilitar la ventana flotante (*picture-in-picture*).
- **`title` obligatorio:** Los lectores de pantalla anuncian este texto para que una persona con discapacidad visual sepa qué reproduce el marco antes de interactuar con él.

> [!IMPORTANT]
> **Rendimiento con iframes:** Los iframes son páginas web completas cargadas dentro de la tuya y consumen mucha memoria. Añade siempre `loading="lazy"` para que no congelen la carga inicial de tu sitio.

### Qué observar en los iframes

- Un `iframe` crea un entorno aislado (*sandbox*). El código del sitio externo no puede espiar ni alterar los estilos o variables de tu página principal por políticas de seguridad del navegador.

### Práctica 5: Incrustación externa responsable (en `index.html`)

1. Copia el `iframe` del mapa o del video de YouTube en tu `index.html`.
2. Asegúrate de que tenga los atributos `title`, `loading="lazy"` y `allowfullscreen`.
3. Inspecciona el elemento con las herramientas de desarrollo (F12) y observa cómo se crea un documento subordinado independiente dentro de la etiqueta.

---

## Reto final de la lección: Reseña Multimedia de un Documental

Ahora que probaste cada etiqueta y atributo en tu laboratorio (`index.html`), demostrarás tu autonomía construyendo una página completa desde cero.

> [!NOTE]
> **Recursos para el reto:**  
> Para resolver este reto puedes utilizar las mismas URLs públicas de prueba que usamos en la lección (como `picsum.photos` o videos de prueba públicos) o, si lo prefieres, descargar archivos cortos propios dentro de tu subcarpeta `assets/`. El objetivo es dominar la arquitectura HTML sin perder tiempo buscando archivos locales pesados.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `05-contenido-embebido`. Construirás una **Página de Lanzamiento y Reseña de un Documental sobre la Naturaleza** que cumpla con todos los puntos de la siguiente lista de control:

- [x] Estructura base completa de HTML5 (`<!DOCTYPE html>`, `<html>`, `<head>` con metadatos y `<body>`).
- [x] Estructura semántica adecuada que organice la página con `<header>`, `<main>`, `<section>` y `<footer>`.
- [x] **Cabecera:** Encabezado `<h1>` con el título del documental y una imagen principal optimizada que use `src`, `alt` descriptivo, dimensiones fijas (`width`, `height`) y `loading="lazy"`.
- [x] **Sección de galería / fotografía:** Al menos una imagen formal dentro de `<figure>` con su respectivo `<figcaption>` que indique la ubicación geográfica y crédito fotográfico.
- [x] **Sección de afiche adaptable:** Un bloque `<picture>` que ofrezca:
  - Un `<source>` panorámico para pantallas grandes (`min-width: 768px`).
  - Una versión vertical para pantallas móviles.
  - Una etiqueta `<img>` de respaldo funcional con su `alt` correspondiente.
- [x] **Sección de trailer y banda sonora:**
  - Un reproductor `<video>` con `controls`, `poster`, `preload="metadata"` y un mensaje de respaldo para navegadores antiguos.
  - Un reproductor `<audio>` con `controls` para escuchar el tema musical principal.
- [x] **Sección de locación:** Un mapa incrustado con `<iframe>` (OpenStreetMap o Google Maps) que incluya obligatoriamente el atributo descriptivo `title` y `loading="lazy"`.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Por qué es fundamental definir siempre `width` y `height` en una etiqueta `<img>` aunque luego cambiemos su tamaño con CSS?
2. ¿Cuál es la diferencia conceptual y de accesibilidad entre el atributo `alt` y la etiqueta `<figcaption>`?
3. ¿En qué escenario técnico preferirías usar una imagen en formato SVG en lugar de WebP o PNG?
4. ¿Por qué dentro de `<picture>` o `<video>` se deben colocar múltiples elementos `<source>`?
5. ¿Por qué todo elemento `<iframe>` debe llevar obligatoriamente un atributo `title`?

---

## 📚 Recursos y documentación oficial

Para profundizar en optimización multimedia y buenas prácticas de accesibilidad, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Imágenes en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Images_in_HTML)
- 📖 [Imágenes adaptables con `<picture>` - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Responsive_images)
- 📖 [Contenido de video y audio en HTML5 - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Video_and_audio_content)
- 📖 [El elemento `<figure>` y `<figcaption>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/figure)
- 📖 [Referencia del elemento `<iframe>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/iframe)
