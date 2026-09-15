![Banner](./banner.png)

# 📊 Portfolio

## 👋 Sobre mí

Soy Pablo Quiñones Gil, profesional en compras, supply chain y especializado en Data Analysis. Cuento con más de 2 años de experiencia en el sector retail, centrado en procesos de extracción, transformación y limpieza de datos (ETL), así como la creación de dashboards para el control de stock, KPIs logísticos y toma de decisiones.

**Stack:** Power BI · QlikView · Excel avanzado (Power Query, Power Pivot) · SQL · Python · Dynamics 365 · Navision

📫 [LinkedIn](https://www.linkedin.com/in/pabloquinonesgil/) · 📧 pabloqgil@gmail.com

Este repositorio recoge mis proyectos de análisis de datos.

---

## Retail Project — Análisis de comportamiento de clientes (2020–2021)

🔗 [Ver proyecto completo](https://github.com/pabloDev171/pabloDev171/tree/main/Retail%20Project)

ETL en Python (Pandas) sobre un dataset JSON de pedidos, con cálculo de métricas de recurrencia de clientes y cuadro de mando interactivo en Power BI, desglosado por año/mes de adquisición y por estado.

**Stack:** Python (Pandas) · Power BI

**Principales conclusiones:** % Clientes Recurrentes (47,81 %) · Importe Medio del Primer Pedido (1.878,49 €) · Importe Medio de los Pedidos Recurrentes (12.268,57 €) · Tiempo Medio entre Recurrencias (31,77 días).

---

## Airbnb Project — Análisis del mercado de alojamientos turísticos

🔗 [Ver proyecto completo](https://github.com/pabloDev171/pabloDev171/tree/main/Airbnb%20Project)

Proyecto de análisis de datos centrado en comparar la oferta de alojamientos turísticos de **Madrid, Barcelona y Valencia**, combinando un dataset histórico con datos actuales obtenidos mediante **web scraping de Airbnb**.

El proyecto se divide en dos notebooks:

- **`Web_scraping_Airbnb.ipynb`** — extracción automatizada de anuncios de Airbnb mediante Selenium y BeautifulSoup, trabajando distrito a distrito en las tres ciudades.
- **`EDA_Fusionado.ipynb`** — limpieza, enriquecimiento y análisis exploratorio conjunto de los datos históricos y los datos scrapeados, incluyendo la respuesta a 8 preguntas de negocio.

**Stack:** Python · Selenium · BeautifulSoup · Pandas · Matplotlib · Seaborn

**Principales conclusiones:** las variables de capacidad son los factores que mejor explican el precio en ambas fuentes; el dataset histórico permite dimensionar el mercado y estudiar su evolución temporal, mientras que el scraping aporta una fotografía actual y variables adicionales de confianza del anfitrión. El solapamiento entre ambas fuentes es mínimo, por lo que se consideran **complementarias y no redundantes**.
