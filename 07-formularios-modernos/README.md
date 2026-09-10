# Lección 7: Formularios modernos y validación nativa

Esta lección continúa la ruta de aprendizaje tras dominar las tablas en [Tablas de Datos](../06-tablas-de-datos/README.md). Ahora aprenderás a construir el mecanismo principal de interactividad y captura de datos en la web: los **formularios**.

> [!TIP]
> **Metodología de trabajo en esta lección:**  
> Usaremos **dos archivos** dentro de tu carpeta `07-formularios-modernos`:
>
> - `index.html`: Será tu **laboratorio de experimentos**. Aquí probarás cada etiqueta y atributo de las micro-prácticas para ver cómo reacciona el navegador en vivo.
> - `reto.html`: Será tu **proyecto independiente**. Al final de la lección crearás este archivo desde cero para resolver un caso real sin ayuda guiada.

---

## 1. Modelo mental: Anatomía del envío de datos

Un formulario no es solo un conjunto de cajas visuales; es un **canal de comunicación estructurado** entre el usuario y un servidor o script de procesamiento:

```html
+-----------------------------------------------------------------------+
|  <form action="https://httpbin.org/post" method="POST">               |
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

- **`action`**: La URL o endpoint adonde se enviarán los datos procesados.
  - *Consejo para pruebas:* Si colocas una ruta relativa que aún no existe (como `/procesar`), tu navegador mostrará un error 404 al enviar. Para practicar en local sin servidor propio, puedes usar el servicio público de pruebas `https://httpbin.org/post` o dejar temporalmente `action="#"`.
- **`method`**: El método HTTP de envío:
  - `GET`: Envía los datos visibles en la barra de direcciones (`/buscar?q=html5`). Ideal para motores de búsqueda y filtros; **nunca para contraseñas o datos sensibles**.
  - `POST`: Envía los datos empaquetados en el cuerpo de la petición HTTP. Indispensable para crear cuentas, contraseñas, pagos o modificar bases de datos.
- **`enctype`**: Especifica cómo se codifican los datos antes de enviarlos.
  - Por defecto es `application/x-www-form-urlencoded`.
  - Si tu formulario permite **adjuntar archivos** (`<input type="file">`), es **estrictamente obligatorio** definir `enctype="multipart/form-data"`. Sin este atributo, el archivo nunca viajará al servidor.

> [!IMPORTANT]
> Todo campo que deba viajar al servidor **debe tener el atributo `name`**. Si un `<input>` no tiene `name`, el navegador lo ignorará por completo al enviar el formulario.

### Ejemplo de estructura básica y envío

Agrega este bloque a tu archivo `index.html`:

```html
<!-- Formulario configurado para pruebas con método POST -->
<form action="https://httpbin.org/post" method="POST">
  <label for="campo-nombre">Tu nombre:</label>
  <input type="text" id="campo-nombre" name="nombre_usuario">

  <button type="submit">Enviar datos</button>
</form>
```

### Qué observar en el envío de formularios

- El atributo `name="nombre_usuario"` define el identificador de la variable (la *clave*), mientras que lo que escribe la persona representa el *valor*.
- Al pulsar el botón "Enviar datos", el navegador compila la información y la despacha al endpoint definido en `action`.
- Si cambias temporalmente el método a `method="GET"` y envías la palabra "Carlos", verás que la URL del navegador se transforma en `...?nombre_usuario=Carlos`.

### Práctica 1: Laboratorio de envío (en `index.html`)

1. Escribe el formulario del ejemplo en tu archivo `index.html`.
2. Pruébalo primero con `method="GET"`: escribe un término, pulsa el botón y observa cómo tus datos viajan visibles en la barra de direcciones.
3. Cambia a `method="POST"` apuntando a `https://httpbin.org/post`, envía tu nombre y observa el JSON estructurado que el servicio de pruebas te devuelve en pantalla.

---

## 2. Accesibilidad: Vinculación con `label` y agrupación con `fieldset`

Para que un formulario sea accesible a lectores de pantalla y cómodo de pulsar en pantallas táctiles, jamás dejes un control sin su etiqueta descriptiva `<label>`.

### Vinculación explícita vs. Vinculación implícita

Existen dos formas válidas de asociar una etiqueta a un control:

```html
<!-- 1. Vinculación explícita (Recomendada para la gran mayoría de campos) -->
<!-- El atributo 'for' del label debe coincidir con el 'id' del input -->
<label for="nombre-usuario">Nombre completo:</label>
<input type="text" id="nombre-usuario" name="nombre_usuario">

<!-- 2. Vinculación implícita (Muy común en casillas de verificación pequeñas) -->
<!-- El input queda contenido directamente dentro del label sin necesidad de 'for' -->
<label>
  <input type="checkbox" name="notificaciones" value="si">
  Deseo recibir novedades por correo
</label>
```

### Agrupación temática con `fieldset` y `legend`

```html
<fieldset>
  <legend>Información de Envío</legend>

  <label for="direccion">Calle y número:</label>
  <input type="text" id="direccion" name="direccion">

  <label for="cp">Código Postal:</label>
  <input type="text" id="cp" name="cp">
</fieldset>
```

#### ¿Se siguen usando `<fieldset>` y `<legend>` en el desarrollo web actual?

**Sí, rotundamente.** Son el estándar de la industria y un requisito en sistemas de diseño profesionales:

1. **Accesibilidad indispensable:** Cuando un usuario con lector de pantalla navega por opciones de radio o casillas, el software lee el `<legend>` antes de cada opción (por ejemplo: *"Modalidad, grupo: Presencial, seleccionado 1 de 2"*). Sin `<fieldset>`, el lector solo diría *"Presencial"*, dejando al usuario sin saber qué le están preguntando.
2. **El estilo visual:** Por defecto, los navegadores les dibujan un borde gris con el título incrustado. En proyectos modernos, ese borde simplemente se retira con CSS (`border: none; padding: 0;`), logrando una apariencia moderna y 100% accesible.

#### ¿Se usan una sola vez o se pueden repetir?

**Se pueden usar tantas veces como bloques temáticos tenga el formulario.**

- **Modelo mental:** Piensa en el `<form>` como un **archivador** y en cada `<fieldset>` como una **carpeta divisoria**.
- En formularios cortos (como un inicio de sesión con email y contraseña), casi nunca se usan.
- En formularios medianos o grandes, es una excelente práctica tener varios: uno para *Datos Personales*, otro para *Dirección de Entrega*, otro para *Información de Pago*, etc.

### Qué observar en etiquetas y agrupaciones

- **Zona de clic ampliada:** Al hacer clic sobre el texto de un `<label>`, el foco se transfiere automáticamente al `<input>` correspondiente. Esto es fundamental para usuarios en pantallas táctiles o con movilidad reducida.
- El valor del atributo `for` del `<label>` debe coincidir con total exactitud con el `id` del `<input>`.

> [!WARNING]
> No confundas `id` con `name`:
>
> - `id`: Es el identificador único en el documento HTML. Sirve para enlazar el `<label for="...">` y para manipularlo con CSS o JavaScript.
> - `name`: Es la variable con la que el servidor recibe el dato al procesar el formulario.

### Práctica 2: Etiquetas y agrupación accesible (en `index.html`)

1. En tu `index.html`, crea un `<fieldset>` con un `<legend>` que diga `Contacto Personal`.
2. Dentro de este bloque, añade dos campos con **vinculación explícita** (`for` e `id`): uno para "Nombre" y otro para "Teléfono".
3. Haz clic sobre el texto de las etiquetas en tu navegador y comprueba que el cursor salte automáticamente al interior de la caja de texto correspondiente.

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
<!-- Selección excluyente agrupada con fieldset propio -->
<fieldset>
  <legend>Turno de preferencia</legend>
  
  <input type="radio" id="turno-manana" name="turno" value="manana" checked>
  <label for="turno-manana">Matutino</label>

  <input type="radio" id="turno-tarde" name="turno" value="tarde">
  <label for="turno-tarde">Vespertino</label>
</fieldset>

<!-- Controles especializados de HTML5 -->
<fieldset>
  <legend>Preferencias del usuario</legend>

  <label for="fecha-cita">Fecha solicitada:</label>
  <input type="date" id="fecha-cita" name="fecha_cita">

  <label for="volumen">Nivel de satisfacción (1 al 10):</label>
  <input type="range" id="volumen" name="satisfaccion" min="1" max="10" value="5">

  <!-- Subida de archivo (requiere enctype="multipart/form-data" en el form) -->
  <label for="comprobante">Subir documento (PDF o imagen):</label>
  <input type="file" id="comprobante" name="documento" accept=".pdf,image/*">
</fieldset>
```

### Qué observar en los tipos de entrada modernos

- **Agrupación de radios:** Para que los botones de radio sean excluyentes (elegir uno desmarque el otro), deben compartir exactamente el **mismo atributo `name`** (`name="turno"`).
- **El atributo `value` en opciones:** En los `radio` y `checkbox`, el atributo `value` es obligatorio. Si no lo especificas, el servidor recibirá un valor genérico `"on"`.
- **Selectores nativos:** Elementos como `type="date"` o `type="color"` despliegan la interfaz propia del sistema operativo o navegador sin requerir plugins externos de JavaScript.

### Práctica 3: Controles especializados y opciones (en `index.html`)

1. Agrega en tu `index.html` un grupo de dos botones de radio para que el usuario elija su método de contacto favorito (*Correo* o *Teléfono*), asegurándote de que compartan el mismo `name`.
2. Añade un control `type="range"` para evaluar del 1 al 100 y un selector de fecha con `type="date"`. Comprueba cómo se comporta el calendario al hacer clic en él.

---

## 4. Controles multilínea, listas y autocompletado

### Texto multilínea con `<textarea>`

A diferencia de `<input>`, `<textarea>` es un elemento con etiqueta de apertura y cierre obligatorias:

```html
<label for="comentarios">Comentarios adicionales:</label>
<textarea id="comentarios" name="comentarios" rows="4" cols="50" placeholder="Escribe aquí tus observaciones..."></textarea>
```

### Menú desplegable con `<select>`, `<optgroup>` y `<option>`

Permite al usuario elegir una opción dentro de un menú colapsable estructurado:

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

Combina la libertad de un campo de texto con una lista de recomendaciones sugeridas:

```html
<label for="framework">Tecnología favorita:</label>
<input type="text" id="framework" name="framework" list="lista-frameworks" placeholder="Escribe o selecciona...">

<datalist id="lista-frameworks">
  <option value="React"></option>
  <option value="Vue"></option>
  <option value="Angular"></option>
  <option value="Svelte"></option>
</datalist>
```

### Qué observar en textarea, select y datalist

- **Espacios en blanco en `<textarea>`:** Todo lo que escribas entre `<textarea>` y `</textarea>` (incluso saltos de línea y tabulaciones) se considerará texto predefinido dentro de la caja. Mantén la etiqueta de cierre pegada si deseas que el campo inicie totalmente limpio.
- **`<select>` vs. `<datalist>`:** En un `<select>` el usuario está restringido exclusivamente a las opciones del menú. Con `<datalist>`, el usuario puede elegir una sugerencia de la lista o escribir un texto completamente libre que no figure en ella.
- El atributo `list` del `<input>` se conecta directamente con el `id` del elemento `<datalist>`.

> [!TIP]
> Para hacer que la primera opción de un `<select>` sirva de instrucción visual y no como una respuesta válida, asígnale los atributos `disabled selected` y deja su valor en blanco: `value=""`.

### Práctica 4: Listas desplegables y sugerencias (en `index.html`)

1. Agrega a tu `index.html` un menú `<select>` con al menos tres opciones agrupadas por categorías usando `<optgroup>`.
2. Agrega un `<input>` con un `<datalist>` que sugiera tres nombres de ciudades. Prueba escribir una letra para ver cómo el navegador filtra las opciones sugeridas de forma automática.

---

## 5. Validación nativa y atributos de restricción

HTML5 permite aplicar reglas de integridad de datos **en el cliente sin escribir código JavaScript**:

| Atributo | Propósito | Ejemplo |
| --- | --- | --- |
| `required` | Campo obligatorio para permitir el envío. | `<input type="text" required>` |
| `placeholder` | Texto de ayuda temporal antes de escribir. | `placeholder="ej. ana@empresa.com"` |
| `minlength` / `maxlength` | Límites de caracteres en campos de texto. | `minlength="3" maxlength="50"` |
| `min` / `max` | Valores numéricos o fechas mínimas y máximas. | `min="18" max="99"` o `min="2026-01-01"` |
| `step` | Intervalo de incremento permitido para números. | `step="5"` o `step="0.5"` |
| `pattern` | Expresión regular (Regex) para formatos exactos. | `pattern="[A-Z]{3}[0-9]{4}"` |
| `autocomplete` | Asiste al gestor de contraseñas del navegador. | `autocomplete="email"` o `autocomplete="name"` |
| `readonly` | Solo lectura (no editable, pero se envía al servidor). | `readonly` |
| `disabled` | Deshabilita el control (no se edita y **NO** se envía). | `disabled` |

> [!WARNING]
> Nunca uses `placeholder` como sustituto de un `<label>`. El placeholder desaparece en cuanto el usuario comienza a escribir, lo que genera desorientación y rompe las pautas básicas de accesibilidad web.

### Ejemplo de validaciones combinadas

```html
<fieldset>
  <legend>Seguridad de la cuenta</legend>

  <label for="clave">Contraseña de acceso (mínimo 8 caracteres):</label>
  <input 
    type="password" 
    id="clave" 
    name="clave" 
    required 
    minlength="8" 
    autocomplete="new-password"
  >

  <label for="codigo-postal">Código Postal (5 dígitos numéricos):</label>
  <input 
    type="text" 
    id="codigo-postal" 
    name="cp" 
    required 
    pattern="[0-9]{5}" 
    placeholder="01000"
  >
</fieldset>
```

### Qué observar en la validación nativa

- Si intentas enviar un formulario que no cumple con las restricciones (por ejemplo, un campo `required` vacío o un correo sin formato correcto), el navegador detiene el envío y muestra un mensaje emergente nativo.
- El atributo `autocomplete` ayuda a los navegadores y gestores de contraseñas a rellenar la información correcta de forma segura (`autocomplete="email"`, `autocomplete="tel"`, etc.).
- Las restricciones nativas activan pseudo-clases en CSS como `:valid`, `:invalid` y `:required`, lo que permite dar estilos visuales dinámicos según el estado del campo.

### Práctica 5: Rompiendo las reglas de validación (en `index.html`)

1. En tu archivo `index.html`, define un campo de correo obligatorio con `required` y `type="email"`.
2. Añade un campo numérico para la edad con `min="18"` y `max="65"`.
3. Intenta enviar el formulario vacío, luego escribe una edad fuera del rango (como 12 o 90) y pulsa enviar para ver los mensajes de error automáticos que detona el navegador.

---

## 6. Botones y envío de formularios

Para detonar acciones dentro de un formulario, la etiqueta estándar y recomendada es `<button>`. Existen tres comportamientos posibles según su atributo `type`:

| Tipo de botón | Propósito | Comportamiento |
| --- | --- | --- |
| `type="submit"` | **Enviar datos** (Por defecto) | Ejecuta las validaciones nativas y procesa el envío al servidor. |
| `type="reset"` | **Restablecer** | Devuelve todos los campos a sus valores iniciales en blanco o por defecto. |
| `type="button"` | **Acción neutra** | No hace nada por sí solo; se utiliza para ser controlado con JavaScript (ej. abrir modales, mostrar contraseñas). |

### Código de ejemplo

```html
<!-- 1. Botón principal de envío -->
<button type="submit">Confirmar y Enviar</button>

<!-- 2. Botón secundario para limpiar campos -->
<button type="reset">Limpiar formulario</button>

<!-- 3. Botón neutral para interactividad (no envía el formulario) -->
<button type="button">Cancelar</button>
```

> [!IMPORTANT]
> **El peligro de olvidar el atributo `type`:**  
> Si colocas un `<button>` dentro de un `<form>` sin especificar su tipo, el navegador le asignará `type="submit"` de manera automática. Si alguna vez agregas un botón como *"Ver contraseña"* o *"Siguiente paso"* y olvidas ponerle `type="button"`, al hacer clic **enviará el formulario y recargará la página por error**.

---

### ¿Dónde debe colocarse el botón? (¿Dentro o fuera del `<form>`?)

#### Caso 1: La regla estándar (DENTRO)

Por defecto, los botones deben residir **dentro** de la etiqueta `<form>`, justo al final de los controles:

```html
<!-- ❌ INCORRECTO: El botón quedó huérfano fuera del formulario -->
<form action="/procesar" method="POST">
  <input type="text" name="usuario">
</form> 
<button type="submit">Enviar</button> <!-- Al hacer clic, no pasa absolutamente nada -->

<!-- ✅ CORRECTO: El botón forma parte del flujo del formulario -->
<form action="/procesar" method="POST">
  <input type="text" name="usuario">
  <button type="submit">Enviar</button>
</form>
```

#### Caso 2: La técnica moderna (FUERA mediante el atributo `form`)

HTML5 permite ubicar un botón en cualquier parte de la página (por ejemplo, en una barra de navegación fija o en el pie de un modal) y vincularlo remotamente a su formulario mediante el atributo `form="id-del-formulario"`:

```html
<!-- Formulario identificado con un id -->
<form id="formulario-registro" action="https://httpbin.org/post" method="POST">
  <label for="asistente">Nombre:</label>
  <input type="text" id="asistente" name="asistente" required>
</form>

<!-- ...otro contenido, un modal o barra fija... -->

<!-- El botón está físicamente AFUERA, pero sabe a qué form activar -->
<button type="submit" form="formulario-registro">Confirmar Asistencia</button>
```

---

### Qué observar en los botones

- **Detonante de validación:** El botón `type="submit"` no solo envía información; es el encargado de disparar la validación nativa de HTML5. Si un campo requerido está vacío, el botón frenará el envío y el navegador mostrará el mensaje de error.
- **Uso prudente de `type="reset"`:** No suele colocarse en formularios largos de producción, ya que un clic involuntario borrará todo el trabajo del usuario sin pedir confirmación.
- **Flexibilidad de `<button>` frente a `<input type="submit">`:** A diferencia del antiguo `<input type="submit" value="Enviar">`, la etiqueta `<button>` tiene etiqueta de apertura y cierre (`<button>...</button>`), lo que permite colocar dentro íconos SVG, negritas, imágenes y estructurar su diseño con CSS flexbox.

### Práctica 6: Disparadores de acción (en `index.html`)

1. Agrega al final de tu formulario de pruebas en `index.html` un botón con `type="submit"` y otro con `type="reset"`.
2. Prueba escribir texto en los campos y pulsa el botón de reset para comprobar cómo los devuelve a su estado inicial.
3. Luego, saca el botón de envío fuera de `</form>` a propósito (sin `form="..."`) para comprobar que deja de responder al clic, y después reconéctalo usando el atributo `form="id-de-tu-formulario"`.

---

## Reto final de la lección: Formulario de Postulación de Empleo

Ahora que dominas la teoría y experimentaste con cada control en tu laboratorio (`index.html`), demostrarás tu autonomía resolviendo un proyecto completamente nuevo y desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `07-formularios-modernos`. Construirás una **Solicitud de Empleo para Desarrollador Web Junior** que cumpla con todos los puntos de la siguiente lista de control:

- [ ] Estructura base completa de HTML5 con `<!DOCTYPE html>`, `<html>`, `<head>` y `<body>`.
- [ ] Un encabezado principal `<h1>Postulación de Empleo: Desarrollador Frontend Jr.</h1>`.
- [ ] La etiqueta `<form>` configurada con `action="https://httpbin.org/post"`, `method="POST"` y **el atributo `enctype` necesario para procesar archivos**.
- [ ] **Primer `<fieldset>` con `<legend>Datos del Candidato</legend>`:**
  - [ ] Nombre completo obligatorio (`required` y `minlength="3"`).
  - [ ] Correo electrónico obligatorio con validación y `autocomplete="email"`.
  - [ ] Teléfono de contacto con `type="tel"`.
  - [ ] Enlace a portafolio o GitHub con `type="url"`.
- [ ] **Segundo `<fieldset>` con `<legend>Perfil Profesional</legend>`:**
  - [ ] Grupo de botones de opción (`radio`) para elegir modalidad preferida (*Remoto*, *Híbrido* o *Presencial*) compartiendo el mismo `name`.
  - [ ] Campo de texto con `<datalist>` para elegir el rol técnico principal (*Frontend*, *Backend*, *Fullstack*, *QA*).
  - [ ] Deslizador (`type="range"`) o campo numérico para indicar la expectativa salarial mensual.
  - [ ] Campo para subir el currículum en PDF con `type="file"` y restricción `accept=".pdf"`.
- [ ] **Tercer `<fieldset>` con `<legend>Carta de Presentación y Términos</legend>`:**
  - [ ] Un `<textarea>` con `name="carta"` para explicar brevemente por qué quieres unirte al equipo.
  - [ ] Una casilla de verificación (`checkbox`) obligatoria (`required`) para aceptar las políticas de privacidad y tratamiento de datos.
- [ ] **Accesibilidad:** Todos los campos deben estar vinculados correctamente a un `<label>` (de forma explícita o implícita).
- [ ] **Acciones:** Un `<button type="submit">Enviar Solicitud</button>` y un `<button type="reset">Limpiar</button>`.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Qué ocurre con los datos de un `<input>` al enviar el formulario si olvidaste asignarle el atributo `name`?
2. ¿Cuál es la diferencia técnica fundamental entre enviar un formulario con `method="GET"` versus `method="POST"`?
3. ¿Por qué es una mala práctica retirar o dejar de usar `<fieldset>` y `<legend>` en preguntas con múltiples opciones de radio?
4. ¿En qué escenario técnico utilizarías un `<datalist>` en lugar de un elemento `<select>` tradicional?
5. ¿Qué atributo debe tener el `<form>` si necesitas enviar un archivo adjunto mediante `<input type="file">` y qué sucede si lo omites?
6. Si necesitas colocar el botón de envío en una barra superior flotante, fuera de la etiqueta `<form>`, ¿cómo logras que envíe los datos?

---

## 📚 Recursos y documentación oficial

Para profundizar en la referencia completa de controles y restricciones de formulario, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Guía de formularios en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Forms)
- 📖 [Referencia del elemento `<form>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/form)
- 📖 [El elemento `<fieldset>` y accesibilidad - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/fieldset)
- 📖 [Validación de datos de formulario en el cliente - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Forms/Client-side_form_validation)
- 📖 [Referencia del elemento `<input>` y sus tipos - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/input)
- 📖 [Atributo enctype y envío de archivos - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/form#enctype)
