# Proyecto final de aula — EcoHogar del Huila

**Asignatura:** Inteligencia de Negocios — Corte 3, 2026-B  
**Institución:** Corporación Universitaria del Huila — CORHUILA  
**Programa:** Ingeniería Ambiental  
**Docente:** Jesús Ariel González Bonilla

**Integrantes:**
- Yury Lorena Castañeda Cedeño
- Larissa Alexandra Molina Borja

## 1. Descripción del proyecto

Este proyecto desarrolla un tablero interactivo de inteligencia de negocios en Power BI para EcoHogar del Huila, una empresa ficticia dedicada a la comercialización de electrodomésticos en Neiva.

Se utilizan datos sintéticos correspondientes al año 2025 para analizar las ventas, los costos y la rentabilidad por sede y tipo de cliente. El objetivo es transformar los registros comerciales en información útil para la toma de decisiones.

## 2. Pregunta de negocio

¿Cómo varían las ventas y el margen bruto de EcoHogar del Huila durante 2025 según la sede y el tipo de cliente, y qué decisiones comerciales pueden tomarse a partir de estos resultados?

## 3. Indicadores clave (KPI)

El indicador principal es el margen bruto porcentual.

**Margen bruto (%) = (Utilidad bruta / Ventas totales) × 100**

Los indicadores complementarios son ventas totales, costos totales, utilidad bruta y unidades vendidas.

| Indicador | Resultado 2025 |
|---|---:|
| Ventas totales | $2.719.167.200 COP |
| Costos totales | $2.012.205.000 COP |
| Utilidad bruta | $706.962.200 COP |
| Margen bruto | 26,00 % aprox. |
| Unidades vendidas | 2.557 |

## 4. Fuente de datos y preparación ETL

La fuente es el archivo `EcoHogar_Ventas_2025.xlsx`, construido con información ficticia para fines académicos.

La tabla original contiene 1.203 registros, de los cuales se eliminaron tres duplicados exactos, obteniendo 1.200 registros únicos.

En Power Query se documentaron los pasos de importación, promoción de encabezados, asignación de tipos de datos, eliminación de duplicados, normalización de mayúsculas y creación de columnas personalizadas.

Se identificaron además diferencias en la presentación de fechas y variaciones de espacios en los textos de origen. No se atribuyen transformaciones adicionales que no estén comprobadas en las evidencias.

**Columnas calculadas:**

- `Venta_Total = Cantidad * Precio_Unitario * (1 - Descuento)`
- `Costo_Total = Cantidad * Costo_Unitario`
- `Utilidad_Bruta = Venta_Total - Costo_Total`

## 5. Modelo estrella y diccionario de datos

Se construyó un modelo dimensional compuesto por:

- `FactVentas_Origen`: tabla de hechos comerciales.
- `DimProducto`: información de productos y categorías.
- `DimCliente`: identificación y tipo de cliente.
- `DimSede`: sedes Neiva Centro y Neiva Norte.
- `DimCanal`: canales comerciales.
- `DimCalendario`: fechas y jerarquía temporal.

Las dimensiones se relacionan con la tabla de hechos mediante relaciones de uno a muchos.

El diccionario de datos completo, con nombres de campos, tipos y ejemplos, se encuentra en el informe técnico.

## 6. Medidas DAX

```dax
Ventas Totales 2025 =
SUM(FactVentas_Origen[Venta_Total])

Costos Totales 2025 =
SUM(FactVentas_Origen[Costo_Total])

Utilidad Bruta 2025 =
[Ventas Totales 2025] - [Costos Totales 2025]

Margen Bruto % =
DIVIDE([Utilidad Bruta 2025], [Ventas Totales 2025], 0)

Unidades Vendidas 2025 =
SUM(FactVentas_Origen[Cantidad])
```

Estas cinco medidas permiten que los indicadores respondan dinámicamente a los filtros del tablero.

## 7. Dashboard e interactividad

El tablero de Power BI incluye:

- Indicador general de ventas.
- Gráfico de barras comparativo por sede.
- Gráfico de anillo por tipo de cliente.
- Gráfico de líneas para la evolución temporal.
- Dos segmentadores: sede y tipo de cliente.
- Filtrado cruzado entre visualizaciones.
- Jerarquía temporal Año → Trimestre → Mes → Día, con drill-down.

Se realizaron tres pruebas de interacción: selección de Neiva Centro, selección de Neiva Norte y selección de clientes empresariales.

| Selección | Ventas (COP) | Utilidad bruta (COP) |
|---|---:|---:|
| Sin filtros | 2.719.167.200 | 706.962.200 |
| Neiva Centro | 1.458.128.350 | 378.906.350 |
| Neiva Norte | 1.261.038.850 | 328.055.850 |
| Empresariales | 1.327.780.300 | 346.749.300 |

## 8. Hallazgos principales

Neiva Centro registró ventas por $1.458.128.350 COP, mientras que Neiva Norte alcanzó $1.261.038.850 COP. La diferencia fue de $197.089.500 COP a favor de Centro.

Ambas sedes presentaron márgenes brutos cercanos al 26 %. Por tanto, la principal diferencia identificada está en el volumen comercial y no en el porcentaje de margen.

Los clientes empresariales representaron el 48,83 % de las ventas, mientras que los particulares aportaron el 51,17 %.

## 9. Recomendaciones

Se recomienda que la administración comercial realice seguimiento mensual de ventas, unidades y margen bruto por sede y tipo de cliente.

Durante el trimestre siguiente, la persona responsable de Neiva Norte debería revisar productos y segmentos de menor participación y evaluar acciones comerciales, controlando que los descuentos no deterioren el margen bruto.

Al finalizar el trimestre, los resultados se compararían con la línea base de 2025 para decidir posibles ajustes.

Estas recomendaciones son propuestas académicas basadas en una empresa ficticia.

## 10. Overview & insights

This project analyzes sales and gross profit margins for EcoHogar del Huila, a fictional appliance retailer located in Neiva, Colombia. The dataset contains 1,200 unique sales records from 2025 after removing three exact duplicates. We used Power Query to prepare the data and Power BI to develop an interactive dashboard. The dashboard includes sales indicators, branch comparisons, customer segments, and monthly trends. Total sales reached COP 2,719,167,200, with a gross profit margin of approximately 26 percent. Neiva Centro generated higher sales than Neiva Norte, while both branches maintained similar profit margins. Business customers accounted for 48.83 percent of total sales. We recommend monitoring branch performance monthly and reviewing commercial strategies for Neiva Norte on a quarterly basis.

## 11. Entregables y evidencias

La entrega académica incluye:

- Archivo original de datos en Excel.
- Archivo de Power BI (`.pbix`).
- Informe técnico en PDF.
- Presentación del proyecto en PDF.
- Capturas de Power Query, modelo de datos, medidas DAX y dashboard.
- Evidencias de tres pruebas de interacción.

Los archivos completos se adjuntan mediante el ZIP de anexos en Moodle, junto con el formato institucional FO-IV-159, que no se publica en GitHub por contener información de identificación.

## 12. Historial del proyecto

El archivo `README.md` ubicado directamente en `15-week/proyecto-aula/` corresponde a una etapa anterior de revisión y correcciones del docente.

Esta carpeta `entrega-final-ecohogar` contiene la documentación de la versión final del proyecto. Se mantiene el archivo anterior sin modificaciones para conservar la trazabilidad académica y el historial de avances.
