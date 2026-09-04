# Lección 6: Tablas de datos estructuradas

Esta lección continúa el trabajo de [Contenido embebido](../05-contenido-embebido/README.md). Aprenderás a estructurar información tabular (horarios, listas de precios, estadísticas, inventarios) de forma semántica y accesible para navegadores y lectores de pantalla.

> [!CAUTION]
> **Regla fundamental del diseño web:** Las tablas solo deben utilizarse para representar **datos tabulares** (filas y columnas con relaciones de datos). Nunca utilices tablas para crear la estructura visual o el diseño de tu página web.

---

## 1. La estructura base de una tabla

Una tabla HTML se organiza mediante filas horizontales (`<tr>` - *table row*). Dentro de cada fila se colocan las celdas de encabezado (`<th>` - *table header*) o las celdas de datos comunes (`<td>` - *table data*).

```html
<table>
  <caption>Horario de Clases de Programación</caption>
  <thead>
    <tr>
      <th scope="col">Día</th>
      <th scope="col">Materia</th>
      <th scope="col">Profesor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lunes</td>
      <td>HTML5 Semántico</td>
      <td>Carlos Silva</td>
    </tr>
    <tr>
      <td>Miércoles</td>
      <td>CSS Moderno</td>
      <td>Ana Morales</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Total de horas semanales</td>
      <td>6 horas</td>
    </tr>
  </tfoot>
</table>
```

---

## 2. Elementos semánticos de una tabla

| Etiqueta | Nombre | ¿Para qué sirve? |
| --- | --- | --- |
| `<table>` | Tabla | Contenedor principal de toda la estructura tabular. |
| `<caption>` | Título / Leyenda | Describe el propósito de la tabla (debe ser el **primer elemento hijo** directo de `table`). |
| `<thead>` | Cabecera | Agrupa las filas que contienen los títulos de las columnas. |
| `<tbody>` | Cuerpo | Agrupa las filas con los datos principales de la tabla. |
| `<tfoot>` | Pie de tabla | Agrupa las filas con totales, resúmenes, promedios o notas finales. |
| `<tr>` | Fila (*Row*) | Cada línea horizontal dentro de la tabla. |
| `<th>` | Encabezado (*Header cell*) | Celda con título de fila o columna (el navegador la muestra en negrita y centrada). |
| `<td>` | Celda de Datos (*Data cell*) | Celda que contiene la información regular. |

---

## 3. Accesibilidad en tablas: el atributo `scope`

El atributo `scope` en las etiquetas `<th>` es fundamental para que las personas que usan lectores de pantalla comprendan si el título describe a una columna o a una fila:

- `scope="col"`: Indica que el encabezado describe a toda la **columna vertical**.
- `scope="row"`: Indica que el encabezado describe a toda la **fila horizontal**.

```html
<tr>
  <!-- scope="row" le dice al lector de pantalla que este título aplica a toda la fila -->
  <th scope="row">Plan Profesional</th>
  <td>$29 / mes</td>
  <td>Soporte 24/7</td>
</tr>
```

---

## 4. Fusión de celdas: `colspan` y `rowspan`

A veces una celda necesita expandirse para ocupar el espacio de varias columnas o varias filas:

- **`colspan="N"`** (*column span*): Expande la celda hacia la derecha a través de *N* columnas.
- **`rowspan="N"`** (*row span*): Expande la celda hacia abajo a través de *N* filas.

```text
COLSPAN (Une columnas horizontalmente):
+-------------------------+------------+
|        Colspan 2        |  Columna 3 |
+-------------------------+------------+

ROWSPAN (Une filas verticalmente):
+--------------+-----------------------+
|              | Fila 1 - Columna 2    |
|  Rowspan 2   +-----------------------+
|              | Fila 2 - Columna 2    |
+--------------+-----------------------+
```

### Ejemplo con fusión de celdas

```html
<table>
  <caption>Reporte de Ventas Trimestrales</caption>
  <thead>
    <tr>
      <th scope="col">Región</th>
      <th scope="col">Mes</th>
      <th scope="col">Ventas ($)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- Ocupa 2 filas hacia abajo -->
      <th scope="rowgroup" rowspan="2">Norte</th>
      <td>Enero</td>
      <td>$15,000</td>
    </tr>
    <tr>
      <td>Febrero</td>
      <td>$18,000</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <!-- Ocupa 2 columnas hacia la derecha -->
      <th scope="row" colspan="2">Total acumulado</th>
      <td>$33,000</td>
    </tr>
  </tfoot>
</table>
```

> [!WARNING]
> Ten cuidado al calcular `colspan` y `rowspan`. Si expandes una celda con `colspan="2"`, debes eliminar una celda `<td>` en esa misma fila; de lo contrario, la tabla se descuadrará hacia la derecha.

---

## Reto final de la lección

Crea una **Tabla Comparativa de Planes de Precios** para un servicio digital en tu archivo `index.html`:

- [x] Un `<caption>` descriptivo sobre los planes de suscripción.
- [x] Una sección `<thead>` con los nombres de los planes y el atributo `scope="col"`.
- [x] Una sección `<tbody>` con al menos 4 características comparadas, usando `scope="row"` en la primera celda de cada fila.
- [x] Al menos una celda que utilice `colspan` (por ejemplo, una característica que aplique a todos los planes) o `rowspan`.
- [x] Una sección `<tfoot>` con el precio total o un resumen de garantía.

### Preguntas de autoevaluación

1. ¿Por qué está prohibido usar tablas para maquetar el diseño visual de una página web?
2. ¿Cuál es la diferencia semántica entre una celda `<th>` y una celda `<td>`?
3. ¿Para qué sirve el atributo `scope="col"` en un encabezado de tabla?
4. ¿Qué sucede si aplicas `colspan="2"` pero olvidas quitar la celda sobrante de la fila?

---

## 📚 Recursos y documentación oficial

Para profundizar en la estructura de tablas en HTML y estándares de accesibilidad, consulta la documentación oficial de **MDN Web Docs**:

- 📖 [Tablas en HTML - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/table)
- 📖 [Accesibilidad en tablas - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Tables)
- 📖 [Atributo `scope` - MDN](https://developer.mozilla.org/es/docs/Web/HTML/Element/th#attr-scope)

---
