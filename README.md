# GUIAS PARA APRENDER HTML5

![HTML5](/assets/html.png)

**Ruta práctica, moderna y orientada a proyectos para dominar HTML5, semántica y accesibilidad web.**

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/es/docs/Web/HTML)
[![W3C Valid](https://img.shields.io/badge/W3C-Standards-blue?style=for-the-badge&logo=w3c&logoColor=white)](https://validator.w3.org/nu/)
[![A11y](https://img.shields.io/badge/Accessibility-WCAG%20AA-success?style=for-the-badge)](https://www.w3.org/WAI/standards-guidelines/wcag/)

---

## 🎯 Sobre este curso

Este repositorio es una guía completa y estructurada paso a paso para aprender desarrollo web con **HTML5 moderno**. No busca que memorices etiquetas, sino que entiendas el **modelo mental**, la **semántica**, la **accesibilidad (A11y)** y las buenas prácticas que exige la industria actual.

> [!TIP]
> **Antes de comenzar:** Prepara tu editor de código (VS Code) y las extensiones recomendadas en la guía de [Configuración del entorno](configuracion/README.md).

---

## 🗺️ Ruta de Aprendizaje

El curso está organizado en **4 fases progresivas** que cubren desde la sintaxis básica hasta proyectos completos de nivel profesional:

### Fase 1: Fundamentos y Semántica Estructural

* 📄 **[01. Estructura HTML5](01-estructura-html/README.md):** El esqueleto base (`html`, `head`, `body`), DOCTYPE y flujo del navegador.
* ✍️ **[02. Texto y Atributos](02-texto-y-atributos/README.md):** Jerarquía de encabezados (`h1`-`h6`), párrafos, formateo semántico y atributos globales.
* 🔗 **[03. Enlaces y Listas](03-enlaces-y-listas/README.md):** Hipervínculos absolutos/relativos, listas ordenadas, desordenadas y de definición.
* 🧱 **[04. Agrupación Semántica](04-agrupacion-semantica/README.md):** Layout moderno con `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>` y `<footer>`.

### Fase 2: Contenido, Datos e Interactividad

* 🖼️ **[05. Contenido Embebido](05-contenido-embebido/README.md):** Imágenes responsivas (`picture`/`srcset`), audio, video nativo con subtítulos e `iframes`.
* 📊 **[06. Tablas de Datos](06-tablas-de-datos/README.md):** Estructuración accesible de datos tabulares (`caption`, `thead`, `tbody`, `scope`, `colspan`/`rowspan`).
* 📝 **[07. Formularios Modernos](07-formularios-modernos/README.md):** Captura de datos, validación nativa sin JS, tipos de `input`, `datalist` y `fieldset`.
* ⚡ **[08. Elementos Interactivos](08-elementos-interactivos/README.md):** Componentes nativos como `<details>`, acordeones, modales con `<dialog>`, `<progress>`, `<meter>` y Popover API.

### Fase 3: Integración, SEO y Accesibilidad

* 🌐 **[09. Metadatos e Integración](09-metadatos-e-integracion/README.md):** Optimización `<head>`, SEO técnico, Open Graph para redes sociales, favicons y scripts (`defer`/`async`).
* ♿ **[10. Accesibilidad y Validación](10-accesibilidad-y-validacion/README.md):** Estándares WCAG, reglas de WAI-ARIA, navegación por teclado y validación oficial del W3C.
* 🗂️ **[11. Sitio Multipágina](11-sitio-multipagina/README.md):** Arquitectura de carpetas escalable, rutas relativas, `aria-current="page"` y migas de pan (*breadcrumbs*).

### Fase 4: Proyectos Reales

* 🚀 **[12. Proyecto Guiado: Landing Page SaaS](12-proyecto-guiado-landing/README.md):** Integración de todos los conceptos construyendo una landing page real estilizada con Pico CSS.
* 🏆 **[13. Desafío Técnico Final](13-desafio-tecnico-final/README.md):** Prueba técnica autónoma sin ayuda para poner a prueba tu dominio profesional.

---

## 🔄 Metodología de Estudio

Para aprovechar al máximo cada lección, sigue este ciclo de aprendizaje activo:

```text
[ 1. Leer Teoría y Modelo Mental ]
               │
               ▼
[ 2. Escribir y Probar los Ejemplos en el Navegador ]
               │
               ▼
[ 3. Romper el Código y Experimentar ]
               │
               ▼
[ 4. Resolver el Reto con su Checklist ]
               │
               ▼
[ 5. Responder las Preguntas de Autoevaluación ]
```

> [!IMPORTANT]
> No avances de lección hasta haber completado el reto práctico y comprobar que tu código no contenga errores de validación.

---

## 📁 Estructura del Repositorio

```text
.
├── configuracion/                  # Configuración de herramientas y extensiones
├── 01-estructura-html/             # Lección 01 + Reto práctico
├── 02-texto-y-atributos/           # Lección 02 + Reto práctico
├── 03-enlaces-y-listas/            # Lección 03 + Reto práctico
├── 04-agrupacion-semantica/        # Lección 04 + Reto práctico
├── 05-contenido-embebido/          # Lección 05 + Reto práctico
├── 06-tablas-de-datos/             # Lección 06 + Reto práctico
├── 07-formularios-modernos/        # Lección 07 + Reto práctico
├── 08-elementos-interactivos/      # Lección 08 + Reto práctico
├── 09-metadatos-e-integracion/     # Lección 09 + Reto práctico
├── 10-accesibilidad-y-validacion/  # Lección 10 + Reto práctico
├── 11-arquitectura-multipagina/    # Lección 11 + Reto práctico
├── 12-proyecto-guiado-landing/     # Proyecto integral con diseño
├── 13-desafio-tecnico-final/       # Prueba técnica autónoma
└── README.md                       # Este índice general
```

---

## 🛠️ Requisitos previos

* Un editor de código (**Visual Studio Code** recomendado).
* Un navegador moderno (**Google Chrome**, **Mozilla Firefox** o **Brave**).
* Ganas de escribir código limpio, experimentar y construir proyectos reales.

---

## 📚 Documentación y Enlaces Oficiales

* 📖 [MDN Web Docs - Referencia oficial de HTML](https://developer.mozilla.org/es/docs/Web/HTML)
* 🌐 [Validador oficial de código Nu HTML Checker (W3C)](https://validator.w3.org/nu/)
* ♿ [Iniciativa de Accesibilidad Web (WAI - W3C)](https://www.w3.org/WAI/)

---
