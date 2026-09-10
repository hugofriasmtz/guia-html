# Lección 6: Tablas de datos estructuradas

Esta lección continúa el trabajo tras dominar [Contenido embebido](../05-contenido-embebido/README.md). Ahora aprenderás a estructurar información tabular (horarios, reportes financieros, estadísticas, inventarios) de forma semántica y accesible para navegadores y lectores de pantalla.

> [!CAUTION]
> **Regla fundamental del diseño web:** Las tablas solo deben utilizarse para representar **datos tabulares** (información que tiene sentido en filas y columnas cruzadas). **Jamás** utilices tablas para maquetar la estructura visual o el diseño de tu página web; para eso existen CSS Flexbox y CSS Grid.

---

## 1. La estructura base y anatomía semántica

Una tabla HTML se organiza mediante filas horizontales (`<tr>` — *table row*). Dentro de cada fila se insertan celdas de encabezado (`<th>` — *table header*) o celdas de datos comunes (`<td>` — *table data*).

Para que la tabla tenga sentido semántico, se divide en tres secciones estructurales obligatorias en datos complejos: cabecera (`<thead>`), cuerpo (`<tbody>`) y pie (`<tfoot>`).

```html
<table>
  <caption>Horario Semanal de Entrenamiento</caption>
  <thead>
    <tr>
      <th>Día</th>
      <th>Disciplina</th>
      <th>Horas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lunes</td>
      <td>Natación</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Miércoles</td>
      <td>Ciclismo</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Viernes</td>
      <td>Atletismo</td>
      <td>1.5</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th>Total</th>
      <td>3 disciplinas</td>
      <td>6.5 hrs</td>
    </tr>
  </tfoot>
</table>
```

### Elementos semánticos de la tabla

| Etiqueta | Nombre | Propósito semántico |
| --- | --- | --- |
| `<table>` | Tabla | Contenedor principal de toda la estructura tabular. |
| `<caption>` | Título / Leyenda | Describe el propósito de la tabla. Debe ser **el primer elemento hijo** directo de `<table>`. |
| `<thead>` | Cabecera | Agrupa las filas con los nombres de las columnas. |
| `<tbody>` | Cuerpo | Agrupa las filas que contienen los datos reales. |
| `<tfoot>` | Pie de tabla | Agrupa las filas con resúmenes, promedios, totales o notas al pie. |
| `<tr>` | Fila (*Row*) | Cada línea horizontal dentro de la tabla. |
| `<th>` | Encabezado (*Header*) | Celda de título (el navegador la muestra en negrita y centrada). |
| `<td>` | Celda de datos (*Data*) | Celda estándar con el dato específico (alineada a la izquierda). |

### Qué observar en la estructura base

- **Ubicación de `<caption>`:** Siempre debe ir inmediatamente después de la etiqueta de apertura `<table>`. Los motores de búsqueda y lectores de pantalla lo usan como el título principal de la tabla.
- **Diferencia visual nativa:** El navegador renderiza las celdas `<th>` automáticamente en negrita y centradas, mientras que los `<td>` tienen texto regular y alineado a la izquierda.
- **El aspecto "desnudo" en HTML puro:** En HTML sin CSS, las tablas no tienen bordes visibles y el texto puede verse apretado. **No te preocupes, tu código no está roto.** Esto es completamente normal.
  - *Truco de depuración:* Puedes agregar temporalmente el atributo `<table border="1">` para visualizar la cuadrícula mientras estudias la estructura. Ten presente que esto es solo un apoyo visual provisional; en proyectos reales los bordes se definen exclusivamente mediante CSS.

### Práctica 1: Creando el esqueleto tabular (en `index.html`)

1. Crea tu archivo `index.html` con la estructura base de HTML5.
2. Construye una tabla con un `<caption>` que describa el inventario de una tienda de tecnología.
3. Define un `<thead>` con 3 columnas: *Producto*, *Stock* y *Precio*.
4. Agrega un `<tbody>` con al menos 2 productos diferentes.
5. Agrega un `<tfoot>` que indique la suma total de productos en stock.

---

## 2. Accesibilidad y relaciones de datos: el atributo `scope`

Las personas videntes comprenden una tabla mirando en dos dimensiones (arriba y a los lados al mismo tiempo). Sin embargo, una persona ciega que usa un lector de pantalla escucha la tabla **celda por celda de forma lineal**.

Para que el lector de pantalla no lea números o textos sueltos sin contexto, usamos el atributo **`scope`** dentro de cada `<th>`:

- **`scope="col"`**: Le indica al lector que ese título describe a **toda la columna vertical** descendente.
- **`scope="row"`**: Le indica al lector que ese título describe a **toda la fila horizontal** hacia la derecha.

```html
<table>
  <caption>Calificaciones del Examen Final</caption>
  <thead>
    <tr>
      <th scope="col">Estudiante</th>
      <th scope="col">Materia</th>
      <th scope="col">Nota Final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- scope="row" convierte a 'María González' en el título de esta fila -->
      <th scope="row">María González</th>
      <td>Bases de Datos</td>
      <td>95/100</td>
    </tr>
    <tr>
      <th scope="row">Luis Pérez</th>
      <td>Programación Web</td>
      <td>88/100</td>
    </tr>
  </tbody>
</table>
```

### Qué observar en el atributo `scope`

- Cuando el lector de pantalla llega a la celda `95/100`, no lee solo el número; anuncia: *"Nota Final, María González: 95/100"*. Gracias a `scope="col"` y `scope="row"`, la relación de datos nunca se pierde.
- `scope` es un atributo exclusivo de las celdas de encabezado `<th>`. **Nunca debe usarse en un `<td>`**.

> [!IMPORTANT]
> Una tabla accesible debe tener encabezados claros tanto en las columnas (`scope="col"`) como en las filas (`scope="row"`), a menos que sea una lista estrictamente unidireccional.

### Práctica 2: Tablas accesibles bidireccionales (en `index.html`)

1. En tu archivo `index.html`, modifica la tabla del inventario para que el nombre de cada producto sea una celda `<th scope="row">` en lugar de un `<td>`.
2. Asegúrate de que todos los títulos de la cabecera en `<thead>` tengan `scope="col"`.
3. Inspecciona en tu navegador cómo el nombre del producto ahora se resalta en negrita por ser un encabezado de fila semántico.

---

## 3. Fusión de celdas: `colspan` y `rowspan`

En reportes y tablas complejas, con frecuencia una celda debe extenderse para cubrir el espacio de varias columnas o de varias filas contiguas:

- **`colspan="N"`** (*column span*): Expande la celda horizontalmente hacia la derecha abarcando *N* columnas.
- **`rowspan="N"`** (*row span*): Expande la celda verticalmente hacia abajo abarcando *N* filas.

```text
COLSPAN (Fusión horizontal):
+-------------------------+------------+
|  colspan="2" (2 cols)   |  Columna 3 |
+-------------------------+------------+

ROWSPAN (Fusión vertical):
+-------------------------+----------------------+
|                         | Fila 1 - Columna 2   |
|  rowspan="2" (2 filas)  +----------------------+
|                         | Fila 2 - Columna 2   |
+-------------------------+----------------------+
```

### El modelo mental: "La matemática de celdas"

Piensa en una tabla como una cuadrícula matemática estricta:

> [!WARNING]
> Si tu tabla tiene **3 columnas en total**:
>
> - Cada fila normal debe sumar exactamente 3 celdas: `1 + 1 + 1 = 3`.
> - Si usas una celda con `colspan="2"`, esa celda ya cuenta por dos. Por lo tanto, en esa fila solo puedes agregar **una celda más** (`2 + 1 = 3`).
> - Si olvidas quitar la celda sobrante, la fila medirá 4 columnas y la tabla se deformará feamente hacia la derecha.

### Ejemplo de fusiones en acción

```html
<table>
  <caption>Reporte de Ventas Regionales</caption>
  <thead>
    <tr>
      <th scope="col">Región</th>
      <th scope="col">Mes</th>
      <th scope="col">Total Ventas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- Esta celda abarca verticalmente la fila actual y la siguiente -->
      <th scope="rowgroup" rowspan="2">Zona Norte</th>
      <td>Enero</td>
      <td>$12,000</td>
    </tr>
    <tr>
      <!-- ¡OJO! Aquí NO colocamos la celda de región porque ya la ocupa el rowspan superior -->
      <td>Febrero</td>
      <td>$15,000</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <!-- Abarca las primeras 2 columnas horizontalmente -->
      <th scope="row" colspan="2">Total Acumulado</th>
      <td>$27,000</td>
    </tr>
  </tfoot>
</table>
```

### Qué observar en la fusión de celdas

- **El efecto de `rowspan`:** En la segunda fila (`Febrero`), solo escribimos **dos celdas** (`<td>Febrero</td>` y `<td>$15,000</td>`). La primera posición ya está ocupada por el `rowspan="2"` que descendió desde la fila superior.
- **El valor `scope="rowgroup"`:** Cuando un `<th>` abarca múltiples filas mediante `rowspan`, el valor semántico más preciso para accesibilidad es `scope="rowgroup"`.
- **`colspan` en resúmenes:** En el pie de tabla (`<tfoot>`), `colspan="2"` permite que la leyenda "Total Acumulado" ocupe el ancho combinado de *Región* y *Mes*, dejando la última columna alineada exclusivamente con las cifras numéricas.

### Práctica 3: Dominando las fusiones (en `index.html`)

1. En tu `index.html`, modifica el `<tfoot>` de tu tabla para que la celda descriptiva ocupe las dos primeras columnas usando `colspan="2"`.
2. Agrega una categoría agrupada en `<tbody>`: utiliza `rowspan="2"` para agrupar dos productos que pertenezcan a la misma familia (ej. "Laptops"). Recuerda restar una celda en la segunda fila para no romper la cuadrícula.

---

## 4. Agrupación de columnas: `<colgroup>` y `<col>`

Cuando trabajas con tablas extensas y deseas aplicar identificadores, anchos o preparar estilos para columnas verticales completas sin tener que repetir clases en cientos de celdas `<td>`, HTML ofrece los elementos `<colgroup>` y `<col>`.

Se colocan **inmediatamente después del `<caption>`** y antes de `<thead>`:

```html
<table>
  <caption>Horario de Atención por Sucursal</caption>
  <!-- Definición estructural de columnas -->
  <colgroup>
    <col class="col-sucursal">
    <!-- El atributo span="2" aplica la definición a las siguientes 2 columnas juntas -->
    <col class="col-horarios" span="2">
  </colgroup>

  <thead>
    <tr>
      <th scope="col">Sucursal</th>
      <th scope="col">Turno Mañana</th>
      <th scope="col">Turno Tarde</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Centro</th>
      <td>08:00 - 13:00</td>
      <td>14:00 - 18:00</td>
    </tr>
    <tr>
      <th scope="row">Norte</th>
      <td>09:00 - 13:00</td>
      <td>15:00 - 19:00</td>
    </tr>
  </tbody>
</table>
```

### Qué observar en `<colgroup>` y `<col>`

- `<col>` es una etiqueta vacía (no requiere etiqueta de cierre `</col>`).
- El atributo `span="2"` indica que esa regla gobierna a dos columnas consecutivas de forma simultánea.
- **Efecto visual invisible:** `<col>` es una etiqueta de **definición estructural**. Al agregarla en HTML puro no verás ningún cambio visible en la pantalla (las columnas no cambiarán de color solas). Su función es organizar las columnas en el código y servir de ancla para cuando apliquemos CSS en módulos posteriores.

> [!NOTE]
> Para confirmar que tus etiquetas `<colgroup>` y `<col>` están bien escritas, abre las **Herramientas de Desarrollador del navegador (tecla F12)** y búscalas dentro de la pestaña *Elementos/Inspector*.

### Práctica 4: Estructurando columnas (en `index.html`)

1. Agrega un bloque `<colgroup>` a la tabla de tu `index.html` justo después del `<caption>`.
2. Define un `<col>` individual para la primera columna de productos y un `<col span="2">` para las dos columnas restantes (stock y precio).
3. Abre las herramientas de desarrollador (F12) e inspecciona la tabla para verificar que el navegador reconozca la estructura de columnas.

---

## Reto final de la lección: Tabla Comparativa de Planes de Precios

Ahora que experimentaste con cada elemento en tu laboratorio (`index.html`), demostrarás tu autonomía resolviendo un proyecto completo y desde cero.

Crea un archivo nuevo llamado **`reto.html`** dentro de tu carpeta `06-tablas-de-datos`. Construirás una **Tabla Comparativa de Planes de Suscripción para una Plataforma Cloud** que cumpla con todos los puntos de la siguiente lista de control:

- [ ] Estructura base completa de HTML5 con `<!DOCTYPE html>`, `<html>`, `<head>` y `<body>`.
- [ ] Un encabezado principal `<h1>Planes y Tarifas del Servicio Cloud</h1>`.
- [ ] Una etiqueta `<table>` con un `<caption>` claro y descriptivo.
- [ ] Un bloque `<colgroup>` que diferencie la columna de características de las columnas de los planes.
- [ ] Una sección `<thead>` con los nombres de las columnas:
  - *Características*, *Plan Básico*, *Plan Pro*, *Plan Enterprise*.
  - Todos los títulos con su atributo `scope="col"`.
- [ ] Una sección `<tbody>` con al menos 4 filas de características:
  - La primera celda de cada fila debe ser un `<th scope="row">` con el nombre de la función (ej. *Almacenamiento*, *Usuarios*, *Soporte*, *Copias de seguridad*).
  - Al menos una característica debe utilizar **`colspan`** (ejemplo: una función como *"Cifrado SSL de grado militar"* que abarque los 3 planes con un solo mensaje: *"Incluido en todos los planes"*).
  - Al menos una agrupación vertical usando **`rowspan`** (ejemplo: agrupar dos filas bajo la categoría *"Soporte Técnico"*).
- [ ] Una sección `<tfoot>` que resuma el costo mensual o la garantía de reembolso:
  - Debe usar `colspan` para alinear la leyenda con los valores finales.
- [ ] Estructura semántica impecable: sin celdas desalineadas ni filas rotas por mal cálculo de fusiones.

---

### Preguntas de autoevaluación

Intenta responder las preguntas mentalmente y luego despliega la sección para comprobar tus respuestas:

1. ¿Por qué está terminantemente prohibido usar tablas para maquetar la estructura visual de un sitio web?
2. ¿Cuál es la diferencia semántica y visual entre una celda `<th>` y una celda `<td>`?
3. ¿Para qué sirve exactamente el atributo `scope="col"` y en qué beneficia a una persona con discapacidad visual?
4. Si una tabla tiene 4 columnas en total y en una fila aplicas `colspan="3"` a la primera celda, ¿cuántas celdas más puedes agregar en esa misma fila?
5. ¿Por qué no vemos cambios visuales en pantalla al agregar `<colgroup>` y `<col>` en HTML puro?

---

## 📚 Recursos y documentación oficial

Para profundizar en la construcción de tablas y buenas prácticas de accesibilidad, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Conceptos básicos de tablas en HTML - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/HTML_table_basics)
- 📖 [Estructuras avanzadas y accesibilidad en tablas - MDN](https://developer.mozilla.org/es/docs/Learn_web_development/Core/Structuring_content/Advanced_HTML_table_features_and_accessibility)
- 📖 [Referencia del elemento `<table>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/table)
- 📖 [Uso del elemento `<colgroup>` y `<col>` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/colgroup)
- 📖 [El atributo de accesibilidad `scope` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/th#scope)
