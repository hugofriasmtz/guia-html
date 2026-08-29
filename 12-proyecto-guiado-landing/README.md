# Lección 12: Proyecto guiado — Landing Page para una Startup SaaS

¡Llegó el momento de unir todas las piezas! En las lecciones anteriores aprendiste estructura, texto, tablas, formularios modernos, componentes interactivos nativos, metadatos y accesibilidad.

En este proyecto construirás una **Landing Page profesional de nivel producción para un producto digital (SaaS)**. Aplicarás el 100% de los conocimientos de HTML5 aprendidos a lo largo del curso.

> [!TIP]
> **Para que la página se vea increíble sin perder el foco en HTML:**
> Enlazaremos **Pico CSS** vía CDN en el `<head>`. Es una librería que le da un diseño moderno y soporte para modo oscuro automático a tu página **basándose únicamente en tus etiquetas semánticas de HTML5**, ¡sin obligarte a escribir cientos de clases de diseño!

---

## 1. Modelo visual: Wireframe y arquitectura de la Landing Page

La landing page se estructurará en secciones semánticas claramente delimitadas dentro de `index.html`:

```text
+-------------------------------------------------------------------------+
|  <header> : Logo de marca + <nav> con enlaces a secciones + Botón CTA    |
+-------------------------------------------------------------------------+
|  <main>                                                                 |
|                                                                         |
|  [ SECCIÓN HERO ] : <h1> Título de impacto + <p> + Botones de acción    |
|                     <picture> / <img> con mockup del producto           |
|                                                                         |
|  [ SECCIÓN FEATURES ] : 3 <article> con beneficios del software         |
|                                                                         |
|  [ SECCIÓN DEMO/MÉTRICAS ] : <progress> y <meter> de rendimiento        |
|                              <dialog> con ventana modal interactiva     |
|                                                                         |
|  [ SECCIÓN PRECIOS ] : <table> semántica comparando planes (Free/Pro)   |
|                                                                         |
|  [ SECCIÓN FAQ ] : Acordeones nativos con <details name="faq">          |
|                                                                         |
|  [ SECCIÓN REGISTRO ] : <form> moderno y validado con <fieldset>        |
+-------------------------------------------------------------------------+
|  <footer> : Mapa del sitio + Enlaces legales + Redes sociales            |
+-------------------------------------------------------------------------+
```

---

## 2. Arquitectura de archivos del proyecto

Crea la siguiente estructura dentro de tu carpeta `12-proyecto-guiado-landing`:

```text
12-proyecto-guiado-landing/
├── index.html                   # Página principal de la landing
├── README.md                    # Esta guía de requerimientos
└── assets/
    ├── css/
    │   └── custom.css           # Pequeños ajustes visuales opcionales
    └── img/
        ├── logo.svg             # Logotipo de la marca
        ├── hero-mockup.webp     # Imagen principal de portada
        └── favicon.svg          # Icono de la pestaña
```

---

## 3. Paso a Paso: Construcción del Proyecto

### Fase 1: Metadatos completos y conexión de estilos en `<head>`

Configura el archivo `index.html` con todos los estándares aprendidos en la Lección 9:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DevFlow | La plataforma definitiva para desarrolladores</title>
  <meta name="description" content="Automatiza tu flujo de trabajo, optimiza tu código y despliega proyectos en segundos con DevFlow.">
  <meta name="robots" content="index, follow">
  <meta name="theme-color" content="#1095c1">

  <!-- Open Graph para redes sociales -->
  <meta property="og:title" content="DevFlow | Automatización para Desarrolladores">
  <meta property="og:description" content="Acelera tu desarrollo con nuestra plataforma en la nube.">
  <meta property="og:type" content="website">
  <meta property="og:image" content="https://ejemplo.com/assets/og-portada.jpg">

  <!-- Estilos semánticos con Pico CSS (CDN) -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.min.css">
  <!-- Estilos propios secundarios -->
  <link rel="stylesheet" href="assets/css/custom.css">
</head>
```

---

### Fase 2: Cabecera (`<header>`) y Sección Principal (*Hero*)

```html
<body>
  <!-- 1. Navegación Principal -->
  <header class="container">
    <nav aria-label="Navegación principal">
      <ul>
        <li><strong>DevFlow</strong></li>
      </ul>
      <ul>
        <li><a href="#caracteristicas">Características</a></li>
        <li><a href="#precios">Precios</a></li>
        <li><a href="#faq">Preguntas</a></li>
        <li><button onclick="document.getElementById('modal-demo').showModal()">Ver Demo</button></li>
      </ul>
    </nav>
  </header>

  <main class="container">
    <!-- 2. Sección Hero de impacto -->
    <section id="hero">
      <hgroup>
        <h1>Despliega tus aplicaciones en tiempo récord</h1>
        <p>DevFlow es la plataforma de integración continua pensada por y para desarrolladores modernos.</p>
      </hgroup>
      <p>
        <a href="#registro" role="button">Comenzar gratis</a>
        <a href="#caracteristicas" role="button" class="secondary">Saber más</a>
      </p>
      <figure>
        <img src="https://picsum.photos/1000/450" alt="Vista previa del panel de control de DevFlow con métricas en tiempo real.">
      </figure>
    </section>
```

---

### Fase 3: Características y Métricas interactivas

Aplica etiquetas semánticas y componentes interactivos nativos (`<progress>`, `<meter>`, `<dialog>`):

```html
    <!-- 3. Características -->
    <section id="caracteristicas">
      <h2>¿Por qué elegir DevFlow?</h2>
      <div class="grid">
        <article>
          <header><h3>🚀 Despliegues Rápidos</h3></header>
          <p>Compila y despliega tus repositorios en menos de 30 segundos.</p>
        </article>
        <article>
          <header><h3>🔒 Seguridad Total</h3></header>
          <p>Análisis estático de código y detección de vulnerabilidades automático.</p>
        </article>
        <article>
          <header><h3>📊 Rendimiento Extremo</h3></header>
          <p>Servidores perimetrales distribuidos en más de 200 regiones globales.</p>
        </article>
      </div>

      <!-- Métricas con progress y meter -->
      <aside>
        <h3>Estado de nuestros servidores</h3>
        <label for="uptime">Disponibilidad de la red (99.9%):</label>
        <progress id="uptime" value="99.9" max="100">99.9%</progress>

        <label for="carga">Capacidad de cómputo utilizada:</label>
        <meter id="carga" min="0" max="100" low="40" high="80" optimum="30" value="45">45%</meter>
      </aside>
    </section>

    <!-- Modal nativo para la demostración -->
    <dialog id="modal-demo">
      <article>
        <header>
          <button aria-label="Cerrar" rel="prev" onclick="document.getElementById('modal-demo').close()"></button>
          <h3>Demostración de DevFlow</h3>
        </header>
        <p>Aquí puedes integrar un video con la etiqueta <code>&lt;video controls&gt;</code> o un recorrido interactivo.</p>
        <footer>
          <form method="dialog">
            <button>Cerrar ventana</button>
          </form>
        </footer>
      </article>
    </dialog>
```

---

### Fase 4: Tabla Comparativa de Precios y FAQ con Acordeones

```html
    <!-- 4. Tabla de Precios -->
    <section id="precios">
      <h2>Planes a tu medida</h2>
      <table>
        <thead>
          <tr>
            <th scope="col">Característica</th>
            <th scope="col">Plan Gratuito</th>
            <th scope="col">Plan Pro</th>
            <th scope="col">Enterprise</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="row">Proyectos simultáneos</th>
            <td>3 proyectos</td>
            <td>Ilimitados</td>
            <td>Ilimitados</td>
          </tr>
          <tr>
            <th scope="row">Tiempo de compilación</th>
            <td>100 min/mes</td>
            <td>1,000 min/mes</td>
            <td>Dedicado</td>
          </tr>
          <tr>
            <th scope="row">Soporte 24/7</th>
            <td>❌</td>
            <td>Comunitario</td>
            <td>✅ Dedicado</td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- 5. Preguntas Frecuentes (Acordeones nativos agrupados) -->
    <section id="faq">
      <h2>Preguntas Frecuentes</h2>
      <details name="faq-group" open>
        <summary>¿Necesito tarjeta de crédito para empezar?</summary>
        <p>No, puedes comenzar con nuestro plan gratuito sin ingresar datos de pago.</p>
      </details>
      <details name="faq-group">
        <summary>¿Puedo cancelar mi suscripción en cualquier momento?</summary>
        <p>Sí, la cancelación se procesa con un solo clic desde tu panel de usuario.</p>
      </details>
      <details name="faq-group">
        <summary>¿Ofrecen descuentos para estudiantes o código abierto?</summary>
        <p>Sí, ofrecemos licencias Pro 100% gratuitas para proyectos de Open Source.</p>
      </details>
    </section>
```

---

### Fase 5: Formulario de Registro y Pie de Página

```html
    <!-- 6. Formulario de Captura de Leads / Registro -->
    <section id="registro">
      <article>
        <h2>Crea tu cuenta gratis hoy mismo</h2>
        <form action="/api/registro" method="POST">
          <fieldset>
            <legend>Información de tu cuenta</legend>
            
            <label for="nombre">Nombre completo:</label>
            <input type="text" id="nombre" name="nombre" required placeholder="ej. Linus Torvalds">

            <label for="correo">Correo electrónico profesional:</label>
            <input type="email" id="correo" name="correo" required placeholder="tu@empresa.com" autocomplete="email">

            <label for="rol">Área de trabajo:</label>
            <input type="text" id="rol" name="rol" list="lista-roles" placeholder="Selecciona o escribe...">
            <datalist id="lista-roles">
              <option value="Frontend Developer"></option>
              <option value="Backend Developer"></option>
              <option value="DevOps Engineer"></option>
              <option value="Fullstack Developer"></option>
            </datalist>

            <label>
              <input type="checkbox" name="terminos" required>
              He leído y acepto los <a href="#">Términos de Servicio</a>.
            </label>

            <button type="submit">Comenzar prueba gratuita</button>
          </fieldset>
        </form>
      </article>
    </section>
  </main>

  <!-- 7. Pie de Página Semántico -->
  <footer class="container">
    <hr>
    <p><small>© 2026 DevFlow Inc. Todos los derechos reservados.</small></p>
  </footer>
</body>
</html>
```

---

## Lista de Verificación del Proyecto (Checklist)

Asegúrate de que tu landing page cumpla con todos los criterios de calidad:

- [ ] **Estructura Semántica:** Uso correcto de `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<hgroup>`, `<aside>`, `<figure>` y `<footer>`.
- [ ] **Jerarquía de Encabezados:** Un único `<h1>` en toda la página y subtemas estructurados ordenadamente con `<h2>` y `<h3>`.
- [ ] **Metadatos Completos:** `viewport`, `charset`, `title`, `description`, `theme-color` y etiquetas Open Graph.
- [ ] **Componentes Interactivos Nativos:**
  - Acordeón de preguntas frecuentes con `<details name="...">` y `<summary>`.
  - Ventana modal nativa con `<dialog>` y botón de apertura mediante `.showModal()`.
  - Indicadores con `<progress>` y `<meter>`.
- [ ] **Tabla Semántica:** Uso de `<table>`, `<thead>`, `<tbody>`, `<th>` con atributo `scope="col"` y `scope="row"`.
- [ ] **Formulario Validado:** Campos con `required`, `type="email"`, `autocomplete`, `<datalist>` y vinculados a su `<label for="...">`.
- [ ] **Accesibilidad (A11y):** Imágenes con textos alternativos contextuales (`alt`), etiquetas accesibles y orden de tabulación limpio.
- [ ] **Validación:** Código probado en el [Validador del W3C](https://validator.w3.org/nu/) sin errores sintácticos.

---

## 📚 Recursos y enlaces de apoyo

- 📖 [Pico CSS - Documentación oficial de estilos semánticos](https://picocss.com/docs)
- 🌐 [Validador HTML oficial del W3C](https://validator.w3.org/nu/)
- 📖 [Guía completa de elementos HTML - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element)
