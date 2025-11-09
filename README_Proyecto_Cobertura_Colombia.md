# 🧩 Proyecto Cobertura Colombia (Python + MySQL)

Este proyecto tiene como objetivo **automatizar la creación y carga de una base de datos relacional sobre la cobertura móvil y condiciones socioeconómicas de Colombia (2017–2024)**.  
Combina un **script Python** que ejecuta el proceso ETL (Extracción, Transformación y Carga) con un archivo **SQL** que replica la estructura final de la base.

---

## ⚙️ Archivos principales

### 📜 1. `crear_y_cargar_cobertura_colombia_final.py`
**Lenguaje:** Python  
**Descripción:**  
Script que crea automáticamente la base de datos `cobertura_colombia` en MySQL, define las tablas normalizadas y carga más de 8.000 registros a partir del archivo CSV limpio `cobertura_colombia_2017_2024_limpio_V2.csv`.

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
```

**Salida esperada:**
```
✅ Conexión exitosa a MySQL.
📦 Base de datos 'cobertura_colombia' lista.
🧱 Tablas creadas correctamente.
📄 Archivo cargado: 8000 registros detectados.
✅ Base de datos creada y 8000 registros cargados correctamente.
```

---

### 🧰 2. `COBER20251108.sql`
**Lenguaje:** SQL (MySQL Dump)  
**Descripción:**  
Contiene la estructura y los datos resultantes generados por el script anterior.  
Permite reconstruir la base `cobertura_colombia` sin necesidad de ejecutar Python, simplemente importándolo desde MySQL Workbench o consola.

#### 📦 Tablas incluidas:
- `departamentos`
- `municipios`
- `centros_poblados`
- `proveedores`
- `indicadores_socioeconomicos`
- `cobertura_movil`

Cada tabla mantiene integridad referencial mediante claves foráneas (`FOREIGN KEY`) y acciones en cascada (`ON UPDATE CASCADE`).

---

## 🧩 Modelo relacional
### 📊 Diagrama visual
![Modelo Entidad-Relación](./Modelo.png)

---

## 🚀 Ejecución rápida

1️⃣ **Instalar dependencias:**
```bash
pip install pandas mysql-connector-python mariadb
```

2️⃣ **Configurar la conexión MySQL** dentro del script (usuario y contraseña).  
3️⃣ **Ejecutar el script:**
```bash
python crear_y_cargar_cobertura_colombia_final.py
```
4️⃣ **Verificar la base creada:**
```sql
SHOW DATABASES;
USE cobertura_colombia;
SHOW TABLES;
```

---

## 🧠 Objetivo del proyecto

El propósito es **automatizar un flujo ETL completo con Python y MySQL**, aplicable a análisis de datos públicos o empresariales.  
Sirve como práctica profesional de modelado relacional, limpieza de datos y carga masiva.


## 📘 Glosario de términos

| Término / Campo | Definición o Explicación |
|-----------------|--------------------------|
| **Base de Datos Relacional (RDBMS)** | Sistema que organiza la información en tablas relacionadas mediante claves primarias y foráneas (en este caso, se usa MySQL/MariaDB). |
| **Normalización de Datos** | Proceso de organizar los datos para reducir redundancias y mejorar la integridad. En el proyecto se aplican varias tablas (departamentos, municipios, proveedores, etc.) en vez de una sola grande. |
| **Departamento** | División territorial principal de Colombia (equivalente a una “región” o “estado”). |
| **Municipio** | Subdivisión administrativa dentro de un departamento. Contiene una o varias localidades o centros poblados. |
| **Centro Poblado** | Área habitada dentro de un municipio (puede ser cabecera municipal o zona rural concentrada). |
| **Cabecera Municipal** | Población principal del municipio, donde usualmente se encuentra la administración local. |
| **Proveedor** | Empresa que ofrece servicios de telecomunicaciones móviles (ej. Claro, Tigo, Movistar). |
| **Nombre Comercial** | Denominación bajo la cual opera el proveedor ante los usuarios (puede diferir del nombre jurídico). |
| **Indicadores Socioeconómicos** | Conjunto de variables que describen el nivel de desarrollo o condiciones de vida de una población (ingresos, pobreza, desempleo, etc.). |
| **Estrato Promedio** | Promedio del nivel socioeconómico de los hogares de un municipio, según clasificación oficial de Colombia (1 a 6). |
| **Ingreso Promedio del Hogar** | Valor promedio mensual o anual que reciben los hogares en un municipio. |
| **Tasa de Pobreza** | Porcentaje de la población con ingresos por debajo del umbral de pobreza definido nacionalmente. |
| **Índice NBI (Necesidades Básicas Insatisfechas)** | Indicador que mide las carencias esenciales en vivienda, educación, servicios, etc. |
| **Tasa de Desempleo** | Porcentaje de personas que no tienen empleo pero buscan activamente trabajo. |
| **Tasa de Electrificación** | Porcentaje de hogares que tienen acceso al servicio de energía eléctrica. |
| **Pct. Hogares con Internet** | Porcentaje de hogares con acceso a Internet fijo o móvil. |
| **Inversión Pública per Cápita** | Monto promedio de inversión pública por persona en un municipio. |
| **Cobertura Móvil** | Disponibilidad o acceso de señal de red móvil (2G, 3G, 4G, LTE, 5G) en una zona determinada. |
| **2G / 3G / 4G / LTE / 5G** | Generaciones de tecnología móvil, donde cada una mejora la velocidad y calidad de conexión. |
| **Cobertura HSPA / HSPA+ / DC-HSPA** | Tecnologías intermedias entre 3G y 4G, que mejoran la velocidad de transmisión. |
| **CSV (Comma Separated Values)** | Formato de archivo de texto en el que los datos se separan por comas, usado para importar/exportar grandes volúmenes de información. |
| **Script en Python** | Archivo que contiene código Python para automatizar tareas (en este caso, crear la base de datos y cargar los datos). |
| **Librería Pandas** | Herramienta de Python para manejo y análisis de datos en estructuras tipo tabla (DataFrames). |
| **MySQL Connector / mariadb** | Módulos de Python que permiten conectarse y ejecutar comandos en bases de datos MySQL o MariaDB. |
| **Cursor SQL** | Objeto que ejecuta consultas y comandos dentro de una conexión a base de datos. |
| **Commit** | Operación que guarda definitivamente los cambios realizados en una transacción de base de datos. |
| **Foreign Key (Clave Foránea)** | Campo que establece una relación entre dos tablas (por ejemplo, `cod_departamento` en municipios apunta a `departamentos`). |
| **Primary Key (Clave Primaria)** | Campo único que identifica de forma exclusiva cada registro dentro de una tabla. |
| **INSERT IGNORE** | Comando SQL que inserta registros nuevos, ignorando los duplicados para evitar errores. |
| **AVG()** | Función SQL que calcula el promedio de los valores de una columna. |
| **ROUND()** | Función SQL que redondea un número a cierta cantidad de decimales. |
| **CASE WHEN ... THEN ... ELSE ... END** | Expresión condicional en SQL que permite evaluar condiciones (similar a un `if` en Python). |
| **JOIN / Relación entre Tablas** | Vinculación entre dos o más tablas mediante claves comunes para combinar información. |
| **Brecha Digital** | Diferencia en el acceso, uso o aprovechamiento de las tecnologías de la información entre diferentes grupos sociales o territoriales. |
| **Dataset** | Conjunto estructurado de datos (en este caso, los registros del archivo CSV cargado). |
| **iterrows()** | Función de Pandas que permite recorrer un DataFrame fila por fila. |
| **DataFrame** | Estructura de datos en Pandas que almacena información tabular (similar a una hoja de cálculo). |
| **UTF-8 / UTF8MB4** | Codificación de texto que permite representar caracteres especiales y acentos de forma segura. |
| **ENGINE=InnoDB** | Motor de almacenamiento de MySQL que permite integridad referencial y transacciones. |
| **Códigos de Centros Poblados** | Sistema de codificación jerárquica usado por el DANE para identificar territorialmente cada unidad. Ejemplo: Departamento Antioquia: 05 Medellín (Municipio): 05001 Palmitas (Centro Poblado): 05001001 Santa Elena (Centro Poblado): 05001004 |
| **Altitud msnm** | Sigla de metros sobre el nivel del mar. Indica la altura de un punto geográfico respecto al nivel medio del mar. |

---

📘 **Versión:** Noviembre 2025  
📍 **Repositorio:** [agaviria-projects / proyecto_cobertura_colombia](https://github.com/agaviria-projects/proyecto_cobertura_colombia)


---

## 👨‍💻 Autores

- **Laura Daniela Hoyos Peña**  
- **Héctor Alejandro Gaviria Marín**  
- **Ángela María López Parra**  
- **Esneider Alonso Sánchez López**  
- **Ana María Agudelo Grisales**

---