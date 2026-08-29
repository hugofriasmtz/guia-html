# Lección 7: Formularios modernos y validación nativa

Esta lección continúa la ruta de aprendizaje tras dominar las tablas en [Tablas de Datos](../06-tablas-de-datos/README.md). Ahora aprenderás a construir el mecanismo principal de interactividad y captura de datos en la web: los **formularios**.

> [!TIP]
> Crea o reutiliza un archivo `index.html` dentro de tu carpeta `07-formularios-modernos`. Abre tu servidor local (o el navegador) para probar cómo interactúan los controles y cómo responde la validación nativa del navegador.

---

## 1. Modelo mental: Anatomía del envío de datos

Un formulario no es solo un conjunto de cajas de texto visuales; es un **canal de comunicación estructurado** entre el usuario y un servidor o script de procesamiento:

```html
+-----------------------------------------------------------------------+
|  <form action="/procesar" method="POST">                              |
|                                                                       |
|   [ label ]  [ Input: name="correo" value="ana@mail.com" ]            |
|   [ label ]  [ Input: name="edad"   value="24"           ]            |
|                                                                       |
|   [ Botón Submit: type="submit" ]                                     |
+-----------------------------------------------------------------------+
                                  |
                                  | Envía pares: clave=valor
                                  v
              Servidor / Backend: { correo: "ana@mail.com", edad: "24" }
```

### La etiqueta contenedora `<form>`

Toda captura de datos debe encapsularse dentro de `<form>`, configurando sus atributos de envío:

- **`action`**: La URL o endpoint donde se enviarán los datos procesados.
- **`method`**: El método HTTP de envío:
  - `GET`: Envía los datos visibles en la barra de direcciones (`/buscar?q=html5`). Ideal para búsquedas y filtros; nunca para contraseñas o datos sensibles.
  - `POST`: Envía los datos empaquetados en el cuerpo de la petición HTTP. Seguro para contraseñas, pagos y modificación de bases de datos.
- **`enctype`**: Solo requerido cuando envías archivos adjuntos (`multipart/form-data`).

> [!IMPORTANT]
> Todo campo que deba viajar al servidor **debe tener el atributo `name`**. Si un `<input>` no tiene `name`, el navegador lo ignorará por completo al enviar el formulario.

---

## 2. Accesibilidad: Vinculación con `label` y agrupación con `fieldset`

Para que un formulario sea accesible a lectores de pantalla y fácil de pulsar en pantallas táctiles, jamás dejes un control sin su etiqueta descriptiva `<label>`.

### Vinculación explícita (Recomendada)

Se asocia el atributo `for` del `<label>` con el `id` del `<input>`:

```html
<label for="nombre-usuario">Nombre completo:</label>
<input type="text" id="nombre-usuario" name="nombre_usuario">
```

### Agrupación temática con `fieldset` y `legend`

Permite agrupar controles relacionados lógica y visualmente:

```html
<fieldset>
  <legend>Información de Envío</legend>

  <label for="direccion">Calle y número:</label>
  <input type="text" id="direccion" name="direccion">

  <label for="cp">Código Postal:</label>
  <input type="text" id="cp" name="cp">
</fieldset>
```

---

## 3. Tipos de entrada modernos (`<input type="...">`)

HTML5 introdujo tipos de entrada especializados que activan teclados adaptados en dispositivos móviles (números, `@`, `.com`) y validaciones automáticas:

| `type` | Uso específico | Comportamiento del navegador / Móvil |
| --- | --- | --- |
| `text` | Texto libre de una sola línea | Teclado estándar genérico. |
| `email` | Direcciones de correo electrónico | Valida formato `@` y muestra teclado con `@` y `.`. |
| `password` | Contraseñas y claves | Oculta los caracteres con puntos o asteriscos. |
| `tel` | Números de teléfono | Abre teclado numérico telefónico en móviles. |
| `url` | Enlaces web absolutos | Valida protocolo (`http://`, `https://`) y ofrece `.com`. |
| `number` | Valores numéricos | Habilita flechas de incremento y teclado numérico. |
| `range` | Selección en escala (deslizador/slider) | Renderiza una barra deslizable de valores relativos. |
| `date` / `time` | Fechas y horas | Abre selectores nativos de calendario y reloj. |
| `color` | Selector de color | Abre la paleta de colores del sistema operativo. |
| `file` | Subida de archivos del usuario | Abre el explorador de archivos local. |
| `checkbox` | Selección booleana o múltiple independiente | Casilla de verificación (marcado/desmarcado). |
| `radio` | Selección única y excluyente de una lista | Círculo seleccionable; comparten el mismo `name`. |
| `hidden` | Datos ocultos al usuario pero enviados al backend | No se renderiza en la pantalla (tokens, IDs de sesión). |

### Ejemplo de entradas modernas en acción

```html
<!-- Selección excluyente con Radio Buttons (comparten el mismo name) -->
<fieldset>
  <legend>Plan de suscripción</legend>
  
  <input type="radio" id="plan-mensual" name="plan" value="mensual" checked>
  <label for="plan-mensual">Mensual ($10/mes)</label>

  <input type="radio" id="plan-anual" name="plan" value="anual">
  <label for="plan-anual">Anual ($100/año)</label>
</fieldset>

<!-- Selección múltiple independiente con Checkbox -->
<label>
  <input type="checkbox" name="terminos" value="aceptados" required>
  Acepto los términos y condiciones del servicio
</label>
```

---

## 4. Controles multilínea, listas y autocompletado

### Texto multilínea con `<textarea>`

A diferencia de `<input>`, `<textarea>` requiere etiqueta de cierre obligatoria:

```html
<label for="comentarios">Comentarios adicionales:</label>
<textarea id="comentarios" name="comentarios" rows="4" cols="50" placeholder="Escribe aquí tu mensaje..."></textarea>
```

### Menú desplegable con `<select>`, `<optgroup>` y `<option>`

```html
<label for="pais">Selecciona tu país:</label>
<select id="pais" name="pais">
  <option value="" disabled selected>-- Elige una opción --</option>
  <optgroup label="América del Norte">
    <option value="mx">México</option>
    <option value="ca">Canadá</option>
  </optgroup>
  <optgroup label="América del Sur">
    <option value="co">Colombia</option>
    <option value="ar">Argentina</option>
  </optgroup>
</select>
```

### Sugerencias dinámicas con `<datalist>`

Permite al usuario escribir texto libre pero ofreciendo una lista precargada de sugerencias automáticas:

```html
<label for="navegador">Tu navegador favorito:</label>
<input type="text" id="navegador" name="navegador" list="lista-navegadores" placeholder="Escribe o elige...">

<datalist id="lista-navegadores">
  <option value="Mozilla Firefox"></option>
  <option value="Google Chrome"></option>
  <option value="Apple Safari"></option>
  <option value="Microsoft Edge"></option>
  <option value="Brave"></option>
</datalist>
```

---

## 5. Validación nativa y atributos de restricción

HTML5 permite validar datos **en el cliente sin necesidad de JavaScript** usando atributos nativos:

| Atributo | Propósito | Ejemplo |
| --- | --- | --- |
| `required` | Campo obligatorio para permitir el envío. | `<input type="text" required>` |
| `placeholder` | Texto de ayuda temporal antes de escribir. | `placeholder="ej. ana@empresa.com"` |
| `minlength` / `maxlength` | Límites de caracteres en campos de texto. | `minlength="8" maxlength="20"` |
| `min` / `max` | Valores mínimo y máximo para números/fechas. | `min="18" max="99"` |
| `step` | Intervalo de salto para campos numéricos. | `step="0.5"` o `step="10"` |
| `pattern` | Expresión regular (Regex) personalizada. | `pattern="[A-Z]{3}[0-9]{4}"` |
| `autocomplete` | Asiste al gestor de contraseñas y autocompletado del navegador. | `autocomplete="current-password"` |
| `readonly` | Solo lectura (el usuario no edita, pero el dato se envía). | `readonly` |
| `disabled` | Deshabilita el control (el dato **NO** se envía al servidor). | `disabled` |

> [!WARNING]
> Nunca uses `placeholder` como sustituto de un `<label>`. El placeholder desaparece en cuanto el usuario comienza a escribir, lo que genera confusión y arruina la accesibilidad.

---

## 6. Botones y envío de formularios

Para detonar acciones dentro de un formulario, la etiqueta recomendada es `<button>`:

```html
<!-- Envía el formulario procesando validaciones -->
<button type="submit">Crear cuenta</button>

<!-- Restablece todos los campos a su valor inicial -->
<button type="reset">Limpiar campos</button>

<!-- Botón neutro para ser controlado posteriormente con JavaScript -->
<button type="button">Ver términos</button>
```

> [!NOTE]
> Todo `<button>` dentro de un `<form>` tiene `type="submit"` por defecto si no le defines un tipo explícito. Especifica siempre `type="button"` si no deseas que dispare el envío.

---

## Reto final de la lección

Construye un formulario completo de **Registro a una Conferencia Tecnológica** en tu archivo `index.html` que cumpla con todos los puntos de la siguiente lista:

- [ ] Un encabezado `<h1>` con el título del evento.
- [ ] La etiqueta `<form action="/registro" method="POST">`.
- [ ] Un primer `<fieldset>` con `<legend>` para **Datos Personales**:
  - Campo de nombre completo con `required` y `minlength="3"`.
  - Campo de correo con `type="email"`, `required` y `autocomplete="email"`.
  - Campo de teléfono con `type="tel"`.
  - Selector de fecha de nacimiento (`type="date"`) con valor máximo (`max`).
- [ ] Un segundo `<fieldset>` con `<legend>` para **Detalles de la Entrada**:
  - Grupo de botones de opción (`radio`) para elegir modalidad (*Presencial* o *Virtual*) compartiendo el mismo `name`.
  - Campo de texto con `<datalist>` para elegir el área de especialidad (ej. *Frontend*, *Backend*, *DevOps*, *UI/UX*).
  - Un deslizador (`type="range"`) para indicar el nivel de experiencia (del 1 al 5) con `min="1"` y `max="5"`.
- [ ] Un tercer `<fieldset>` con `<legend>` para **Información Adicional**:
  - Un `<textarea>` opcional para requerimientos dietéticos o accesibilidad.
  - Una casilla de verificación (`checkbox`) obligatoria (`required`) para aceptar el código de conducta.
- [ ] Todos los campos vinculados obligatoriamente a su respectivo `<label for="...">`.
- [ ] Un `<button type="submit">` para enviar y un `<button type="reset">` para limpiar el formulario.

### Preguntas de autoevaluación

1. ¿Qué ocurre con los datos de un `<input>` al enviar el formulario si olvidaste asignarle el atributo `name`?
2. ¿Cuál es la diferencia técnica entre enviar un formulario con `method="GET"` versus `method="POST"`?
3. ¿Por qué es fundamental asociar un `<label>` mediante el atributo `for` en lugar de poner texto suelto junto a un control?
4. ¿En qué escenario utilizarías un `<datalist>` en lugar de un elemento `<select>` tradicional?

---

## 📚 Recursos y documentación oficial

Para consultar la referencia completa de controles y restricciones de formulario, revisa la documentación de **MDN Web Docs**:

- 📖 [Guía de formularios en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Forms)
- 📖 [Referencia del elemento `<form>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/form)
- 📖 [Validación de datos de formulario en el cliente - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Forms/Client-side_form_validation)
- 📖 [Referencia del elemento `<input>` y sus tipos - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/input)
