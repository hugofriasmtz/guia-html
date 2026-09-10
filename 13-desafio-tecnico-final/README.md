# Lección 13: Desafío Técnico Final — Portal de Alebrijes de Oaxaca

¡Llegaste a la prueba final de la ruta de aprendizaje de HTML5!

Atrás quedaron las lecciones guiadas y los fragmentos de código listos para copiar. Este módulo es una **evaluación técnica autónoma** diseñada para simular un encargo profesional del mundo real.

Pondrás a prueba el 100% de los conocimientos adquiridos entre las Lecciones 1 y 12: semántica estructural, accesibilidad web universal (WCAG), tablas avanzadas, formularios modernos de cotización artesanal, interactividad nativa, metadatos SEO y arquitectura web.

---

## 1. El Brief del Cliente: "Voces de Copal — Taller y Galería de Alebrijes"

Un colectivo de maestros talladores y maestras pintoras de **San Martín Tilcajete y San Antonio Arrazola, Oaxaca**, necesita lanzar su portal web oficial: **Voces de Copal**.

Su objetivo es comercializar piezas únicas talladas a mano en madera de copal, educar al público internacional sobre el valor cultural del *Tonal* y *Nahual* zapoteco, permitir la cotización de piezas por encargo y promover talleres de pintura tradicional.

El cliente exige una web rápida, con excelente posicionamiento internacional (SEO), accesible para personas con cualquier tipo de discapacidad y que refleje la dignidad y el detalle de su arte sin depender de librerías pesadas de JavaScript.

> [!WARNING]
> **Condiciones de la prueba técnica:**
>
> - **Prohibido el uso de frameworks de JavaScript:** No utilices React, Vue, Angular ni scripts complejos. Toda la interactividad debe resolverse con las etiquetas y atributos nativos de HTML5 (`<dialog>`, `<details>`, etc.).
> - **Enfoque en HTML puro:** Para los estilos visuales puedes utilizar un framework semántico sin clases (como **Pico CSS** vía CDN) o tu propio archivo CSS. La evaluación juzgará el **100% de la arquitectura, accesibilidad, semántica y validación de tu código HTML**.
> - **Autonomía:** Este proyecto debe ser concebido, estructurado y programado íntegramente por ti desde una hoja en blanco.

---

## 2. Arquitectura de Archivos del Proyecto

El proyecto se construirá dentro de la carpeta `13-desafio-tecnico-final` bajo la siguiente estructura modular:

```text
13-desafio-tecnico-final/
├── index.html                   # Portal principal de la galería de alebrijes
├── README.md                    # Esta guía de requerimientos técnicos
└── assets/
    ├── css/
    │   └── custom.css           # Estilos propios o ajustes visuales
    └── img/
        ├── logo.svg             # Logotipo de la tostaduría/taller artesanal
        ├── favicon.svg          # Favicon para la pestaña
        └── alebrije-hero.webp   # Fotografía principal de una pieza
```

---

## 3. Especificaciones Técnicas Obligatorias

Tu archivo `index.html` debe cumplir rigurosamente con los requerimientos técnicos divididos en las siguientes áreas de calidad:

---

### Área A: Sala de Control y SEO Técnico (`<head>`)

- [ ] **Estructura base:** Declaración formal `<!DOCTYPE html>` con `<html lang="es">`.
- [ ] **Metadatos esenciales:**
  - `<meta charset="UTF-8">` ubicado en las primeras líneas del `<head>`.
  - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.
  - `<meta name="theme-color">` con un color representativo de la identidad de la marca (ej. barro negro ocre ocre, añil ocre ocre).
- [ ] **SEO y Visibilidad Internacional:**
  - `<title>` profesional: *Voces de Copal | Alebrijes y Arte Zapoteco de Oaxaca* (máximo 60 caracteres).
  - `<meta name="description">` persuasiva sobre el arte en madera de copal y comercio justo (entre 140 y 160 caracteres).
  - Directiva `<meta name="robots" content="index, follow">`.
  - Enlace canónico `<link rel="canonical" href="...">`.
- [ ] **Optimización e Identidad:**
  - Pistas de preconexión (`<link rel="preconnect">`) hacia tipografías de Google Fonts.
  - Favicon vectorial en formato `.svg` y enlace `apple-touch-icon`.
- [ ] **Tarjetas para Redes Sociales:**
  - Metadatos completos de Open Graph (`og:title`, `og:description`, `og:image`, `og:url`, `og:type`).
  - La imagen en `og:image` debe utilizar una **URL absoluta** (`https://...`).
  - Tarjeta de Twitter configurada con `summary_large_image`.

---

### Área B: Accesibilidad Web y Navegación Universal (A11y)

- [ ] **Skip Link:** Un enlace de salto al contenido principal como primer elemento interactivo de `<body>` (`<a href="#contenido-principal">Saltar al contenido de la galería</a>`), visible al recibir el foco del teclado.
- [ ] **Navegación por teclado:** Toda la página debe poder recorrerse y activarse de principio a fin usando exclusivamente las teclas `Tab`, `Shift + Tab`, `Enter` y `Espacio`.
- [ ] **Identificación accesible:** Uso de `aria-label` en controles que no tengan texto visual explícito (como botones con iconos o enlaces a redes).
- [ ] **Encabezados ordenados:** Jerarquía estricta que inicie en un único `<h1>` y avance lógicamente por `<h2>` y `<h3>` sin saltarse niveles estructurales.
- [ ] **Imágenes descriptivas:**
  - Cada alebrije debe contar con un `alt` detallado que describa la figura híbrida, colores y motivos zapotecos (ej. *alt="Alebrije de jaguar alado con cuernos de venado, decorado con grecas zapotecas en azul añil y amarillo brillante"*).
  - Los separadores o adornos gráficos deben silenciarse con `alt=""` y `aria-hidden="true"`.

---

### Área C: Maquetación Semántica y Multimedia

- [ ] **Contenedores semánticos:** La página debe estructurarse mediante `<header>`, `<nav>`, `<main id="contenido-principal">`, `<section>`, `<article>`, `<aside>`, `<figure>` y `<footer>`.
- [ ] **Sección Hero:**
  - Título de impacto `<h1>` y lema cultural agrupados mediante `<hgroup>`.
  - Botones de llamado a la acción (CTA) hacia la cotización de piezas y la galería.
- [ ] **Prevención de saltos de pantalla (CLS):** Todas las etiquetas `<img>` deben incluir obligatoriamente sus atributos de dimensión intrínseca `width`, `height` y carga diferida `loading="lazy"`.
- [ ] **Imágenes adaptables:** Al menos un bloque `<picture>` con dos etiquetas `<source>` que aplique dirección de arte (una imagen panorámica del taller para pantallas grandes con `min-width` y una versión vertical/cerrada de un alebrije para móviles).
- [ ] **Ubicación accesible:** Un marco `<iframe>` con el mapa de ubicación del taller en los Valles Centrales de Oaxaca que incluya obligatoriamente `title="Mapa con la ubicación física del taller en San Martín Tilcajete"`, `loading="lazy"` y `allowfullscreen`.

---

### Área D: Datos Tabulares de Colección (`<table>`)

- [ ] La página debe incluir una **Tabla Comparativa de Líneas de Alebrijes y Maderas**:
  - Encabezado con un `<caption>` descriptivo sobre las características y tiempos de elaboración de las piezas.
  - División estructural obligatoria: `<thead>`, `<tbody>` y `<tfoot>`.
  - Encabezados de columna (`<th scope="col">`) y encabezados de fila (`<th scope="row">`).
  - Al menos una combinación horizontal usando **`colspan`** (ej. una fila de garantía: *"Madera de copal curada contra plagas y certificada por la comunidad artesanal"* que abarque todas las columnas).
  - Al menos una combinación vertical usando **`rowspan`** (ej. agrupar dos tipos de figuras bajo la misma categoría de talla: *Piezas de un solo tronco*).
  - Resumen o totalización en el pie de tabla (`<tfoot>`).

---

### Área E: Componentes Interactivos Nativos

- [ ] **Métricas Artesanales y Ecológicas:**
  - Un elemento `<meter>` que indique el porcentaje de pigmentos naturales utilizados (grana cochinilla, añil, cempasúchil) frente a acrílicos modernos, configurando sus umbrales (`min`, `max`, `low`, `high`, `optimum`, `value`).
  - Un elemento `<progress>` que represente la meta del programa comunitario de reforestación de árboles de copal en Oaxaca (ej. 85% de la meta anual plantada).
- [ ] **Preguntas Frecuentes (FAQ Cultural):**
  - Al menos tres elementos `<details>` agrupados con el **mismo atributo `name="faq-alebrijes"`** para funcionar como acordeón exclusivo nativo:
    1. *¿Qué significado espiritual tiene el Tonal y el Nahual en cada pieza?*
    2. *¿Cómo distinguir una pieza original oaxaqueña de una imitación industrial?*
    3. *¿Cómo se empacan y protegen las piezas para envíos internacionales?*
  - Cada uno con su respectivo `<summary>` y respuesta descriptiva dentro.
- [ ] **Modal de Experiencia en el Taller:**
  - Una ventana emergente nativa implementada con `<dialog id="modal-taller">` para reservar una visita guiada o cata de mezcal con los artesanos.
  - Un botón exterior que abra el modal ejecutando `.showModal()`.
  - Un formulario interno con `<form method="dialog">` para permitir el cierre nativo con botón y soporte automático de la tecla `Escape`.

---

### Área F: Formulario de Cotización y Encargo de Alebrije (`<form>`)

- [ ] **Configuración de envío:** `<form action="https://httpbin.org/post" method="POST" enctype="multipart/form-data">`.
- [ ] **Agrupación temática:** Al menos dos bloques delimitados con `<fieldset>` y titulados con `<legend>` (*Datos del Coleccionista* y *Diseño de la Criatura Mística*).
- [ ] **Controles de entrada especializados:**
  - Nombre completo con `required` y `minlength="3"`.
  - Correo electrónico con `type="email"`, `required` y `autocomplete="email"`.
  - Teléfono con `type="tel"`.
  - Texto asistido con `<datalist>` para elegir el animal o ser protector base (*Jaguar*, *Colibrí*, *Serpiente emplumada*, *Búho*, *Iguana*, *Coyote*).
  - Grupo de botones de opción (`radio`) compartiendo el mismo `name` para el acabado de pintura (*Pigmentos Naturales Históricos* o *Acrílico Extra Fino con Grecas Zapotecas*).
  - Deslizador `<input type="range">` para la escala o tamaño deseado de la pieza (de miniatura a monumental).
  - Campo `<input type="file" accept="image/*,.pdf">` para que el cliente pueda subir un boceto o fotografía de inspiración.
  - Casilla de verificación (`checkbox`) obligatoria para aceptar los tiempos de tallado artesanal y la política de comercio justo.
- [ ] **Accesibilidad en formularios:** Cero inputs huérfanos; todos los controles vinculados formalmente a su `<label for="...">`.
- [ ] **Acciones:** Un `<button type="submit">Solicitar Cotización Artesanal</button>` y un `<button type="reset">Restablecer Formulario</button>`.

---

### Área G: Certificación Oficial de Salud Sintáctica (W3C)

- [ ] El código HTML debe someterse al [Validador Oficial del W3C (Nu Html Checker)](https://validator.w3.org/nu/) y obtener un reporte final con **0 errores sintácticos**.

---

## 4. Matriz de Evaluación Profesional (Rúbrica)

Tu solución será calificada bajo los mismos estándares que una prueba técnica laboral para desarrolladores frontend:

| Criterio | Ponderación | Nivel Excelente (Cumplimiento total) |
| --- | :---: | --- |
| **Arquitectura Semántica y Layout** | **20%** | Uso preciso de etiquetas HTML5 estructurales. Jerarquía de encabezados perfecta (`h1` a `h3`) sin saltos de nivel. Cero etiquetas visuales obsoletas o "divitis" injustificada. |
| **Accesibilidad Universal (A11y)** | **20%** | Navegación 100% fluida por teclado, Skip Link funcional, textos `alt` con criterio contextual describiendo el arte zapoteco, controles con `aria-label` y sin atributos ARIA redundantes. |
| **Formulario y Captura de Datos** | **20%** | Implementación rigurosa de validaciones nativas, tipos de entrada móviles adaptados, soporte para subida de archivos con `enctype`, agrupación temática con `fieldset`/`legend` y vinculación con `<label>`. |
| **Tablas y Datos Estructurados** | **15%** | Cuadrícula matemática perfecta sin celdas desalineadas. Uso correcto de `scope="col"`, `scope="row"`, fusiones con `colspan`/`rowspan` y pie de tabla `<tfoot>`. |
| **Componentes Interactivos Nativos** | **15%** | Funcionamiento correcto de `<dialog>` con `.showModal()`, acordeón exclusivo con `name` en `<details>` y diferenciación conceptual entre `<meter>` y `<progress>`. |
| **SEO, Metadatos y W3C** | **10%** | `<head>` impecable con Open Graph en URLs absolutas, favicon vectorial, viewport responsivo y reporte final con **0 errores** en el validador del W3C. |

---

## 5. Publicación a Producción: Tu Proyecto en Internet (GitHub Pages)

Un proyecto artesanal merece ser visto por el mundo. Sigue estos pasos para publicar tu portal web de forma gratuita:

1. **Prepara tu repositorio:** Asegúrate de que tu archivo principal se llame exactamente `index.html` en la raíz de la carpeta del desafío.
2. **Accede a la configuración:** Dentro de tu repositorio en GitHub, haz clic en la pestaña **Settings** (Configuración).
3. **Sección Pages:** En el menú lateral izquierdo, haz clic en **Pages**.
4. **Rama de despliegue:** En la sección *Build and deployment*, selecciona la rama `main` (o `master`) y la carpeta raíz (`/root`). Pulsa **Save**.
5. **¡Tu web está en línea!:** En pocos minutos, GitHub te entregará el enlace público de tu portal:  
   `https://tu-usuario.github.io/tu-repositorio/`

> [!TIP]
> Incluye este enlace en tu perfil de LinkedIn y en tu portafolio personal. Demostrarás no solo que dominas el código HTML5 moderno, sino que sabes resolver un caso de negocio cultural con identidad visual y accesibilidad universal.

---

## 6. Lista de Control Previa a la Entrega (Self-Checklist)

Antes de dar por concluido tu desafío final, audita tu propio código con esta lista:

- [ ] ¿El documento pasa la prueba del teclado (puedes recorrer y activar toda la web sin usar el ratón)?
- [ ] ¿El modal de reserva se cierra tanto con la tecla `Escape` como con el botón interno sin recargar la página?
- [ ] ¿El formulario exige los campos obligatorios antes de permitir el envío al servidor de pruebas?
- [ ] ¿La tabla de piezas artesanales tiene sus encabezados con `scope` y no se deforma al cambiar el tamaño de la pantalla?
- [ ] ¿Todas las imágenes de los alebrijes tienen declarados sus atributos `width`, `height`, `loading="lazy"` y textos `alt` descriptivos?
- [ ] ¿Pegaste tu código en [validator.w3.org/nu/](https://validator.w3.org/nu/) y confirmaste que el reporte final está completamente en verde (0 errores)?

---

>[!NOTE]
> *"En Oaxaca, una rama de copal no es solo madera: es una criatura esperando a ser liberada con la gubia. En la web, el código HTML no es solo texto: es la estructura que le da vida, dignidad y permanencia a las ideas."*
> **¡Mucho éxito en la construcción de tu proyecto final de certificación!**
