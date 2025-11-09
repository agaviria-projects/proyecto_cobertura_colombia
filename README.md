# 🧩 Proyecto Cobertura Colombia (Python + MySQL)

Este proyecto tiene como objetivo **automatizar la creación y carga de una base de datos relacional sobre la cobertura móvil y condiciones socioeconómicas de Colombia (2017–2024)**.  
Combina un **script Python** que ejecuta el proceso ETL (Extracción, Transformación y Carga) con un archivo **SQL** que replica la estructura final de la base.

---

## ⚙️ Archivos principales

### 📜 1. `crear_y_cargar_cobertura_colombia_final.py`
**Lenguaje:** Python  
**Descripción:**  
Script que crea automáticamente la base de datos `cobertura_colombia` en MySQL, define las tablas normalizadas y carga de 8.000 registros a partir del archivo CSV limpio `cobertura_colombia_2017_2024_limpio_V2.csv`.

#### 🔹 Funcionalidades principales:
- Conexión automática a MySQL usando `mysql.connector` o `mariadb`.  
- Creación de las tablas:  
  `departamentos`, `municipios`, `centros_poblados`, `proveedores`, `indicadores_socioeconomicos`, `cobertura_movil`.  
- Inserción masiva de registros con `executemany()`.  
- Validación de claves foráneas (relaciones jerárquicas entre departamentos, municipios y centros poblados).  
- Cierre controlado de conexión con mensajes de éxito y registro de errores.

#### 🧱 Ejemplo de ejecución
```bash
python crear_y_cargar_cobertura_colombia_final.py

✅ Conexión exitosa a MySQL.
📦 Base de datos 'cobertura_colombia' lista.
🧱 Tablas creadas correctamente.
📄 Archivo cargado: 8000 registros detectados.
✅ Base de datos creada y 8000 registros cargados correctamente.

🧰 2. COBER20251108.sql

Lenguaje: SQL (MySQL Dump)
Descripción:
Contiene la estructura y los datos resultantes generados por el script anterior.
Permite reconstruir la base cobertura_colombia sin necesidad de ejecutar Python, simplemente importándolo desde MySQL Workbench o consola.

📦 Tablas incluidas:

departamentos

municipios

centros_poblados

proveedores

indicadores_socioeconomicos

cobertura_movil

Cada tabla mantiene integridad referencial mediante claves foráneas (FOREIGN KEY) y acciones en cascada (ON UPDATE CASCADE).

🧩 Modelo relacional
### 📊 Diagrama visual

![Modelo Entidad-Relación](./modelo.png)

🚀 Ejecución rápida

1️⃣ Instalar dependencias:
pip install pandas mysql-connector-python mariadb.

2️⃣ Configurar la conexión MySQL dentro del script (usuario y contraseña).
3️⃣ Ejecutar el script:
python crear_y_cargar_cobertura_colombia_final.py

4️⃣ Verificar la base creada:
SHOW DATABASES;
USE cobertura_colombia;
SHOW TABLES;

🧠 Objetivo del proyecto

El propósito es automatizar un flujo ETL completo con Python y MySQL, aplicable a análisis de datos públicos o empresariales.
Sirve como práctica profesional de modelado relacional, limpieza de datos y carga masiva.

👨‍💻 Autores:
•	Laura Daniela Hoyos Peña
•	Héctor Alejandro Gaviria Marín
•	Angela María López Parra
•	Esneider Alonso Sánchez López
•	Ana María Agudelo Grisales
