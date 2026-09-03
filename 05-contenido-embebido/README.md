# Lección 5: Contenido embebido y multimedia

Esta lección continúa el trabajo de [Agrupación semántica](../04-agrupacion-semantica/README.md). Ahora aprenderás a enriquecer tu estructura semántica incorporando imágenes accesibles, leyendas formales, audio, video nativo e incrustación de contenido externo con `iframe`.

> [!TIP]
> Crea una subcarpeta llamada `assets/` o `imagenes/` dentro de tu proyecto. Mantener los archivos multimedia separados del código HTML es una regla básica de organización profesional.

---

## 1. Imágenes con la etiqueta `img`

`<img>` es una **etiqueta vacía** (autocontenida, no tiene cierre `</img>`) que inserta una imagen en el documento mediante atributos.

```html
<img 
  src="imagenes/paisaje.webp" 
  alt="Montañas nevadas al atardecer en los Alpes suizos" 
  width="800" 
  height="450" 
  loading="lazy"
>
```

### Atributos indispensables de `img`

| Atributo | Propósito | Regla de Oro |
| --- | --- | --- |
| `src` (*source*) | Ruta relativa o absoluta del archivo de imagen. | Revisa siempre que la ruta, el nombre y la extensión (`.webp`, `.png`, `.jpg`, `.svg`) sean exactos. |
| `alt` (*alternative text*) | Descripción textual de la imagen para accesibilidad y SEO. | **Obligatorio siempre.** Si la imagen no carga o el usuario utiliza un lector de pantalla, este texto es lo que se leerá. |
| `width` / `height` | Ancho y alto intrínseco en píxeles (se escribe solo el número, sin `px`). | Ayuda al navegador a reservar el espacio exacto antes de que la imagen termine de descargar, evitando saltos molestos en la pantalla (*Cumulative Layout Shift*). |
| `loading="lazy"` | Carga diferida (*Lazy Loading*). | La imagen solo se descarga cuando el usuario hace scroll cerca de ella, ahorrando datos y acelerando la carga inicial de tu web. |

> [!CAUTION]
> **Accesibilidad con `alt`:**
>
> * Si la imagen aporta información: describe brevemente lo que muestra.
> * Si la imagen es puramente decorativa (un adorno o fondo): déjala como `alt=""`. Nunca omitas el atributo, porque si lo omites, el lector de pantalla leerá la ruta del archivo completa en voz alta.
> * **Prohibido:** No uses frases redundantes como `alt="Foto de..."` o `alt="Imagen de..."`.

---

## 2. Figuras con `figure` y `figcaption`

Cuando una imagen, infografía, diagrama o fragmento de código forma parte del contenido principal y requiere un pie de foto explicativo o atribución formal, se utiliza `<figure>`:

```html
<figure>
  <img 
    src="imagenes/museo-arte.webp" 
    alt="Fachada moderna del Museo de Arte Contemporáneo con iluminación nocturna"
    width="600" 
    height="400"
  >
  <figcaption>Figura 1: Vista exterior del Museo durante su reapertura en 2026. Fotografía de Elena Ramos.</figcaption>
</figure>
```

* `<figure>`: Contenedor semántico de la unidad multimedia independiente.
* `<figcaption>`: Pie de foto o leyenda explicativa (debe colocarse como el primer o el último elemento hijo dentro de `figure`).

---

## 3. Imágenes adaptables con `picture` y `source`

La etiqueta `<picture>` permite servir diferentes versiones de una imagen según dos escenarios:

1. **Formatos modernos:** Servir `.webp` o `.avif` a navegadores modernos, con respaldo `.jpg` para navegadores viejos.
2. **Diseño adaptable (*Art Direction*):** Mostrar una imagen recortada para celulares y una panorámica para computadoras.

```html
<picture>
  <!-- 1. Si la pantalla mide 768px o más, sirve la versión de escritorio en formato WebP -->
  <source media="(min-width: 768px)" srcset="imagenes/banner-desktop.webp" type="image/webp">
  
  <!-- 2. Para móviles, sirve la versión vertical/optimizada en formato WebP -->
  <source srcset="imagenes/banner-mobile.webp" type="image/webp">
  
  <!-- 3. Respaldo obligatorio si el navegador no soporta <picture> o WebP -->
  <img src="imagenes/banner-fallback.jpg" alt="Oferta especial de cursos de desarrollo web" width="1200" height="600">
</picture>
```

---

## 4. Audio y Video nativo con HTML5

HTML5 permite reproducir archivos multimedia directamente sin instalar reproductores de terceros.

### Video con `<video>`

```html
<video 
  controls 
  width="640" 
  height="360" 
  poster="imagenes/portada-video.webp" 
  preload="metadata"
>
  <source src="videos/tutorial.webm" type="video/webm">
  <source src="videos/tutorial.mp4" type="video/mp4">
  
  <!-- Subtítulos accesibles -->
  <track src="subtitulos/es.vtt" kind="subtitles" srclang="es" label="Español" default>
  
  <!-- Mensaje de respaldo -->
  <p>Tu navegador no soporta video HTML5. Puedes <a href="videos/tutorial.mp4">descargar el video aquí</a>.</p>
</video>
```

* `controls`: Muestra la barra de reproducción, pausa, tiempo y volumen.
* `poster`: Imagen de portada que se muestra antes de reproducir el video.
* `preload="metadata"`: Solo descarga la duración y datos básicos al cargar la página, ahorrando ancho de banda.
* `<track>`: Permite añadir subtítulos o transcripciones en formato `.vtt`.

### Audio con `<audio>`

```html
<audio controls preload="none">
  <source src="audios/episodio-1.mp3" type="audio/mpeg">
  <source src="audios/episodio-1.ogg" type="audio/ogg">
  <p>Tu navegador no soporta el reproductor de audio.</p>
</audio>
```

> [!WARNING]
> Existe el atributo `autoplay` (reproducción automática), pero **los navegadores modernos lo bloquean por defecto** para no molestar al usuario con ruidos inesperados. Evita usar `autoplay` salvo que el video esté silenciado (`muted autoplay`).

---

## 5. Contenido incrustado externo con `iframe`

La etiqueta `<iframe>` (*inline frame*) permite incrustar un documento externo dentro de tu página web, como un mapa de Google Maps o un video de YouTube:

```html
<iframe 
  src="https://www.google.com/maps/embed?pb=..." 
  width="600" 
  height="450" 
  title="Mapa con la ubicación física de nuestra oficina central" 
  loading="lazy" 
  allowfullscreen>
</iframe>
```

### Reglas para usar `iframe` de forma profesional

1. **Atributo `title` obligatorio:** Los lectores de pantalla necesitan el `title` para anunciarle al usuario ciego qué hay dentro del iframe sin tener que cargarlo.
2. **`loading="lazy"`:** Evita que el mapa o video externo ralentice la carga de tu sitio web principal.

---

## Reto final de la lección

Crea una página de **Reseña de una Película, Álbum Musical o Documental** en tu archivo `index.html`:

1. [x] Una imagen principal que utilice atributos `src`, `alt` descriptivo, `width`, `height` y `loading="lazy"`.
2. [x] Una sección que incluya una imagen dentro de `<figure>` con su respectivo `<figcaption>`.
3. [x] Una implementación de imagen adaptable con `<picture>` que ofrezca al menos un formato alternativo (`<source>`) y un `<img>` de respaldo.
4. [x] Un reproductor `<video>` o `<audio>` con `controls` y un texto de respaldo con enlace de descarga.
5. [x] Un mapa o contenido incrustado con `<iframe>` que incluya su atributo `title` descriptivo.
6. [x] Toda la multimedia debe estar organizada dentro de su estructura semántica (`<main>`, `<section>`, `<article>`).

### Preguntas de autoevaluación

1. ¿Por qué es fundamental definir siempre `width` y `height` en una etiqueta `<img>` aunque después cambiemos su tamaño con CSS?
2. ¿Cuál es la diferencia entre el texto del atributo `alt` y el texto de un `<figcaption>`?
3. ¿Por qué se recomienda listar múltiples etiquetas `<source>` dentro de `<video>` o `<picture>`?
4. ¿Por qué todo `<iframe>` debe llevar un atributo `title`?

---

## 📚 Recursos y documentación oficial

Para profundizar en multimedia adaptable y optimización, consulta la documentación oficial de **MDN Web Docs**:

* 📖 [Imágenes en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Images_in_HTML)
* 📖 [Imágenes adaptables con `<picture>` - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Responsive_images)
* 📖 [Contenido de video y audio en HTML5 - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Video_and_audio_content)
