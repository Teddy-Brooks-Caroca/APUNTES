# Introducción a las Bases de Datos y SQL

Las bases de datos son sistemas de almacenamiento de información estructurada que permiten la gestión eficiente de grandes cantidades de datos. El lenguaje SQL (Structured Query Language) es el lenguaje estándar utilizado para interactuar con bases de datos relacionales, permitiendo crear, manipular y consultar datos.

## Conceptos preliminares

- **Bases de Datos**: Conjunto de datos relacionados entre sí, organizados y estructurados de manera que se puedan extraer y actualizar fácilmente.
- **Tablas**: Estructuras bidimensionales compuestas por filas (registros) y columnas (campos), donde se almacenan los datos.
- **SQL**: Lenguaje de programación utilizado para gestionar y manipular bases de datos relacionales.

## Modificación de estructuras

Las bases de datos son dinámicas, lo que significa que su estructura puede modificarse según las necesidades. SQL proporciona comandos para crear, alterar y eliminar tablas, así como para agregar, modificar o eliminar campos dentro de ellas.

Ejemplo de creación de una tabla:

```sql
CREATE TABLE Estudiantes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    edad INT
);
```

## Inserción de datos

Una vez creada la estructura de la tabla, se pueden insertar registros utilizando el comando `INSERT INTO`.

```sql
INSERT INTO Estudiantes (nombre, edad) VALUES ('Juan', 20), ('María', 22);
```

# Importación de tablas externas

## Generar tablas desde Scripts SQL

Los scripts SQL son archivos de texto que contienen una serie de comandos SQL. Pueden utilizarse para crear tablas, insertar datos y realizar otras operaciones en la base de datos.

```sql
-- Crear tabla Profesores
CREATE TABLE Profesores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    asignatura VARCHAR(30)
);

-- Insertar datos en la tabla Profesores
INSERT INTO Profesores (nombre, asignatura) VALUES
    ('Ana', 'Matemáticas'),
    ('Pedro', 'Historia'),
    ('Lucía', 'Física');
```

## Consultar tablas

El comando `SELECT` se utiliza para consultar y recuperar datos de una o más tablas. Permite especificar qué campos se desean mostrar y aplicar filtros y ordenamientos.

```sql
SELECT nombre, asignatura FROM Profesores;
```

## Predicado de consulta SQL

Los predicados son condiciones que se aplican en las consultas SQL para filtrar los resultados. Los operadores más comunes son `=`, `<>`, `>`, `<`, `LIKE`, `IN`, etc.

```sql
SELECT * FROM Estudiantes WHERE edad > 21;
```

# Respaldar Base de datos

## Backup con MySQL Workbench

MySQL Workbench es una herramienta gráfica que permite realizar backups de bases de datos de manera sencilla. Basta con seleccionar la base de datos, especificar la ruta de destino y elegir las opciones deseadas.

## Restaurar un backup

Para restaurar un backup, se utiliza el comando `SOURCE` o `\. nombreArchivo.sql` en la línea de comandos de MySQL. También se puede hacer desde MySQL Workbench importando el archivo de backup.

## Funciones integradas de texto

MySQL proporciona varias funciones para manipular cadenas de texto, como `CONCAT()`, `SUBSTRING()`, `REPLACE()`, `TRIM()`, `LOWER()`, `UPPER()`, entre otras.

```sql
SELECT CONCAT(nombre, ' ', apellido) AS nombre_completo FROM Estudiantes;
```

## Funciones integradas de fecha

Existen funciones específicas para trabajar con fechas, como `DATE()`, `MONTH()`, `YEAR()`, `DATEDIFF()`, `DATE_FORMAT()`, etc.

```sql
SELECT DATE_FORMAT(fecha_nacimiento, '%d/%m/%Y') AS fecha_formato FROM Estudiantes;
```

## Funciones matemáticas integradas

MySQL incluye funciones matemáticas como `ABS()`, `ROUND()`, `SQRT()`, `POW()`, `SIN()`, `COS()`, `TAN()`, entre otras.

```sql
SELECT ROUND(PI(), 2) AS valor_pi;
```

## Funciones de agregado y agrupamiento

Las funciones de agregado (como `SUM()`, `COUNT()`, `AVG()`, `MAX()`, `MIN()`) se utilizan en combinación con la cláusula `GROUP BY` para resumir y agrupar datos.

```sql
SELECT asignatura, COUNT(*) AS cantidad_profesores FROM Profesores GROUP BY asignatura;
```

# Consulta de creación de tabla: CREATE TABLE

Ya se ha visto un ejemplo de la consulta `CREATE TABLE` al principio. Esta sentencia permite crear nuevas tablas en la base de datos, definiendo los campos y sus tipos de datos.

# Consulta de actualización: DML UPDATE

La consulta `UPDATE` se utiliza para modificar los valores de uno o más campos en registros existentes de una tabla.

```sql
UPDATE Estudiantes SET edad = 21 WHERE id = 3;
```

# Consulta de eliminación: DML DELETE

El comando `DELETE` elimina uno o más registros de una tabla según las condiciones especificadas.

```sql
DELETE FROM Estudiantes WHERE edad < 18;
```

# Consulta de datos anexados: DML INSERT

Ya se ha visto un ejemplo de `INSERT INTO` al principio. Esta consulta se utiliza para insertar nuevos registros en una tabla.

# Creación, actualización, modificación de tablas

Además de `CREATE TABLE`, existen otras consultas para modificar la estructura de las tablas:

- `ALTER TABLE`: Agrega, modifica o elimina campos en una tabla existente.
- `DROP TABLE`: Elimina completamente una tabla y todos sus datos.
- `RENAME TABLE`: Cambia el nombre de una tabla.

# Subconsultas

Las subconsultas son consultas SQL anidadas dentro de otras consultas. Permiten realizar operaciones complejas y filtrar datos de manera eficiente.

```sql
SELECT nombre, edad
FROM Estudiantes
WHERE edad > (SELECT AVG(edad) FROM Estudiantes);
```

## Uso del condicional CASE

La construcción `CASE` es una expresión condicional que permite evaluar diferentes condiciones y devolver diferentes resultados según la condición que se cumpla.

```sql
SELECT nombre,
    CASE
        WHEN edad < 18 THEN 'Menor de edad'
        WHEN edad >= 18 AND edad <= 25 THEN 'Joven'
        ELSE 'Adulto'
    END AS categoria_edad
FROM Estudiantes;
```

## Combinación de consultas - UNION

La cláusula `UNION` se utiliza para combinar los resultados de dos o más consultas `SELECT` en un solo conjunto de resultados.

```sql
SELECT nombre, edad FROM Estudiantes
UNION
SELECT nombre, edad FROM Profesores;
```

## Consultas relacionadas

Las consultas relacionadas se utilizan para combinar datos de varias tablas mediante la cláusula `JOIN`. Existen diferentes tipos de `JOIN` (INNER, LEFT, RIGHT, FULL) que determinan cómo se combinan los registros.

```sql
SELECT Estudiantes.nombre, Profesores.nombre AS profesor, Profesores.asignatura
FROM Estudiantes
INNER JOIN Profesores ON Estudiantes.id_profesor = Profesores.id;
```

## Otros tipos de JOIN

Además del `INNER JOIN` (que devuelve solo los registros coincidentes en ambas tablas), existen otros tipos de JOIN:

- `LEFT JOIN`: Devuelve todos los registros de la tabla izquierda y los registros coincidentes de la tabla derecha.
- `RIGHT JOIN`: Devuelve todos los registros de la tabla derecha y los registros coincidentes de la tabla izquierda.
- `FULL JOIN`: Devuelve todos los registros de ambas tablas, con `NULL` en los campos que no coincidan.

