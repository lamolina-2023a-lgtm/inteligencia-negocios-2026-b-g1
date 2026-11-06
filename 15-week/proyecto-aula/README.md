# PROYECTO DE AULA
## EcoHogar del Huila

**Título:** Diseño e implementación de un tablero de control en Power BI para el análisis de ventas y margen bruto de la empresa EcoHogar del Huila.

**Institución:** Corporación Universitaria del Huila – CORHUILA  
**Programa académico:** Ingeniería Ambiental  
**Asignatura:** Inteligencia de Negocios  
**Docente:** Jesús Ariel González Bonilla  
**Periodo académico:** 2026-B

**Integrantes:**
- Yury Lorena Castañeda Cedeño
- Larissa Alexandra Molina Borja

---

## 1. Descripción de la empresa

EcoHogar del Huila es una empresa ficticia dedicada a la comercialización de electrodomésticos en Neiva, Huila.

Cuenta con dos sedes comerciales:

- Neiva Centro.
- Neiva Norte.

Las ventas se realizan mediante dos canales:

- Mostrador.
- Domicilio.

Los clientes se clasifican en Empresariales y Particulares.

Esta estructura permite analizar las ventas y los resultados económicos por sede, canal comercial, producto y tipo de cliente.

## 2. Planteamiento del problema

EcoHogar del Huila necesita determinar cuáles de sus sedes y tipos de clientes generan mejores resultados económicos para distribuir adecuadamente el inventario y orientar sus promociones.

Sin embargo, analizar únicamente el valor de las ventas no permite identificar qué operaciones generan un mayor margen bruto, porque no considera el costo de los productos vendidos.

Esta limitación puede ocasionar que la empresa concentre sus esfuerzos comerciales en las unidades que más venden, aunque no necesariamente sean las que generan mejores resultados económicos.

Por esta razón, se propone implementar un tablero de control en Power BI que permita comparar ventas, costos y margen bruto para apoyar decisiones comerciales basadas en datos.

## 3. Pregunta de negocio

**¿Qué sede y qué tipo de cliente generan mayor margen bruto durante 2025, y dónde conviene concentrar las promociones durante el primer semestre de 2026?**

## 4. Objetivo general

Diseñar e implementar un tablero de control en Power BI para analizar las ventas y el margen bruto de EcoHogar del Huila durante 2025, con el fin de apoyar las decisiones relacionadas con la distribución del inventario y las estrategias de promoción comercial.

## 5. Objetivos específicos

1. Construir y depurar una base de datos simulada de transacciones comerciales correspondiente al año 2025.
2. Aplicar procesos de extracción, transformación y carga de datos mediante Power Query.
3. Diseñar un modelo estrella que relacione ventas, productos, clientes, sedes, canales y fechas.
4. Calcular indicadores comerciales mediante medidas DAX.
5. Elaborar un dashboard interactivo que permita comparar los resultados económicos.
6. Formular recomendaciones sobre inventario y promociones a partir de los resultados obtenidos.

## 6. Fuente de datos y alcance

El proyecto utilizará una base de datos sintética, creada exclusivamente con fines académicos para representar las operaciones comerciales de EcoHogar del Huila.

**Características definidas del conjunto de datos:**

- Periodo: 1 de enero al 31 de diciembre de 2025.
- Volumen previsto: 1.200 registros de ventas.
- Cobertura temporal: 12 meses.
- Sedes: Neiva Centro y Neiva Norte.
- Canales: Mostrador y Domicilio.
- Tipos de clientes: Empresarial y Particular.
- Moneda: pesos colombianos (COP).
- Archivo de origen: `EcoHogar_Ventas_2025.xlsx`.

La base contendrá identificadores de transacciones, fechas, productos, cantidades, precios unitarios, descuentos y costos unitarios.

Se incorporarán inconsistencias controladas para documentar su identificación y corrección mediante Power Query.

Los datos serán simulados y no representarán transacciones reales de una empresa.

## 7. Modelo de datos

Se implementará un modelo estrella compuesto por una tabla de hechos y cinco dimensiones.

### FactVentas

Tabla central con una fila por línea de factura.

**Columnas:**

- ID_Factura
- Fecha
- ID_Sede
- ID_Canal
- ID_Cliente
- ID_Producto
- Cantidad
- Precio_Unitario
- Descuento
- Costo_Unitario

### DimProducto

Contendrá:

- ID_Producto
- Producto
- Categoria
- Marca
- Costo_Referencia

Categorías: neveras, lavadoras, televisores y pequeños electrodomésticos.

### DimCliente

Contendrá:

- ID_Cliente
- Tipo_Cliente
- Ciudad

Los tipos de clientes serán Empresarial y Particular. No se utilizarán datos personales reales.

### DimSede

Contendrá:

- ID_Sede
- Sede

Valores: Neiva Centro y Neiva Norte.

### DimCanal

Contendrá:

- ID_Canal
- Canal
- Costo_Envio

Valores: Mostrador y Domicilio.

### DimCalendario

Contendrá:

- Fecha
- Año
- Trimestre
- Mes
- Nombre_Mes
- Temporada

Las dimensiones se relacionarán con FactVentas mediante relaciones de uno a muchos.

## 8. Proceso ETL

El archivo de origen se importará a Power BI Desktop y se transformará mediante Power Query.

El proceso incluirá:

**Extracción:** Carga de los datos desde el archivo Excel.

**Transformación:**

1. Corrección de formatos de fecha.
2. Estandarización de nombres de categorías y tipos de clientes.
3. Identificación y eliminación de registros duplicados.
4. Verificación de valores nulos y tipos de datos.
5. Validación de cantidades, precios, descuentos y costos.

**Carga:** Incorporación de los datos depurados al modelo de Power BI.

Se conservarán evidencias de al menos tres problemas de calidad, incluyendo el estado anterior, la transformación aplicada y el resultado final.

## 9. Indicadores de gestión (KPI)

### KPI principal: Margen bruto porcentual

Permite determinar qué porcentaje de las ventas netas queda después de descontar el costo de los productos vendidos.

**Fórmula:**

Margen bruto (%) = [(Ventas netas - Costo de ventas) / Ventas netas] × 100

**Unidad:** Porcentaje (%).

**Utilidad:** Comparar el desempeño económico entre sedes, canales y tipos de clientes.

### KPI de apoyo 1: Ventas totales

Representa el valor acumulado de las ventas netas durante el periodo analizado.

**Fórmula:**

Ventas totales = Σ [Cantidad × Precio unitario × (1 - Descuento)]

**Unidad:** Pesos colombianos (COP).

### KPI de apoyo 2: Participación de ventas por tipo de cliente

Permite conocer qué proporción de las ventas corresponde a clientes Empresariales y Particulares.

**Fórmula:**

Participación (%) = (Ventas del tipo de cliente / Ventas totales) × 100

**Unidad:** Porcentaje (%).

## 10. Medidas DAX

Las medidas se implementarán en Power BI con los siguientes nombres y criterios.

El descuento se almacenará como proporción decimal entre 0 y 1.

### Ventas Totales

```DAX
Ventas Totales =
SUMX(
    FactVentas,
    FactVentas[Cantidad] *
    FactVentas[Precio_Unitario] *
    (1 - FactVentas[Descuento])
)
```

### Costo de Ventas

```DAX
Costo de Ventas =
SUMX(
    FactVentas,
    FactVentas[Cantidad] *
    FactVentas[Costo_Unitario]
)
```

### Margen Bruto

```DAX
Margen Bruto =
[Ventas Totales] - [Costo de Ventas]
```

### Margen Bruto %

```DAX
Margen Bruto % =
DIVIDE(
    [Margen Bruto],
    [Ventas Totales],
    0
)
```

La medida Margen Bruto % tendrá formato de porcentaje en Power BI.

### Participación de Ventas %

```DAX
Participacion Ventas % =
DIVIDE(
    [Ventas Totales],
    CALCULATE(
        [Ventas Totales],
        REMOVEFILTERS(DimCliente[Tipo_Cliente])
    ),
    0
)
```

Esta medida permitirá calcular la participación de cada tipo de cliente sobre las ventas totales del contexto seleccionado.

## 11. Diseño del dashboard

El dashboard se organizará para responder la pregunta de negocio mediante indicadores, gráficos y filtros interactivos.

**Indicadores principales:**

- Ventas Totales (COP).
- Costo de Ventas (COP).
- Margen Bruto (COP).
- Margen Bruto (%).

**Visualizaciones:**

1. Gráfico de barras: margen bruto porcentual por sede.
2. Gráfico de columnas: ventas totales por sede.
3. Gráfico de barras: margen bruto por tipo de cliente.
4. Gráfico de líneas: evolución mensual de las ventas.
5. Gráfico de columnas: comparación de ventas por canal.
6. Gráfico de participación de ventas por tipo de cliente.

**Segmentadores:**

- Sede.
- Canal.
- Tipo de cliente.
- Periodo.

Las visualizaciones permitirán realizar comparaciones y observar cómo cambian los resultados al aplicar filtros.

## 12. Análisis para la toma de decisiones

El análisis se centrará en comparar los resultados comerciales de 2025 para orientar decisiones del primer semestre de 2026.

Se evaluará:

- Qué sede obtiene mayores ventas.
- Qué sede presenta un mejor margen bruto porcentual.
- Qué tipo de cliente aporta mayor margen bruto en pesos.
- Qué productos y categorías generan mejores resultados.
- Cómo se distribuyen las ventas entre Mostrador y Domicilio.
- Qué variaciones se presentan durante los meses del año.

Las recomendaciones comerciales se formularán a partir de los resultados calculados y verificados en el dashboard.

## 13. Diccionario de datos

Se elaborará un diccionario que describa cada tabla y columna del modelo.

Para cada campo se registrará:

- Nombre.
- Descripción.
- Tipo de dato.
- Tabla de origen.
- Regla de validación.
- Relación con otras tablas, cuando corresponda.

Este documento permitirá comprender la estructura de los datos y facilitar su revisión.

## 14. Validación de resultados

Antes de presentar los resultados definitivos, se verificarán los siguientes aspectos:

- Cantidad de registros cargados.
- Cobertura completa de los 12 meses de 2025.
- Ausencia de duplicados indebidos.
- Integridad de las relaciones del modelo.
- Coherencia de los cálculos de ventas, costos y margen.
- Funcionamiento de los filtros y las interacciones del dashboard.

La validación permitirá comprobar que los indicadores coincidan con la información de origen.

## 15. Archivos y evidencias del proyecto

La entrega técnica estará organizada con los siguientes archivos:

- `README.md`: descripción y documentación del proyecto.
- `EcoHogar_Ventas_2025.xlsx`: archivo de origen con los datos simulados.
- `Diccionario_Datos_EcoHogar.xlsx`: descripción de tablas y campos.
- `Proyecto_BI_EcoHogar.pbix`: modelo de datos, medidas y dashboard.
- `Anexo_1_ETL_PowerQuery.png`: evidencia del proceso ETL.
- `Anexo_2_Modelo_Estrella.png`: evidencia de las relaciones.
- `Anexo_3_Dashboard_Final.png`: evidencia del tablero.
- Informe académico institucional FO-IV-159.

Los archivos permitirán revisar la trazabilidad desde el origen de los datos hasta las visualizaciones y recomendaciones.

## 16. Resultados esperados

Se espera obtener un tablero interactivo que permita identificar diferencias entre sedes, canales y tipos de clientes.

El análisis del margen bruto complementará las ventas totales y permitirá reconocer que vender más no necesariamente significa obtener un mejor resultado económico.

Los hallazgos servirán para fundamentar recomendaciones sobre distribución de inventario y estrategias de promoción.

Los valores definitivos de los indicadores se incorporarán después de ejecutar y validar el modelo con los datos simulados.

## 17. Conclusión

El proyecto EcoHogar del Huila propone aplicar herramientas de inteligencia de negocios para transformar datos comerciales en información útil para la toma de decisiones.

Mediante Power Query, Power BI y DAX se organizarán las transacciones, se calcularán indicadores y se visualizará el desempeño comercial de las sedes, canales y tipos de clientes.

El resultado permitirá orientar decisiones de inventario y promoción con base en las ventas y el margen bruto, en lugar de depender únicamente del volumen de ingresos.

## 18. Autorización y uso de datos

EcoHogar del Huila es una empresa ficticia. Los datos serán simulados exclusivamente para fines académicos y no contendrán información personal real de clientes.

Por lo tanto, no se requiere autorización de una empresa externa.
