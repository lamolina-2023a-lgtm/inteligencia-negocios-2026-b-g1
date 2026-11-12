# Código fuente – EcoHogar del Huila (2025)

**Proyecto de aula – Inteligencia de Negocios**

**Integrantes:**
- Yury Lorena Castañeda Cedeño
- Larissa Alexandra Molina Borja

## 1. Herramientas utilizadas

- **Excel:** almacenamiento de los datos de ventas de 2025.
- **Power Query (lenguaje M):** extracción, transformación y limpieza de datos.
- **Power BI Desktop:** modelado, creación de medidas DAX y visualización interactiva.

## 2. Código de transformación de datos (Power Query)

La tabla principal `FactVentas_Origen` fue procesada mediante las siguientes operaciones:

1. Importación del archivo Excel.
2. Promoción de encabezados.
3. Asignación de tipos de datos.
4. Eliminación de registros duplicados mediante `ID_Factura`.
5. Normalización de campos de texto a mayúsculas.
6. Cálculo de ventas, costos y utilidad bruta.

### Fragmentos principales del código M

**Eliminar duplicados:**

```powerquery
#"Duplicados quitados" =
    Table.Distinct(#"Tipo cambiado", {"ID_Factura"})
```

**Normalizar textos:**

```powerquery
#"Texto en mayúsculas" =
    Table.TransformColumns(
        #"Duplicados quitados",
        {
            {"Sede_Origen", Text.Upper, type text},
            {"Canal_Origen", Text.Upper, type text},
            {"Tipo_Cliente_Origen", Text.Upper, type text}
        }
    )
```

**Calcular ventas:**

```powerquery
#"Personalizada agregada" =
    Table.AddColumn(
        #"Texto en mayúsculas",
        "Venta_Total",
        each [Cantidad] * [Precio_Unitario] * (1 - [Descuento])
    )
```

**Calcular costos:**

```powerquery
#"Personalizada agregada1" =
    Table.AddColumn(
        #"Personalizada agregada",
        "Costo_Total",
        each [Cantidad] * [Costo_Unitario]
    )
```

**Calcular utilidad bruta:**

```powerquery
#"Personalizada agregada2" =
    Table.AddColumn(
        #"Personalizada agregada1",
        "Utilidad_Bruta",
        each [Venta_Total] - [Costo_Total]
    )
```

## 3. Medidas DAX utilizadas

**Ventas Totales 2025**

```dax
Ventas Totales 2025 =
SUM(FactVentas_Origen[Venta_Total])
```

**Costos Totales 2025**

```dax
Costos Totales 2025 =
SUM(FactVentas_Origen[Costo_Total])
```

**Utilidad Bruta 2025**

```dax
Utilidad Bruta 2025 =
[Ventas Totales 2025] - [Costos Totales 2025]
```

**Margen Bruto %**

```dax
Margen Bruto % =
DIVIDE([Utilidad Bruta 2025], [Ventas Totales 2025], 0)
```

**Unidades Vendidas 2025**

```dax
Unidades Vendidas 2025 =
SUM(FactVentas_Origen[Cantidad])
```

## 4. Modelo de datos

Se utilizó un modelo dimensional tipo estrella, compuesto por:

- **Tabla de hechos:** `FactVentas_Origen`.
- **Dimensiones:** `DimCalendario`, `DimCanal`, `DimCliente`, `DimProducto` y `DimSede`.

Las dimensiones permiten analizar las ventas por fecha, canal, tipo de cliente, producto y sede.

## 5. Indicadores del tablero

| Indicador | Resultado general de 2025 |
|---|---:|
| Ventas totales | $2.719.167.200 COP |
| Costos totales | $2.012.205.000 COP |
| Utilidad bruta | $706.962.200 COP |
| Margen bruto | 26,00 % |
| Unidades vendidas | 2.557 |

Los indicadores se recalculan cuando se aplican filtros en el tablero.

## 6. Visualizaciones y mejoras realizadas

El dashboard incluye:

- Gráfico de líneas para analizar las ventas mensuales.
- Gráfico de barras para comparar Neiva Centro y Neiva Norte.
- Gráfico circular para comparar los tipos de clientes.
- Segmentadores interactivos por sede y tipo de cliente.
- Cinco tarjetas KPI.
- Narrativa con contexto, hallazgo y recomendación.

Se mejoró la presentación visual mediante una paleta de azul petróleo y verde esmeralda, un encabezado destacado y una distribución más organizada de los indicadores.

## 7. Archivos del proyecto

El repositorio contiene el archivo Excel con los datos, el archivo `.pbix` original, la versión mejorada del dashboard, las evidencias y los documentos de presentación.

**Nota:** Los fragmentos anteriores documentan las principales transformaciones. El código completo de las consultas y la configuración del modelo pueden revisarse en el archivo de Power BI.
