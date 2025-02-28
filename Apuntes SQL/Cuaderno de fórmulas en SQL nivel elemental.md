
## ESTRUCTURA DE CONSULTAS EN SQL

#### SELECT
```sql
SELECT 
	columna
```
Seleccionamos una columna en específico.

#### FROM
```sql
SELECT 
	columna 
FROM  
	tabla
```
Seleccionamos una columna de una tabla especifica.

#### WHERE
```sql
SELECT 
	columna 
FROM 
	tabla 
WHERE 
	condición
```
Seleccionamos una condición especifica de una determina columna de una tabla en particular.

#### GROUP BY
```sql
SELECT 
	columna 
FROM 
	tabla 
WHERE 
	condición 
GROUP BY 
	condición para agrupar por un determinado atributo
```
Se utiliza para agrupar filas que comparten los mismos valores en las columnas especificadas.

#### HAVING
```sql
SELECT 
	columna 
FROM 
	tabla 
WHERE 
	condición 
GROUP BY 
	condición para agrupar por un determinado atributo 
HAVING
	filtrado de agrupamiento
```
Se utiliza junto con `GROUP BY` para filtrar los grupos resultantes aplicando una condición a los grupos.
Solo se ocupa con el `GROP BY`.

#### ORDER BY
```sql
SELECT 
	columna 
FROM 
	tabla 
WHERE 
	condición 
GROUP BY 
	condición para agrupar por un determinado atributo 
HAVING
	filtrado de agrupamiento
ORDER BY
	Ordenamiento de los datos ASC o DESC
``` 
Ordena los resultados ascendente o descendentemente según una o más columnas especificadas.

#### LIMIT
```sql
# Consulta standard
SELECT
	columna
FROM
	tabla
WHERE
	condición
ORDER BY
	Ordenamiento de los datos ASC o DESC
LIMIT
	Cantidad de registros, según lo seleccionado

# SQL SERVER
SELECT
	top
FROM 
	tabla
WHERE
	condición
ORDER BY
	Ordenamiento de los datos ASC o DESC
```

#### EJEMPLO DE UNA CONSULTA BÁSICA SQL CON PRINCIPALES CLÁUSULAS
```sql
SELECT columnas
FROM tabla
WHERE condición
GROUP BY columnas_agrupamiento
HAVING condición_agrupamiento
ORDER BY columnas_orden;
```

```sql
SELECT columna1, columna2, COUNT(*) AS conteo
FROM tabla
WHERE condicion  -- Filtra filas individuales
GROUP BY columna1, columna2
HAVING COUNT(*) > 5  -- Filtra grupos donde el conteo es mayor a 5
ORDER BY conteo DESC;
```

## FORMULAS DE MODIFICACIÓN DE ESTRUCTURAS DE TABLAS (ALTER TABLE)

#### FORMULA PARA CAMBIAR EL NOMBRE A UNA TABLA
```sql
# STANDARD

ALTER TABLE nombre_tabla RENAME nuevo_nombre

# En POSTGREESQL

ALTER TABLE nombre_tabla RENAME TO nuevo_nombre
```

#### FORMULA CAMBIAR EL TIPO DE DATOS
```sql
ALTER TABLE tabla MODIFY columna atributos
```

#### FORMULA CAMBIAR NOMBRE A COLUMNA
```sql
# En MYSQL:

ALTER TABLE tabla CHANGE columna nueva_columna atributos;

# En POSTGREE SQL - PGADMIN:

ALTER TABLE tabla RENAME COLUMN columna TO nueva_columna;
```

#### FORMULA AGREGAR NUEVA COLUMNA
```sql
ALTER TABLE tabla ADD COLUMN nueva_columna atributo AFTER columna que va antes;
```

#### FORMULA ELIMINAR UNA COLUMNA
```sql
ALTER TABLE tabla DROP COLUMN columna;
```

#### FORMULA ELIMINAR UNA TABLA
```sql
DROP TABLE tabla;
```

#### FORMULA CONVERSIÓN TIPO DE DATO
```sql
CAST(TIPO DE DATO, CONVERSIÓN)
```

#### FORMULA NO NULO
```sql
COALESCE(ARGUMENTO, 0)
```
Esta formula transforma los valores nulos a la cifra que ponemos (en este caso 0)
Esto evita que se listen valores nulos y facilita realizar cálculos posteriores.
También funciona con cadena de textos.

#### FORMULA ISNULL (SQL SERVER)
```sql
ISNULL(ARGUMENTO, valor_sustitución)
```
Funciona como `COALESCE`, pero es propia de SQL SERVER  y se diferencia de la anterior ya que
`ISNULL` solo puede tomar dos argumentos, mientras que la otra puede soporta mas.

## FUNCIONES DE TIEMPO

RECORDAR  que las funciones tiempo SOLO funcionan si el tipo de dato es `DATE` o `DATETIME`

#### FORMULA PARA SABER EL AÑO
```sql
SELECT YEAR(fecha) as 'Año' FROM facturas;
```

#### FORMULA PARA SABER EL MES
```sql
SELECT MONTH(fecha) as 'Mes' FROM facturas;
```

#### FORMULA PARA SABER EL DÍA
```sql
SELECT DAY(fecha) as 'DIA' FROM facturas;
```

#### FORMULA PARA SABER LA HORA
```sql
SELECT HOUR(fecha) as 'HORA' FROM facturas;
```
El tipo de dato debe ser `DATETIME`

#### FORMULA PARA FORMATEAR TIEMPO
```sql
DATE_FORMAT(FECHA,FORMATO)
```

#### FORMULA FECHA ACTUAL
```sql
# EN MYSQL: 

# Esta función devuelve solo la fecha actual, sin incluir la hora. El formato de retorno es 'YYYY-MM-DD'.
SELECT CURDATE() as 'FECHA ACTUAL';

# Esta función devuelve la fecha y hora actuales, similar a GETDATE() en SQL Server. El formato de retorno es 'YYYY-MM-DD HH:MM:SS'
SELECT NOW() as 'FECHA ACTUAL'

# EN SQL SERVER:

# Esta función devuelve la fecha y hora actuales del servidor de base de datos.
SELECT GETDATE() AS FechaHoraActual;
```

#### FORMULA PARA CALCULAR TRANSCURSO DE MESES O AÑOS
```sql
SELECT TIMESTAMPDIFF(MONTH, '2020-01-01', '2020-06-30') as 'MESES TRANSCURRIDOS';
```

```sql
SELECT TIMESTAMPDIFF(YEAR, fecha_emision, CURDATE()) as 'AÑOS TRANSCURRIDOS' FROM facturas;
```

#### FUNCIÓN PARA EL NOMBRE DEL DÍA
```sql
SELECT DAYNAME(CURDATE()) as 'Nombre del día';
```

#### FUNCION PARA EL NOMBRE DEL MES
```sql
SELECT MONTHNAME(CURDATE()) as 'Nombre del mes';
```

#### FUNCION PARA UN DETERMINADO DÍA EN LA SEMANA
```sql
SELECT DAYOFWEEK(CURDATE()) as 'Número del día de la semana';
``` 

#### FUNCION PARA UN DETERMINADO DIA EN EL AÑO
```sql
SELECT DAYOFYEAR(CURDATE()) as 'Día del año';
```

#### FUNCION PARA INTERVALOS DETERMINADOS DE FECHAS
```sql
ADDDATE(CURDATE(), INTERVAL 2 MONTH) AS 'Vencimiento a 2 meses'
```
Se antepone un `SELECT`
La función utilizada es siempre la misma (`ADDDATE`); lo que varía es el argumento `INTERVAL`.

## FUNCIONES DE CADENA

**FORMULA PARA CONCATENAR:**
```sql
# concat
SELECT CONCAT('Sr./a. ', NOMBRE, ' ', APELLIDO) as 'Nombre completo' FROM clientes;

#concat_ws
SELECT CONCAT_WS(',', nombre, apellido, cuit, direccion) as 'Datos Completos' FROM clientes;
```

**FORMULA PARA MAYÚSCULA:**
```sql
SELECT UPPER(nombre) Nombres FROM clientes;
```

**FORMULA PARA MINÚSUCLA:**
```sql
SELECT LOWER(apellido) FROM clientes;
```

**FORMULA PARA EXTRAER DESDE LA IZQUIERDA:**
```sql
SELECT CONCAT(LEFT(nombre, 1), '.') As Inicial_nombre FROM clientes;
```
Esta función permite obtener los primeros caracteres de una cadena

**FORMULA PARA EXTRAER DESDE LA DERECHA:**
```sql
SELECT RIGHT(cuit, 1) as 'Dígito verificador' FROM clientes;
```
Esta función permite extraer los últimos caracteres de una cadena.

**FORMULA PARA REEMPLAZAR CARACTERES:**
```sql
SELECT REPLACE(COLUMNA,' ', '-') FROM TABLA;
```

**FORMULA PARA EXTRAER CARACTERES:**
```sql				  
SELECT SUBSTRING(COLUMNA,POSICION DE DONDE EMPEZAR, CANTIDAD QUE QUIERO EXTRAER) FROM TABLA;
```
Esta función permite extraer, a partir de una determinada 
posición, una determinada cantidad de caracteres.

**FORMULA PARA DIVIDIR CADENAS POR DELIMITADOR (PROPIA DE POSTGREE):
```SQL
split_part(string text, delimiter text, field int)
```
No confundir con la función `SUBSTRING` ya que esta extrae por delimitador mientras que la otra por posición

**SUBSTRING VS SPLIT_PART:**
```SQL
-- Usando split_part
SELECT split_part('hola,mundo,postgresql', ',', 2);
-- Resultado: 'mundo'

-- Usando substring
SELECT substring('hola,mundo,postgresql' from 6 for 5);
-- Resultado: 'mundo'
```

**FORMULA PARA CONTABILIZAR CARACTERES:**
```sql
SELECT direccion, CHAR_LENGTH(direccion) as ‘Cantidad de caracteres’ FROM clientes;
```
Esta función permite contabilizar la cantidad de 
caracteres que contiene una cadena, e incluye los 
espacios en blanco.

**FORMULA DE LOCALIZACION:**
```sql
SELECT direccion, LOCATE('ara',direccion) 'Posición' FROM clientes;
```
Esta función devuelve la primera posición en la que 
aparece una cadena

**FORMULA PARA RECORTAR:**
```sql
SELECT TRIM(direccion) Direccion_Correcta FROM clientes;
```
Esta función permite quitar los espacios en blanco, tanto 
iniciales como finales, de una cadena

**FORMULA PARA RECORTAR DESDE LA IZQUIERDA:**
```sql
SELECT LTRIM(direccion) Direccion_Correcta FROM clientes;
```
Esta función permite quitar los espacios en blanco 
iniciales de una cadena

**FORMULA PARA RECORTAR DESDE LA DERECHA:**
```sql
SELECT RTRIM(direccion) Direccion_Correcta FROM clientes;
```
Esta función permite quitar los espacios en blanco finales 
de una cadena.

**FORMULA PARA LA GENERACION DE CONTRASEÑAS ALEATORIAS (MYSQL):**
```sql
SELECT 
  UPPER(CONCAT(
    SUBSTRING(MD5(RAND()) FROM 1 FOR 4),
    SUBSTRING(MD5(RAND()) FROM 1 FOR 4)
  )) AS contrasena
FROM usuarios;
```
`RAND()` genera un número aleatorio
`MD5()` calcula el hash MD5 de ese número, dando una cadena aleatoria
`SUBSTRING()` obtiene los primeros 4 caracteres del hash
`CONCAT()` une dos subcadenas de 4 caracteres
`UPPER()` convierte a mayúsculas

### USO DEL COMODÍN `%`:

El comodín `%` en SQL es una herramienta muy útil y versátil, principalmente utilizada en operaciones de búsqueda de patrones con la cláusula `LIKE`. 

1. Función principal:
   El % representa cualquier secuencia de cero o más caracteres.

2. Uso común:
   Se utiliza principalmente con el operador LIKE en cláusulas WHERE para realizar búsquedas de patrones.

3. Ejemplos de uso:

   a) Buscar palabras que empiezan con una letra:
      ```sql
      SELECT * FROM tabla WHERE columna LIKE 'A%';
      ```
      Esto encontrará todas las entradas que comienzan con 'A'.

   b) Buscar palabras que terminan con una secuencia:
      ```sql
      SELECT * FROM tabla WHERE columna LIKE '%ción';
      ```
      Esto encontrará palabras como "acción", "producción", etc.

   c) Buscar palabras que contienen una secuencia:
      ```sql
      SELECT * FROM tabla WHERE columna LIKE '%or%';
      ```
      Esto encontrará palabras como "amor", "color", "ornamento", etc.

4. Combinación con otros caracteres:
   Puedes combinar % con caracteres específicos o con el comodín _ (que representa un solo carácter).

5. Sensibilidad a mayúsculas y minúsculas:
   Dependiendo de la configuración de la base de datos, LIKE puede ser o no sensible a mayúsculas y minúsculas.

6. Uso en diferentes SGBD:
   El comodín % es estándar y funciona de manera similar en la mayoría de los sistemas de gestión de bases de datos SQL.

7. Rendimiento:
   Las búsquedas con comodines, especialmente al inicio de la cadena (como '%texto'), pueden ser menos eficientes en términos de rendimiento, especialmente en grandes conjuntos de datos.

## FUNCIONES MATEMATICAS INTEGRADAS

**FORMULA DE REDONDEO:**
```sql
SELECT ROUND(columna o valor, cantidad de decimales) FROM tabla;
```

**FORMULA REDONDEAR HACIA ARRIBA:**
```sql
SELECT CEIL(columna o valor) FROM tabla;
```

**FORMULA REDONDEAR HACIA ABAJO:**
```sql
SELECT FLOOR(columna o valor) FROM tabla; 
```

**FORMULA RESTO DE DIVISIÓN:**
```sql
SELECT MOD(divisor,dividendo)
```

**FORMULA POTENCIA:**
```sql
SELECT POW(multiplicador, multiplicando)
```

## FUNCIONES MATEMATICAS Y AGRUPAMIENTO

**FORMULA DE CONTEO:**
```sql
SELECT COUNT(*) FROM tabla

# Util para agrupamiento  

SELECT COUNT(*) FROM tabla GROUP BY condición
```

**FOMULA DE SUMA:**
```sql
SELECT SUM(*) FROM tabla

# Util para agrupamiento  

SELECT SUM(*) FROM tabla GROUP BY condición
```

**FORMULA DE MÍNIMO:**
```sql
SELECT MIN(*) FROM tabla

# Util para agrupamiento  

SELECT MIN(*) FROM tabla GROUP BY condición
```

**FORMULA DE MÁXIMO:**
```sql
SELECT MAX(*) FROM tabla

# Util para agrupamiento  

SELECT MAX(*) FROM tabla GROUP BY condición
```

**FORMULA DE PROMEDIO:**
```sql
SELECT AVG(*) FROM tabla

# Util para agrupamiento  

SELECT AVG(*) FROM tabla GROUP BY condición
```

**FORMULA DE GENERACIÓN DE SUPER AGREGADOS (ROLLUP):**
```SQL
# Sintaxis para una columna

SELECT columna1, columna2, función_agregación(columna)
FROM tabla
GROUP BY ROLLUP(columna1, columna2)

# Sintaxis para una columna (SQL SERVER)

SELECT columna, función_agregación(columna)
FROM tabla
GROUP BY columna WITH ROLLUP

# Ejemplo

SELECT COALESCE(Departamento, 'Total') AS Departamento, 
       SUM(Ventas) AS Total_Ventas
FROM Ventas
GROUP BY Departamento WITH ROLLUP

#Sintaxis para más de una columna

SELECT columna1, columna2, ..., función_agregación(columna)
FROM tabla
GROUP BY ROLLUP (columna1, columna2, ...)

#Ejemplo

SELECT COALESCE(Año, 'Total') AS Año,
       COALESCE(Mes, 'Total') AS Mes,
       SUM(Ventas) AS Total_Ventas
FROM Ventas
GROUP BY ROLLUP (Año, Mes)
```

`ROLLUP`  es una extensión de `GROUP BY` que genera automáticamente múltiples niveles de subtotales y un total general (super agregado) en una sola consulta.

Crea una jerarquía de agrupación de izquierda a derecha
Genera N+1 niveles de agregación, donde N es el número de columnas en `ROLLUP`
Produce filas de subtotales con `NULL` en las columnas agregadas.
El último nivel es el super agregado (total general).

### SENSIBILIDAD CON `GROUP_BY`

1. Sensibilidad al GROUP BY: Efectivamente, las funciones de agregación son "sensibles" al GROUP BY. Esto significa que ajustan su comportamiento según cómo se agrupen los datos.

2. Cálculo según criterios de agrupamiento: Exactamente. Cuando usas GROUP BY, las funciones de agregación realizan sus cálculos dentro de cada grupo definido, en lugar de hacerlo sobre toda la tabla.

3. Columnas calculables: Las funciones de agregación operan sobre columnas que contienen valores numéricos (para SUM, AVG, etc.) o cualquier tipo de dato (para COUNT).

4. Flexibilidad: Sin GROUP BY, una función de agregación trata toda la tabla como un solo grupo grande.

5. Combinación con columnas no agregadas: Cuando combinas funciones de agregación con columnas no agregadas en un SELECT, generalmente necesitas incluir esas columnas no agregadas en el GROUP BY.

6. Subconsultas: Las subconsultas pueden ser una forma de usar funciones de agregación sin GROUP BY en la consulta principal.

## FUNCIONES DE RELACION DE CONJUNTOS

### FORMULAS DE EXCPECIONES/UNION

**FORMULA DE EXCEPCION:**
```sql 
SELECT cliente FROM tabla1
EXCEPT
SELECT cliente FROM tabla2
```
Sirve para devolver la diferencia o registros no coincidentes entre dos consultas o sets de resultados.

**FORMULA DE UNION:**
 ```sql
SELECT cliente FROM tabla1
UNION (ALL)
SELECT cliente FROM tabla2
```

`UNION`: Combina los resultados de dos consultas y elimina filas duplicadas (como `DISTINCT`).
`UNION ALL`: Combina todos los resultados, incluso filas duplicadas.
`EXCEPT`: Devuelve filas de la primera consulta que no están en la segunda (diferencia).

Otras diferencias clave:
`UNION/UNION ALL` pueden combinar varias consultas, `EXCEPT` solo compara dos resultados.
El número y tipo de columnas debe coincidir con `UNION`, con `EXCEPT` solo importa que sean compatibles.

`UNION` y `EXCEPT` eliminan filas duplicadas, `UNION ALL` conserva todas las filas.
El orden de las consultas importa en `EXCEPT` pero no en `UNION`.

Una pista para usar el `UNION` sería el "que hacer" con el `WHERE`, o sea cuando no sabes especificar con el cual de las debes poner el `WHERE` porque el campo es el mismo.

```sql
#uso incorrecto del JOIN
SELECT * FROM top_spotify tp JOIN ultimos_lanzamientos ul ON tp.ID = ul.ID WHERE [NO SABES A QUE TABLA REMITIR]TITULO LIKE '%break%';

#uso correcto del UNION
SELECT *, 'ANTERIOR' AS ESTADO FROM TOP_SPOTIFY
WHERE TITULO LIKE '%BREAK%'
UNION
SELECT *, 'ULTIMO' AS ESTADO FROM ULTIMOS_LANZAMIENTOS
WHERE TITULO LIKE '%BREAK%'
ORDER BY TITULO;
```

Un "tip" a considerar, con el `UNION ALL` se puede agregar una nueva fila que sirva, por ejemplo, a mostrar el total de un conteo hecho anteriormente con un `GROUP BY`  
### `JOIN` EN SQL

JOIN es una operación que permite combinar filas de dos o más tablas basándose en una condición relacionada entre ellas.

Sintaxis básica:
```sql
SELECT columnas
FROM tabla1
[TIPO DE] JOIN tabla2
ON tabla1.columna = tabla2.columna
```

**INNER JOIN**
Retorna solo las filas que tienen coincidencias en ambas tablas.
```sql
SELECT * FROM clientes
INNER JOIN pedidos ON clientes.id = pedidos.cliente_id
```

**LEFT JOIN**
Retorna todas las filas de la tabla izquierda y las coincidencias de la tabla derecha.
```sql
SELECT * FROM clientes
LEFT JOIN pedidos ON clientes.id = pedidos.cliente_id
```

**RIGHT JOIN**
Retorna todas las filas de la tabla derecha y las coincidencias de la tabla izquierda.
```sql
SELECT * FROM pedidos
RIGHT JOIN clientes ON pedidos.cliente_id = clientes.id
```

**FULL JOIN**
Retorna todas las filas cuando hay una coincidencia en una de las tablas.
```sql
SELECT * FROM clientes
FULL JOIN pedidos ON clientes.id = pedidos.cliente_id
```

Notas adicionales:
- Se pueden unir más de dos tablas en una sola consulta.
- La condición ON puede incluir múltiples condiciones usando AND, OR, etc.
- INNER JOIN puede abreviarse como JOIN en muchos sistemas de bases de datos.

### CONDICIONES EN EL `ON` DE UN `JOIN`

**Poner condiciones en el ON del JOIN**

   - Filtrar datos durante la operación de unión
   - Crear relaciones más complejas entre tablas
   - Mejorar el rendimiento de las consultas
   - Simplificar consultas complejas

**Sintaxis de uso de cláusulas en el ON**
```sql
SELECT *
FROM tabla1 t1
JOIN tabla2 t2 ON t1.columna = t2.columna AND/OR [otras condiciones]
```

**Esas condiciones reemplazan las subconsultas**
   - En muchos casos sí, pueden reemplazar subconsultas, mejorando la eficiencia y legibilidad
   - No siempre, algunas subconsultas siguen siendo necesarias para ciertas operaciones
   - 
**Ejemplos de cada cláusula**

**AND**

```sql
JOIN tabla2 ON tabla1.id = tabla2.id AND tabla2.fecha > '2024-01-01'
```

**OR**

```sql
JOIN departamentos ON empleados.dept_id = departamentos.id OR empleados.secundario_dept_id = departamentos.id
```

**IN**

```sql
JOIN categorias ON productos.categoria_id IN (categorias.id, categorias.parent_id)
   ```

**LIKE**

```sql
JOIN clientes ON pedidos.cliente_id = clientes.id AND clientes.email LIKE '%@empresa.com'
```

**BETWEEN**

```sql
JOIN productos ON ventas.producto_id = productos.id AND ventas.fecha BETWEEN '2024-01-01' AND '2024-12-31'
```

**Comparación**

```sql
JOIN empleados ON proyectos.responsable_id = empleados.id AND empleados.nivel >= 'Senior'
```

**IS NULL**

```sql
JOIN pedidos ON clientes.id = pedidos.cliente_id AND pedidos.fecha_cancelacion IS NULL
```

**Función de base de datos**

```sql
JOIN productos ON ventas.producto_id = productos.id AND YEAR(ventas.fecha) = 2024
```

Estos ejemplos demuestran la versatilidad de las condiciones en el ON del JOIN, permitiéndote crear consultas más eficientes y expresivas.
## FUNCIONES DML

**FORMULA CREACIÓN DE UNA TABLA A PARTIR DE UNA EXISTENTE (MYSQL)**
```sql
CREATE TABLE nueva_tabla
SELECT * FROM tabla_orignal;

#ejemplo
CREATE TABLE ultimos_lanzamientos
SELECT * FROM top_spotify WHERE permanencia <= 3;
```

**FORMULA CREACIÓN DE UNA TABLA A PARTIR DE UNA EXISTENTE (SQL SERVER)**
```sql
SELECT *
INTO NUEVA TABLA
FROM TABLA DE ORIGEN
```

**FORMULA UPDATE (STANDARD)**
```sql
UPDATE TABLA
SET VARIABLE
FROM UTIL PARA MAS DE UNA TABLA
WHERE ALGUNA CONDICIÓN

#ejemplo
UPDATE passengers SET fare = fare * 1.10 WHERE pclass = 1; 
```
El `SET` entenderlo como un WHERE ya sea el básico o de subconsulta

**FORMULA INSERT (STANDARD)**
```sql
INSERT INTO TABLA (COLUMNAS)
VALUES
(NUEVOS REGISTROS)

#ejemplo
INSERT INTO passengers(passengerid,survived,pclass,name,sex,age)
VALUES
(892,true,1,'Brooks,Mr. Teddy Lee','male',21)
```

**FORMULA PARA COPIAR DE UNA TABLA A OTRA**
```sql
INSERT INTO Tabla_Destino (COLUMNAS) 
SELECT (COLUMNAS) FROM Tabla_Origen;
```
Se le puede poner una condición con la cláusula `WHERE`

**FORMULA DELETE (STANDARD)**
```sql
DELETE FROM TABLA WHERE COLUMNA O CONDICION

#ejemplo
DELETE FROM passengers WHERE survived = false;
```

**FORMULA BORRADO DE CONTENIDO**
```sql
TRUNCATE TABLE NOMBRE DE TABLA
```

**FORMUA BORRADO DE TABLA**
```sql
DROP TABLE NOMBRE DE TABLA
```

## SUBCONSULTA 

**LOGICA SUBCONSULTA EN WHERE:**
```sql
SELECT columnas
FROM tabla
WHERE expresion [operador] (
  SELECT columnas
  FROM tabla
  WHERE condicion
);
```
Operadores comúnmente utilizados:

- `IN` / `NOT IN`: Verifica si un valor está o no en el resultado de la subconsulta.
- `EXISTS` / `NOT EXISTS`: Comprueba si la subconsulta devuelve o no resultados.
- Operadores de comparación (`=`, `>`, `<`, etc.): Compara un valor con el resultado de la subconsulta.

**EJEMPLO SUBCONSULTA EN WHERE:**
```sql
# Obtener los nombres de los clientes que han realizado algún pedido en febrero de 2024:

SELECT CONCAT(nombre, ' ', apellido) AS cliente
FROM clientes
WHERE id IN (
  SELECT cliente_id
  FROM pedidos
  WHERE fecha_pedido BETWEEN '2024-02-01' AND '2024-02-28'
);

# Obtener los productos cuyo precio sea mayor al promedio:

SELECT *
FROM productos
WHERE precio > (
  SELECT AVG(precio)
  FROM productos
);

# Verificar si existe algún pedido realizado por el cliente con id 10:

SELECT EXISTS (
  SELECT 1
  FROM pedidos
  WHERE cliente_id = 10
) AS existe_pedido;
```

**SUBCONSULTAS CORRELACIONADAS:**
```sql
SELECT columnas
FROM tabla_principal TP
WHERE expresion (
  SELECT columnas
  FROM tabla_secundaria TS
  WHERE TS.columna = TP.columna
);
```
Son subconsultas que hacen referencia a columnas de la consulta principal. 
Se ejecutan una vez por cada fila de la consulta principal.

**EJEMPLOS SUBCONSULTAS ANIDADAS:**
```sql
# Mostrar los nombres de los empleados contratados después del empleado con id 15:

SELECT nombre, apellido
FROM empleados E1
WHERE fecha_contratacion > (
  SELECT fecha_contratacion
  FROM empleados E2
  WHERE E2.id = 15
);
```

**LÓGICA SUBCONSULTAS EN SELECT :**
```sql
SELECT columna1, columna2, (subconsulta) AS alias_subconsulta
FROM tabla
``` 

- `columna1`, `columna2` son las columnas regulares de la tabla principal.
- `subconsulta` es la consulta SQL anidada que se ejecuta para cada fila de la tabla principal.
- `alias_subconsulta` es un alias obligatorio que se asigna al resultado de la subconsulta.

**EJEMPLO DE SUBCONSULTA EN SELECT:**
```sql
# Subconsultas en SELECT:
SELECT
  (SELECT COUNT(*) FROM pedidos WHERE cliente_id = C.id) AS num_pedidos,
  C.nombre, C.apellido
FROM clientes C;
```

**LÓGICA SUBCONSULTA EN FROM:**
```sql
SELECT columnas_deseadas
FROM (subconsulta) AS alias_subconsulta
```

- `columnas_deseadas` son las columnas que deseas seleccionar de la subconsulta.
- `subconsulta` es la consulta SQL anidada que se ejecuta primero y devuelve un conjunto de resultados.
- `alias_subconsulta` es un alias opcional que se puede asignar al resultado de la subconsulta para poder hacer referencia a él de manera más sencilla.

**EJEMPLO DE SUBCONSULTA EN FROM:**
```sql
# Subconsultas en FROM:

SELECT *
FROM (
  SELECT cliente_id, producto_id, cantidad
  FROM pedidos
) AS pedidos_temp
WHERE cantidad > 2;

# EJEMPLO: Usa una subconsulta en FROM para encontrar el país con la mayor densidad de población (población/superficie).

SELECT 
    Name, 
    Densidad_por_pais  
FROM
(SELECT 
       Name, 
       Population / SurfaceArea AS Densidad_por_pais 
 FROM 
     country 
 WHERE  
      SurfaceArea > 0
) AS Densidad 
ORDER BY 
	Densidad_por_pais DESC
LIMIT 1;

```

Permiten realizar cálculos o transformaciones en los resultados de la consulta principal.
La subconsulta actúa como una tabla temporal dentro de la consulta principal.
Aunque menos comunes, las subconsultas también pueden ser utilizadas en las cláusulas SELECT y FROM.

**TABLA DUAL:**
```sql
SELECT 'Existen pedidos'
FROM DUAL
WHERE EXISTS (
  SELECT 1
  FROM pedidos
  WHERE cliente_id = 10
);
```
La tabla `DUAL` es una tabla especial que contiene una sola fila y una sola columna. 
Se utiliza principalmente cuando se necesita realizar consultas que no requieren acceder a ninguna otra tabla real, como en el caso de evaluar expresiones o utilizar subconsultas con `EXISTS` o `IN`.

**FORMULA BOLEANA**
```sql
SELECT columna FROM tabla WHERE EXISTS (subconsulta comprobadora)
```
Te da un valor positivo o negativo dependiendo de la condición puesta en tu subconsulta
Muy util usarla con la `DUAL`, la cual es una caracteristica de algunos programas SQL y se utiliza principalmente cuando se necesita realizar consultas que no requieren acceder a ninguna otra tabla real

## ÍNDICES Y CREACIÓN DE VISTAS

**FORMULA DE INDICE**
```sql
CREATE INDEX nombre_indice ON tabla (columna1, columna2, ...)
```
Un índice es una estructura de datos auxiliar en las bases de datos que mejora significativamente la velocidad de las operaciones de búsqueda y recuperación de datos.
Se crea sobre una o más columnas de una tabla.
Cuando se ejecuta una consulta que involucra columnas indexadas, la base de datos utiliza el índice en lugar de escanear toda la tabla, acelerando la consulta.

**FORMULA DE VISTA**
```SQL
CREATE VIEW nombre_de_la_vista AS
SELECT columnas
FROM tabla_procedencia
WHERE condición;
```
Las vistas se pueden utilizar para simplificar consultas complejas, mejorar la seguridad al restringir el acceso directo a las tablas y proporcionar una capa de abstracción sobre los datos.
## USO DEL `CASE`:

**LÓGICA DE CASE:**
```SQL
# CASE simple:
CASE valor_a_comparar
    WHEN valor1 THEN resultado1
    WHEN valor2 THEN resultado2
    ...
    [ELSE resultado_default]
END

# Searched CASE:
CASE 
	WHEN condición1 THEN resultado1
	WHEN condición2 THEN resultado2
	...
	ELSE [resultado_default]
END
```
La sintaxis del CASE es generalmente la misma, independientemente de dónde se use en la consulta. Puede ser utilizada en SELECT, WHERE, ORDER BY, y otras cláusulas.

Se puede usar CASE en varias cláusulas, incluyendo:

- SELECT: Para calcular valores condicionales.
- WHERE: Para filtrar filas basadas en condiciones complejas.
- ORDER BY: Para ordenar resultados de manera condicional, como en tu ejemplo.
- HAVING: Para filtrar grupos basados en condiciones.

**FORMA "CONDENSADA" DEL CASE:**
```sql
CASE WHEN condición THEN valor_si_verdadero ELSE valor_si_falso END
```

Esta es esencialmente una versión abreviada del CASE buscado que se usa comúnmente para expresar una lógica `if-else` simple. Es similar a un operador ternario en otros lenguajes de programación.

Algunos ejemplos de uso:
1. En SELECT:
```sql
SELECT CASE WHEN condición THEN valor1 ELSE valor2 END AS columna_resultado

SELECT 
    BusinessEntityID,
    SalariedFlag,
    CASE WHEN SalariedFlag = 1 THEN Salary ELSE 0 END AS AdjustedSalary
FROM HumanResources.Employee;
```

2. En WHERE:
```sql
WHERE CASE WHEN condición THEN valor1 ELSE valor2 END = algún_valor

WHERE 
    CASE WHEN Department = 'Sales' THEN Revenue ELSE Expenses END > 1000
```

3. En ORDER BY:
```sql
ORDER BY CASE WHEN condición THEN valor1 ELSE valor2 END [ASC|DESC]

ORDER BY
    CASE WHEN SalariedFlag = 1 THEN BusinessEntityID ELSE NULL END DESC,
    BusinessEntityID ASC;
```

4. En otras clausulas:
```sql
#HAVING
HAVING 
    AVG(CASE WHEN SalariedFlag = 1 THEN Salary ELSE 0 END) > 50000

#UPDATE
UPDATE HumanResources.Employee
SET Salary = CASE WHEN SalariedFlag = 1 THEN Salary * 1.1 ELSE Salary END

#INSERT
INSERT INTO SalaryReport (EmployeeID, ReportedSalary)
SELECT 
    BusinessEntityID,
    CASE WHEN SalariedFlag = 1 THEN Salary ELSE 0 END
FROM HumanResources.Employee;
```

Esta forma condensada es especialmente útil cuando solo tienes dos posibles resultados basados en una condición simple. Es concisa y fácil de leer, lo que la hace popular en muchas situaciones.

