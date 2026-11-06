# Proyecto de Aula: Inteligencia de Negocios - EcoHogar del Huila (Fase 1)

## 1. Ficha del Proyecto
- **Institución:** Corporación Universitaria del Huila (CORHUILA)
- **Programa Académico:** Ingeniería Ambiental
- **Asignatura:** Inteligencia de Negocios
- **Integrantes:** 
  - Larissa Alexandra Molina Borja
  - Yury Lorena Castañeda Cedeño
- **Docente:** Jesús Ariel González Bonilla
- **Empresa Objeto de Estudio:** EcoHogar del Huila (Comercializadora de Electrodomésticos)
- **Periodo Evaluado:** Año 2025 (12 meses / 1.050 registros transaccionales)

---

## 2. Planteamiento del Problema
Actualmente, la directiva de EcoHogar del Huila enfrenta incertidumbre al asignar su presupuesto promocional y la distribución de inventarios entre sus sedes físicas (Neiva Centro y Neiva Norte) y sus canales comerciales (Mostrador y Domicilio). Al no disponer de una medición centralizada del **Margen Bruto real (%)**, la empresa corre el riesgo de tomar malas decisiones operativas, como destinar inventario de alto valor o promociones a canales de baja rentabilidad durante el primer semestre de 2026.

---

## 3. Pregunta de Investigación
¿Qué unidad comercial (Sede Neiva Centro o Neiva Norte) y qué tipo de canal de distribución (Mostrador o Domicilio) dejaron el mayor **Margen Bruto (%)** durante el año 2025 en la empresa EcoHogar del Huila, y dónde conviene concentrar las promociones e inventario para el primer semestre de 2026?

---

## 4. Indicadores Clave de Rendimiento (KPIs)

### KPI Principal: Margen Bruto (%)
```dax
Margen Bruto % = DIVIDE([Ventas Totales] - [Costo Total], [Ventas Totales], 0) * 100
