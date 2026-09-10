# Lección 3: Enlaces y listas

Esta lección continúa el trabajo tras dominar [Texto, etiquetas y atributos](../02-texto-y-atributos/README.md). Ya sabes cómo dar formato semántico al contenido escrito; ahora aprenderás a conectar documentos mediante hipervínculos y a estructurar conjuntos de datos mediante listas ordenadas, no ordenadas y de descripción.

---

## 1. Enlaces con la etiqueta `a`

La etiqueta `<a>` (*anchor* o ancla) es el núcleo de la web: convierte texto o elementos visuales en enlaces interactivos que conducen a otros destinos mediante su atributo fundamental `href` (*hypertext reference*).

| Tipo de enlace | ¿A dónde conduce? | Sintaxis de ejemplo |
| --- | --- | --- |
| **Absoluto / Externo** | A un sitio web completo en cualquier servidor de internet. | `href="https://developer.mozilla.org"` |
| **Relativo / Interno** | A otro archivo dentro de tu propio proyecto. | `href="contacto.html"` o `href="paginas/acerca.html"` |
| **Ancla interna** | A una sección específica dentro de la misma página. | `href="#proyectos"` |
| **Acción funcional** | Abre aplicaciones del sistema (correo o teléfono). | `href="mailto:hola@ejemplo.com"` o `href="tel:+525512345678"` |
| **Descarga directa** | Fuerza la descarga de un archivo al disco duro. | `href="documento.pdf" download` |

### Código de ejemplo: Enlaces básicos y funcionales

```html
<!-- Enlace externo absoluto -->
<p>Consulta la <a href="https://developer.mozilla.org/es/">documentación oficial de MDN</a> para aprender más.</p>

<!-- Enlace relativo a otra página local -->
<p>Conoce más sobre mi trabajo en la página de <a href="contacto.html">contacto</a>.</p>

<!-- Enlaces funcionales del sistema operativo -->
<p>
  Escríbeme a mi <a href="mailto:contacto@ejemplo.com">correo electrónico</a> o 
  llámame a mi <a href="tel:+525512345678">teléfono de oficina</a>.
</p>

<!-- Enlace de descarga asistida -->
<p>Descarga mi <a href="cv-profesional.pdf" download>Currículum en formato PDF</a>.</p>
```

### Qué observar en los enlaces

- **El peligro de "Haz clic aquí" (La Lista de Enlaces en Lectores de Pantalla):**  
  Las personas ciegas utilizan atajos de teclado (como el *Rotor* en VoiceOver o `Insert + F7` en NVDA) para extraer una lista con **todos los enlaces de la página en una sola columna**. Si tu texto dice diez veces *"haz clic aquí"* o *"leer más"*, la persona solo escuchará una lista inútil de frases idénticas sin saber a dónde conducen.
- **Vista previa de URL:** Al pasar el cursor sobre cualquier enlace en tu navegador, observa la esquina inferior izquierda de la pantalla: el navegador siempre muestra la dirección de destino antes de hacer clic.

> [!IMPORTANT]
> El texto entre `<a>` y `</a>` debe ser **autoexplicativo y descriptivo por sí solo** (ejemplo: `<a href="precios.html">Consultar tabla de precios</a>` en lugar de `Para ver precios <a href="precios.html">haz clic aquí</a>`).

### Práctica 1: Enlaces básicos y funcionales (en `index.html`)

1. Crea tu archivo `index.html` con la estructura base de HTML5.
2. Agrega dentro de `<body>` un párrafo con un enlace externo a la documentación de HTML en MDN.
3. Añade un enlace funcional de correo con `mailto:` y un enlace de teléfono con `tel:`.
4. Pasa el cursor sobre ellos y comprueba en la esquina del navegador cómo se preparan las URLs.

---

## 2. Enlaces con atributos: nuevas pestañas y anclas internas

Los enlaces pueden abrir destinos en pestañas secundarias o desplazarse verticalmente dentro del mismo documento.

```html
<!-- Abrir en una pestaña nueva de forma segura -->
<p>
  Visita el sitio oficial del consorcio
  <a href="https://w3.org" target="_blank" rel="noopener noreferrer">W3C</a>.
</p>

<!-- Enlace que salta a una sección inferior -->
<p><a href="#proyectos">Ir directo a mis proyectos recientes</a></p>

<!-- Sección de destino (debe tener el id idéntico) -->
<section id="proyectos">
  <h2>Mis proyectos destacados</h2>
  <p>Aquí se listan los trabajos desarrollados durante el curso.</p>
  <!-- Enlace que regresa al encabezado de la página -->
  <p><a href="#inicio">Volver al inicio de la página</a></p>
</section>
```

### Qué observar en anclas y pestañas

- **El símbolo `#` solo va en el `href`:** El enlace busca `href="#proyectos"`, pero la etiqueta de destino se define limpiamente como `id="proyectos"` (sin el numeral `#`).
- **Seguridad con `rel="noopener noreferrer"`:** Al abrir una pestaña nueva con `target="_blank"`, el sitio externo podría acceder al objeto `window.opener` de tu página. Incluir `rel="noopener noreferrer"` corta esa conexión protegiendo la seguridad y el rendimiento de tu web.
- **Cambio en la URL:** Al hacer clic en un ancla interna, la barra de direcciones del navegador añade el fragmento (ej. `index.html#proyectos`), permitiendo que el usuario copie y comparta ese enlace directo a esa sección específica.

> [!WARNING]
> Comprueba siempre tus destinos. Un enlace que apunta a un archivo inexistente provocará un error 404, y un ancla con un `id` mal escrito no moverá la pantalla en absoluto.

### Práctica 2: Saltos de página internos con anclas (en `index.html`)

1. Asigna el atributo `id="inicio"` a tu encabezado principal `<h1>`.
2. Añade varios párrafos de texto de relleno para que la página tenga barra de desplazamiento vertical (*scroll*).
3. Crea al final del documento una `<section id="contacto">` con un enlace que diga `<a href="#inicio">Volver arriba</a>`. Haz clic y comprueba cómo la pantalla salta automáticamente al inicio.

---

## 3. Listas no ordenadas con `ul`

Usa la etiqueta `<ul>` (*unordered list*) cuando el orden cronológico o secuencial de los elementos no altera el significado del contenido. Cada elemento dentro de la lista se encierra obligatoriamente en una etiqueta `<li>` (*list item*).

```html
<h2>Herramientas de Desarrollo</h2>
<ul>
  <li>Editor de código Visual Studio Code</li>
  <li>Navegador web con DevTools</li>
  <li>Control de versiones con Git</li>
  <li>Servidor local de desarrollo</li>
</ul>
```

### Qué observar en `ul`

- **Hijos directos estrictos:** La etiqueta `<ul>` **solo puede tener elementos `<li>` como hijos directos**. Nunca coloques párrafos `<p>`, encabezados `<h3>` o enlaces `<a>` sueltos directamente dentro de `<ul>` sin envolverlos en un `<li>`.
- **Anuncios para accesibilidad:** Los lectores de pantalla informan al usuario al entrar a una lista diciendo: *"Lista con 4 elementos"*, lo que ayuda a dimensionar la cantidad de información disponible.

> [!NOTE]
> No utilices guiones (`-`), asteriscos (`*`) ni viñetas manuales dentro de párrafos para simular listas. La etiqueta semántica `<ul>` le comunica formalmente a los buscadores y tecnologías de asistencia la existencia de una colección estructurada.

### Práctica 3: Tu lista de herramientas técnicas (en `index.html`)

Agrega a tu `index.html` una lista no ordenada `<ul>` con al menos cuatro tecnologías o lenguajes que te gustaría aprender este año.

---

## 4. Listas ordenadas con `ol`

Usa la etiqueta `<ol>` (*ordered list*) cuando los elementos representan pasos secuenciales, clasificaciones, recetas o prioridades donde **el orden numérico sí altera el significado**:

```html
<h2>Pasos para publicar una página web</h2>
<ol>
  <li>Planear la arquitectura y redactar el contenido.</li>
  <li>Escribir el código HTML semántico y accesible.</li>
  <li>Validar el código en el validador oficial del W3C.</li>
  <li>Subir los archivos al servidor de producción.</li>
</ol>
```

### Atributos avanzados de `ol`

- **`start="N"`:** Inicia la numeración en un número diferente a 1.
- **`reversed`:** Invierte el orden numérico (ideal para cuentas regresivas o rankings de mejores elementos).

```html
<!-- Cuenta regresiva de lanzamiento -->
<h2>Cuenta regresiva para el evento</h2>
<ol reversed>
  <li>Despegue y transmisión en vivo</li>
  <li>Comprobación final de sistemas</li>
  <li>Inicio de la cuenta atrás</li>
</ol>
```

### Qué observar en `ol`

- **Numeración automática:** El navegador calcula y renderiza los números por su cuenta. **Nunca escribas los números a mano dentro del texto** (ejemplo incorrecto: `<li>1. Paso uno</li>`), ya que el navegador terminaría mostrando `1. 1. Paso uno`.
- **La prueba de intercambio:** Si cambias de lugar dos elementos de la lista y el resultado se arruina (como los pasos de una receta de cocina), debes usar `<ol>`. Si el orden no afecta la comprensión (como una lista de compras), usa `<ul>`.

> [!TIP]
> Si agregas o eliminas un `<li>` intermedio dentro de un `<ol>`, el navegador recalcula la numeración de toda la lista automáticamente sin que tengas que editar nada.

### Práctica 4: Pasos secuenciales y cuentas regresivas (en `index.html`)

1. Crea una lista ordenada `<ol>` con los 3 pasos principales que sigues para preparar tu espacio de estudio.
2. Debajo, crea otra lista `<ol reversed>` que represente un Top 3 de tus videojuegos, libros o películas favoritas, ordenadas del puesto 3 al puesto 1.

---

## 5. Listas de descripción: `dl`, `dt` y `dd`

HTML ofrece un tercer tipo de lista pensado para estructurar pares de términos y definiciones, glosarios, preguntas frecuentes (FAQ) o metadatos de productos:

```html
<h2>Glosario de Arquitectura Web</h2>
<dl>
  <!-- Término a definir -->
  <dt>HTML</dt>
  <!-- Definición o detalle asociado -->
  <dd>Lenguaje de marcado utilizado para estructurar semánticamente el contenido de la web.</dd>

  <dt>DNS</dt>
  <dd>Sistema que traduce nombres de dominio legibles en direcciones IP numéricas.</dd>
</dl>
```

- `<dl>` (*description list*): Contenedor general de la lista.
- `<dt>` (*description term*): El término, concepto o pregunta.
- `<dd>` (*description details*): La explicación, respuesta o valor asociado.

### Qué observar en `dl`

- Un mismo término (`<dt>`) puede tener múltiples descripciones (`<dd>`), y múltiples términos pueden compartir una sola descripción.
- Por defecto, los navegadores muestran las etiquetas `<dd>` con una sangría visual hacia la derecha para indicar subordinación al `<dt>`.

### Práctica 5: Glosario de términos web (en `index.html`)

Crea dentro de tu archivo `index.html` una lista de descripción `<dl>` con al menos tres conceptos fundamentales aprendidos hasta el momento (por ejemplo: *Etiqueta*, *Atributo* y *Elemento*).

---

## 6. Listas anidadas y menús de navegación

Una lista puede contener otra lista en su interior. Esta técnica es la base estándar para maquetar esquemas detallados, tablas de contenido y menús de navegación con subsecciones (`<nav>`):

### La regla de oro de la anidación (❌ vs. ✅)

El error sintáctico más común entre principiantes es colocar una sublista directamente dentro del contenedor `<ul>` padre sin envolverla en un `<li>`:

```html
<!-- ❌ INCORRECTO: 'ul' no puede ser hijo directo de otro 'ul' -->
<ul>
  <li>Temas de estudio</li>
  <ul> <!-- ¡ERROR! Debe estar dentro de un li -->
    <li>Enlaces</li>
  </ul>
</ul>

<!-- ✅ CORRECTO: La sublista vive DENTRO del <li> padre antes de que se cierre -->
<ul>
  <li>
    Temas de estudio
    <ul>
      <li>Enlaces</li>
      <li>Listas</li>
    </ul>
  </li> <!-- El li padre se cierra después de la sublista -->
</ul>
```

### Código de ejemplo: Menú de navegación semántico anidado

```html
<nav aria-label="Menú principal del sitio">
  <h2>Mapa de navegación</h2>
  <ul>
    <li><a href="#inicio">Inicio</a></li>
    <li>
      <a href="#cursos">Nuestros Cursos</a>
      <!-- Sublista anidada dentro del li de cursos -->
      <ul>
        <li><a href="#html">HTML5 Semántico</a></li>
        <li><a href="#css">CSS Moderno</a></li>
      </ul>
    </li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
</nav>
```

### Qué observar en listas anidadas

- La sublista secundaria debe colocarse **después del texto del elemento padre, pero antes de su etiqueta de cierre `</li>`**.
- Los lectores de pantalla informan al usuario del cambio de nivel diciendo: *"Nivel de lista 2"*, lo que permite a las personas con discapacidad visual comprender la jerarquía de categorías y subcategorías.

> [!CAUTION]
> Toda etiqueta hija directa de un `<ul>` o de un `<ol>` debe ser **exclusivamente un `<li>`**. Cualquier otra etiqueta suelta colocada allí romperá la validación sintáctica del W3C.

### Práctica 6: Menú de navegación anidado (en `index.html`)

Construye en tu `index.html` una barra de navegación `<nav>` con una lista `<ul>` que contenga tres secciones principales, y añade una sublista con dos temas anidados dentro del segundo elemento `<li>`.

---

## Reto final de la lección: Guía de Viaje para una Ciudad

Ahora que dominas los enlaces relativos, absolutos, funcionales y todos los tipos de listas en tu laboratorio (`index.html`), demostrarás tu autonomía construyendo un documento completo desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `03-enlaces-y-listas`. Construirás una **Guía Turística de una Ciudad** que cumpla estrictamente con la siguiente lista de control:

- [ ] Estructura base completa de HTML5 (`<!DOCTYPE html>`, `<html lang="es">`, `<head>` con metadatos y `<body>`).
- [ ] Un encabezado principal `<h1>` con el nombre de la ciudad y el atributo `id="inicio"`.
- [ ] Una barra de navegación semántica `<nav aria-label="Navegación de la guía">` que contenga una lista `<ul>` con enlaces internos que salten a las diferentes secciones (`#lugares`, `#itinerario`, `#glosario`).
- [ ] **Sección de Lugares de Interés (`#lugares`):**
  - Una **lista no ordenada** (`<ul>`) con al menos 4 sitios turísticos recomendados.
  - Al menos uno de los elementos debe contener una sublista anidada con recomendaciones específicas.
- [ ] **Sección de Itinerario (`#itinerario`):**
  - Una **lista ordenada** (`<ol>`) que describa la secuencia paso a paso para recorrer la ciudad en un día (mañana, tarde y noche).
- [ ] **Sección de Modismos Locales (`#glosario`):**
  - Una **lista de descripción** (`<dl>`) con al menos 3 palabras o expresiones típicas de esa ciudad con su respectiva definición (`<dt>` y `<dd>`).
- [ ] **Enlaces externos y funcionales:**
  - Al menos un enlace externo que abra en pestaña nueva con `target="_blank"` y `rel="noopener noreferrer"` apuntando a la web oficial de turismo de esa ciudad.
  - Un enlace funcional de contacto (`mailto:` o `tel:`) para pedir informes turísticos.
- [ ] **Navegación de retorno:**
  - Un enlace al pie del documento que apunte a `#inicio` para regresar al inicio de la página.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Por qué es una pésima práctica de accesibilidad utilizar textos como "haz clic aquí" o "más información" en un enlace `<a>`?
2. ¿Cuál es la regla semántica definitiva para decidir si una colección de elementos debe estructurarse con `<ul>` o con `<ol>`?
3. Si colocas `target="_blank"` en un enlace que lleva a un sitio web externo, ¿por qué es indispensable incluir el atributo `rel="noopener noreferrer"`?
4. ¿Cuál es el error sintáctico al crear listas anidadas y cómo se corrige según los estándares del W3C?
5. ¿En qué se diferencia una lista de descripción (`<dl>`) de una lista tradicional (`<ul>` u `<ol>`) y para qué casos de uso fue concebida?

---

## 📚 Recursos y documentación oficial

Para profundizar en la creación de hipervínculos y listas semánticas, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Creación de hiperenlaces en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Creating_hyperlinks)
- 📖 [Listas en HTML (`<ul>`, `<ol>`, `<dl>`) - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/HTML_text_fundamentals#listas)
- 📖 [Referencia del elemento de anclaje `<a>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/a)
- 📖 [El elemento de descripción `<dl>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/dl)
- 📖 [Accesibilidad en enlaces: textos significativos - W3C WAI](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
