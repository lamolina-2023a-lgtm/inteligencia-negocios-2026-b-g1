# PROYECTO DE AULA – FASE 0
## EcoHogar del Huila

### 1. Integrantes
- Yury Lorena Castañeda Cedeño
- Larissa Alexandra Molina Borja

### 2. Empresa y tipo
**Nombre:** EcoHogar del Huila.

**Tipo:** Empresa ficticia.

**Actividad:** Comercialización de electrodomésticos en Neiva, Huila.

El proyecto analiza las ventas de tres unidades comerciales:
- Sede Neiva Centro.
- Sede Neiva Norte.
- Canal Domicilios.

### 3. Planteamiento del problema
EcoHogar del Huila presenta dificultades para analizar y comparar
de manera centralizada las ventas de sus diferentes unidades comerciales.

Esta situación dificulta identificar cuáles generan mayores ingresos
y cómo se distribuyen las ventas entre los diferentes tipos de clientes.

Por ello, se propone utilizar Power BI para organizar y visualizar
la información, facilitando la toma de decisiones comerciales.

### 4. Pregunta de negocio
¿Qué unidades comerciales y tipos de clientes generan mayores
ingresos por ventas en EcoHogar del Huila?

### 5. KPI principal
**Nombre:** Ventas Totales.

**Definición:** Indicador que mide el valor total de las ventas
registradas por la empresa.

**Fórmula DAX:**

Ventas Totales = SUM(FactVentas[Venta_Total])

**Unidad de medida:** Pesos colombianos (COP).

**Cifra de control reportada:** $5.360.000 COP.

### 6. KPI de apoyo

**KPI 1: Margen Bruto**

Permite estimar la diferencia entre las ventas y los costos
asociados a los productos vendidos.

**KPI 2: Participación porcentual de ventas por tipo de cliente**

Permite conocer qué porcentaje de las ventas corresponde
a clientes empresariales y particulares.

**Fórmula:**

Participación (%) = (Ventas del tipo de cliente / Ventas totales) × 100

### 7. Fuentes de datos y formato
Se utilizan datos simulados de transacciones comerciales,
creados y trabajados en Power BI con fines académicos.

**Tablas utilizadas:**
- FactVentas: registros de ventas.
- DimCliente: información de clientes.
- DimSede: información de unidades comerciales.
- DimProducto: información de productos.

**Herramientas:** Power BI Desktop y Power Query.

**Formato del proyecto:** .pbix.

**Archivo:** Proyecto_BI_EcoHogar.pbix.

### 8. Autorización
No aplica, debido a que EcoHogar del Huila es una empresa
ficticia y utiliza datos simulados con fines académicos.
