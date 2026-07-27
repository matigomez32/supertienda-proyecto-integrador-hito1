# 🛒 SuperTienda Retail - Construcción del Dataset Analítico (Proyecto Integrador - Hito 1)

Primer hito del **Proyecto Integrador de Data Analytics**. En esta etapa se abordó un escenario real de la empresa de retail **SuperTienda**, cuyo objetivo fue conectar una base de datos relacional SQLite (`.db`), extraer información transaccional clave, aplicar transformaciones de calidad de datos en Python (Pandas) y construir un **Dataset Analítico Unificado** estructurado para futuros Dashboards e Inteligencia de Negocio.

---

## 🎯 Escenario de Negocio y Objetivo
SuperTienda centraliza su información operativa en múltiples tablas relacionales. Para permitir la toma de decisiones estratégicas por parte de la gerencia, se definió el **Enfoque de Ventas y Rendimiento Comercial**, unificando la información de transacciones, productos y campañas publicitarias para analizar ingresos reales, rentabilidad y tiempos logísticos.

---

## 🛠️ Flujo de Trabajo (Pipeline de Datos)

El flujo de trabajo se desarrolló en 4 fases estructuradas dentro de Jupyter Notebook / Google Colab:

### 1. Exploración de la Base de Datos (`SQLite`)
* Inspección de la base de datos `SuperTienda_Espanol.db` compuesta por 8 tablas relacionales.
* **Selección Estratégica:** Se seleccionaron 4 tablas clave (`Pedidos`, `Detalle_Pedido`, `Productos` y `Campanias`) y se descartaron tablas de soporte y datos demográficos no alineados con el objetivo del hito.

### 2. Extracción de Datos (`SQL + Pandas`)
* Construcción de una consulta SQL avanzada integrando las 4 tablas mediante cláusulas `JOIN` y `LEFT JOIN` (para conservar ventas sin campaña publicitaria asignada).
* Carga del resultado estructurado directamente a un DataFrame de Pandas para su manipulación en memoria.

### 3. Limpieza, Transformación y Feature Engineering (`Pandas`)
* **Parsing de Fechas:** Conversión de `Fecha_Pedido` y `Fecha_Envio` al tipo `datetime64` de Pandas para análisis de series temporales.
* **Casting de Tipos Numéricos:** Asignación explícita de tipos numéricos a `Cantidad`, `Descuento`, `Ventas`, `Ganancia`, `Precio_Lista` y `Costo_Unitario`.
* **Estandarización de Textos:** Aplicación de `.str.lower().str.strip()` en variables categóricas (`Categoria`, `Modo_Envio`, etc.) e imputación de nulos categóricos con `'sin dato'`.
* **Variables Calculadas (`Feature Engineering`):**
  * `Ingreso_Neto`: Mide la facturación real descontando la tasa aplicada (`Ventas * (1 - Descuento)`).
  * `Venta_Promedio_Unidad`: Ticket unitario promedio de cada transacción.
  * `Mes_Pedido`: Variable temporal para evaluar la estacionalidad de la demanda.
  * `Dias_Envio`: Indicador logístico (*lead time*) que mide la demora en días entre la compra y el despacho.

### 4. Exportación y Calidad de Datos
* Verificación final de calidad de datos (0 valores nulos críticos y 0 duplicados en transacciones).
* Exportación del dataset procesado a formato CSV optimizado (`sep=';'`, `encoding='utf-8-sig'`) para lectura directa en Microsoft Excel y Power BI.

---

## 📊 Preguntas de Negocio que Responde el Dataset

1. **Rentabilidad vs. Descuentos:** ¿Qué productos o categorías generan pérdidas debido a políticas de descuento agresivas?
2. **Efectividad de Marketing:** ¿Cuál es el impacto y retorno de las distintas campañas y canales publicitarios sobre el volumen total de ingresos?
3. **Eficiencia Logística:** ¿Cuántos días tarda en despacharse un pedido según el `Modo_Envio` seleccionado?
4. **Comportamiento Temporal:** ¿En qué meses se concentran los picos de mayor facturación del año?

---

## 💻 Tecnologías Utilizadas
* **SQL (SQLite)** - Extracción, filtrado y unificación de tablas relacionales.
* **Python 3.x / Pandas** - Limpieza, estandarización, imputación y creación de métricas derivadas.
* **Jupyter Notebook / Google Colab** - Entorno de desarrollo interactivo.

---

## 👥 Equipo de Trabajo
* Facundo Vazquez
* Matías Alejandro Gómez
* Federico Ezequiel Castillo
* José Luis Rodríguez
* Fidel Fernández Fontenla
