## 🚀 Descripción del Proyecto

**RetailPro** surge de la necesidad de unificar y analizar transacciones de venta, inventario, clientes y sucursales en una cadena de retail. El objetivo principal es transformar datos transaccionales crudos en métricas accionables para responder preguntas clave del negocio:
* ¿Cuáles son los productos y categorías con mayor margen de contribución?
* ¿Cómo se comportan los ingresos mensuales por región y sucursal?
* ¿Quiénes conforman el top de clientes recurrentes (programa de fidelización)?

---

## 🛢️ Modelo Relacional

El diseño de la base de datos cumple con la **3era Forma Normal (3FN)** para garantizar la integridad referencial y optimizar el rendimiento de las consultas analíticas.

```text
[clientes] (1) ------< (N) [ventas] >------ (1) [sucursales]
                              |
                             (N)
                              |
                    [detalle_ventas] (N) >------ (1) [productos]
```

* **`clientes`**: Información demográfica y de contacto del comprador.
* **`sucursales`**: Ubicación, gerente a cargo y tipo de tienda.
* **`productos`**: Catálogo, SKU, categoría y costo unitario.
* **`ventas`**: Cabecera de la transacción (fecha, ID cliente, ID sucursal, método de pago).
* **`detalle_ventas`**: Tabla de relación con cantidades, precios de venta unitarios y descuentos aplicados.

---

## 🛠️ Tecnologías y Herramientas Utilizadas

| Categoría | Herramienta / Tecnología | Propósito |
| :--- | :--- | :--- |
| **Base de Datos** | **PostgreSQL 18** | Motor de base de datos relacional y ejecución de consultas SQL. |
| **Lenguaje Query** | **SQL (ANSI / PL/pgSQL)** | DDL, DML, CTEs, Joins complejos y funciones de ventana (`ROW_NUMBER`, `RANK`). |
| **Análisis / EDA** | **Python 3.11** | Extracción, limpieza y validación de datos. |
| **Visualización** | **Pandas / Matplotlib / Seaborn** | Generación de gráficos exploratorios preliminares. |
| **Control de Versiones** | **Git / GitHub** | Versionado del código y documentación. |

---

## 📁 Estructura del Repositorio

```text
Proyecto-RetailPro/
│
├── data/                       # Datasets crudos y procesados (.csv / .sql dumps)
│   ├── raw/
│   └── processed/
│
├── sql/                        # Scripts SQL ordenados por fase
│   ├── 01_schema_ddl.sql       # Creación de tablas, PK, FK y restricciones
│   ├── 02_seed_data.sql        # Inserción de datos de prueba / ETL inicial
│   └── 03_business_kpis.sql    # Consultas analíticas, JOINs y KPIs
│
├── notebooks/                  # Análisis exploratorio en Jupyter
│   └── 01_eda_retailpro.ipynb  # Visualizaciones preliminares y estadísticas
│
├── img/                        # Gráficos y diagramas exportados
│   └── ERD_RetailPro.png
│
├── .gitignore
└── README.md                   # Documentación principal del proyecto
```

---

## ⚡ Instrucciones Paso a Paso para Ejecutar los Scripts

Sigue estos pasos en tu terminal o cliente SQL favorito (**pgAdmin**, **DBeaver**, **psql**):

### 1. Clonar el repositorio
```bash
git clone https://github.com
cd Proyecto-RetailPro
```

### 2. Crear la base de datos en PostgreSQL 18
Abre tu consola de PostgreSQL o cliente y ejecuta:
```sql
CREATE DATABASE retailpro_db\(; \c\) retailpro_db;
```

### 3. Ejecutar el DDL (Estructura de tablas)
```bash
psql -U postgres -d retailpro_db -f sql/01_schema_ddl.sql
```

### 4. Cargar los datos (Seed / ETL)
```bash
psql -U postgres -d retailpro_db -f sql/02_seed_data.sql
```

### 5. Ejecutar las consultas de negocio y KPIs
```bash
psql -U postgres -d retailpro_db -f sql/03_business_kpis.sql
```

---

## 📊 Consultas y KPIs Destacados

Ejemplo de consulta extraída de `sql/03_business_kpis.sql` para calcular el **Top 3 de categorías por ingresos**:

```sql
SELECT 
    p.categoria,
    COUNT(dv.venta_id) AS total_unidades_vendidas,
    SUM(dv.cantidad * dv.precio_unitario) AS ingresos_totales
FROM productos p
INNER JOIN detalle_ventas dv ON p.producto_id = dv.producto_id
GROUP BY p.categoria
ORDER BY ingresos_totales DESC
LIMIT 3;
```

---

## 👤 Autor y Contacto

* **Analista / Desarrollador:** [Alicia Vulcano)
* **Rol:** Data Analyst / SQL Developer
* **GitHub:** [@coquivulcano84-png](https://github.com)
