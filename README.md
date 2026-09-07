# 📊 Análisis de Comportamiento de Clientes — Retail 2020–2021

Proyecto de portfolio de análisis de datos: pipeline completo desde un dataset semi-estructurado en JSON hasta un cuadro de mando interactivo en Power BI, pasando por un proceso de ETL en Python con Pandas.

![Python](https://img.shields.io/badge/Python-Pandas-informational)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)
![Status](https://img.shields.io/badge/status-completado-brightgreen)

---

## 🎯 Objetivo del proyecto

Una tienda retail dispone de un histórico de pedidos de 2020 y 2021 y quiere entender el comportamiento de sus clientes según su año de adquisición y la evolución de sus hábitos de compra.

El proyecto construye un flujo completo de análisis: ingesta y limpieza de un dataset en bruto (JSON), cálculo de las métricas de negocio solicitadas y un cuadro de mando interactivo en Power BI para que negocio pueda explorar los resultados.

**Requisitos cubiertos:**
- Desglose por año y mes de adquisición del cliente.
- Desglose por estado / provincia del cliente.
- Cálculo, en gráfico y en tabla resumen, de:
  - % de clientes recurrentes
  - Importe de primeros pedidos
  - Importe de pedidos recurrentes
  - Tiempo medio entre recurrencias

---

## 🗂️ Dataset

Dataset en formato JSON (una línea por pedido), con información del cliente, de la cabecera del pedido y de las líneas de producto (`sku`, `qty_ordered`, `price`, `discount_amount`, `product_category`).

Al no existir un campo explícito de "cliente", se usa el **email** como clave de identificación de cliente por ser el campo más estable y menos propenso a duplicidades.

---

## 🔧 Proceso ETL (Python + Pandas)

Todo el procesamiento se realiza en el notebook [`script_Retail.ipynb`](./script_Retail.ipynb):

1. **Carga** del JSON línea a línea con `pd.read_json(..., lines=True)`.
2. **Desanidado** de `order_items` con `explode` + `json_normalize` para trabajar a nivel de línea de producto.
3. **Normalización** de nombres de columnas a castellano para facilitar el análisis de negocio.
4. **Parseo y tipado** de fechas, importes y cantidades, con validación de tipos y de valores anómalos (`describe()`).
5. **Campos derivados**, como el importe de cada línea (`precio × cantidad`).
6. **Construcción de tablas agregadas**:
   - `pedidos`: una fila por pedido, con importe total y número de pedido del cliente (1º, 2º, 3º...).
   - `clientes`: una fila por cliente, con nº de pedidos, fecha de adquisición, condición de recurrente, importe del primer pedido, importe acumulado de pedidos recurrentes y tiempo medio entre recurrencias.
7. **Exportación** de `dataset_limpio.csv`, `pedidos.csv` y `clientes.csv` como fuente para Power BI.

---

## 📈 Resultados clave

| Métrica | Definición | Resultado |
|---|---|---|
| % clientes recurrentes | Proporción de clientes con más de un pedido | **47,81 %** |
| Importe primer pedido | Promedio del importe del primer pedido | **1.878,49 €** |
| Importe pedidos recurrentes | Promedio del importe acumulado en pedidos posteriores al primero | **12.268,57 €** |
| Tiempo medio entre recurrencias | Media de días entre pedidos consecutivos del mismo cliente | **31,77 días** |

---

## 📊 Cuadro de mando (Power BI)

El fichero [`dashboard.pbix`](./dashboard.pbix) contiene dos vistas construidas a partir de `pedidos.csv` y `clientes.csv`:

- **Dashboard**: indicadores clave (nº de clientes, % recurrencia, tiempo medio entre pedidos, facturación total, importe medio de primer pedido y de pedidos recurrentes), evolución mensual de facturación, desglose por categoría de producto, por género y filtro interactivo por estado.
- **Tablas resumen**: detalle numérico de las métricas desglosado por año/mes de adquisición y por estado/provincia.

---

## 💡 Principales insights y recomendaciones de negocio

- **Priorizar la fidelización sobre la captación**: el importe medio de los pedidos recurrentes multiplica por más de 6 el del primer pedido. Conviene destinar presupuesto a incentivar la segunda compra en lugar de centrarse solo en adquisición.
- **Campañas de reactivación en torno al día 30**: dado que el tiempo medio entre recurrencias es de ~32 días, automatizar comunicaciones alrededor de los días 25–28 tras la última compra puede mejorar la tasa de reactivación.
- **Interpretar con cautela el descenso de recurrencia** observado a lo largo de 2021, ya que en parte responde al menor tiempo de maduración de los clientes captados más tarde.
- **Ticket de entrada creciente**: el importe medio del primer pedido ha aumentado de forma sostenida a lo largo del periodo analizado; conviene estudiar su relación con la recurrencia posterior.
- **Diferencias de fidelización por estado**, que sugieren replicar buenas prácticas de los estados con mejor recurrencia en los más rezagados.
- **Alta dependencia de la categoría Mobiles & Tablets** en facturación frente a su peso en volumen de venta, lo que aconseja potenciar categorías con mejor equilibrio volumen/fidelización.

---

## 🗃️ Estructura del repositorio

```
├── dataset.json          # Dataset original de partida
├── script_Retail.ipynb   # Notebook con la limpieza, transformación y cálculo de métricas
├── dataset_limpio.csv    # Detalle a nivel de línea de pedido, limpio y tipado
├── pedidos.csv           # Tabla agregada a nivel de pedido
├── clientes.csv          # Tabla agregada a nivel de cliente con las métricas calculadas
└── dashboard.pbix        # Cuadro de mando en Power BI (Dashboard + Tablas resumen)
```

---

## 🛠️ Tecnologías utilizadas

- **Python** (Pandas) — ETL y cálculo de métricas
- **Jupyter Notebook** — desarrollo y documentación del proceso
- **Power BI** — visualización y cuadro de mando interactivo

---

## ▶️ Cómo reproducir el análisis

1. Clona el repositorio y asegúrate de tener Python 3 y Pandas instalados.
2. Ejecuta `script_Retail.ipynb` de principio a fin para generar `dataset_limpio.csv`, `pedidos.csv` y `clientes.csv`.
3. Abre `dashboard.pbix` en Power BI Desktop y actualiza el origen de datos si es necesario para apuntar a los CSV generados.

---

## 📄 Documentación

Puedes consultar la documentación técnica completa del proyecto (contexto, ETL detallado, definición de métricas y capturas del dashboard) en [`Documentacion_Retail_Project.pdf`](./Documentacion_Retail_Project.pdf).
