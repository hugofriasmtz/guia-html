# Lección 3: Enlaces y listas

Esta lección continúa el documento que preparaste en [Texto, etiquetas y atributos](../02-texto-y-atributos/README.md). Ya puedes organizar títulos, párrafos y dar formato semántico al contenido; ahora aprenderás a conectar páginas mediante enlaces y a estructurar conjuntos de datos con listas.

> [!TIP]
> Continúa trabajando sobre el archivo `index.html` de las lecciones anteriores o crea una carpeta para esta lección. Guarda los cambios con frecuencia y recarga el navegador para comprobar los destinos de tus enlaces.

## 1. Enlaces con la etiqueta `a`

La etiqueta `a` (*anchor* o ancla) convierte texto o elementos en enlaces que llevan a otros destinos. Utiliza el atributo `href` (*hypertext reference*) para definir la dirección de llegada.

| Tipo de enlace | ¿A dónde apunta? | Ejemplo de `href` |
| --- | --- | --- |
| **Absoluto / Externo** | A un sitio web completo en internet. | `href="https://developer.mozilla.org"` |
| **Relativo / Interno** | A otro archivo dentro de tu propio proyecto. | `href="contacto.html"` o `href="paginas/acerca.html"` |
| **Ancla interna** | A una sección específica de la misma página. | `href="#contacto"` |
| **Funcional** | A una acción del sistema (correo, teléfono). | `href="mailto:correo@ejemplo.com"` |

### Ejemplo de enlaces básicos

Agrega estos enlaces dentro de `body`:

```html
<!-- Enlace externo -->
<p>Consulta la <a href="https://developer.mozilla.org/es/">documentación de MDN</a> para aprender más.</p>

<!-- Enlace relativo a otra página del proyecto -->
<p>Conoce más sobre mi trabajo en la página de <a href="contacto.html">contacto</a>.</p>

<!-- Enlace funcional -->
<p>Escríbeme a mi <a href="mailto:hola@ejemplo.com">correo electrónico</a>.</p>
```

### Qué observar en los enlaces

- El texto entre `<a>` y `</a>` es el enlace visible y clickeable.
- El texto debe ser descriptivo por sí solo; evita frases vacías como "haz clic aquí" o "más info".
- Los enlaces externos deben incluir el protocolo completo (`https://`).

> [!IMPORTANT]
> El texto del enlace debe explicar claramente a dónde conduce antes de pulsar en él. Esto es indispensable para la accesibilidad y para personas que navegan con lectores de pantalla.

### Práctica de enlaces básicos

Agrega a tu página:

- Un enlace a una fuente de documentación oficial.
- Un enlace relativo a un archivo ficticio llamado `sobre-mi.html`.
- Un enlace de correo con `mailto:`.

---

## 2. Enlaces con atributos: nuevas pestañas y anclas internas

Los enlaces pueden cambiar su comportamiento o navegar dentro del mismo documento utilizando atributos adicionales.

```html
<!-- Abrir en una pestaña nueva -->
<p>
  Visita el sitio de 
  <a href="https://w3.org" target="_blank" rel="noopener noreferrer">W3C</a>.
</p>

<!-- Enlace que salta a una sección inferior -->
<p><a href="#proyectos">Ir directo a mis proyectos</a></p>

<!-- Sección de destino -->
<section id="proyectos">
  <h2>Mis proyectos</h2>
  <p>Aquí se listan los trabajos recientes.</p>
  <p><a href="#inicio">Volver al inicio</a></p>
</section>
```

- `target="_blank"` abre la página en una pestaña o ventana nueva.
- `rel="noopener noreferrer"` protege la seguridad y el rendimiento al abrir sitios externos en pestañas nuevas.
- `href="#id"` busca un elemento que tenga el atributo `id` exactamente con ese mismo nombre.

### Qué observar en anclas y pestañas

- Para que un ancla interna funcione, debe existir un elemento con el `id` correspondiente (sin el símbolo `#` en el `id`, solo en el `href`).
- Si haces clic en `#proyectos`, el navegador se desplazará verticalmente hasta esa sección.

> [!WARNING]
> Comprueba cada destino. Un enlace que apunta a un archivo inexistente dará un error 404, y un ancla con un `id` mal escrito no moverá la pantalla.

### Práctica de anclas

Asigna un `id="inicio"` a tu encabezado `h1` y crea un enlace al final de tu documento que regrese al inicio de la página.

---

## 3. Listas no ordenadas con `ul`

Usa la etiqueta `ul` (*unordered list*) cuando el orden de los elementos no altera el significado del contenido. Cada elemento dentro de la lista se encierra en una etiqueta `li` (*list item*).

```html
<h2>Habilidades técnicas</h2>
<ul>
  <li>Estructura semántica con HTML5</li>
  <li>Organización de archivos</li>
  <li>Control de versiones con Git</li>
</ul>
```

### Qué observar en `ul`

- `ul` representa el contenedor de la lista completa.
- Solo las etiquetas `li` deben ser hijas directas de `ul`.
- Por defecto, el navegador muestra puntos o viñetas a la izquierda de cada elemento.

> [!NOTE]
> No uses guiones o asteriscos manuales dentro de párrafos para simular listas. La etiqueta `ul` le comunica a los motores de búsqueda y lectores de pantalla cuántos elementos componen el grupo.

### Práctica de listas sin orden

Crea una lista `ul` con cuatro herramientas o tecnologías que te gustaría dominar este año.

---

## 4. Listas ordenadas con `ol`

Usa la etiqueta `ol` (*ordered list*) cuando los elementos representan pasos, secuencias, clasificaciones o prioridades donde el orden sí importa.

```html
<h2>Pasos para publicar una página web</h2>
<ol>
  <li>Planear la estructura y el contenido.</li>
  <li>Escribir el código HTML semántico.</li>
  <li>Comprobar los enlaces y la accesibilidad.</li>
  <li>Subir los archivos a un servidor.</li>
</ol>
```

Atributos útiles en `ol`:

- `start="5"`: Inicia la numeración en un número diferente a 1.
- `reversed`: Invierte el orden numérico (útil para cuentas regresivas o tops de mejores elementos).

```html
<h2>Cuenta regresiva</h2>
<ol reversed>
  <li>Lanzamiento</li>
  <li>Revisión final</li>
  <li>Preparación</li>
</ol>
```

### Qué observar en `ol`

- El navegador numera automáticamente cada `li`. No debes escribir los números a mano dentro del texto.
- Si eliminas o agregas un elemento intermedio, el navegador recalcula la numeración de forma automática.

> [!TIP]
> Regla sencilla: si cambias el orden de los elementos y el significado se arruina (como una receta de cocina), usa `ol`. Si el orden no afecta la comprensión (como una lista de compras), usa `ul`.

### Práctica de listas ordenadas

Escribe una lista ordenada con los pasos que sigues para encender tu computadora y preparar tu espacio de estudio.

---

## 5. Listas de descripción: `dl`, `dt` y `dd`

HTML cuenta con un tercer tipo de lista para pares de términos y definiciones, preguntas frecuentes o metadatos:

```html
<h2>Glosario web</h2>
<dl>
  <dt>HTML</dt>
  <dd>Lenguaje de marcado utilizado para estructurar el contenido de la web.</dd>

  <dt>Navegador</dt>
  <dd>Programa que interpreta el código web y lo muestra en pantalla.</dd>
</dl>
```

- `dl` (*description list*) es el contenedor general.
- `dt` (*description term*) es el término o concepto.
- `dd` (*description details*) es la definición o explicación asociada al término.

### Qué observar en `dl`

- Un término (`dt`) puede tener múltiples descripciones (`dd`) asociadas.
- Es la estructura semántica correcta para diccionarios, glosarios o listas de preguntas y respuestas (FAQ).

### Reto de términos

Crea un glosario con al menos tres conceptos que hayas aprendido hasta ahora (por ejemplo: etiqueta, atributo y elemento).

---

## 6. Listas anidadas y menús de navegación

Una lista puede contener otra lista en su interior. Esto es fundamental para crear esquemas detallados o menús de navegación (`nav`).

```html
<nav>
  <h2>Menú de navegación</h2>
  <ul>
    <li><a href="#inicio">Inicio</a></li>
    <li>
      <a href="#temas">Temas de estudio</a>
      <ul>
        <li><a href="#enlaces">Enlaces</a></li>
        <li><a href="#listas">Listas</a></li>
      </ul>
    </li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
</nav>
```

### Qué observar en listas anidadas

- La sublista `ul` o `ol` debe colocarse **dentro** de un `li` padre, justo antes de que este se cierre.
- Los enlaces (`a`) se colocan comúnmente dentro del `li` para construir barras y menús de navegación web.

> [!CAUTION]
> No coloques una lista secundaria directamente dentro de un `ul` padre sin envolverla en un `li`. Toda etiqueta hija directa de `ul` u `ol` debe ser un `li`.

### Práctica de navegación

Crea un menú de navegación para tu página utilizando la etiqueta semántica `<nav>` que contenga una lista `ul` con tres enlaces a diferentes secciones de tu documento.

---

## Reto final de la lección

Crea una **Guía de Viaje para una Ciudad** en tu página web que incluya todos los conceptos vistos en esta lección:

- [ ] Un encabezado principal `h1` con el `id="inicio"`.
- [ ] Una barra de navegación `<nav>` con una lista de enlaces que salten a las diferentes secciones (`#lugares`, `#itinerario`, `#glosario`).
- [ ] Una sección (`#lugares`) con una **lista no ordenada** de al menos 4 sitios recomendados.
- [ ] Una sección (`#itinerario`) con una **lista ordenada** que describa el paso a paso para recorrer la ciudad en un día.
- [ ] Una sección (`#glosario`) con una **lista de descripción** (`dl`) que explique 2 palabras o modismos típicos de ese lugar.
- [ ] Al menos un enlace externo con `target="_blank"` y `rel="noopener noreferrer"` hacia la página oficial de turismo.
- [ ] Un enlace al final de la página que te devuelva a `#inicio`.

Comprueba en tu navegador que cada enlace cumpla su función y que todas las listas mantengan su estructura limpia y semántica.

---

## 📚 Recursos y documentación oficial

Para profundizar en la creación de hipervínculos y listas, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Creación de hiperenlaces en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Creating_hyperlinks)
- 📖 [Listas en HTML (`<ul>`, `<ol>`, `<dl>`) - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/HTML_text_fundamentals#listas)
- 📖 [Referencia del elemento de navegación `<nav>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/nav)
