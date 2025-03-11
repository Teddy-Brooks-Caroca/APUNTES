
---

# CUADERNO DE FÓRMULAS EN SQL – NIVEL ELEMENTAL

## ÍNDICE

1. ESTRUCTURA DE CONSULTAS EN SQL
2. OPERADORES LÓGICOS Y DE COMPARACIÓN
3. MODIFICACIÓN DE ESTRUCTURAS DE TABLAS (ALTER TABLE)
4. FUNCIONES DE TIEMPO
5. FUNCIONES DE CADENA
6. FUNCIONES DE CONVERSIÓN Y MANEJO DE VALORES NULOS
7. FUNCIONES MATEMÁTICAS
8. FUNCIONES DE AGREGACIÓN Y AGRUPAMIENTO
9. OPERADORES Y FUNCIONES DE CONJUNTOS (UNION, EXCEPT)
10. JOIN EN SQL
11. FUNCIONES DML
12. SUBCONSULTAS
13. ÍNDICES Y VISTAS
14. USO DEL CASE

---

## 1. ESTRUCTURA DE CONSULTAS EN SQL

### CLÁUSULAS BÁSICAS

- **SELECT**  
    _Explicación:_ Permite especificar las columnas que se desean obtener de una o varias tablas.  
    Ejemplo:
    
    ```sql
    SELECT columna
    FROM tabla;
    ```
    
- **FROM**  
    _Explicación:_ Indica la fuente de datos (tabla) de donde se extraerán las columnas especificadas.
    
- **WHERE**  
    _Explicación:_ Filtra las filas según una condición específica, retornando solo aquellas que cumplen el criterio.  
    Ejemplo:
    
    ```sql
    SELECT columna
    FROM tabla
    WHERE condición;
    ```
    

### AGRUPACIÓN Y FILTRADO DE GRUPOS

- **GROUP BY**  
    _Explicación:_ Agrupa las filas que comparten los mismos valores en las columnas especificadas para poder aplicar funciones de agregación sobre cada grupo.
    
- **HAVING**  
    _Explicación:_ Filtra los grupos creados con GROUP BY según una condición, similar a cómo WHERE filtra filas.  
    Ejemplo:
    
    ```sql
    SELECT columna
    FROM tabla
    WHERE condición
    GROUP BY columna
    HAVING condición;
    ```
    

### ORDENAMIENTO, LÍMITES Y OFFSET

- **ORDER BY**  
    _Explicación:_ Ordena el conjunto de resultados de la consulta en forma ascendente (ASC) o descendente (DESC).  
    Ejemplo:
    
    ```sql
    SELECT columna
    FROM tabla
    WHERE condición
    ORDER BY columna ASC|DESC;
    ```
    
- **LIMIT**  
    _Explicación:_ Restringe el número de registros que se muestran en el resultado.  
    Ejemplo:
    
    ```sql
    SELECT columna
    FROM tabla
    WHERE condición
    LIMIT cantidad;
    ```
    
- **OFFSET**  
    _Explicación:_ Omite un número determinado de filas antes de comenzar a devolver los resultados. Es útil para paginar resultados en conjunto con LIMIT.  
    Ejemplo:
    
    ```sql
    SELECT columna
    FROM tabla
    ORDER BY columna
    LIMIT cantidad OFFSET número_de_filas_a_omitir;
    ```
    

### CONSULTA STANDARD Y SQL SERVER

- **Consulta Standard:**  
    _Explicación:_ Estructura básica de una consulta SQL utilizando las cláusulas vistas.
    
    ```sql
    SELECT columna
    FROM tabla
    WHERE condición
    ORDER BY columna ASC|DESC
    LIMIT cantidad OFFSET número_de_filas_a_omitir;
    ```
    
- **TOP (SQL SERVER):**  
    _Explicación:_ Limita el número de registros devueltos; es equivalente a LIMIT en otros SGBD.  
    Ejemplo:
    
    ```sql
    SELECT TOP cantidad columna
    FROM tabla;
    ```
    

---

## 2. OPERADORES LÓGICOS Y DE COMPARACIÓN

- **AND**  
    _Explicación:_ Combina dos o más condiciones que deben cumplirse simultáneamente.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE condicion1 AND condicion2;
    ```
    
- **OR**  
    _Explicación:_ Permite que se cumpla al menos una de las condiciones especificadas.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE condicion1 OR condicion2;
    ```
    
- **NOT**  
    _Explicación:_ Niega una condición, devolviendo los registros que no cumplen la condición.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE NOT condicion;
    ```
    
- **IN**  
    _Explicación:_ Verifica si un valor se encuentra dentro de un conjunto de valores.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE columna IN (valor1, valor2, valor3);
    ```
    
- **BETWEEN**  
    _Explicación:_ Especifica un rango de valores, incluyendo los extremos.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE columna BETWEEN valor_inferior AND valor_superior;
    ```
    
- **LIKE**  
    _Explicación:_ Permite buscar patrones en cadenas de texto utilizando comodines (por ejemplo, `%`).  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE columna LIKE '%texto%';
    ```
    
- **IS NULL / IS NOT NULL**  
    _Explicación:_ Verifica si una columna contiene valores nulos o no nulos.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE columna IS NULL;
    
    SELECT * FROM tabla
    WHERE columna IS NOT NULL;
    ```
    
- **Operadores de comparación (=, <, >, <=, >=, <>)**  
    _Explicación:_ Comparan valores numéricos o de texto para determinar relaciones de igualdad, desigualdad o mayor/menor.  
    Ejemplo:
    
    ```sql
    SELECT * FROM tabla
    WHERE columna = 'valor';
    
    SELECT * FROM tabla
    WHERE columna <> 'valor';
    ```
    

---

## 3. MODIFICACIÓN DE ESTRUCTURAS DE TABLAS (ALTER TABLE)

### RENOMBRAR TABLAS

- **ALTER TABLE ... RENAME / RENAME TO**  
    _Explicación:_ Se utiliza para cambiar el nombre de una tabla existente.  
    Ejemplo Standard:
    
    ```sql
    ALTER TABLE nombre_tabla RENAME nuevo_nombre;
    ```
    
    En PostgreSQL:
    
    ```sql
    ALTER TABLE nombre_tabla RENAME TO nuevo_nombre;
    ```
    

### CAMBIAR TIPO DE DATOS Y NOMBRES DE COLUMNAS

- **MODIFY (MySQL)**  
    _Explicación:_ Permite cambiar el tipo de dato o modificar las propiedades de una columna en MySQL.  
    Ejemplo:
    
    ```sql
    ALTER TABLE tabla MODIFY columna NUEVO_TIPO;
    ```
    
- **CHANGE (MySQL)**  
    _Explicación:_ Permite renombrar una columna y, a la vez, cambiar sus atributos.  
    Ejemplo:
    
    ```sql
    ALTER TABLE tabla CHANGE columna nueva_columna atributos;

	# En POSTGREE SQL - PGADMIN:

	ALTER TABLE tabla RENAME COLUMN columna TO nueva_columna;
    ```
    

### AGREGAR Y ELIMINAR COLUMNAS O TABLAS

- **ADD COLUMN**  
    _Explicación:_ Agrega una nueva columna a la estructura de una tabla.  
    Ejemplo en PostgreSQL (PgAdmin):
    
    ```sql
    ALTER TABLE tabla ADD COLUMN nueva_columna atributo AFTER columna_que_va_antes;
    ```
    
- **DROP COLUMN**  
    _Explicación:_ Elimina una columna de una tabla existente.  
    Ejemplo:
    
    ```sql
    ALTER TABLE tabla DROP COLUMN columna;
    ```
    
- **DROP TABLE**  
    _Explicación:_ Elimina por completo una tabla y todos sus registros del sistema de bases de datos.  
    Ejemplo:
    
    ```sql
    DROP TABLE tabla;
    ```
    

---

## 4. FUNCIONES DE TIEMPO

_Recuerda que estas funciones operan correctamente cuando el tipo de dato es DATE o DATETIME._

- **YEAR()**  
    _Explicación:_ Extrae y devuelve el componente de año de una fecha.  
    Ejemplo:
    
    ```sql
    SELECT YEAR(fecha) AS 'Año' FROM facturas;
    ```
    
- **MONTH()**  
    _Explicación:_ Devuelve el mes de una fecha.  
    Ejemplo:
    
    ```sql
    SELECT MONTH(fecha) AS 'Mes' FROM facturas;
    ```
    
- **DAY()**  
    _Explicación:_ Extrae y devuelve el día de la fecha.  
    Ejemplo:
    
    ```sql
    SELECT DAY(fecha) AS 'DIA' FROM facturas;
    ```
    
- **HOUR()**  
    _Explicación:_ Extrae la hora de un valor DATETIME.  
    Ejemplo:
    
    ```sql
    SELECT HOUR(fecha) AS 'HORA' FROM facturas;
    ```
    
- **CURDATE()**  
    _Explicación:_ Devuelve la fecha actual sin incluir la hora en MySQL.  
    Ejemplo:
    
    ```sql
    SELECT CURDATE() AS 'FECHA ACTUAL';
    ```
    
- **NOW()**  
    _Explicación:_ Retorna la fecha y hora actuales en MySQL.  
    Ejemplo:
    
    ```sql
    SELECT NOW() AS 'FECHA ACTUAL';
    ```
    
- **GETDATE()**  
    _Explicación:_ Obtiene la fecha y hora actuales del servidor en SQL Server.  
    Ejemplo:
    
    ```sql
    SELECT GETDATE() AS FechaHoraActual;
    ```
    
- **DATE_FORMAT()**  
    _Explicación:_ Permite formatear una fecha de acuerdo a un formato especificado en MySQL.  
    Ejemplo:
    
    ```sql
    DATE_FORMAT(FECHA, FORMATO);
    ```
    
- **TIMESTAMPDIFF()**  
    _Explicación:_ Calcula la diferencia entre dos fechas en la unidad especificada (meses, años, etc.).  
    Ejemplo:
    
    ```sql
    SELECT TIMESTAMPDIFF(MONTH, '2020-01-01', '2020-06-30') AS 'MESES TRANSCURRIDOS';
    ```
    
- **DAYNAME()**  
    _Explicación:_ Devuelve el nombre del día de la semana de una fecha.  
    Ejemplo:
    
    ```sql
    SELECT DAYNAME(CURDATE()) AS 'Nombre del día';
    ```
    
- **MONTHNAME()**  
    _Explicación:_ Extrae y devuelve el nombre del mes de una fecha.  
    Ejemplo:
    
    ```sql
    SELECT MONTHNAME(CURDATE()) AS 'Nombre del mes';
    ```
    
- **DAYOFWEEK()**  
    _Explicación:_ Retorna un número que representa el día de la semana.  
    Ejemplo:
    
    ```sql
    SELECT DAYOFWEEK(CURDATE()) AS 'Número del día de la semana';
    ```
    
- **DAYOFYEAR()**  
    _Explicación:_ Devuelve el número del día en el año para una fecha dada.  
    Ejemplo:
    
    ```sql
    SELECT DAYOFYEAR(CURDATE()) AS 'Día del año';
    ```
    
- **ADDDATE()**  
    _Explicación:_ Suma un intervalo de tiempo (por ejemplo, meses) a una fecha dada.  
    Ejemplo:
    
    ```sql
    ADDDATE(CURDATE(), INTERVAL 2 MONTH) AS 'Vencimiento a 2 meses';
    ```
    

---

## 5. FUNCIONES DE CADENA

### MANIPULACIÓN DE TEXTO

- **CONCAT()**  
    _Explicación:_ Une dos o más cadenas de texto en una sola cadena.  
    Ejemplo:
    
    ```sql
    SELECT CONCAT('Sr./a. ', NOMBRE, ' ', APELLIDO) AS 'Nombre completo' FROM clientes;
    ```
    
- **CONCAT_WS()**  
    _Explicación:_ Une cadenas utilizando un separador especificado entre cada valor.  
    Ejemplo:
    
    ```sql
    SELECT CONCAT_WS(',', nombre, apellido, cuit, direccion) AS 'Datos Completos' FROM clientes;
    ```
    
- **UPPER()**  
    _Explicación:_ Convierte todos los caracteres de una cadena a mayúsculas.  
    Ejemplo:
    
    ```sql
    SELECT UPPER(nombre) AS Nombres FROM clientes;
    ```
    
- **LOWER()**  
    _Explicación:_ Convierte todos los caracteres de una cadena a minúsculas.  
    Ejemplo:
    
    ```sql
    SELECT LOWER(apellido) FROM clientes;
    ```
    
- **LEFT()**  
    _Explicación:_ Extrae los primeros N caracteres de una cadena.  
    Ejemplo:
    
    ```sql
    SELECT CONCAT(LEFT(nombre, 1), '.') AS Inicial_nombre FROM clientes;
    ```
    
- **RIGHT()**  
    _Explicación:_ Extrae los últimos N caracteres de una cadena.  
    Ejemplo:
    
    ```sql
    SELECT RIGHT(cuit, 1) AS 'Dígito verificador' FROM clientes;
    ```
    
- **REPLACE()**  
    _Explicación:_ Sustituye todas las ocurrencias de una subcadena por otra dentro de una cadena.  
    Ejemplo:
    
    ```sql
    SELECT REPLACE(COLUMNA, ' ', '-') FROM TABLA;
    ```
    
- **SUBSTRING()**  
    _Explicación:_ Extrae una subcadena a partir de una posición específica y con una longitud determinada.  
    Ejemplo:
    
    ```sql
    SELECT SUBSTRING(COLUMNA, POSICIÓN_DE_INICIO, CANTIDAD_A_EXTRAER) FROM TABLA;
    ```
    
- **CHAR_LENGTH()**  
    _Explicación:_ Cuenta el número total de caracteres en una cadena, incluyendo los espacios.  
    Ejemplo:
    
    ```sql
    SELECT direccion, CHAR_LENGTH(direccion) AS 'Cantidad de caracteres' FROM clientes;
    ```
    
- **LOCATE()**  
    _Explicación:_ Devuelve la posición de la primera aparición de una subcadena dentro de otra cadena.  
    Ejemplo:
    
    ```sql
    SELECT direccion, LOCATE('ara', direccion) AS 'Posición' FROM clientes;
    ```
    
- **TRIM()**  
    _Explicación:_ Elimina los espacios en blanco al inicio y al final de una cadena.  
    Ejemplo:
    
    ```sql
    SELECT TRIM(direccion) AS Direccion_Correcta FROM clientes;
    ```
    
- **LTRIM()**  
    _Explicación:_ Elimina los espacios en blanco solo al inicio de una cadena.  
    Ejemplo:
    
    ```sql
    SELECT LTRIM(direccion) AS Direccion_Correcta FROM clientes;
    ```
    
- **RTRIM()**  
    _Explicación:_ Elimina los espacios en blanco solo al final de una cadena.  
    Ejemplo:
    
    ```sql
    SELECT RTRIM(direccion) AS Direccion_Correcta FROM clientes;
    ```
    

### FUNCIONES ESPECIALES DE TEXTO Y ALEATORIEDAD

- **RAND()**  
    _Explicación:_ Genera un número aleatorio (generalmente entre 0 y 1).  
    Ejemplo:
    
    ```sql
    SELECT RAND();
    ```
    
- **MD5()**  
    _Explicación:_ Calcula el hash MD5 de un valor, generando una cadena única de 32 caracteres.  
    Ejemplo:
    
    ```sql
    SELECT MD5('texto');
    ```
    
- **SPLIT_PART()**  
    _Explicación:_ Divide una cadena utilizando un delimitador y devuelve la parte especificada. (Principalmente en PostgreSQL)  
    Ejemplo:
    
    ```sql
    SELECT SPLIT_PART('hola,mundo,sql', ',', 2) AS resultado;
    ```
    

---

## 6. FUNCIONES DE CONVERSIÓN Y MANEJO DE VALORES NULOS

- **CAST()**  
    _Explicación:_ Convierte un valor de un tipo de dato a otro especificado.  
    Ejemplo:
    
    ```sql
    SELECT CAST('123' AS SIGNED);
    ```
    
- **COALESCE()**  
    _Explicación:_ Retorna el primer valor no nulo de una lista de argumentos, útil para evitar valores nulos.  
    Ejemplo:
    
    ```sql
    SELECT COALESCE(NULL, 'Valor por defecto');
    ```
    
- **ISNULL()**  
    _Explicación:_ Función propia de SQL Server que reemplaza un valor nulo por otro valor especificado; acepta solo dos argumentos.  
    Ejemplo:
    
    ```sql
    SELECT ISNULL(NULL, 'Valor por defecto');
    ```
    

---

## 7. FUNCIONES MATEMÁTICAS

- **ROUND()**  
    _Explicación:_ Redondea un número a una cantidad determinada de decimales.  
    Ejemplo:
    
    ```sql
    SELECT ROUND(columna_o_valor, cantidad_de_decimales) FROM tabla;
    ```
    
- **CEIL()**  
    _Explicación:_ Redondea un número hacia arriba, devolviendo el entero inmediatamente mayor o igual al número.  
    Ejemplo:
    
    ```sql
    SELECT CEIL(columna_o_valor) FROM tabla;
    ```
    
- **FLOOR()**  
    _Explicación:_ Redondea un número hacia abajo, devolviendo el entero inmediatamente menor o igual al número.  
    Ejemplo:
    
    ```sql
    SELECT FLOOR(columna_o_valor) FROM tabla;
    ```
    
- **MOD()**  
    _Explicación:_ Devuelve el resto de la división entre dos números.  
    Ejemplo:
    
    ```sql
    SELECT MOD(divisor, dividendo);
    ```
    
- **POW()**  
    _Explicación:_ Eleva un número a la potencia de otro, calculando el valor resultante.  
    Ejemplo:
    
    ```sql
    SELECT POW(multiplicador, multiplicando);
    ```
    

---

## 8. FUNCIONES DE AGREGACIÓN Y AGRUPAMIENTO

- **COUNT()**  
    _Explicación:_ Cuenta el número de filas o registros en un conjunto de datos.  
    Ejemplo:
    
    ```sql
    SELECT COUNT(*) FROM tabla;
    ```
    
- **SUM()**  
    _Explicación:_ Suma todos los valores de una columna numérica.  
    Ejemplo:
    
    ```sql
    SELECT SUM(columna) FROM tabla;
    ```
    
- **MIN()**  
    _Explicación:_ Devuelve el valor mínimo encontrado en una columna.  
    Ejemplo:
    
    ```sql
    SELECT MIN(columna) FROM tabla;
    ```
    
- **MAX()**  
    _Explicación:_ Devuelve el valor máximo encontrado en una columna.  
    Ejemplo:
    
    ```sql
    SELECT MAX(columna) FROM tabla;
    ```
    
- **AVG()**  
    _Explicación:_ Calcula el promedio de los valores de una columna numérica.  
    Ejemplo:
    
    ```sql
    SELECT AVG(columna) FROM tabla;
    ```
    
- **ROLLUP**  
    _Explicación:_ Extiende la cláusula GROUP BY para generar subtotales y un total general (super agregado).  
    Ejemplo:
    
    ```sql
    SELECT columna1, columna2, función_agregación(columna)
    FROM tabla
    GROUP BY ROLLUP(columna1, columna2);
    ```
    
    En SQL Server:
    
    ```sql
    SELECT columna, función_agregación(columna)
    FROM tabla
    GROUP BY columna WITH ROLLUP;
    ```
    
    _Ejemplo práctico:_
    
    ```sql
    SELECT COALESCE(Departamento, 'Total') AS Departamento,
           SUM(Ventas) AS Total_Ventas
    FROM Ventas
    GROUP BY Departamento WITH ROLLUP;
    ```
    

---

## 9. OPERADORES Y FUNCIONES DE CONJUNTOS (UNION, EXCEPT)

- **UNION**  
    _Explicación:_ Combina los resultados de dos consultas, eliminando filas duplicadas.  
    Ejemplo:
    
    ```sql
    SELECT cliente FROM tabla1
    UNION
    SELECT cliente FROM tabla2;
    ```
    
- **UNION ALL**  
    _Explicación:_ Combina los resultados de dos consultas sin eliminar duplicados; conserva todas las filas.  
    Ejemplo:
    
    ```sql
    SELECT cliente FROM tabla1
    UNION ALL
    SELECT cliente FROM tabla2;
    ```
    
- **EXCEPT**  
    _Explicación:_ Retorna las filas que están en la primera consulta pero no en la segunda, mostrando la diferencia entre conjuntos.  
    Ejemplo:
    
    ```sql
    SELECT cliente FROM tabla1
    EXCEPT
    SELECT cliente FROM tabla2;
    ```
    

### Ejemplo: Uso de UNION para Evitar Ambigüedad en el WHERE

_A veces, al unir tablas que tienen columnas con el mismo nombre, resulta ambiguo aplicar un filtro en la cláusula WHERE en un JOIN (pues no se sabe a cuál tabla referirse). Con UNION se pueden separar las consultas y aplicar el filtro de forma individual, eliminando la ambigüedad y permitiendo agregar una columna que indique el origen de los registros._

```sql
-- Uso incorrecto del JOIN (ambigüedad en TITULO)
SELECT * 
FROM top_spotify tp 
JOIN ultimos_lanzamientos ul ON tp.ID = ul.ID 
WHERE [NO SABES A QUE TABLA REMITIR] TITULO LIKE '%break%';

-- Uso correcto con UNION
SELECT *, 'ANTERIOR' AS ESTADO 
FROM TOP_SPOTIFY
WHERE TITULO LIKE '%BREAK%'
UNION
SELECT *, 'ULTIMO' AS ESTADO 
FROM ULTIMOS_LANZAMIENTOS
WHERE TITULO LIKE '%BREAK%'
ORDER BY TITULO;
```

> _Nota:_ Aunque en un JOIN también se puede resolver calificando las columnas (por ejemplo, `tp.TITULO` o `ul.TITULO`), el uso de UNION en este caso permite eliminar la ambigüedad de forma directa.

---

## 10. JOIN EN SQL

- **INNER JOIN**  
    _Explicación:_ Retorna únicamente las filas que tienen coincidencias en ambas tablas involucradas en la unión.  
    Ejemplo:
    
    ```sql
    SELECT * FROM clientes
    INNER JOIN pedidos ON clientes.id = pedidos.cliente_id;
    ```
    
- **LEFT JOIN**  
    _Explicación:_ Devuelve todas las filas de la tabla de la izquierda y las filas coincidentes de la tabla de la derecha (o NULL si no hay coincidencia).  
    Ejemplo:
    
    ```sql
    SELECT * FROM clientes
    LEFT JOIN pedidos ON clientes.id = pedidos.cliente_id;
    ```
    
- **RIGHT JOIN**  
    _Explicación:_ Devuelve todas las filas de la tabla de la derecha y las filas coincidentes de la tabla de la izquierda (o NULL si no hay coincidencia).  
    Ejemplo:
    
    ```sql
    SELECT * FROM pedidos
    RIGHT JOIN clientes ON pedidos.cliente_id = clientes.id;
    ```
    
- **FULL JOIN**  
    _Explicación:_ Combina las filas de ambas tablas, mostrando registros coincidentes y no coincidentes (rellenando con NULL cuando corresponda).  
    Ejemplo:
    
    ```sql
    SELECT * FROM clientes
    FULL JOIN pedidos ON clientes.id = pedidos.cliente_id;
    ```
    
- **ON (cláusula en JOIN)**  
    _Explicación:_ Especifica la condición de unión entre las tablas, determinando cómo se relacionan sus columnas.  
    Ejemplo:
    
    ```sql
    SELECT *
    FROM tabla1 t1
    JOIN tabla2 t2 ON t1.columna = t2.columna AND t2.fecha > '2024-01-01';
    ```
    

---

## 11. FUNCIONES DML

- **CREATE TABLE ... SELECT**  
    _Explicación:_ Crea una nueva tabla a partir de los resultados de una consulta, copiando estructura y datos.  
    Ejemplo (MySQL):
    
    ```sql
    CREATE TABLE nueva_tabla
    SELECT * FROM tabla_original;
    ```
    
- **SELECT INTO**  
    _Explicación:_ En SQL Server, crea una nueva tabla y la llena con los datos resultantes de una consulta.  
    Ejemplo:
    
    ```sql
    SELECT *
    INTO NUEVA_TABLA
    FROM TABLA_DE_ORIGEN;
    ```
    
- **UPDATE**  
    _Explicación:_ Modifica los valores de una o varias columnas en los registros que cumplen con una condición.  
    Ejemplo:
    
    ```sql
    UPDATE passengers
    SET fare = fare * 1.10
    WHERE pclass = 1;
    ```
    
- **INSERT INTO ... VALUES**  
    _Explicación:_ Inserta nuevos registros en una tabla, especificando los valores para cada columna.  
    Ejemplo:
    
    ```sql
    INSERT INTO passengers(passengerid, survived, pclass, name, sex, age)
    VALUES (892, true, 1, 'Brooks,Mr. Teddy Lee', 'male', 21);
    ```
    
- **INSERT INTO ... SELECT**  
    _Explicación:_ Copia datos de una tabla a otra, utilizando una consulta SELECT para obtener los registros a insertar.  
    Ejemplo:
    
    ```sql
    INSERT INTO Tabla_Destino (COLUMNAS)
    SELECT COLUMNAS FROM Tabla_Origen;
    ```
    
- **DELETE**  
    _Explicación:_ Elimina uno o varios registros de una tabla basándose en una condición.  
    Ejemplo:
    
    ```sql
    DELETE FROM passengers
    WHERE survived = false;
    ```
    
- **TRUNCATE TABLE**  
    _Explicación:_ Elimina todos los registros de una tabla de forma rápida, manteniendo su estructura.  
    Ejemplo:
    
    ```sql
    TRUNCATE TABLE NOMBRE_DE_TABLA;
    ```
    
- **DROP TABLE**  
    _Explicación:_ Elimina completamente una tabla y todos sus datos del sistema de bases de datos.  
    Ejemplo:
    
    ```sql
    DROP TABLE NOMBRE_DE_TABLA;
    ```
    

---

## 12. SUBCONSULTAS

- **SUBCONSULTA EN WHERE**  
    _Explicación:_ Una consulta anidada dentro de la cláusula WHERE que se utiliza para comparar valores o filtrar resultados basándose en otra consulta.  
    Ejemplo:
    
    ```sql
    SELECT columnas
    FROM tabla
    WHERE expresión [operador] (
      SELECT columnas
      FROM tabla
      WHERE condición
    );
    ```
    
- **SUBCONSULTA EN SELECT**  
    _Explicación:_ Una consulta anidada dentro de la lista de selección que calcula un valor para cada fila del resultado principal.  
    Ejemplo:
    
    ```sql
    SELECT (SELECT COUNT(*) FROM pedidos WHERE cliente_id = C.id) AS num_pedidos,
           C.nombre, C.apellido
    FROM clientes C;
    ```
    
- **SUBCONSULTA EN FROM**  
    _Explicación:_ Una consulta anidada que actúa como una tabla temporal para la consulta principal.  
    Ejemplo:
    
    ```sql
    SELECT *
    FROM (
      SELECT cliente_id, producto_id, cantidad
      FROM pedidos
    ) AS pedidos_temp
    WHERE cantidad > 2;
    ```
    
- **EXISTS**  
    _Explicación:_ Verifica si la subconsulta devuelve al menos un registro; se usa para comprobar la existencia de datos que cumplen una condición.  
    Ejemplo:
    
    ```sql
    SELECT EXISTS (
      SELECT 1
      FROM pedidos
      WHERE cliente_id = 10
    ) AS existe_pedido;
    ```
    
- **TABLA DUAL**  
    _Explicación:_ Una tabla especial (disponible en algunos SGBD) que contiene una sola fila y columna, utilizada para evaluaciones o consultas que no requieren datos de una tabla real.  
    Ejemplo:
    
    ```sql
    SELECT 'Existen pedidos'
    FROM DUAL
    WHERE EXISTS (
      SELECT 1
      FROM pedidos
      WHERE cliente_id = 10
    );
    ```
    

---

## 13. ÍNDICES Y VISTAS

- **CREATE INDEX**  
    _Explicación:_ Crea un índice sobre una o varias columnas de una tabla para acelerar las consultas de búsqueda.  
    Ejemplo:
    
    ```sql
    CREATE INDEX nombre_indice ON tabla (columna1, columna2, ...);
    ```
    
- **CREATE VIEW**  
    _Explicación:_ Crea una vista, que es una consulta almacenada que se comporta como una tabla virtual, facilitando consultas complejas y mejorando la seguridad.  
    Ejemplo:
    
    ```sql
    CREATE VIEW nombre_de_la_vista AS
    SELECT columnas
    FROM tabla_procedencia
    WHERE condición;
    ```
    

---

## 14. USO DEL CASE

- **CASE (SIMPLE)**  
    _Explicación:_ Evalúa un valor comparándolo con distintos casos y retorna un resultado según la coincidencia encontrada.  
    Ejemplo:
    
    ```sql
    CASE valor_a_comparar
      WHEN valor1 THEN resultado1
      WHEN valor2 THEN resultado2
      [ELSE resultado_default]
    END;
    ```
    
- **CASE (SEARCHED)**  
    _Explicación:_ Evalúa múltiples condiciones independientes y retorna el resultado correspondiente a la primera condición verdadera.  
    Ejemplo:
    
    ```sql
    CASE
      WHEN condición1 THEN resultado1
      WHEN condición2 THEN resultado2
      ...
      ELSE resultado_default
    END;
    ```
    
- **USO EN DIVERSAS CLÁUSULAS (SELECT, WHERE, ORDER BY, HAVING, UPDATE, INSERT)**  
    _Explicación:_ Permite incorporar lógica condicional en consultas para retornar o modificar valores basados en condiciones específicas, similar a una estructura if-else en otros lenguajes.  
    Ejemplos:
    
    - En SELECT:
        
        ```sql
        SELECT CASE WHEN condición THEN valor1 ELSE valor2 END AS columna_resultado
        FROM tabla;
        ```
        
        _Ejemplo práctico:_
        
        ```sql
        SELECT BusinessEntityID,
               SalariedFlag,
               CASE WHEN SalariedFlag = 1 THEN Salary ELSE 0 END AS AdjustedSalary
        FROM HumanResources.Employee;
        ```
        
    - En WHERE:
        
        ```sql
        WHERE CASE WHEN Department = 'Sales' THEN Revenue ELSE Expenses END > 1000;
        ```
        
    - En ORDER BY:
        
        ```sql
        ORDER BY CASE WHEN SalariedFlag = 1 THEN BusinessEntityID ELSE NULL END DESC,
                 BusinessEntityID ASC;
        ```
        
    - En HAVING:
        
        ```sql
        HAVING AVG(CASE WHEN SalariedFlag = 1 THEN Salary ELSE 0 END) > 50000;
        ```
        
    - En UPDATE:
        
        ```sql
        UPDATE HumanResources.Employee
        SET Salary = CASE WHEN SalariedFlag = 1 THEN Salary * 1.1 ELSE Salary END;
        ```
        
    - En INSERT:
        
        ```sql
        INSERT INTO SalaryReport (EmployeeID, ReportedSalary)
        SELECT BusinessEntityID,
               CASE WHEN SalariedFlag = 1 THEN Salary ELSE 0 END
        FROM HumanResources.Employee;
        ```
        

---

