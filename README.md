# 🛒 Proyecto RetailPro — Data Analytics
## 🚀 Descripción del Proyecto
RetailPro es un proyecto de análisis de datos desarrollado sobre una base transaccional de retail y e-commerce. El objetivo principal es transformar registros transaccionales en métricas clave para la toma de decisiones comerciales:
* Facturación total mensual y ticket promedio.
* Ranking y concentración de ingresos por producto estrella.
* Identificación de clientes y productos sin transacciones asociadas.
* Consolidado de ventas por canal (Online vs. Presencial).
## 🛢️ Modelo Relacional
El esquema relacional implementado en **PostgreSQL 18** consta de 4 tablas vinculadas mediante restricciones de clave primaria y foránea:
* **categorias:** Identificador, nombre de la categoría y descripción.
* **clientes:** Datos demográficos, correo, ciudad y fecha de registro.
* **productos:** Catálogo de artículos, categoría, precio unitario, stock y estado activo.
* **ventas:** Registro transaccional con cliente, producto, cantidad, fecha y precio unitario histórico.
## 🛠️ Tecnologías Utilizadas
* **Motor de Base de Datos:** PostgreSQL 18
* **Entorno de Gestión:** pgAdmin 4
* **Lenguaje:** SQL (DDL, DML, Joins, Agrupaciones y Funciones de agregación)
## 📁 Estructura del Repositorio
* `sql/` : Scripts DDL (creación de tablas), DML (inserción de datos) y consultas analíticas de negocio.
* `README.md` : Documentación técnica del proyecto.
## ⚡ Instrucciones de Ejecución (pgAdmin 4)
1. Abrir **pgAdmin 4** y conectarse al servidor de **PostgreSQL 18**.
2. Crear una nueva base de datos llamada `retailpro_db`.
3. Abrir la herramienta de consultas (**Query Tool**).
4. Ejecutar las secciones en el siguiente orden:
   * **Sección 1 y 2 (DDL):** `DROP TABLE` y `CREATE TABLE` para construir la estructura relacional.
   * **Sección 3 (DML):** `INSERT INTO` para cargar los datos de categorías, clientes, productos y ventas.
   * **Sección 4 (Validación y Consultas):** Ejecutar las consultas de negocio (Pre-entrega 4 y Pre-entrega 5).
## 📊 Consulta Destacada: Vista Base (INNER JOIN)
```sql
SELECT 
    v.fecha_venta,
    c.id_cliente,
    c.nombre AS nombre_cliente,
    c.ciudad,
    p.id_producto,
    p.nombre_producto,
    p.id_categoria,
    v.cantidad,
    v.precio_unitario,
    (v.cantidad * v.precio_unitario) AS total_venta
FROM ventas AS v
INNER JOIN clientes AS c ON v.id_cliente = c.id_cliente
INNER JOIN productos AS p ON v.id_producto = p.id_producto
ORDER BY v.fecha_venta ASC;


Autor y Contacto
•	Analista: [Alicia Carmen del Milagro Vulcano)
•	GitHub: @coquivulcano84-png
