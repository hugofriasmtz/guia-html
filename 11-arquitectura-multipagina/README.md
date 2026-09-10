# Lección 11: Arquitectura de sitios multipágina y navegación estructurada

Esta lección continúa la ruta tras dominar los estándares de [Accesibilidad y Validación](../10-accesibilidad-y-validacion/README.md). En el desarrollo profesional rara vez trabajarás en un solo archivo aislado; los sitios web reales están compuestos por decenas o cientos de documentos interconectados.

En este capítulo aprenderás a diseñar **arquitecturas de carpetas escalables**, dominar la **resolución de rutas relativas**, evitar los errores clásicos de enlaces rotos al trabajar en subcarpetas y construir sistemas de navegación consistentes y accesibles (como migas de pan o *breadcrumbs* y estados de página activa con `aria-current`).

---

## 1. Modelo mental: Árbol de directorios y resolución de rutas

Para que las páginas, imágenes y hojas de estilo se comuniquen entre sí, debes comprender cómo moverte hacia arriba o hacia abajo en el árbol de carpetas de tu proyecto:

```text
MI-SITIO-WEB/
│
├── index.html                  <-- Página de inicio (Raíz)
├── nosotros.html               <-- Página al mismo nivel
│
├── servicios/
│   ├── index.html              <-- Página principal de la sección
│   └── consultoria.html        <-- Subpágina anidada en la subcarpeta
│
└── assets/
    ├── css/
    │   └── estilos.css         <-- Hoja de estilos compartida
    └── img/
        └── logo.svg            <-- Imagen compartida
```

### Reglas matemáticas de navegación entre carpetas

```text
1. MISMO NIVEL:
   nosotros.html busca a index.html:           href="index.html" (o "./index.html")

2. BAJAR A UNA SUBCARPETA:
   index.html busca a consultoria.html:        href="servicios/consultoria.html"

3. SUBIR UN NIVEL HACIA ATRÁS (..):
   consultoria.html busca a nosotros.html:     href="../nosotros.html"

4. SUBIR Y VOLVER A ENTRAR EN OTRA CARPETA:
   consultoria.html busca el logo:             src="../assets/img/logo.svg"
```

### Qué observar en la resolución de rutas

- **Cada `../` equivale a dar un salto hacia atrás:** Si estás dos niveles adentro (ej. `tienda/ropa/camisas.html`) y necesitas llegar a la raíz, debes escribir `../../index.html` (un salto sale de `ropa/` y el segundo sale de `tienda/`).
- **Sensibilidad a mayúsculas:** En tu computadora personal (Windows o macOS) escribir `Logo.png` o `logo.png` puede funcionar igual, pero en servidores de producción (Linux) una mayúscula incorrecta causará un **error 404 de archivo no encontrado**. Nombra siempre carpetas y archivos en **minúsculas y separados por guiones** (`mi-pagina.html`).

### Práctica 1: Creando el árbol de laboratorio

1. Dentro de tu carpeta `11-sitio-multipagina`, crea una subcarpeta llamada `laboratorio/`.
2. Dentro de `laboratorio/`, crea un archivo `index.html` y una subcarpeta llamada `paginas/`.
3. Dentro de `paginas/`, crea un archivo llamado `detalle.html`.
4. En `index.html`, crea un enlace que baje hacia `paginas/detalle.html`.
5. En `detalle.html`, crea un enlace que use `../index.html` para regresar al inicio.
6. Abre `index.html` en el navegador y haz clic en ambos enlaces para comprobar que puedes ir y volver sin errores 404.

---

## 2. Rutas relativas vs. Rutas absolutas

Existen diferentes formas de apuntar a un recurso dependiendo del entorno donde se ejecute tu sitio:

| Tipo de Ruta | Sintaxis de ejemplo | ¿Cómo funciona en el navegador? | ¿Cuándo utilizarla? |
| --- | --- | --- | --- |
| **Relativa simple** | `href="contacto.html"` | Busca el archivo en la misma carpeta donde vive el documento actual. | Enlaces entre páginas hermanas en el mismo directorio. |
| **Relativa ascendente** | `href="../index.html"` | Retrocede un nivel en el árbol de carpetas antes de buscar. | Salir de subcarpetas hacia la raíz o hacia carpetas hermanas. |
| **Relativa a la raíz** | `href="/contacto.html"` | Inicia la búsqueda desde la raíz absoluta del dominio o servidor web. | Proyectos con servidores locales configurados o en producción. |
| **Absoluta externa** | `href="https://sitio.com"` | URL completa con protocolo (`https://`) y dominio. | Enlaces hacia sitios web externos ajenos a tu proyecto. |

> [!WARNING]
> **La trampa de la barra `/` inicial en GitHub Pages y modo local:**  
> Una ruta como `href="/nosotros.html"` funciona perfecto si usas *Live Server* en VS Code. Sin embargo:
>
> 1. Si abres el archivo con doble clic en tu explorador (`file:///C:/...`), la barra `/` buscará en la raíz de tu disco duro `C:\`, rompiendo todos los enlaces.
> 2. Si publicas tu proyecto en **GitHub Pages** en un subdirectorio (ej. `usuario.github.io/mi-proyecto/`), la barra `/` saltará a `usuario.github.io/nosotros.html` fuera de tu carpeta, provocando un error 404 generalizado.  
> **Regla de oro:** En sitios estáticos HTML puros, utiliza siempre **rutas relativas explícitas** (`./` y `../`).

### Qué observar en los tipos de ruta

- Las rutas relativas calculadas (`../`) garantizan la portabilidad total de tu proyecto: puedes mover toda la carpeta de tu sitio a otra computadora, memoria USB o servidor y ningún enlace se romperá.

### Práctica 2: Comprobando enlaces relativos y externos (en `laboratorio/`)

1. En el archivo `laboratorio/index.html`, añade un enlace hacia un sitio web externo oficial (como MDN) usando una ruta absoluta con `https://`, `target="_blank"` y `rel="noopener noreferrer"`.
2. Añade debajo un enlace relativo hacia `paginas/detalle.html`.
3. Inspecciona ambos enlaces en DevTools y comprueba cómo el navegador resuelve la URL destino en la esquina inferior izquierda antes de hacer clic.

---

## 3. El error clásico del desarrollador junior: Recursos en subcarpetas

El error más común al trabajar en sitios multipágina ocurre cuando se copia y pega la cabecera `<head>` de `index.html` en una página dentro de una subcarpeta:

```html
<!-- Archivo: index.html (Ubicado en la raíz) -->
<head>
  <!-- ✅ CORRECTO para la raíz: el archivo está en assets/ -->
  <link rel="stylesheet" href="assets/css/estilos.css">
</head>
```

Si copias y pegas esa misma línea en `servicios/consultoria.html`:

```html
<!-- Archivo: servicios/consultoria.html (Ubicado en la subcarpeta) -->
<head>
  <!-- ❌ ERROR: El navegador buscará 'servicios/assets/css/estilos.css' que NO existe -->
  <link rel="stylesheet" href="assets/css/estilos.css">

  <!-- ✅ CORRECTO: Debe subir un nivel para encontrar la carpeta assets/ -->
  <link rel="stylesheet" href="../assets/css/estilos.css">
</head>
```

```text
CUANDO EL NAVEGADOR INTENTA CARGAR EL CSS:
servicios/consultoria.html con href="assets/css/estilos.css":
  Busca en: mi-sitio/servicios/assets/css/estilos.css ----> ❌ ERROR 404 (Página sin estilos)

servicios/consultoria.html con href="../assets/css/estilos.css":
  Sube a:   mi-sitio/
  Entra en: mi-sitio/assets/css/estilos.css           ----> ✅ ÉXITO 200 (Estilos cargados)
```

### Qué observar al enlazar recursos desde subcarpetas

- Cada vez que crees una subcarpeta, **todos los enlaces cambian de perspectiva**: los archivos CSS, los scripts JS, las imágenes del logo y los enlaces del menú deben actualizar sus rutas con `../` para compensar la profundidad.
- Si abres una subpágina y notas que perdió el diseño o las imágenes aparecen rotas, abre la pestaña **Red (Network)** o la **Consola** de DevTools: verás los errores en rojo indicando exactamente qué ruta falló.

### Práctica 3: Enlazando recursos en profundidad (en `laboratorio/`)

1. Dentro de `laboratorio/`, crea una carpeta `css/` con un archivo `estilos.css` que tenga:  
   `body { background-color: #f0fdf4; font-family: sans-serif; }`
2. Enlaza el CSS en `laboratorio/index.html` usando `href="css/estilos.css"`.
3. Ahora enlaza el mismo CSS en `laboratorio/paginas/detalle.html` utilizando la ruta ascendente correcta: `href="../css/estilos.css"`.
4. Abre ambos archivos en el navegador y comprueba que ambos compartan el mismo fondo visual.

---

## 4. Navegación global consistente y estado activo (`aria-current`)

En un sitio multipágina profesional, la estructura de la cabecera (`<header>`) y del pie de página (`<footer>`) debe mantenerse simétrica e idéntica en todas las vistas para no desorientar al usuario.

Para que los usuarios que ven la pantalla y aquellos que usan tecnologías de asistencia sepan con certeza en qué página están ubicados, se utiliza el atributo oficial de accesibilidad **`aria-current="page"`**:

### 1. En la página de inicio (`laboratorio/index.html`)

```html
<header>
  <nav aria-label="Navegación principal">
    <ul>
      <!-- aria-current le indica al lector de pantalla: 'Esta es la página actual' -->
      <li><a href="index.html" aria-current="page" class="activo">Inicio</a></li>
      <li><a href="paginas/detalle.html">Detalle</a></li>
    </ul>
  </nav>
</header>
```

### 2. En la subpágina (`laboratorio/paginas/detalle.html`)

```html
<header>
  <nav aria-label="Navegación principal">
    <ul>
      <!-- Nota cómo las rutas se ajustan a la perspectiva de esta subcarpeta -->
      <li><a href="../index.html">Inicio</a></li>
      <li><a href="detalle.html" aria-current="page" class="activo">Detalle</a></li>
    </ul>
  </nav>
</header>
```

### Qué observar en la navegación consistente

- **Doble función:** La clase CSS `.activo` le da estilos visuales al botón (ej. un borde inferior o color distintivo), mientras que `aria-current="page"` hace que el lector de pantalla anuncie explícitamente: *"Inicio, enlace, página actual"*.
- **Ajuste de rutas del menú:** Observa con atención cómo el enlace a "Inicio" es `href="index.html"` en la raíz, pero se convierte en `href="../index.html"` cuando el menú vive en una subcarpeta. El menú debe adaptarse a la ubicación del archivo que lo aloja.

> [!NOTE]
> `aria-current` solo debe colocarse en un único enlace por página (aquel que apunta a la vista que está abierta en ese momento).

### Práctica 4: El menú sincronizado (en `laboratorio/`)

1. Copia el menú de navegación correspondiente en `laboratorio/index.html` y en `laboratorio/paginas/detalle.html`.
2. Navega entre ambas páginas haciendo clic en el menú.
3. Abre las herramientas de desarrollador (F12) en el panel de Accesibilidad e inspecciona el enlace activo: comprueba cómo el navegador le asigna el estado accesible `current: page`.

---

## 5. Migas de pan semánticas (*Breadcrumbs*)

Las migas de pan indican la jerarquía estructural de páginas secundarias o anidadas. Permiten que el usuario entienda dónde está parado y le facilitan regresar a secciones superiores con un solo clic.

```html
<!-- Ubicación del archivo: servicios/consultoria.html -->
<nav aria-label="Migas de pan" class="breadcrumbs">
  <ol>
    <li><a href="../index.html">Inicio</a></li>
    <li><a href="index.html">Servicios</a></li>
    <li aria-current="page">Consultoría Estratégica</li>
  </ol>
</nav>
```

### ¿Por qué se utiliza `<ol>` (Lista ordenada) en lugar de `<ul>`?

El estándar de accesibilidad del W3C exige que las migas de pan se construyan con **`<ol>` (ordered list)** por una razón semántica estricta:

> [!IMPORTANT]
> Una miga de pan no es un listado cualquiera; **representa una jerarquía lineal estricta con orden de procedencia** (Nivel 1: Raíz $\rightarrow$ Nivel 2: Categoría $\rightarrow$ Nivel 3: Vista actual). Si cambias el orden de los elementos, la ruta pierde todo su significado lógico. Al usar `<ol>`, los lectores de pantalla anuncian al usuario: *"Elemento 1 de 3: Inicio; Elemento 2 de 3: Servicios; Elemento 3 de 3: Consultoría"*.

### Qué observar en las migas de pan

- **La última posición no lleva enlace:** La página en la que el usuario ya se encuentra (`Consultoría Estratégica`) se escribe como texto plano dentro del `<li>` y se marca con `aria-current="page"`. No tiene sentido colocar un enlace que apunte a la misma página donde ya estás.
- **Separadores visuales:** Los símbolos separadores (como `/` o `>`) deben agregarse preferentemente mediante CSS (`::after`) o con caracteres que tengan `aria-hidden="true"` para que los lectores de pantalla no lean *"Inicio barra Servicios barra Consultoría"*.

### Práctica 5: Construyendo migas de pan (en `laboratorio/`)

1. En el archivo `laboratorio/paginas/detalle.html`, agrega una barra de migas de pan semántica justo antes del encabezado `<h1>`.
2. Utiliza la estructura `<nav aria-label="Migas de pan"><ol>...`.
3. Asegúrate de que el enlace de retorno a "Inicio" use `../index.html` y que la posición final sea texto plano con `aria-current="page"`.

---

## 6. Arquitectura profesional de proyectos estáticos

A medida que un sitio web crece, una estructura de carpetas desordenada genera enlaces rotos y dificulta el mantenimiento en equipo. La arquitectura estándar en la industria sigue esta distribución modular:

```text
mi-proyecto/
│
├── index.html                   # Portada principal (Home)
├── nosotros.html                # Vista institucional
├── contacto.html                # Formulario de contacto
│
├── servicios/                   # Subsección temática
│   ├── index.html               # Catálogo general de servicios
│   └── consultoria.html         # Ficha específica de un servicio
│
└── assets/                      # Recursos compartidos (Estáticos)
    ├── css/
    │   └── estilos.css          # Reglas de estilo globales
    ├── js/
    │   └── main.js              # Lógica interactiva
    └── img/
        ├── brand/               # Identidad: logo.svg, favicon.ico
        └── content/             # Contenido: fotos de artículos, banners
```

---

## Reto final de la lección: Sitio Web Multipágina para una Agencia Creativa

Ahora que dominas las rutas relativas, la navegación consistente y las migas de pan en el laboratorio, demostrarás tu autonomía construyendo un proyecto web multipágina completo y profesional desde cero.

Crea una subcarpeta llamada **`proyecto/`** dentro de tu carpeta `11-sitio-multipagina`. Construirás el sitio web de **"Studio Pixel - Agencia de Diseño y Desarrollo Web"** con **4 vistas interconectadas** que cumpla estrictamente con la siguiente lista de verificación:

### 1. Estructura de carpetas y archivos

Crea exactamente la siguiente arquitectura física dentro de `proyecto/`:

```text
proyecto/
├── index.html                   # Vista 1: Portada de la agencia
├── nosotros.html                # Vista 2: Quiénes somos y equipo
├── contacto.html                # Vista 3: Formulario de contacto
├── servicios/
│   └── desarrollo-web.html      # Vista 4: Ficha especializada en subcarpeta
└── assets/
    ├── css/
    │   └── main.css             # Estilo común con colores de marca
    └── img/
        └── logo.svg             # Logotipo compartido (puede ser un SVG simple)
```

### 2. Requisitos de desarrollo y navegación

- [ ] **Estructura base completa de HTML5:** En los 4 archivos con su `<!DOCTYPE html>`, `<html lang="es">` y metadatos individuales (`<title>` y `<meta name="description">` únicos y adaptados a cada página).
- [ ] **Hoja de estilos compartida:** Las 4 páginas deben conectarse con éxito a `assets/css/main.css` (recuerda usar la ruta relativa adecuada en `desarrollo-web.html`).
- [ ] **Navegación global idéntica:**
  - Las 4 páginas deben tener la misma barra de navegación dentro de `<nav aria-label="Navegación principal">`.
  - Los enlaces deben tener sus rutas relativas correctamente resueltas según la ubicación de cada archivo.
  - El atributo `aria-current="page"` debe estar colocado **únicamente en el enlace correspondiente a la página activa** en cada uno de los 4 archivos.
- [ ] **Migas de pan en la subpágina:**
  - El archivo `servicios/desarrollo-web.html` debe incluir una barra de migas de pan accesible construida con `<nav aria-label="Migas de pan">` y una lista ordenada `<ol>`.
  - Debe permitir regresar a Inicio (`index.html`) con una ruta relativa ascendente funcional.
  - El último elemento debe ser el título de la página actual sin enlace y con `aria-current="page"`.
- [ ] **Pie de página consistente:** Un `<footer>` simétrico en las 4 páginas con derechos reservados y enlaces secundarios relativos.
- [ ] **Cero enlaces rotos:** Navega por las 4 páginas en tu navegador asegurándote de que ningún enlace o recurso arroje error 404 en la consola de DevTools.
- [ ] **Validación W3C:** Pasa los 4 archivos por el [Nu Html Checker del W3C](https://validator.w3.org/nu/) asegurando **0 errores sintácticos**.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. Si estás editando el archivo `servicios/desarrollo-web.html`, ¿qué ruta relativa exacta debes escribir para enlazar una hoja de estilos situada en `assets/css/main.css`?
2. ¿Por qué es una mala práctica técnica utilizar rutas que inician con una barra diagonal (ej. `href="/nosotros.html"`) en proyectos estáticos que se van a publicar en plataformas como GitHub Pages?
3. ¿Por qué las pautas de accesibilidad del W3C exigen que las migas de pan (*breadcrumbs*) se maqueten con una lista ordenada `<ol>` en lugar de una lista desordenada `<ul>`?
4. ¿Qué función cumple el atributo `aria-current="page"` y por qué no es suficiente con cambiar únicamente el color del enlace activo con una clase de CSS?
5. ¿Qué diferencia práctica existe entre escribir `href="contacto.html"`, `href="./contacto.html"` y `href="../contacto.html"`?

---

## 📚 Recursos y documentación oficial

Para profundizar en la navegación web, estructuración de URLs y buenas prácticas de enlazado, consulta la documentación de **MDN Web Docs**:

- 📖 [Creando hipervínculos y rutas relativas en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Creating_hyperlinks)
- 📖 [Patrón de diseño accesible de Migas de Pan (Breadcrumb Pattern) - W3C WAI](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)
- 📖 [El atributo de navegación `aria-current` - MDN](https://developer.mozilla.org/es/docs/Web/Accessibility/ARIA/Attributes/aria-current)
- 📖 [Estructura del documento y URLs en la web - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL)
- 🌐 [Nu Html Checker - Validador Oficial del W3C](https://validator.w3.org/nu/)
