# Lección 8: Elementos interactivos y componentes nativos

Esta lección continúa la ruta tras dominar la captura de datos en [Formularios Modernos](../07-formularios-modernos/README.md). Hasta hace pocos años, construir acordeones, modales emergentes o barras de progreso requería decenas de líneas de JavaScript y librerías externas. Hoy en día, **HTML5 ofrece componentes interactivos nativos** integrados directamente en el navegador.

> [!TIP]
> Crea tu archivo `index.html` dentro de la carpeta `08-elementos-interactivos`. La mayoría de estos elementos tienen comportamiento interactivo por defecto sin necesidad de programar JavaScript complejo.

---

## 1. Acordeones y revelación de contenido: `<details>` y `<summary>`

El elemento `<details>` crea un contenedor desplegable de información (*disclosure widget*), y `<summary>` define el título visible que el usuario puede pulsar para abrir o cerrar el bloque.

```text
ESTADO CERRADO (Por defecto):
▶ Preguntas frecuentes sobre envíos

ESTADO ABIERTO (Al hacer clic o con atributo open):
▼ Preguntas frecuentes sobre envíos
  Los envíos nacionales tardan entre 24 y 48 horas hábiles.
  Incluyen número de seguimiento en tiempo real.
```

### Sintaxis básica

```html
<details>
  <summary>¿Cuáles son los métodos de pago aceptados?</summary>
  <p>Aceptamos tarjetas de crédito, débito, transferencias bancarias y PayPal.</p>
</details>

<!-- Con el atributo "open" aparece abierto desde que carga la página -->
<details open>
  <summary>Términos de garantía</summary>
  <p>Todos nuestros productos cuentan con 12 meses de garantía oficial directa.</p>
</details>
```

### Acordeones exclusivos nativos (Agrupación con `name`)

En versiones modernas del estándar HTML, puedes agregar el atributo `name` a múltiples `<details>`. Al abrir uno, los demás que compartan el mismo `name` se cerrarán automáticamente:

```html
<details name="faq">
  <summary>Paso 1: Crear tu cuenta</summary>
  <p>Ingresa tu correo y define una contraseña segura.</p>
</details>

<details name="faq">
  <summary>Paso 2: Confirmar identidad</summary>
  <p>Revisa el enlace de verificación enviado a tu bandeja.</p>
</details>

<details name="faq">
  <summary>Paso 3: Empezar a comprar</summary>
  <p>Explora el catálogo y añade productos a tu carrito.</p>
</details>
```

---

## 2. Ventanas modales nativas con `<dialog>`

El elemento `<dialog>` representa una ventana superpuesta (diálogo, modal emergente o alerta) integrada al navegador con gestión accesible de foco y teclado (se cierra nativamente con la tecla `Escape`).

```html
<!-- Modal nativo en HTML -->
<dialog id="modal-confirmacion">
  <h2>¿Confirmar eliminación?</h2>
  <p>Esta acción no se puede deshacer. Todos los datos asociados se perderán.</p>
  
  <!-- Cerrar modal usando formularios nativos sin JS -->
  <form method="dialog">
    <button value="cancelar">Cancelar</button>
    <button value="confirmar">Sí, eliminar</button>
  </form>
</dialog>

<!-- Botón para abrir el diálogo (controlado con JS mínimo nativo) -->
<button onclick="document.getElementById('modal-confirmacion').showModal()">
  Abrir ventana modal
</button>
```

### Métodos de apertura de `<dialog>`

| Método JS | Tipo de diálogo | Comportamiento |
| --- | --- | --- |
| `elemento.showModal()` | **Modal real** | Bloquea la interacción con el resto de la página, oscurece el fondo con el pseudoelemento `::backdrop` y activa el cierre con `Esc`. |
| `elemento.show()` | **No modal** | Muestra el diálogo como una ventana flotante flotando sobre el contenido, pero permite seguir interactuando con el resto de la web. |

> [!IMPORTANT]
> Para cerrar un diálogo modal sin recurrir a scripts complejos, incluye un `<form method="dialog">`. Cualquier botón pulsado dentro de ese formulario cerrará la ventana automáticamente.

---

## 3. Indicadores de estado: `<progress>` vs. `<meter>`

Aunque ambos muestran una barra visual de valor, tienen propósitos semánticos completamente distintos:

```text
<progress> (Progreso de una tarea):
[=======================>          ] 70% Completado

<meter> (Medición escalar / Indicador de nivel):
[ Óptimo | Regular | Crítico ] -> Nivel actual: 85% de capacidad de disco
```

### Comparativa: ¿Cuándo usar cada uno?

| Elemento | Significado semántico | Ejemplo de uso real |
| --- | --- | --- |
| `<progress>` | Avance de una **tarea en progreso** hacia su finalización. | Subida de archivos, descarga, pasos completados de un asistente. |
| `<meter>` | Medición de un **valor escalar fijo** dentro de un rango conocido. | Uso de memoria RAM, nivel de batería, temperatura, puntaje de examen. |

### Ejemplos prácticos de código

```html
<!-- Progreso de carga conocido -->
<label for="subida">Cargando archivo:</label>
<progress id="subida" max="100" value="65">65%</progress>

<!-- Medidor de almacenamiento con rangos óptimos y críticos -->
<label for="almacenamiento">Espacio en disco:</label>
<meter id="almacenamiento"
       min="0"
       max="100"
       low="30"
       high="80"
       optimum="20"
       value="85">
  85 GB de 100 GB
</meter>
```

> [!NOTE]
> En `<meter>`, los atributos `low`, `high` y `optimum` le indican al navegador qué valores son considerados seguros o de advertencia, adaptando el color del indicador visual en muchos navegadores.

---

## 4. La API nativa de Popovers (`popover` y `popovertarget`)

HTML moderno permite mostrar menús flotantes, tarjetas contextuales y tooltips interactivos **sin una sola línea de JavaScript** mediante el atributo global `popover`:

```html
<!-- Botón detonador vinculado por ID -->
<button popovertarget="tarjeta-ayuda">¿Necesitas ayuda?</button>

<!-- Contenedor flotante -->
<div id="tarjeta-ayuda" popover>
  <h3>Centro de soporte</h3>
  <p>Escríbenos a soporte@ejemplo.com para resolver tus dudas de inmediato.</p>
</div>
```

- Al pulsar el botón, el popover aparece automáticamente en la capa superior (*top-layer*).
- Al pulsar fuera del popover (*light dismiss*) o presionar `Esc`, se cierra solo.

---

## 5. Plantillas reutilizables con `<template>`

El elemento `<template>` almacena fragmentos de código HTML que **no se muestran en pantalla** cuando la página carga. Su contenido se mantiene invisible hasta que JavaScript lo clona e inserta en el documento dinámicamente.

```html
<!-- Estructura base para generar tarjetas de producto dinámicas -->
<template id="plantilla-producto">
  <article class="tarjeta-producto">
    <h3 class="producto-nombre"></h3>
    <p class="producto-precio"></p>
    <button type="button">Añadir al carrito</button>
  </article>
</template>
```

> [!WARNING]
> Todo lo que pongas dentro de `<template>` (imágenes, scripts, estilos) no se descarga ni se ejecuta hasta que sea instanciado en el DOM con JavaScript. Es ideal para optimizar el rendimiento.

---

## Reto final de la lección

Construye un **Panel de Control de Usuario Interactivo** dentro de tu `index.html` que integre todos los componentes nativos aprendidos y cumpla los siguientes requerimientos:

- [ ] Un encabezado `<h1>` con el título del panel.
- [ ] Una sección de **Estado del Sistema**:
  - Un elemento `<progress>` que represente la sincronización de datos en la nube (ej. 45%).
  - Un elemento `<meter>` que indique el uso de almacenamiento con rangos definidos (`min`, `max`, `low`, `high`, `optimum`, `value`).
- [ ] Una sección de **Preguntas Frecuentes (FAQ)**:
  - Al menos 3 elementos `<details>` agrupados con el mismo atributo `name="ayuda"`, de modo que solo uno pueda estar abierto a la vez.
  - Cada uno con su respectivo `<summary>` y contenido explicativo dentro.
- [ ] Un elemento `<dialog>` para **Editar Perfil**:
  - Título secundario `<h2>` y un formulario interno con `method="dialog"`.
  - Dos campos básicos (`<input>` con sus respectivos `<label>`).
  - Un botón para cancelar y otro para guardar cambios que cierren el modal de forma nativa.
- [ ] Un `<button>` fuera del modal que dispare la apertura mediante el método `.showModal()`.
- [ ] Un botón con `popovertarget` que abra una tarjeta informativa con el atributo `popover`.

### Preguntas de autoevaluación

1. ¿Por qué es semánticamente incorrecto utilizar una barra `<progress>` para mostrar el nivel de batería restante de un dispositivo?
2. ¿Qué ventaja ofrece el atributo `name` compartido en los elementos `<details>` en el HTML moderno?
3. ¿Cuál es la diferencia entre abrir un `<dialog>` con `.show()` y abrirlo con `.showModal()`?
4. ¿Qué sucede con los elementos dentro de una etiqueta `<template>` cuando el navegador carga el documento por primera vez?

---

## 📚 Recursos y documentación oficial

Para profundizar en la implementación de interactividad nativa en HTML, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Elemento `<details>`: Componente desplegable - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/details)
- 📖 [Elemento `<dialog>`: Ventanas de diálogo modales - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/dialog)
- 📖 [Elemento `<progress>` vs. `<meter>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/meter)
- 📖 [Guía de la Popover API en HTML - MDN](https://developer.mozilla.org/es/docs/Web/API/Popover_API)
