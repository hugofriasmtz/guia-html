# Lección 10: Accesibilidad web (A11y), ARIA y validación de código

Esta lección continúa la ruta tras dominar la configuración del documento en [Metadatos e Integración](../09-metadatos-e-integracion/README.md). La web fue concebida para ser universal: cualquier persona, independientemente de sus capacidades físicas, sensoriales, cognitivas o del dispositivo que utilice, debe poder percibir, entender, navegar e interactuar con tu sitio.

En esta lección aprenderás los estándares de **accesibilidad web (a11y)**, el uso responsable de atributos **WAI-ARIA**, las técnicas de navegación por teclado y cómo validar que tu código cumpla con los estándares oficiales del **W3C**.

> [!TIP]
> Desconecta tu ratón por unos minutos. Abre el archivo `index.html` de esta lección e intenta navegar por toda tu página utilizando únicamente las teclas `Tab`, `Shift + Tab`, `Enter`, `Espacio` y las flechas de dirección. Si no puedes acceder o activar algún elemento, existe un problema de accesibilidad.

---

## 1. Modelo mental: El Árbol de Accesibilidad

Los navegadores no solo crean el DOM (árbol de elementos visuales) para pintar la pantalla; en paralelo generan el **Árbol de Accesibilidad** (*Accessibility Tree*), que es la estructura que leen los lectores de pantalla (como NVDA en Windows, VoiceOver en macOS/iOS o TalkBack en Android):

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
                                          | (La imagen decorativa es ignorada)        |
                                          +-------------------------------------------+
```

### Los 4 Principios Fundamentales de WCAG (POUR)

Las pautas de accesibilidad (*Web Content Accessibility Guidelines*) se basan en cuatro pilares:

1. **Perceptible:** La información no puede ser invisible a todos los sentidos del usuario (debe haber alternativas de texto para audio/imágenes y buen contraste de color).
2. **Operable:** La interfaz debe ser navegable al 100% mediante teclado y dar tiempo suficiente para interactuar.
3. **Comprensible:** Los textos deben ser legibles, los formularios predecibles y los errores deben explicarse con claridad.
4. **Robusto:** El código debe ser compatible con la mayor variedad de navegadores y tecnologías de asistencia.

---

## 2. La Primera Regla de ARIA

WAI-ARIA (*Accessible Rich Internet Applications*) es una especificación que agrega atributos especiales para comunicar roles, estados y propiedades a las tecnologías de asistencia cuando el HTML nativo no es suficiente.

> [!IMPORTANT]
> **Primera Regla de ARIA:** *"Si puedes usar un elemento o atributo nativo de HTML5 con la semántica y comportamiento que necesitas, **NO uses ARIA**; usa el elemento nativo."*

```html
<!-- ❌ INCORRECTO: Reinventar la rueda con ARIA sobre elementos neutros -->
<div role="button" tabindex="0" onclick="enviarFormulario()">Enviar</div>

<!--  CORRECTO: Usar el elemento nativo de HTML5 -->
<button type="submit">Enviar</button>
```

---

## 3. Atributos ARIA indispensables

Cuando construyes interfaces dinámicas o componentes avanzados, estos son los atributos ARIA más utilizados:

| Atributo / Rol | Propósito | Ejemplo de uso |
| --- | --- | --- |
| `aria-label` | Asigna una etiqueta de texto invisible para lectores a un elemento sin texto visual. | `<button aria-label="Cerrar menú">✕</button>` |
| `aria-labelledby` | Vincula el nombre accesible de un elemento al `id` de otro texto visible en pantalla. | `<section aria-labelledby="titulo-seccion">` |
| `aria-describedby` | Asocia una descripción secundaria o mensaje de ayuda/error al campo. | `<input aria-describedby="ayuda-password">` |
| `aria-hidden="true"` | Oculta elementos puramente decorativos o duplicados al lector de pantalla. | `<span aria-hidden="true">🚀</span>` |
| `aria-expanded` | Comunica si un menú desplegable, acordeón o modal está abierto (`true`) o cerrado (`false`). | `<button aria-expanded="false">Menú</button>` |
| `aria-live="polite"` | Le avisa al lector de pantalla que lea en voz alta cualquier cambio dinámico sin interrumpir. | `<div aria-live="polite" id="alerta-carrito"></div>` |

---

## 4. Navegación por teclado y gestión de foco (`tabindex`)

El orden natural de foco por teclado sigue la secuencia exacta en la que los elementos interactivos están escritos en el código HTML.

```text
FLUJO DE TABULACIÓN NATURAL:
[ Enlace 1 ] ----(Tab)----> [ Enlace 2 ] ----(Tab)----> [ Input Texto ] ----(Tab)----> [ Botón Enviar ]
```

### Control del foco con el atributo `tabindex`

```html
<!-- tabindex="0": Permite que un elemento no interactivo reciba foco en el orden natural -->
<div tabindex="0" class="tarjeta-interactiva">Elemento enfocable</div>

<!-- tabindex="-1": El elemento NO recibe foco con la tecla Tab, pero SÍ puede recibirlo por JavaScript -->
<dialog id="modal" tabindex="-1">...</dialog>
```

> [!WARNING]
> **Nunca utilices valores positivos (`tabindex="1"`, `tabindex="2"`, etc.)**. Alterar artificialmente el orden natural de tabulación desorienta por completo a los usuarios de lectores de pantalla y crea inconsistencias graves de navegación.

### Enlaces de salto al contenido principal (*Skip Links*)

Los usuarios que solo usan teclado agradecen no tener que presionar `Tab` 50 veces a través de toda la barra de navegación para llegar al artículo principal:

```html
<body>
  <!-- Enlace oculto visualmente que se hace visible al recibir foco con Tab -->
  <a href="#contenido-principal" class="skip-link">Saltar al contenido principal</a>

  <header>
    <nav>
      <!-- Menú extenso de navegación -->
    </nav>
  </header>

  <main id="contenido-principal">
    <h1>Título del artículo</h1>
    <!-- Contenido real -->
  </main>
</body>
```

---

## 5. Accesibilidad en imágenes y multimedia

El texto alternativo (`alt`) en las imágenes no es opcional, pero su contenido depende de la función de la imagen:

```html
<!-- 1. Imagen informativa: Describe el contenido relevante -->
<img src="grafico-ventas-2025.png" alt="Gráfico de barras que muestra un incremento del 25% en las ventas de 2025.">

<!-- 2. Imagen decorativa: alt vacío para que el lector de pantalla la ignore por completo -->
<img src="separador-ondas-adorno.svg" alt="" role="presentation">

<!-- 3. Imagen dentro de un botón interactivo: Describe la ACCIÓN, no la imagen -->
<button>
  <img src="lupa.svg" alt="">
  Buscar
</button>
```

> [!NOTE]
> Si omites el atributo `alt` por completo (`<img src="foto.jpg">`), el lector de pantalla se verá forzado a leer la URL completa del archivo (`"f-o-t-o-punto-j-p-g"`), generando una pésima experiencia. Si la imagen es puramente decorativa, escribe `alt=""` (con las comillas vacías).

---

## 6. Validación de código con el estándar W3C

Un código HTML libre de errores sintácticos garantiza que los navegadores interpreten el árbol del documento de forma predecible y sin comportamientos inesperados.

### Errores comunes que rompen la validación

- Etiquetas que quedaron abiertas o mal anidadas (ej. `<p>Texto <strong>aquí</p></strong>`).
- Atributos `id` duplicados en un mismo documento.
- Etiquetas interactivas anidadas dentro de otras etiquetas interactivas (ej. un `<button>` dentro de un `<a>`).
- Elementos obligatorios faltantes (como olvidar `alt` en un `<img>` o `title` en un `<iframe>`).

---

## Reto final de la lección

Crea un archivo `index.html` para un **Portal de Noticias Accesible** que resuelva todas las siguientes directrices de accesibilidad y validación:

- [ ] Incluye un enlace de salto al contenido principal (*Skip Link*) al inicio de `<body>` que apunte al `id` del `<main>`.
- [ ] Construye una cabecera con navegación semántica (`<header>`, `<nav>`) y enlaces claros.
- [ ] Crea un botón interactivo de "Modo Oscuro" que utilice únicamente un icono gráfico, pero cuente con su respectivo `aria-label="Cambiar a modo oscuro"`.
- [ ] Un elemento de búsqueda con su `<label>` asociado correctamente mediante `for` e `id`, o mediante `aria-label`.
- [ ] Un artículo principal (`<article>`) que contenga:
  - Una imagen informativa con su descripción contextual en `alt`.
  - Un icono puramente decorativo con `alt=""` y `aria-hidden="true"`.
  - Un bloque de texto con marcado semántico.
- [ ] Una sección de comentarios con un contenedor dinámico configurado con `aria-live="polite"` para futuros mensajes del sistema.
- [ ] Un pie de página (`<footer>`) con información legal y enlaces de contacto.
- [ ] **Validación obligatoria:** Pasa el código completo de tu archivo por el [Nu Html Checker del W3C](https://validator.w3.org/nu/) y asegúrate de obtener **0 errores** de validación.

### Preguntas de autoevaluación

1. ¿Cuál es el riesgo de usar `tabindex="3"` o cualquier número entero positivo en un elemento de tu página?
2. Si tienes un icono decorativo que acompaña al texto de un botón ("Descargar archivo 📥"), ¿qué texto alternativo debes ponerle al icono y por qué?
3. ¿Por qué la regla de oro de ARIA desaconseja colocar `role="button"` sobre una etiqueta `<div>` en lugar de usar `<button>`?
4. ¿Qué función cumple la técnica del *Skip Link* y para qué tipo de usuarios es de vital importancia?

---

## 📚 Recursos y documentación oficial

Para auditar y profundizar en los estándares internacionales de accesibilidad, consulta las siguientes herramientas y guías:

- 🌐 [Nu Html Checker - Validador Oficial de HTML del W3C](https://validator.w3.org/nu/)
- 📖 [Pautas de accesibilidad web (WCAG) - W3C Web Accessibility Initiative](https://www.w3.org/WAI/standards-guidelines/wcag/)
- 📖 [Guía de Accesibilidad en HTML - MDN Web Docs](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Accessibility)
- 📖 [Uso práctico de WAI-ARIA - MDN Web Docs](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Accessibility/WAI-ARIA_basics)
- 🛠️ [Extensión axe DevTools para auditorías de accesibilidad en el navegador](https://www.deque.com/axe/devtools/)
