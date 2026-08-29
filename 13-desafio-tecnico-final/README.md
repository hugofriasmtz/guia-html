# Desafío Técnico Final: Portal Web Profesional para una Conferencia Global

¡Bienvenido al desafío técnico final del curso de HTML5!

Atrás quedaron las guías paso a paso y los fragmentos de código listos para copiar y pegar. Este módulo es una **evaluación técnica autónoma** diseñada para simular una prueba de selección laboral o un encargo profesional del mundo real.

Tu objetivo es construir desde cero un **portal web accesible, semántico y optimizado** para **TechPulse 2026**, una conferencia internacional de tecnología, diseño e innovación.

> [!WARNING]
> **Condiciones de la prueba:**
>
> - No uses librerías ni frameworks de JavaScript (React, Vue, Angular, etc.).
> - Si decides incluir diseño, utiliza únicamente un framework CSS semántico/classless (como Pico CSS o Water.css) o tu propio CSS limpio. La evaluación juzgará el **100% de la arquitectura, accesibilidad y semántica de tu código HTML5**.
> - El proyecto debe resolver todas las especificaciones funcionales descritas a continuación.

---

## 1. Arquitectura de Archivos Obligatoria

El proyecto debe constar de un sitio multipágina organizado bajo la siguiente estructura de carpetas:

```text
13-desafio-tecnico-final/
├── index.html                   # Página de Inicio (Hero, speakers, métricas, FAQ)
├── cronograma.html              # Agenda y tabla de conferencias
├── registro.html                # Formulario avanzado de compra de entradas
├── prensa-y-medios.html         # Galería multimedia, videos y descargas
│
└── assets/
    ├── css/
    │   └── custom.css           # Estilos personalizados (opcional)
    ├── img/                     # Imágenes, mockups y logotipos
    └── media/                   # Archivos de audio/video o subtítulos .vtt
```

---

## 2. Requerimientos Técnicos y Funcionales por Página

### 🌐 1. Requerimientos Globales (En todos los archivos `.html`)

- [ ] **DOCTYPE e Idioma:** Declaración correcta de `<!DOCTYPE html>` con `<html lang="es">`.
- [ ] **Sala de Control (`<head>`):**
  - Codificación universal `UTF-8` y configuración responsiva con `viewport`.
  - Etiqueta `<title>` única, atractiva y descriptiva por cada vista.
  - `<meta name="description">` personalizada para cada página (140 - 160 caracteres).
  - Configuración completa de **Open Graph** (`og:title`, `og:description`, `og:image`, `og:url`, `og:type`) y **Twitter Cards**.
  - Enlace canónico (`<link rel="canonical">`) correspondiente a la URL de cada página.
  - Enlace a favicon e icono de dispositivos móviles (`apple-touch-icon`).
- [ ] **Navegación y Layout:**
  - `<header>` con logotipo semántico y barra `<nav aria-label="Navegación principal">`.
  - Atributo `aria-current="page"` implementado con precisión en el enlace activo de cada vista.
  - Enlace de salto al contenido principal (*Skip Link*) funcional al inicio de `<body>`.
  - `<footer>` consistente en las 4 páginas con datos de copyright, mapa del sitio y enlaces a redes sociales.

---

### 📄 2. Página de Inicio (`index.html`)

- [ ] **Sección Hero:**
  - Un único `<h1>` en el documento con el nombre del evento, fecha y lema.
  - Párrafo de valor con enlaces de llamado a la acción (CTA) que dirijan a `registro.html` y `cronograma.html`.
  - Imagen representativa del evento con texto alternativo contextual (`alt`).
- [ ] **Panel de Estadísticas / Métricas:**
  - Elemento `<meter>` para indicar el porcentaje de entradas vendidas con rangos `low`, `high`, `optimum`, `min` y `max`.
  - Elemento `<progress>` que represente la cuenta regresiva o porcentaje de preparación del evento.
- [ ] **Sección de Oradores Destacados (*Speakers*):**
  - Mínimo tres tarjetas de oradores encapsuladas en elementos `<article>` individuales.
  - Cada una con su respectivo `<h3>`, fotografía, biografía corta, cargo y enlaces a sus perfiles.
- [ ] **Componentes Interactivos Nativos:**
  - Sección de **Preguntas Frecuentes (FAQ)** con al menos 4 elementos `<details>` agrupados con el atributo `name`, permitiendo que solo uno esté abierto a la vez.
  - Ventana modal con `<dialog>` que muestre los detalles del "Código de Conducta" y se pueda abrir con un botón y cerrar mediante un `<form method="dialog">` sin dependencias externas.

---

### 📅 3. Cronograma del Evento (`cronograma.html`)

- [ ] **Barra de Migas de Pan (*Breadcrumbs*):**
  - Implementada con `<nav aria-label="Migas de pan">` y lista `<ol>` que permita volver a `index.html`.
- [ ] **Tabla de Datos Completa y Semántica:**
  - Estructura obligatoria: `<table>`, `<caption>`, `<thead>`, `<tbody>` y `<tfoot>`.
  - Uso correcto de encabezados `<th>` con `scope="col"` y `scope="row"`.
  - Mínimo dos combinaciones de celdas utilizando los atributos `colspan` (ej. para el almuerzo o inauguración que abarca todas las salas) y `rowspan` (para talleres de doble duración).
  - Resumen total de horas de contenido registrado en el `<tfoot>`.

---

### 🎟️ 4. Formulario de Registro y Venta (`registro.html`)

- [ ] **Estructura y Agrupación:**
  - Formulario con `action="/procesar-registro"` y `method="POST"`.
  - Dividido en al menos tres `<fieldset>` con sus respectivos `<legend>`:
    1. *Datos del Asistente*: Nombre, correo con `autocomplete="email"`, teléfono, empresa/universidad.
    2. *Tipo de Entrada y Modalidad*: Selección excluyente (`radio`) entre modalidades *Presencial VIP*, *Presencial Estándar* o *Streaming Global*.
    3. *Preferencias y Talleres*: Casillas (`checkbox`) para selección de talleres simultáneos, `<datalist>` para elegir el lenguaje de programación principal, y control `<input type="range">` para nivel de experiencia.
- [ ] **Validación Nativa Estricta:**
  - Uso riguroso de `required`, `minlength`, `maxlength`, `min`, `max`, `step` y `pattern` (expresión regular para código postal o teléfono).
  - **Cero inputs huérfanos:** Cada campo debe estar vinculado explícitamente a su `<label for="...">`.
- [ ] **Subida de Documentos:**
  - Campo `<input type="file">` para subir comprobante de estudiante (si aplica) con restricción de formatos mediante `accept`.

---

### 🎥 5. Prensa y Recursos Multimedia (`prensa-y-medios.html`)

- [ ] **Video con Accesibilidad:**
  - Elemento `<video controls poster="...">` con el tráiler de la edición anterior.
  - Al menos una pista de subtítulos en español o transcripción mediante la etiqueta `<track kind="subtitles" srclang="es" label="Español">`.
- [ ] **Audio:**
  - Elemento `<audio controls>` con un episodio del podcast oficial de la conferencia.
- [ ] **Imágenes Responsivas:**
  - Implementación de `<picture>` con diferentes fuentes (`<source media="...">`) para servir versiones adaptadas a pantallas móviles y de escritorio.
- [ ] **Contenido Embebido Seguro:**
  - Un `<iframe>` interactivo con el mapa de la sede (Google Maps / OpenStreetMap), con su respectivo atributo `title` accesible, `loading="lazy"` y permisos controlados.

---

## 3. Matriz de Evaluación (Rúbrica Profesional)

Tu solución será evaluada bajo los mismos criterios de calidad utilizados en la industria:

| Criterio | Peso | Indicador de Éxito |
| --- | :---: | --- |
| **Semántica Estructural** | 25% | Uso preciso de etiquetas HTML5 (`<main>`, `<article>`, `<section>`, `<hgroup>`, etc.). Ausencia total de "divitis" innecesaria. Jerarquía de encabezados (`h1` a `h6`) perfecta sin saltos de nivel. |
| **Accesibilidad (A11y)** | 25% | Navegación fluida 100% por teclado, *Skip Links* operativos, textos alternativos contextuales en `<img>`, etiquetas `<label>` vinculadas y uso correcto de atributos ARIA indispensables (`aria-current`, `aria-label`). |
| **Formularios e Interactividad** | 25% | Validación nativa completa en el cliente, pares `name`/`value` correctos, funcionamiento nativo de `<dialog>`, `<details>` y `<datalist>` sin scripts bloqueantes. |
| **Metadatos, SEO y Enlazado** | 15% | `<head>` impecable con Open Graph, Twitter Cards, enlaces canónicos, `viewport`, tipografías optimizadas con `preconnect` y resolución exacta de rutas relativas. |
| **Validación W3C** | 10% | **0 errores** al someter los 4 archivos al [Nu Html Checker del W3C](https://validator.w3.org/nu/). |

---

## 4. Lista de Control Previa a la Entrega (Checklist Final)

Antes de considerar tu desafío terminado, revisa punto por punto:

- [ ] ¿Los 4 archivos navegan entre sí sin ningún enlace roto usando rutas relativas correctas?
- [ ] ¿El archivo `index.html` cuenta con un único encabezado `<h1>`?
- [ ] ¿Cada formulario tiene sus botones `<button type="submit">` y `<button type="reset">`?
- [ ] ¿Probaste navegar todo el sitio utilizando únicamente la tecla `Tab` de tu teclado?
- [ ] ¿El modal de `<dialog>` se abre con el botón y se cierra con la tecla `Esc` y con su formulario interno?
- [ ] ¿Pasaste cada una de las 4 páginas por el validador oficial del W3C y obtuviste cero advertencias/errores críticos?

---

> *"El código bien estructurado no necesita explicaciones: su semántica habla por sí misma."*
> **¡Mucho éxito en la construcción de tu proyecto!**
