# Cómo Ocultar Totales en KendoPivotGrid

Este documento explica las diferentes formas de ocultar filas, columnas y celdas de totales en un KendoPivotGrid de Kendo UI jQuery.

## Métodos Disponibles

### 1. Configuración en el DataSource (Recomendado)

La forma más eficiente es configurar los totales directamente en el DataSource:

```javascript
$("#pivotgrid").kendoPivotGrid({
    dataSource: {
        // ... otras configuraciones
        totals: {
            rows: false,    // Ocultar filas de totales
            columns: false  // Ocultar columnas de totales
        }
    }
});
```

**Para alternar dinámicamente:**
```javascript
function toggleTotals() {
    var dataSource = pivotGrid.dataSource;
    dataSource.options.totals = {
        rows: !dataSource.options.totals.rows,
        columns: !dataSource.options.totals.columns
    };
    dataSource.read();
}
```

### 2. CSS para Ocultar Totales

Puedes usar CSS para ocultar totales específicos:

```css
/* Ocultar todos los totales */
.hide-totals .k-pivotgrid-total {
    display: none !important;
}

/* Ocultar solo filas de totales */
.hide-total-rows .k-pivotgrid-total-row {
    display: none !important;
}

/* Ocultar solo columnas de totales */
.hide-total-columns .k-pivotgrid-total-column {
    display: none !important;
}
```

**JavaScript para aplicar las clases:**
```javascript
function hideAllTotals() {
    $("#pivotgrid").addClass("hide-totals");
}

function hideTotalRows() {
    $("#pivotgrid").addClass("hide-total-rows");
}

function hideTotalColumns() {
    $("#pivotgrid").addClass("hide-total-columns");
}

function showAllTotals() {
    $("#pivotgrid").removeClass("hide-totals hide-total-rows hide-total-columns");
}
```

### 3. Configuración Inicial sin Totales

Si quieres que el PivotGrid nunca muestre totales, configura así desde el inicio:

```javascript
$("#pivotgrid").kendoPivotGrid({
    dataSource: {
        // ... otras configuraciones
        totals: {
            rows: false,
            columns: false
        }
    }
});
```

## Ejemplos Prácticos

### Para tu implementación actual (pivot-v3.html)

Basándome en tu archivo `pivot-v3.html`, aquí están las modificaciones que necesitas:

1. **Agregar configuración de totales en el DataSource:**
```javascript
dataSource: {
    // ... configuración existente
    totals: {
        rows: false,    // Cambiar a true si quieres mostrar
        columns: false  // Cambiar a true si quieres mostrar
    }
}
```

2. **Agregar CSS para control dinámico:**
```css
.hide-totals .k-pivotgrid-total {
    display: none !important;
}
.hide-total-rows .k-pivotgrid-total-row {
    display: none !important;
}
.hide-total-columns .k-pivotgrid-total-column {
    display: none !important;
}
```

3. **Agregar funciones JavaScript:**
```javascript
function hideAllTotals() {
    $("#pivotgrid").addClass("hide-totals");
}

function showAllTotals() {
    $("#pivotgrid").removeClass("hide-totals");
}

function toggleTotalsDataSource() {
    var dataSource = pivotGrid.dataSource;
    var currentTotals = dataSource.options.totals;
    
    dataSource.options.totals = {
        rows: !currentTotals.rows,
        columns: !currentTotals.columns
    };
    
    dataSource.read();
}
```

## Ventajas y Desventajas

### Método 1 (DataSource)
**Ventajas:**
- Más eficiente en rendimiento
- Los datos no se calculan
- Cambios inmediatos

**Desventajas:**
- Requiere recargar los datos

### Método 2 (CSS)
**Ventajas:**
- Cambios instantáneos
- No requiere recargar datos
- Más flexible para estilos

**Desventajas:**
- Los datos siguen calculándose
- Puede afectar el rendimiento con grandes datasets

## Recomendaciones

1. **Para ocultar totales permanentemente:** Usa la configuración del DataSource
2. **Para alternar totales dinámicamente:** Usa CSS para cambios rápidos
3. **Para control granular:** Combina ambos métodos

## Archivos de Ejemplo

- `pivot-hide-totals.html`: Ejemplo completo con los 3 métodos
- `pivot-v3-hide-totals.html`: Versión modificada de tu archivo actual

## Notas Importantes

- Los selectores CSS pueden variar según la versión de Kendo UI
- Siempre prueba en tu entorno específico
- Considera el impacto en el rendimiento con datasets grandes
- Los totales se calculan en el servidor, por lo que ocultarlos con CSS no mejora el rendimiento del cálculo