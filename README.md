# Proyecto RappiPlus: De Datos a Decisiones de Negocio 🚀

## 📋 Descripción del Proyecto
Este proyecto analiza el desempeño integral del servicio **RappiPlus** con el fin de transformar datos crudos en **decisiones de negocio accionables**. A través de un flujo estructurado de ciencia de datos, se evalúa la calidad de la información, la rentabilidad financiera, el comportamiento del usuario en el embudo de conversión, la retención por cohortes y el impacto de experimentos A/B.

---

## 🛠️ Tecnologías y Librerías Utilizadas
* **Lenguaje:** Python 3.x
* **Manipulación y Análisis de Datos:** `pandas`, `numpy`
* **Estadística y Pruebas de Hipótesis:** `scipy.stats`, `statsmodels`
* **Visualización de Datos:** `seaborn`, `matplotlib`
* **Bases de Datos y SQL:** `SQLAlchemy`, `psycopg` (Conexión a base de datos PostgreSQL)
* **Business Intelligence:** Tableau Public

---

## 📂 Estructura del Repositorio
```text
├── S12 Estudiante_Proyecto_Final.ipynb  # Notebook principal con el análisis en Python y SQL
├── orders_clean.csv                     # Dataset limpio de pedidos
├── catalog_clean.csv                    # Dataset limpio de catálogo y costos
├── marketing_clean.csv                  # Dataset limpio de inversión publicitaria
├── Funnel_conversion.txt                # Consulta SQL para el análisis del embudo de conversión
├── Nirvana_Alzate_Proyecto_Final.twb    # Workbook de Tableau con el Dashboard ejecutivo
└── README.md                            # Documentación principal del proyecto
```

---

## 🔍 Fases del Análisis

### 1️⃣ Validación y Calidad de Datos (`Paso 1`)
* **Limpieza:** Conversión de tipos de datos, corrección de fechas y estandarización de variables categóricas (países y categorías de productos).
* **Consistencia Financiera:** Validación matemática entre `cantidad * precio_unitario - monto_descuento` y el `monto_total` registrado, identificando mínimas variaciones por efectos de redondeo.
* **Control de Duplicados y Nulos:** Eliminación de registros duplicados en pedidos y tratamiento de valores nulos mediante imputación estratégica (`"Desconocido"`) en marketing y eliminación de registros nulos no significativos en órdenes.

### 2️⃣ Análisis de Rentabilidad y KPIs del Negocio (`Paso 2`)
Se consolidaron las fuentes de datos (`orders`, `catalog`, `marketing`) para evaluar la salud financiera global:
* **Ingreso Total (Revenue):** \$51,836,375.14
* **Costo Total:** \$43,078,678.80
* **Inversión en Marketing:** \$2,871,843.53
* **Profit Total:** \$5,885,852.80 (**Margen de ganancia:** 11.36%)
* **Ticket Promedio:** \$2,107.16 por orden (con un promedio de 7.2 productos por orden).
* **Producto más vendido:** *Laptop-Gaming-16GB*.
* **Inversión por Canal:** El canal con mayor gasto fue `social`, seguido de `organic`.

### 3️⃣ Embudo de Conversión (Funnel Analysis) (`Paso 3`)
Mediante consultas SQL sobre la tabla de eventos (`events`), se analizó el flujo de usuarios a través de las etapas clave (`first_visit` → `select_item` → `add_to_cart` → `begin_checkout` → `add_payment_info` → `purchase`):
* **Conversión Final:** 49.47% de los usuarios que inician completan la compra.
* **Puntos Críticos de Abandono:** Las mayores tasas de caída se presentan en las etapas finales del proceso: transición hacia `add_payment_info` (21.95%) y confirmación de pago a `purchase` (22.34%).
* **Recomendación:** Revisar fricciones en formularios de pago, costos ocultos en el checkout y posibles fallas técnicas al procesar datos bancarios.

### 4️⃣ Retención de Usuarios por Cohortes (`Paso 4`)
Análisis de la actividad semanal posterior al registro (`users` y `user_activity`):
* Se identificó un patrón de disminución constante en la retención acumulada promedio:
  * **Semana 1:** 86.32%
  * **Semana 2:** 78.72%
  * **Semana 3:** 64.21%
* **Recomendación:** Cruzar estos datos con frecuencias de compra en la tabla `orders` para asegurar que la actividad registrada en la plataforma se traduzca en transacciones reales y valor económico recurrente.

### 5️⃣ Validación de Experimentos A/B (Test Estadístico) (`Paso 5`)
Se evaluó el impacto de una modificación en la interfaz de usuario (UI) del checkout (`experiment_checkout_ui.csv`):
* **Hipótesis:** Evaluar si existe una diferencia estadísticamente significativa en la tasa de conversión entre el grupo de `control` y el de `tratamiento`.
* **Prueba aplicada:** Prueba Z para proporciones (`proportions_ztest`) con un nivel de significancia $\alpha = 0.05$.
* **Resultado:** Se obtuvo un **p-valor de 0.416**, superior al umbral de 0.05, con tasas de conversión muy similares entre grupos (16.29% en tratamiento frente a una diferencia marginal del 0.6%).
* **Conclusión:** No existe evidencia estadística suficiente para rechazar la hipótesis nula. No se recomienda implementar el cambio en la UI de forma masiva.

---

## 📊 Dashboard Ejecutivo en Tableau (`Paso 6`)
Los datasets limpios fueron integrados en Tableau para construir un reporte ejecutivo interactivo:
* **Overview Ejecutivo:** Tarjetas KPI con Revenue Total, Profit Total, Margen de Ganancia, Ticket Promedio y Cantidad Promedio de Productos por Orden.
* **Evolución Temporal:** Gráfico de líneas con la tendencia mensual de ventas.
* **Desglose por Categoría:** Análisis de ingresos distribuidos por categorías de productos.

🔗 **[Visualiza el Dashboard Interactivo en Tableau Public](https://public.tableau.com/app/profile/nirvana.alzate/viz/Nirvana_Alzate_Proyecto_Final/Overview#1)**

---

## 💡 Conclusiones y Recomendaciones de Negocio
1. **Optimización del Checkout:** Priorizar mejoras en las pasarelas de pago y simplificar los formularios finales donde se concentra la mayor tasa de abandono.
2. **Eficiencia en Marketing:** Evaluar el Retorno de Inversión (ROI) por canal para optimizar la asignación de presupuesto entre pauta en redes sociales (`social`) y estrategias orgánicas.
3. **Experimentación Basada en Evidencia:** Mantener el rigor estadístico antes de desplegar cambios en el producto, evitando invertir recursos en modificaciones de interfaz sin impacto comprobado en la conversión.

---
✍️ **Autora:** Nirvana Alzate
