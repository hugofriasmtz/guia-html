# Lección 12: Proyecto guiado — Landing Page para una Startup SaaS

¡Llegó el momento de conectar todas las piezas! En las lecciones anteriores aprendiste estructura, texto semántico, tablas complejas, formularios modernos, componentes interactivos nativos, metadatos y accesibilidad.

En este taller guiado construirás paso a paso una **Landing Page profesional de nivel producción para una Startup de Software (SaaS)** llamada **DevFlow**. Aprenderás cómo se orquestan decenas de etiquetas para crear una experiencia web real y completa.

---

## 1. Modelo visual: Wireframe y arquitectura de la Landing Page

Toda la página se estructurará dentro de un único archivo `index.html` dividido en bloques semánticos estandarizados:

```text
+-------------------------------------------------------------------------+
|  <header> : Logotipo + <nav> con enlaces a secciones + Botón CTA Modal  |
+-------------------------------------------------------------------------+
|  <main>                                                                 |
|                                                                         |
|  [ SECCIÓN HERO ] : <hgroup> con <h1> y subtítulo + Botones de acción   |
|                     <figure> con imagen optimizada del producto         |
|                                                                         |
|  [ SECCIÓN CARACTERÍSTICAS ] : Contenedor con 3 <article> de beneficios |
|                                <aside> con métricas (<progress>/<meter>)|
|                                <dialog> modal nativo para ver la Demo   |
|                                                                         |
|  [ SECCIÓN PRECIOS ] : <table> semántica comparando planes (Free/Pro)   |
|                                                                         |
|  [ SECCIÓN FAQ ] : Acordeones nativos agrupados (<details name="faq">)  |
|                                                                         |
|  [ SECCIÓN REGISTRO ] : <form> validado con <fieldset> y <datalist>     |
+-------------------------------------------------------------------------+
|  <footer> : Separador <hr> + Derechos de autor + Enlaces secundarios    |
+-------------------------------------------------------------------------+
```

---

## 2. Arquitectura de archivos del proyecto

Crea la siguiente estructura dentro de tu carpeta `12-proyecto-guiado-landing`:

```text
12-proyecto-guiado-landing/
├── index.html                   # Documento principal de la landing
├── README.md                    # Esta guía del proyecto
└── assets/
    ├── css/
    │   └── custom.css           # Pequeños ajustes visuales opcionales
    └── img/
        └── favicon.svg          # Icono de la pestaña
```

---

## 3. Paso a paso: Construcción guiada del proyecto

---

### Fase 1: La sala de máquinas (Metadatos, SEO, Open Graph y Pico CSS)

Abre tu archivo `index.html` y escribe el bloque de cabecera aplicando los estándares de la Lección 9:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <!-- 1. Codificación y Viewport móvil -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 2. SEO Básico -->
  <title>DevFlow | Plataforma de Automatización para Desarrolladores</title>
  <meta name="description" content="Automatiza tu flujo de trabajo, optimiza tu código y despliega aplicaciones en segundos con la infraestructura global de DevFlow.">
  <meta name="robots" content="index, follow">
  <meta name="theme-color" content="#1095c1">

  <!-- 3. Redes Sociales (Open Graph y Twitter) -->
  <meta property="og:title" content="DevFlow | Automatización para Desarrolladores">
  <meta property="og:description" content="Acelera tu ciclo de desarrollo y despliega proyectos en tiempo récord.">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://devflow.ejemplo.com">
  <meta property="og:image" content="https://picsum.photos/1200/630">
  <meta name="twitter:card" content="summary_large_image">

  <!-- 4. Estilos Semánticos con Pico CSS v2 (CDN) -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.min.css">
  
  <!-- 5. Estilos locales secundarios -->
  <link rel="stylesheet" href="assets/css/custom.css">
</head>
```

#### Qué observar en la fase 1

- **Detección automática de tema:** Al incluir Pico CSS, la página adapta automáticamente sus colores según si el sistema operativo del usuario tiene activo el **Modo Claro o Modo Oscuro**.
- **Metadatos completos:** Declarar `theme-color`, `description` y Open Graph garantiza que la página esté lista para buscadores y redes sociales desde el primer minuto.

#### Paso de verificación 1

Guarda el archivo y ábrelo en tu navegador. Presiona `F12` y comprueba en la consola que no existan errores de carga de la hoja de estilos de Pico CSS.

---

### Fase 2: Navegación fija (`<header>`) y Sección de Impacto (*Hero*)

Dentro de `<body>`, construiremos la cabecera y el bloque principal de presentación:

```html
<body>
  <!-- 1. Navegación Principal Global -->
  <header class="container">
    <nav aria-label="Navegación principal">
      <ul>
        <li><strong>⚡ DevFlow</strong></li>
      </ul>
      <ul>
        <li><a href="#caracteristicas">Características</a></li>
        <li><a href="#precios">Precios</a></li>
        <li><a href="#faq">Preguntas</a></li>
        <li>
          <button type="button" onclick="document.getElementById('modal-demo').showModal()">
            Ver Demo
          </button>
        </li>
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
        <img 
          src="https://picsum.photos/1000/450" 
          alt="Vista previa del panel de control de DevFlow mostrando gráficos de despliegue en tiempo real"
          width="1000"
          height="450"
          loading="lazy"
        >
      </figure>
    </section>
```

#### Qué observar en la fase 2

Puedes notar varios detalles de semántica y estilo que Pico CSS aplica automáticamente:

- **El contenedor semántico de Pico:** La clase `.container` centra el contenido y le da márgenes responsivos automáticos.
- **Flexbox nativo en `<nav>`:** Observa cómo Pico CSS coloca el logo a la izquierda y los enlaces a la derecha simplemente usando dos listas `<ul>` dentro de `<nav>`.
- **Agrupación con `<hgroup>`:** Mantiene el `<h1>` y su párrafo de subtítulo unidos semánticamente para los lectores de pantalla.
- **Rendimiento de imagen (CLS):** La imagen incluye `width="1000"`, `height="450"` y `loading="lazy"` para prevenir saltos de pantalla (CLS) y optimizar el consumo de datos móviles.

#### Paso de verificación 2

Recarga la página en el navegador. Haz clic en los enlaces del menú ("Características", "Precios") y observa cómo la barra de direcciones se actualiza con los identificadores de sección (`#`).

---

### Fase 3: Características modulares y métricas nativas (`<progress>`, `<meter>`, `<dialog>`)

Agregaremos los beneficios del software en tarjetas, los medidores de estado del servidor y la ventana modal interactiva:

```html
    <!-- 3. Sección de Características -->
    <section id="caracteristicas">
      <h2>¿Por qué elegir DevFlow?</h2>
      <div class="grid">
        <article>
          <header><h3>🚀 Despliegues Rápidos</h3></header>
          <p>Compila y despliega tus repositorios en menos de 30 segundos gracias a nuestra red de caché global.</p>
        </article>
        <article>
          <header><h3>🔒 Seguridad Integrada</h3></header>
          <p>Análisis estático de código y detección automatizada de vulnerabilidades en cada pull request.</p>
        </article>
        <article>
          <header><h3>📊 Rendimiento Extremo</h3></header>
          <p>Servidores perimetrales distribuidos en más de 200 regiones para garantizar baja latencia.</p>
        </article>
      </div>

      <!-- Métricas de estado con progress y meter -->
      <aside>
        <h3>Estado de nuestros servidores en tiempo real</h3>
        <label for="uptime">Disponibilidad de la red (99.9% objetivo):</label>
        <progress id="uptime" value="99.9" max="100">99.9%</progress>

        <label for="carga">Capacidad de cómputo utilizada:</label>
        <meter id="carga" min="0" max="100" low="40" high="80" optimum="30" value="45">45%</meter>
      </aside>
    </section>

    <!-- Modal nativo para la demostración -->
    <dialog id="modal-demo">
      <article>
        <header>
          <button type="button" aria-label="Cerrar" rel="prev" onclick="document.getElementById('modal-demo').close()"></button>
          <h3>Demostración de DevFlow</h3>
        </header>
        <p>Observa cómo se configura una canalización de despliegue en menos de un minuto.</p>
        <figure>
          <img 
            src="https://picsum.photos/600/300" 
            alt="Captura interactiva de la terminal de comandos ejecutando DevFlow" 
            width="600" 
            height="300" 
            loading="lazy"
          >
        </figure>
        <footer>
          <form method="dialog">
            <button type="submit">Entendido, cerrar ventana</button>
          </form>
        </footer>
      </article>
    </dialog>
```

#### Qué observar en la fase 3

Puedes notar varios detalles de semántica y estilo que Pico CSS aplica automáticamente:

- **La rejilla automática (`.grid`):** La clase utilitaria `grid` de Pico CSS distribuye los elementos `<article>` en columnas proporcionales que se apilan solas en pantallas de teléfonos móviles.
- **La semántica de `<article>`:** Cada característica utiliza `<article>` con su propio `<header>`, convirtiéndose en una tarjeta de contenido independiente y accesible.
- **El `<dialog>` accesible:** Al pulsar el botón "Ver Demo" del menú, se ejecuta `.showModal()`, oscureciendo el fondo con `::backdrop` y permitiendo el cierre inmediato al pulsar la tecla `Escape` o el botón con `<form method="dialog">`.

#### Paso de verificación 3

Haz clic en el botón "Ver Demo" de la cabecera. Comprueba que el modal se abre en la capa superior, oscurece el fondo y se cierra correctamente al presionar la tecla `Escape`.

---

### Fase 4: Tabla comparativa de precios y preguntas frecuentes

Añadiremos la tabla de planes y el acordeón exclusivo de soporte:

```html
    <!-- 4. Tabla Comparativa de Planes -->
    <section id="precios">
      <h2>Planes transparentes a tu medida</h2>
      <table>
        <caption>Comparativa detallada de características por nivel de suscripción</caption>
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
            <td>Servidor dedicado</td>
          </tr>
          <tr>
            <th scope="row">Soporte técnico</th>
            <td>Comunitario</td>
            <td>Por correo (< 24h)</td>
            <td>Dedicado 24/7</td>
          </tr>
          <tr>
            <th scope="row">Cifrado SSL automático</th>
            <td colspan="3">Incluido en todos los planes</td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <th scope="row">Inversión mensual</th>
            <td>$0 / mes</td>
            <td>$29 / mes</td>
            <td>Contactar ventas</td>
          </tr>
        </tfoot>
      </table>
    </section>

    <!-- 5. Preguntas Frecuentes (Acordeones nativos con name) -->
    <section id="faq">
      <h2>Preguntas Frecuentes</h2>
      <details name="faq-group" open>
        <summary>¿Necesito ingresar una tarjeta de crédito para empezar?</summary>
        <p>No, puedes crear tu cuenta en el Plan Gratuito sin ingresar ningún dato bancario.</p>
      </details>
      <details name="faq-group">
        <summary>¿Puedo cancelar o cambiar de plan en cualquier momento?</summary>
        <p>Sí, puedes actualizar o cancelar tu suscripción con un solo clic directamente desde tu panel de usuario.</p>
      </details>
      <details name="faq-group">
        <summary>¿Ofrecen descuentos para proyectos de código abierto o estudiantes?</summary>
        <p>Sí, ofrecemos licencias Pro 100% gratuitas para repositorios de Open Source y estudiantes universitarios acreditados.</p>
      </details>
    </section>
```

---

#### Qué observar en la fase 4

Si observas con atención, notarás varios detalles de semántica y estilo que Pico CSS aplica automáticamente:

- **Tablas con estilo automático:** Nota cómo Pico CSS aplica bordes limpios, sangrías y alineación a la tabla sin que hayas escrito una sola línea de CSS; todo gracias a la presencia de `<caption>`, `<thead>`, `<tbody>` y `<tfoot>`.
- **`colspan="3"` en acción:** La fila de cifrado SSL abarca las 3 columnas de planes de forma limpia, demostrando la matemática de celdas aprendida en la Lección 6.
- **Acordeón exclusivo nativo:** Gracias al atributo `name="faq-group"`, abrir una pregunta cierra automáticamente la que estaba abierta sin utilizar JavaScript.

#### Paso de verificación 4

Abre la segunda pregunta frecuente del FAQ y comprueba cómo el navegador cierra automáticamente la primera pregunta.

---

### Fase 5: Formulario de conversión (`<form>`) y Pie de página (`<footer>`)

Completaremos la página con el formulario de registro asistido y el cierre semántico del documento:

```html
    <!-- 6. Formulario de Captura de Leads / Registro -->
    <section id="registro">
      <article>
        <h2>Crea tu cuenta gratis hoy mismo</h2>
        <p>Comienza a desplegar en segundos. No requerimos tarjeta de crédito.</p>

        <!-- Formulario configurado con endpoint de pruebas para evitar errores 404 -->
        <form action="https://httpbin.org/post" method="POST">
          <fieldset>
            <legend>Información de tu cuenta</legend>
            
            <label for="nombre">Nombre completo:</label>
            <input 
              type="text" 
              id="nombre" 
              name="nombre_completo" 
              required 
              minlength="3" 
              placeholder="ej. Ada Lovelace"
            >

            <label for="correo">Correo electrónico profesional:</label>
            <input 
              type="email" 
              id="correo" 
              name="correo_electronico" 
              required 
              placeholder="ada@empresa.com" 
              autocomplete="email"
            >

            <label for="rol">Especialidad técnica principal:</label>
            <input 
              type="text" 
              id="rol" 
              name="rol_tecnico" 
              list="lista-roles" 
              placeholder="Selecciona o escribe..."
            >
            <datalist id="lista-roles">
              <option value="Frontend Developer"></option>
              <option value="Backend Developer"></option>
              <option value="DevOps & Cloud Engineer"></option>
              <option value="Fullstack Developer"></option>
              <option value="Estudiante / Aprendiz"></option>
            </datalist>

            <label>
              <input type="checkbox" name="terminos" value="aceptados" required>
              He leído y acepto los <a href="#">Términos de Servicio</a> y la Política de Privacidad.
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
    <p><small>© 2026 DevFlow Inc. Todos los derechos reservados. Construido con HTML5 semántico puro.</small></p>
  </footer>
</body>
</html>
```

#### Qué observar en la fase 5

- **Validación nativa estilizada:** Pico CSS resalta automáticamente los campos en verde (`:valid`) o rojo (`:invalid`) conforme el usuario interactúa con ellos.
- **Envío real a `httpbin.org`:** Al usar `https://httpbin.org/post`, puedes probar el botón de envío y verás la respuesta JSON con todos los datos procesados, sin provocar errores 404 en tu entorno local.

#### Paso de verificación 5

1. Pulsa el botón "Comenzar prueba gratuita" dejando los campos en blanco: comprueba cómo el navegador detiene el envío y resalta el primer campo obligatorio.
2. Llena los datos correctamente, marca la casilla de términos y pulsa enviar: observa la respuesta JSON estructurada que devuelve el servidor de pruebas.

---

## 4. Lista de verificación integral (Checklist de calidad)

Audita tu archivo `index.html` terminado y confirma que cumpla con todos los criterios de excelencia del curso:

- [ ] **Estructura Semántica:** Uso correcto y jerárquico de `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<hgroup>`, `<aside>`, `<figure>` y `<footer>`.
- [ ] **Jerarquía de Encabezados:** Existe un único `<h1>` en el Hero y las secciones secundarias utilizan `<h2>` y `<h3>` de forma ordenada sin saltarse niveles.
- [ ] **Metadatos Completos:** Configuración de `viewport`, `charset="UTF-8"`, `title`, `description`, `theme-color` y tarjetas Open Graph.
- [ ] **Componentes Interactivos Nativos:**
  - Acordeón de FAQ exclusivo con `<details name="...">` y `<summary>`.
  - Ventana modal con `<dialog>`, botón de apertura con `type="button"` y cierre con `<form method="dialog">`.
  - Indicadores con `<progress>` y `<meter>`.
- [ ] **Tabla Semántica:** Estructura completa con `<caption>`, `<thead>`, `<tbody>`, `<tfoot>` y encabezados accesibles con `scope="col"` y `scope="row"`.
- [ ] **Formulario Moderno:** Campos con `required`, `type="email"`, `autocomplete`, sugerencias con `<datalist>` y vinculación accesible de etiquetas `<label>`.
- [ ] **Prevención de CLS:** Dimensiones explícitas (`width` y `height`) y `loading="lazy"` en todas las imágenes.
- [ ] **Validación Oficial W3C:** Pasa el código completo por el [Validador Oficial del W3C](https://validator.w3.org/nu/) y asegura **0 errores sintácticos**.

---

## 5. Preguntas de autoevaluación (Integración global)

Intenta responder las preguntas mentalmente para comprobar tu comprensión de la arquitectura y luego despliega la sección:

1. ¿Por qué en la sección Hero se utilizó la etiqueta `<hgroup>` para envolver el título `<h1>` y el párrafo explicativo?
2. ¿Cómo logra Pico CSS que la barra de navegación `<nav>` se alinee en extremos opuestos (logo a la izquierda y enlaces a la derecha) sin haber escrito clases de CSS flexbox?
3. ¿Cuál es la ventaja de utilizar `colspan="3"` en la fila de cifrado SSL de la tabla en lugar de escribir tres celdas separadas con el mismo texto?
4. Si cambias el tema de tu computadora a modo oscuro, ¿por qué la página cambia de color automáticamente sin haber escrito código JavaScript?
5. ¿Por qué el botón que abre la ventana modal debe llevar explícitamente el atributo `type="button"`?

---

## 📚 Recursos y enlaces de apoyo

- 📖 [Pico CSS - Documentación oficial de estilos semánticos](https://picocss.com/docs)
- 🌐 [Nu Html Checker - Validador Oficial del W3C](https://validator.w3.org/nu/)
- 📖 [Guía completa de elementos HTML - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element)
- 📖 [Pautas de accesibilidad web (WCAG) - W3C WAI](https://www.w3.org/WAI/standards-guidelines/wcag/)
