# Lección 8: Elementos interactivos y componentes nativos

Esta lección continúa la ruta tras dominar la captura de datos en [Formularios Modernos](../07-formularios-modernos/README.md). Hasta hace poco tiempo, construir acordeones, modales emergentes o menús flotantes requería decenas de líneas de JavaScript y librerías externas pesadas. Hoy en día, **HTML ofrece componentes interactivos nativos** con comportamientos accesibles integrados directamente en el navegador.

---

## 1. Acordeones y revelación de contenido: `<details>` y `<summary>`

El elemento `<details>` crea un contenedor desplegable de información (*disclosure widget*), y `<summary>` define el encabezado interactivo que el usuario pulsa para abrir o cerrar el bloque.

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
<!-- Desplegable cerrado por defecto -->
<details>
  <summary>¿Cuáles son los métodos de pago aceptados?</summary>
  <p>Aceptamos tarjetas de crédito, débito, transferencias bancarias y PayPal.</p>
</details>

<!-- Con el atributo "open" aparece desplegado desde que carga la página -->
<details open>
  <summary>Términos de garantía oficial</summary>
  <p>Todos nuestros productos cuentan con 12 meses de garantía directa de fábrica.</p>
</details>
```

### Acordeones exclusivos nativos (Agrupación con `name`)

El estándar HTML permite agrupar varios `<details>` compartiendo el mismo atributo `name`. Al abrir uno, **todos los demás del mismo grupo se cierran automáticamente**, creando un acordeón perfecto sin una sola línea de JavaScript:

```html
<details name="faq-compra">
  <summary>Paso 1: Crear tu cuenta</summary>
  <p>Ingresa tu correo y define una contraseña segura.</p>
</details>

<details name="faq-compra">
  <summary>Paso 2: Confirmar identidad</summary>
  <p>Revisa el enlace de verificación enviado a tu bandeja de entrada.</p>
</details>

<details name="faq-compra">
  <summary>Paso 3: Empezar a comprar</summary>
  <p>Explora el catálogo y añade productos a tu carrito.</p>
</details>
```

### Qué observar en `details` y `summary`

- **Accesibilidad y teclado nativo:** No necesitas programar eventos de clic; el usuario puede navegar hasta el `<summary>` con la tecla `Tab` y abrirlo/cerrarlo pulsando `Enter` o `Espacio`.
- **El triángulo indicador:** El navegador dibuja automáticamente una flecha giratoria usando el pseudoelemento `::marker`. Si se desea ocultar o personalizar con CSS, se estiliza sobre ese marcador.
- **Contenido polivalente:** Dentro de `<details>` puedes colocar párrafos, listas, imágenes e incluso formularios completos.

### Práctica 1: Acordeones exclusivos (en `index.html`)

1. Crea tu archivo `index.html` con la estructura base de HTML5.
2. Construye un grupo de tres elementos `<details>` para preguntas frecuentes que compartan el atributo `name="soporte"`.
3. Abre tu navegador, haz clic en cada uno y comprueba cómo el navegador cierra automáticamente el anterior al abrir uno nuevo.

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

<!-- Botón para abrir el diálogo (disparado con una sola línea nativa) -->
<button type="button" onclick="document.getElementById('modal-confirmacion').showModal()">
  Abrir ventana modal
</button>
```

### Métodos de apertura de `<dialog>`

| Método JS nativo | Tipo de ventana | Comportamiento |
| --- | --- | --- |
| `dialog.showModal()` | **Modal real** | Bloquea la interacción con el resto de la página, oscurece el fondo con el pseudoelemento `::backdrop`, atrapa el foco del teclado y activa el cierre automático con la tecla `Escape`. |
| `dialog.show()` | **No modal (Flotante)** | Muestra el diálogo como una ventana flotante sobre el contenido, pero permite seguir interactuando y haciendo clic en el resto de la página. |

> [!IMPORTANT]
> **Cierre sin JavaScript:**  
> Para cerrar un diálogo modal sin escribir scripts complejos, incluye dentro un `<form method="dialog">`. Cualquier botón pulsado dentro de ese formulario cerrará la ventana automáticamente y registrará el `value` del botón pulsado en la propiedad `dialog.returnValue`.

### Qué observar en `<dialog>`

- **Capa superior (*Top Layer*):** Al abrirse con `.showModal()`, el diálogo se renderiza en una capa especial del navegador que se coloca por encima de absolutamente todo el contenido, sin importar qué valores de `z-index` tengan tus otros elementos en CSS.
- **Fondo oscurecido (`::backdrop`):** El navegador genera un telón de fondo detrás del modal que puedes personalizar con CSS (por ejemplo, aplicando un desenfoque o color semitransparente).
- **El clic en el fondo oscuro no lo cierra:** A diferencia de los menús flotantes, hacer clic sobre el fondo oscuro (`::backdrop`) **no cierra el modal de forma predeterminada**. El estándar lo diseñó así intencionalmente para evitar que el usuario pierda datos de un formulario por un clic accidental fuera de la ventana. Solo se cerrará presionando `Escape` o pulsando un botón interno.

### Práctica 2: Modales con cierre por teclado (en `index.html`)

1. En tu `index.html`, agrega una ventana `<dialog>` con un formulario interno `<form method="dialog">`.
2. Coloca un botón fuera del diálogo que ejecute `.showModal()`.
3. Abre el modal en el navegador y comprueba dos formas nativas de cerrarlo: pulsando el botón interno y presionando la tecla `Escape` de tu teclado físico.

---

## 3. Indicadores de estado: `<progress>` vs. `<meter>`

Aunque visualmente ambos muestran una barra de valor, tienen propósitos semánticos completamente distintos que no deben confundirse:

```text
<progress> (Progreso dinámico hacia una meta):
[=======================>          ] 70% Completado

<meter> (Medición estática / Nivel en escala fija):
[ Óptimo | Advertencia | Peligro ] -> Nivel actual: 85% de capacidad de disco
```

### Comparativa semántica

| Elemento | Propósito | Ejemplo de uso real |
| --- | --- | --- |
| `<progress>` | Avance de una **tarea en proceso** que tiene un final. | Subida de archivos, descarga, porcentaje completado de un curso. |
| `<meter>` | Medición de un **valor escalar puntual** dentro de un rango conocido. | Uso de memoria RAM, nivel de batería, temperatura, velocidad, puntaje. |

### Ejemplos prácticos de código

```html
<!-- 1. Progreso conocido (determinado): 65 de 100 completado -->
<label for="subida">Cargando archivo al servidor:</label>
<progress id="subida" max="100" value="65">65%</progress>

<!-- 2. Progreso desconocido (indeterminado): animación continua nativa -->
<label for="conexion">Conectando con la base de datos...</label>
<progress id="conexion"></progress>

<!-- 3. Medidor escalar con umbrales calculados -->
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
> En `<meter>`, los atributos `low`, `high` y `optimum` le enseñan al navegador qué zonas son seguras y cuáles peligrosas. Si `value` supera el valor de `high`, muchos navegadores cambian el color de la barra automáticamente de verde a amarillo o rojo.

### Qué observar en `<progress>` y `<meter>`

- **Animación indeterminada:** Al omitir el atributo `value` en `<progress>` (`<progress></progress>`), el navegador activa automáticamente una animación de vaivén continuo sin necesidad de escribir CSS. Es ideal para estados de carga donde aún no conoces el porcentaje exacto.
- **Texto interno de respaldo:** El texto dentro de las etiquetas (`65%` o `85 GB`) es el respaldo que leerán navegadores antiguos o lectores de pantalla que no interpreten el elemento gráfico.

### Práctica 3: Comparando mediciones (en `index.html`)

1. Añade a tu `index.html` una barra `<progress>` con `max="100"` y `value="40"`.
2. Justo debajo, coloca un `<progress>` sin atributo `value` para observar la animación nativa de carga.
3. Añade un `<meter>` con `min="0"`, `max="100"`, `low="25"`, `high="75"` y `optimum="10"`. Asigna a `value` un valor de `90` y observa cómo cambia de color al entrar en zona crítica.

---

## 4. Menús y tarjetas flotantes con la Popover API

HTML moderno permite mostrar menús emergentes, tarjetas de información y tooltips flotantes **sin escribir código JavaScript ni manipular `z-index`**, utilizando el atributo global `popover`:

```html
<!-- Botón detonador vinculado por ID -->
<button type="button" popovertarget="tarjeta-ayuda">¿Necesitas ayuda?</button>

<!-- Contenedor flotante -->
<div id="tarjeta-ayuda" popover>
  <h3>Centro de Asistencia</h3>
  <p>Escríbenos a soporte@ejemplo.com para resolver cualquier duda.</p>
  
  <!-- Botón interno para cerrar el popover de forma nativa sin JS -->
  <button type="button" popovertarget="tarjeta-ayuda" popovertargetaction="hide">Cerrar ✕</button>
</div>
```

### Control de acciones con `popovertargetaction`

Cuando conectas un botón a un popover mediante `popovertarget`, puedes definir qué acción exacta ejecutará mediante `popovertargetaction`:

- `toggle` (Por defecto): Si está cerrado lo abre; si está abierto lo cierra.
- `show`: Solo abre el popover.
- `hide`: Solo cierra el popover (ideal para crear botones de "Cerrar" o íconos de "X" dentro del menú).

### Tipos de comportamiento del popover

- **`popover="auto"` (Por defecto):** Al hacer clic fuera del popover (*light dismiss*) o presionar la tecla `Escape`, se cierra automáticamente. Además, abrir un popover nuevo cerrará cualquier otro popover abierto en pantalla.
- **`popover="manual"`:** No se cierra al hacer clic fuera; requiere un botón explícito con `popovertargetaction="hide"` para cerrarse.

### ¿Cuál es la diferencia entre `<dialog>` y `popover`?

| Característica | Elemento `<dialog>` | Atributo `popover` |
| --- | --- | --- |
| **Finalidad** | Modales críticos que requieren confirmación o captura de datos. | Elementos contextuales flotantes: tooltips, menús, notificaciones. |
| **Bloqueo del fondo** | Sí (con `.showModal()` bloquea toda interacción externa). | No (el usuario puede interactuar con el resto de la página). |
| **Atrapamiento de foco** | Obliga al teclado a permanecer dentro del diálogo. | No atrapa el foco del teclado; es ligero y no invasivo. |
| **Cierre al clic exterior** | No se cierra al hacer clic afuera (requiere `Esc` o botón). | Sí se cierra automáticamente con un clic exterior (*light dismiss*). |

### Práctica 4: Notificación flotante nativa (en `index.html`)

1. En tu `index.html`, crea un `<div>` con el atributo `popover` que contenga un mensaje breve y un botón de cierre interno con `popovertargetaction="hide"`.
2. Crea un `<button>` externo con `popovertarget` enlazado al `id` de tu popover.
3. Pruébalo en el navegador: ábrelo, ciérralo pulsando el botón interno y vuelve a abrirlo para cerrarlo haciendo clic en cualquier parte fuera de la tarjeta (*light dismiss*).

---

## 5. Plantillas reutilizables con `<template>`

El elemento `<template>` almacena fragmentos de código HTML que **no se renderizan en pantalla** cuando la página carga. Su contenido permanece completamente inactivo hasta que un script de JavaScript lo clona e inserta en el documento dinámicamente.

```html
<!-- Estructura base para generar tarjetas de usuario dinámicas -->
<template id="plantilla-tarjeta">
  <article class="tarjeta-usuario">
    <h3 class="nombre-usuario">Nombre por defecto</h3>
    <p class="rol-usuario">Rol no definido</p>
    <button type="button">Ver perfil completo</button>
  </article>
</template>
```

> [!WARNING]
> Todo lo que pongas dentro de un `<template>` (imágenes con `src`, videos, scripts) **no se descarga ni se ejecuta** durante la carga inicial de la página. El navegador solo analiza su sintaxis y lo guarda en memoria, lo que lo convierte en una excelente herramienta de optimización de rendimiento.

### Qué observar en `<template>`

- Si inspeccionas la página con las herramientas de desarrollador (F12), verás que el contenido de `<template>` vive dentro de un contenedor especial llamado `#document-fragment`.
- No afecta el diseño, no ocupa espacio visual ni compite con el CSS de la página hasta que es clonado en el DOM.

### Práctica 5: El contenedor inerte (en `index.html`)

1. Añade el bloque `<template>` del ejemplo a tu `index.html`.
2. Guarda el archivo y abre la página en tu navegador: comprueba que en la pantalla no aparece absolutamente nada.
3. Abre el inspector de elementos (F12) y comprueba cómo el navegador tiene el código almacenado silenciosamente en memoria dentro de la etiqueta `<template>`.

---

## Reto final de la lección: Panel de Diagnóstico y Cuenta de Usuario

Ahora que probaste cada componente interactivo en tu laboratorio (`index.html`), demostrarás tu autonomía resolviendo un proyecto completo y desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `08-elementos-interactivos`. Construirás un **Panel de Estado y Configuración de Cuenta de Usuario** que cumpla con todos los puntos de la siguiente lista de control:

- [ ] Estructura base completa de HTML5 (`<!DOCTYPE html>`, `<html>`, `<head>` con metadatos y `<body>`).
- [ ] Un encabezado principal `<h1>Panel de Control del Sistema</h1>`.
- [ ] **Sección de Estado y Métricas:**
  - [ ] Un elemento `<progress>` con `max` y `value` que represente el porcentaje de sincronización de datos con la nube.
  - [ ] Un elemento `<progress>` indeterminado (sin `value`) que indique que hay una verificación en curso.
  - [ ] Un elemento `<meter>` que indique el consumo de almacenamiento en disco, configurando sus umbrales (`min`, `max`, `low`, `high`, `optimum`, `value`).
  - [ ] Cada indicador debe contar con su respectivo `<label>` o texto accesible explicativo.
- [ ] **Sección de Centro de Ayuda (FAQ):**
  - [ ] Al menos tres elementos `<details>` agrupados con el **mismo atributo `name="centro-ayuda"`** para que funcionen como un acordeón exclusivo nativo.
  - [ ] Cada bloque debe tener su respectivo `<summary>` descriptivo y contenido detallado dentro.
- [ ] **Sección de Notificaciones:**
  - [ ] Un botón con `popovertarget` que active un menú o tarjeta flotante con el atributo `popover`.
  - [ ] El popover debe incluir una lista breve de avisos y un botón de cierre interno con `popovertargetaction="hide"`.
- [ ] **Gestión de Seguridad con Modal:**
  - [ ] Un elemento `<dialog id="modal-seguridad">` con un encabezado secundario `<h2>Actualizar Contraseña</h2>`.
  - [ ] Un formulario interno con `method="dialog"` que contenga:
    - Dos campos de entrada (`<input type="password">`) vinculados a sus respectivos `<label>`.
    - Un botón para cancelar (`value="cancelar"`) y otro para guardar cambios (`value="guardar"`).
  - [ ] Un botón exterior accesible que abra el modal ejecutando `.showModal()`.
- [ ] **Plantilla inerte:**
  - [ ] Un bloque `<template>` al final del documento que almacene la estructura HTML de una tarjeta de alerta para ser clonada dinámicamente.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Por qué es semánticamente incorrecto utilizar una barra `<progress>` para mostrar el nivel de batería restante de una computadora portatil?
2. ¿Qué ventaja técnica aporta el atributo compartido `name` en los elementos `<details>` en el estándar HTML actual?
3. ¿Cuál es la diferencia fundamental de comportamiento entre hacer clic fuera de un `popover` versus hacer clic fuera de un `<dialog>` modal?
4. ¿Para qué sirve el atributo `popovertargetaction="hide"` en un botón dentro de un menú emergente?
5. ¿Qué sucede con las imágenes o scripts que colocas dentro de una etiqueta `<template>` cuando el navegador carga la página por primera vez?

---

## 📚 Recursos y documentación oficial

Para profundizar en los componentes interactivos nativos y estándares web modernos, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Elemento `<details>`: Componente desplegable interactivo - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/details)
- 📖 [Elemento `<dialog>`: Ventanas de diálogo modales - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/dialog)
- 📖 [Elemento `<meter>`: Indicador de rango escalar - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/meter)
- 📖 [Elemento `<progress>`: Indicador de avance de tarea - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/progress)
- 📖 [Guía completa de la Popover API en HTML - MDN](https://developer.mozilla.org/es/docs/Web/API/Popover_API)
- 📖 [Elemento `<template>`: Plantilla de contenido HTML - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/template)
