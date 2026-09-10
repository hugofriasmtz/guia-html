# Lección 10: Accesibilidad web (A11y), ARIA y validación de código

Esta lección continúa la ruta tras dominar la configuración del documento en [Metadatos e Integración](../09-metadatos-e-integracion/README.md). La web fue concebida para ser universal: cualquier persona, independientemente de sus capacidades físicas, sensoriales, cognitivas o del dispositivo que utilice, debe poder percibir, entender, navegar e interactuar con tu sitio.

En este capítulo aprenderás los estándares de **accesibilidad web (a11y)**, el uso responsable de atributos **WAI-ARIA**, las técnicas de navegación exclusiva por teclado y cómo certificar que tu código cumpla con los estándares oficiales del **W3C**.

---

## 1. Modelo mental: El Árbol de Accesibilidad

Los navegadores no solo crean el DOM (árbol de elementos visuales) para pintar la pantalla; en paralelo generan el **Árbol de Accesibilidad** (*Accessibility Tree*), que es la estructura de datos que leen los lectores de pantalla (como NVDA en Windows, VoiceOver en macOS/iOS o TalkBack en Android):

```text
CÓDIGO HTML:
<button>Comprar ahora</button>
<img src="icono.png" alt="">

               |
               v
ÁRBOL DOM (Visual / Renderizado)           ÁRBOL DE ACCESIBILIDAD (Lectores de pantalla)
+-------------------------------+         +-------------------------------------------+
| Button (Rectángulo azul)      | ------> | Rol: button                               |
| Image  (Icono de carrito)     |         | Nombre accesible: "Comprar ahora"         |
+-------------------------------+         | Estado: clickable, focusable              |
                                          | (La imagen decorativa con alt="" se ignora|
                                          +-------------------------------------------+
```

### Los 4 Principios Fundamentales de WCAG (POUR)

Las pautas internacionales de accesibilidad (*Web Content Accessibility Guidelines*) se resumen en cuatro pilares:

1. **Perceptible:** La información debe presentarse en formas que todos puedan percibir (textos alternativos en imágenes, subtítulos en video y buen contraste de color).
2. **Operable:** La interfaz debe poder controlarse al 100% mediante teclado, sin trampas de foco y con tiempo suficiente para interactuar.
3. **Comprensible:** El lenguaje debe ser claro, la navegación predecible y los errores en formularios deben explicarse con soluciones concretas.
4. **Robusto:** El código debe seguir los estándares oficiales para que cualquier navegador o tecnología de asistencia lo interprete sin fallos.

### Qué observar en el Árbol de Accesibilidad

- Puedes ver este árbol en tu propio navegador: abre **DevTools (F12)** $\rightarrow$ pestaña **Elementos** $\rightarrow$ pestaña lateral **Accesibilidad** (o el icono de la persona/árbol en la esquina superior derecha del panel).
- Para cada elemento interactivo, el navegador calcula tres propiedades críticas:
  - **Rol (*Role*):** Qué es (botón, enlace, encabezado, casilla).
  - **Nombre accesible (*Name*):** Qué dice o qué acción realiza.
  - **Estado (*State*):** Si está enfocado, expandido, deshabilitado o marcado.

### Práctica 1: Inspeccionando el Árbol de Accesibilidad (en `index.html`)

1. Crea tu archivo `index.html` con un `<button>Iniciar Sesión</button>` y un enlace `<a href="#">Ver catálogo</a>`.
2. Abre DevTools (`F12`), ve a la pestaña **Elementos** y selecciona la pestaña lateral **Accesibilidad**.
3. Haz clic sobre el botón e inspecciona sus propiedades calculadas: comprueba cómo el navegador le asignó el rol `button` y el nombre accesible `"Iniciar Sesión"` de forma 100% automática.

---

## 2. La Primera Regla de ARIA: Lo nativo siempre gana

WAI-ARIA (*Accessible Rich Internet Applications*) es una especificación que agrega atributos especiales (`role`, `aria-*`) para comunicar información a las tecnologías de asistencia cuando el HTML nativo se queda corto.

Sin embargo, el estándar de accesibilidad del W3C establece una advertencia categórica:

> [!IMPORTANT]
> **Primera Regla de ARIA:**  
> *"Si puedes usar un elemento o atributo nativo de HTML con la semántica y comportamiento que necesitas, **NO uses ARIA**; usa el elemento nativo."*

### Comparativa: Elemento falso vs. Elemento nativo

```html
<!-- ❌ INCORRECTO: Reinventar la rueda con divs y ARIA -->
<!-- Requiere JavaScript para el clic, JS para escuchar las teclas Enter/Espacio,
     tabindex manual y estilos CSS para el foco. ¡Frágil y propenso a errores! -->
<div role="button" tabindex="0" onclick="enviar()" onkeydown="manejarTeclado(event)">
  Enviar formulario
</div>

<!-- ✅ CORRECTO: El elemento nativo de HTML5 -->
<!-- Accesible por teclado de inmediato (Enter y Espacio), anuncia el rol nativo,
     atrapa el foco automáticamente y funciona aunque falle JavaScript -->
<button type="submit">Enviar formulario</button>
```

> [!WARNING]
> **El peligro del "Mal ARIA":**  
> Usar mal los atributos ARIA es mucho peor que no usarlos en absoluto. Por ejemplo, colocarle `role="navigation"` a una etiqueta `<nav>` es redundante; pero colocarle `role="button"` a un enlace `<a>` confunde al lector de pantalla, que esperará que el elemento se active con la barra espaciadora como un botón en lugar de la tecla Enter como un enlace.

### Qué observar en la primera regla de ARIA

- Los elementos nativos como `<button>`, `<select>`, `<details>` o `<dialog>` traen integradas de fábrica decenas de reglas de teclado y compatibilidad con lectores de pantalla que requerirían cientos de líneas de JavaScript para emularse sobre un `<div>`.

### Práctica 2: Comparando la navegación por teclado (en `index.html`)

1. Copia ambos ejemplos (el `div` simulado y el `button` nativo) dentro del `<body>` de tu `index.html`.
2. Guarda el archivo, abre la página en el navegador y presiona la tecla `Tab` repetidamente.
3. Observa cómo el `<button>` recibe el anillo de foco del navegador de forma natural y puede pulsarse con la barra espaciadora.

---

## 3. Atributos ARIA indispensables y regiones dinámicas

Cuando creas componentes interactivos avanzados donde HTML nativo no tiene una etiqueta específica, estos son los atributos ARIA esenciales que debes dominar:

| Atributo / Rol | Propósito | Ejemplo de uso |
| --- | --- | --- |
| `aria-label` | Asigna una etiqueta de texto invisible en pantalla a un control sin texto visual (ej. botones con solo un icono). | `<button aria-label="Cerrar ventana">✕</button>` |
| `aria-labelledby` | Define el nombre accesible vinculándolo al `id` de otro texto visible en pantalla. | `<section aria-labelledby="titulo-faq">` |
| `aria-describedby` | Vincula un campo con un texto secundario explicativo o mensaje de error. | `<input aria-describedby="reglas-clave">` |
| `aria-hidden="true"` | Oculta elementos puramente decorativos o duplicados para que el lector los ignore. | `<span aria-hidden="true">🎉</span>` |
| `aria-expanded` | Comunica si un menú desplegable o acordeón está abierto (`true`) o cerrado (`false`). | `<button aria-expanded="false">Menú</button>` |
| `aria-live="polite"` | Anuncia en voz alta actualizaciones dinámicas de contenido sin interrumpir al usuario. | `<div aria-live="polite" id="mensaje-estado"></div>` |

### Ejemplo contextual de componentes con ARIA

```html
<!-- 1. Botón con icono accesible y estado de apertura -->
<button type="button" aria-expanded="false" aria-controls="menu-lateral" aria-label="Abrir menú de navegación">
  <span aria-hidden="true">☰</span>
</button>

<!-- 2. Campo de formulario asistido con instrucciones -->
<label for="clave">Contraseña:</label>
<input type="password" id="clave" name="clave" aria-describedby="ayuda-clave">
<p id="ayuda-clave">Debe incluir al menos 8 caracteres, un número y una mayúscula.</p>

<!-- 3. Región en vivo para notificaciones o carritos de compra -->
<!-- Cuando JavaScript inserte texto aquí, el lector de pantalla lo anunciará automáticamente -->
<div aria-live="polite" id="notificacion-sistema">
  Producto añadido al carrito con éxito.
</div>
```

### Qué observar en los atributos ARIA

- **`aria-label` sobreescribe el contenido visible:** Si escribes `<button aria-label="Cerrar">X</button>`, el lector de pantalla dirá *"Cerrar, botón"* e ignorará por completo la letra "X".
- **`aria-live="polite"` vs. `aria-live="assertive"`:**
  - `polite`: El lector de pantalla espera a que termine de leer la frase actual antes de anunciar el cambio (ideal para la mayoría de avisos).
  - `assertive`: El lector interrumpe inmediatamente lo que esté diciendo para anunciar el cambio (reservado para emergencias críticas o errores graves del sistema).

> [!CAUTION]
> Nunca uses `aria-label` como reemplazo de un `<label>` visible en campos de texto de formularios regulares. Las personas con problemas cognitivos o memoria a corto plazo necesitan que la etiqueta permanezca visible en la pantalla todo el tiempo.

### Práctica 3: Notificaciones accesibles con Live Regions (en `index.html`)

1. En tu `index.html`, agrega un contenedor `<div aria-live="polite" id="alerta"></div>`.
2. Agrega un botón `<button type="button" onclick="document.getElementById('alerta').textContent = 'Guardado a las ' + new Date().toLocaleTimeString()">Guardar cambios</button>`.
3. Inspecciona el contenedor en DevTools y comprueba cómo la propiedad accesible de región en vivo queda registrada en el navegador.

---

## 4. Navegación por teclado y gestión de foco (`tabindex` y Skip Links)

El orden natural de tabulación sigue la secuencia exacta en la que los elementos interactivos están ordenados en el código HTML:

```text
FLUJO DE TABULACIÓN NATURAL:
[ Enlace 1 ] ----(Tab)----> [ Enlace 2 ] ----(Tab)----> [ Input Texto ] ----(Tab)----> [ Botón Enviar ]
```

### Control del foco con el atributo `tabindex`

```html
<!-- tabindex="0": Permite que un elemento normalmente estático reciba foco con la tecla Tab en su orden natural -->
<div tabindex="0" class="tarjeta-interactiva">Contenido enfocable</div>

<!-- tabindex="-1": NO recibe foco al presionar Tab, pero SÍ puede recibir foco mediante JavaScript con .focus() -->
<dialog id="modal" tabindex="-1">...</dialog>
```

> [!WARNING]
> **PROHIBIDO usar números positivos (`tabindex="1"`, `tabindex="2"`):**  
> Alterar artificialmente la secuencia de tabulación rompe el flujo lógico del documento, desorienta a los usuarios de lectores de pantalla y crea inconsistencias visuales severas. Usa exclusivamente `0` o `-1`.

### Enlaces de salto al contenido principal (*Skip Links*)

En páginas con barras de navegación gigantes que contienen decenas de enlaces, una persona que navega exclusivamente con teclado debe presionar la tecla `Tab` decenas de veces en cada página antes de poder leer el contenido principal.

Para solucionarlo, se incluye un **Skip Link** al inicio de todo el documento:

```html
<body>
  <!-- Enlace de salto: debe ser el PRIMER elemento interactivo del body -->
  <a href="#contenido-principal" class="skip-link">Saltar al contenido principal</a>

  <header>
    <nav>
      <!-- Decenas de enlaces de navegación -->
      <a href="/inicio">Inicio</a>
      <a href="/nosotros">Nosotros</a>
      <a href="/servicios">Servicios</a>
      <a href="/contacto">Contacto</a>
    </nav>
  </header>

  <!-- Destino del salto con su id coincidente -->
  <main id="contenido-principal">
    <h1>Noticia principal del día</h1>
    <p>Texto del artículo...</p>
  </main>
</body>
```

### Qué observar en los Skip Links

- Visualmente se suelen ocultar fuera de la pantalla mediante CSS y se hacen visibles en la esquina superior izquierda únicamente cuando reciben el foco del teclado (`.skip-link:focus`).
- Al pulsar `Enter` sobre el enlace de salto, el cursor de navegación se traslada directamente al interior de `<main>`, omitiendo toda la cabecera.

### Práctica 4: Implementando un Skip Link funcional (en `index.html`)

1. En tu `index.html`, coloca el Skip Link como el primer elemento dentro de `<body>`.
2. Agrega una lista de 5 enlaces dentro de un `<nav>` y luego tu `<main id="contenido-principal">` con un encabezado `<h1>`.
3. Recarga la página y presiona la tecla `Tab` **una sola vez**: presiona `Enter` y comprueba cómo el navegador salta de inmediato hacia el `main` sin pasar por los enlaces del menú.

---

## 5. Accesibilidad en imágenes, iconos y elementos gráficos

El atributo `alt` no solo sirve para describir paisajes; cumple diferentes funciones según el rol del gráfico:

```html
<!-- 1. Imagen informativa: Describe el contenido relevante para el contexto -->
<img src="grafico-ventas.png" alt="Gráfico de barras que muestra un incremento del 25% en ventas durante el tercer trimestre.">

<!-- 2. Imagen puramente decorativa: alt vacío para que el lector la ignore en silencio -->
<img src="adorno-ondas.svg" alt="" role="presentation">

<!-- 3. Icono gráfico dentro de un botón: El texto del botón ya explica la acción -->
<!-- Si pusieras alt="Lupa", el lector diría: "Lupa Buscar, botón", lo cual es redundante -->
<button type="button">
  <img src="lupa.svg" alt="" aria-hidden="true">
  Buscar productos
</button>

<!-- 4. Botón con SOLO un icono (sin texto visible): ARIA le da el nombre accesible -->
<button type="button" aria-label="Descargar reporte en formato PDF">
  <img src="icono-descarga.svg" alt="" aria-hidden="true">
</button>
```

### Qué observar en la accesibilidad gráfica

- Si una imagen tiene texto adyacente que ya explica exactamente lo mismo, la imagen debe considerarse decorativa (`alt=""` y `aria-hidden="true"`).
- Nunca dejes un botón que solo contenga un icono sin `aria-label`; de lo contrario, el lector de pantalla solo anunciará *"Botón"* sin ninguna pista sobre qué hace.

### Práctica 5: Imágenes con propósito semántico (en `index.html`)

1. Agrega en tu `index.html` un botón con un icono y texto visible, asegurándote de silenciar el icono decorativo con `alt=""` y `aria-hidden="true"`.
2. Agrega un segundo botón que no tenga texto visible (solo un icono de "X") y configúrale su nombre accesible con `aria-label="Cerrar notificación"`.
3. Inspecciona ambos botones en el panel de Accesibilidad de DevTools y comprueba qué nombre accesible calculó el navegador para cada uno.

---

## 6. Validación de código con el estándar W3C

El navegador web es tolerante a fallos: si olvidas cerrar una etiqueta, intentará "adivinar" lo que quisiste hacer. Sin embargo, ese comportamiento benevolente provoca que los lectores de pantalla fallen, que el CSS se descuadre o que JavaScript arroje errores inesperados.

El **Nu Html Checker del W3C** es el validador oficial internacional que certifica la salud sintáctica de tu código:

```text
PROCESO DE AUDITORÍA:
Tu código HTML ----> [ Nu Html Checker del W3C ] ----> 0 Errores (Conforme a la norma)
                                                 ----> Advertencias / Errores críticos
```

### Errores fatales comunes que rompen la validación

| Error común | Ejemplo incorrecto | Corrección conforme a la norma |
| --- | --- | --- |
| **Etiquetas solapadas** | `<p>Texto <strong>aquí</p></strong>` | `<p>Texto <strong>aquí</strong></p>` |
| **Identificadores `id` duplicados** | `<input id="correo"> ... <input id="correo">` | Cada `id` debe ser **único e irrepetible** en todo el archivo. |
| **Interactivos anidados** | `<a href="/ver"><button>Ver</button></a>` | Usa solo el enlace `<a>` o solo el botón `<button>`, nunca uno dentro de otro. |
| **Atributos obligatorios omitidos** | `<img src="foto.jpg">` | Todo `<img>` debe llevar obligatoriamente `alt` (aunque esté vacío). |

### Práctica 6: Rompiendo y reparando el validador (en `index.html`)

1. En tu archivo `index.html`, escribe deliberadamente dos elementos con el mismo `id="test"` y un `<img>` sin atributo `alt`.
2. Ingresa a la herramienta oficial del W3C: [validator.w3.org/nu/](https://validator.w3.org/nu/).
3. Selecciona la opción **Check by text input** (comprobar por entrada de texto), pega tu código y haz clic en **Check**.
4. Observa los mensajes de error en rojo. Corrige los errores en tu editor, vuelve a validar y comprueba cómo el reporte se tiñe de verde.

---

## Reto final de la lección: Portal de Noticias Accesible

Ahora que dominas los principios de accesibilidad, la navegación por teclado y la validación técnica, demostrarás tu autonomía construyendo un proyecto completo y certificándolo ante el validador del W3C.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `10-accesibilidad-y-validacion`. Construirás la portada de un **Portal de Noticias y Divulgación Científica** que cumpla estrictamente con la siguiente lista de verificación:

- [ ] Estructura base completa y válida de HTML5 con `<!DOCTYPE html>`, `<html lang="es">`, `<head>` y `<body>`.
- [ ] **Navegación y Foco:**
  - [ ] Un enlace de salto (*Skip Link*) como primer elemento interactivo del `<body>` que apunte al `id` del contenedor principal (`<main id="contenido">`).
  - [ ] El flujo completo de la página debe ser navegable al 100% utilizando exclusivamente la tecla `Tab` sin quedar atrapado en ningún elemento.
- [ ] **Cabecera y Búsqueda:**
  - [ ] Encabezado semántico `<header>` con un `<nav aria-label="Menú principal">` con al menos 4 enlaces de secciones.
  - [ ] Un botón de "Cambiar tema" (Modo oscuro) que contenga solo un icono gráfico, pero cuente con su respectivo `aria-label="Alternar modo oscuro"`.
  - [ ] Un formulario de búsqueda que asocie su campo de texto a una etiqueta accesible mediante `<label for="...">` o `aria-label`.
- [ ] **Contenido Principal:**
  - [ ] Un elemento `<main id="contenido">` con el encabezado principal `<h1>`.
  - [ ] Un artículo destacado (`<article>`) que contenga:
    - Una imagen informativa con su descripción contextual detallada en `alt`.
    - Un icono puramente decorativo con `alt=""` y `aria-hidden="true"`.
    - Texto estructurado con títulos semánticos coherentes (`<h2>`, `<h3>`).
- [ ] **Región Dinámica y Notificaciones:**
  - [ ] Una zona de avisos o suscripción al boletín con un contenedor configurado con `aria-live="polite"` para mensajes de confirmación sin interrupciones.
- [ ] **Pie de página:**
  - [ ] Un contenedor `<footer>` con información legal, enlaces secundarios y un aviso de accesibilidad.
- [ ] **Certificación Oficial W3C:**
  - [ ] Pasa el código completo de tu `reto.html` por el [Nu Html Checker del W3C](https://validator.w3.org/nu/) y asegura un reporte final con **0 errores** de validación.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Cuál es el riesgo técnico de utilizar valores positivos como `tabindex="2"` o `tabindex="5"` en elementos interactivos?
2. Si tienes un botón con texto visible e icono ("Descargar reporte 📥"), ¿qué texto alternativo debe llevar el icono y por qué?
3. ¿Por qué la primera regla de oro de ARIA desaconseja colocar `role="button"` sobre una etiqueta `<div>` en lugar de utilizar un `<button>` nativo?
4. ¿Para qué sirve un *Skip Link* y por qué es una de las primeras pautas exigidas en auditorías de accesibilidad WCAG?
5. ¿Qué diferencia práctica existe entre anunciar un cambio dinámico con `aria-live="polite"` versus `aria-live="assertive"`?

---

## 📚 Recursos y documentación oficial

Para auditar y profundizar en los estándares internacionales de accesibilidad y validación, consulta las siguientes herramientas oficiales:

- 🌐 [Nu Html Checker - Validador Oficial de HTML del W3C](https://validator.w3.org/nu/)
- 📖 [Pautas de accesibilidad web (WCAG 2.2) - W3C WAI](https://www.w3.org/WAI/standards-guidelines/wcag/)
- 📖 [Guía de Accesibilidad en HTML - MDN Web Docs](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Accessibility)
- 📖 [Uso práctico y conceptos básicos de WAI-ARIA - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Accessibility/WAI-ARIA_basics)
- 🛠️ [Extensión axe DevTools para auditorías de accesibilidad en el navegador](https://www.deque.com/axe/devtools/)
- 📖 [Referencia de roles y atributos ARIA - MDN](https://developer.mozilla.org/es/docs/Web/Accessibility/ARIA/Roles)
