## FUNCIONES DE "SETEO" (setting) EN CONSOLA E IDE

Muchas de estas funciones se remiten al `sys.column` o `information_schema`, sin embargo la lógica es la misma,
se configura como si fuese una consulta, las variaciones remiten tanto al programa en uso como a lo que se desea buscar.
 
#### FORMULA PARA ENCONTRAR UNA TABLA A TRAVÉS DE UNA COLUMNA CONOCIDA:
```sql
# En SQL SERVER:

SELECT OBJECT_NAME(object_id) 
FROM sys.columns
WHERE name = 'NOMBRE_COLUMNA'

# En MYSQL:

SELECT * 
FROM information_schema.columns
WHERE column_name = 'NOMBRE_COLUMNA';
```
#### FORMULA PARA SABER LA INFORMACIÓN DE UNA TABLA (POSTGREE SQL - PGADMIN):
```sql
SELECT column_name, data_type
FROM information_schema.columns
WHERE table_name = 'nombre_tabla';
```
Postgree no tiene una función `DESC` para las tablas, esta formula cumple ese rol.

#### FORMULA SETEAR LLAVES FORANEAS
```sql
SET FOREIGN_KEY_CHECKS = 0;
SET FOREIGN_KEY_CHECKS = 1;
```
Con 0 se deshabilita temporalmente las comprobaciones de las llaves foráneas, con 1 
se vuelven a habilitar.

#### FORMULA SETEAR ACTUALIZACIONES
```sql
SQL_SAFE_UPDATES = 0;
SQL_SAFE_UPDATES = 1;
```
Con 0 se deshabilita temporalmente las comprobaciones de actualizaciones en tablas, con 1 
se vuelven a habilitar.

#### FORMULA DE REPARACION DE COLUMNAS
```sql
REPAIR TABLE mysql.proc;
```

#### FORMULA PARA VISUALIZAR LAS BASES DE DATOS
```sql
SHOW DATABASES;
```

#### FORMULA PARA VISUALIZAR TABLAS DE UN BASE DE DATOS
```sql
SHOW TABLES IN base_de_datos;
```

#### FORMULA PARA REINICIO DE SECUENCIAS (COMPLEMENTO A ALTER TABLE Y ERORRES DE INSERCIÓN)

**FORMULA DE NOMENCLATURA:**
```SQL
# Nomenclatura de secuencias en PostgreSQL:
[nombre_tabla]_[nombre_columna]_seq

# Para verificar el nombre de una secuencia:
SELECT pg_get_serial_sequence('[nombre_tabla]', '[nombre_columna]');
```

**FORMULA  DE DIAGNOSTICO Y REINICIO DE SECUENCIA (PostgreSQL):**
```SQL
# Diagnóstico de secuencia:
SELECT last_value FROM [nombre_secuencia];

# Reinicio de secuencia:
SELECT setval('[nombre_secuencia]', (SELECT MAX([columna_id]) FROM [nombre_tabla]));
```

Usar el diagnóstico para verificar el estado actual de la secuencia. 
Si es necesario corregir, usar el reinicio.

**FORMULA GENERAL:**
```SQL
SELECT setval(pg_get_serial_sequence('nombre_de_la_tabla', 'columna_id'), 
              (SELECT MAX(columna_id) FROM nombre_de_la_tabla));
```

**EJEMPLO DE USO:**
```SQL
SELECT last_value FROM passengers_passengerid_seq;
SELECT setval('passengers_passengerid_seq', (SELECT MAX(passengerid) FROM passengers));
```
En este caso, debido al mal procedimiento de insertar un registro, sucedió que el programa no reconocía las columnas, el reinicio ayudó a ordenar el el ingreso del nuevo registro.

**FORMULA  DE DIAGNOSTICO Y REINICIO DE SECUENCIA (MYSQL):**
```SQL
# Verificar el ultimo valor
SELECT AUTO_INCREMENT
FROM information_schema.tables
WHERE table_name = 'nombre_tabla' AND table_schema = 'nombre_base_de_datos';

# Reiniciar AUTO_INCREMENT
ALTER TABLE nombre_tabla AUTO_INCREMENT = nuevo_valor;
```

MySQL no usa secuencias de la misma manera que PostgreSQL. En su lugar, utiliza `AUTO_INCREMENT` para columnas de incremento automático

**EJEMPLO DE USO:**
```SQL
# Verificamos el valor actual del AUTO_INCREMENT

SELECT AUTO_INCREMENT
FROM information_schema.tables
WHERE table_name = 'passengers' AND table_schema = 'nombre_de_tu_base_de_datos';

# Reiniciar AUTO_INCREMENT al máximo valor actual en la tabla

ALTER TABLE passengers AUTO_INCREMENT = 1; -- Primero lo reiniciamos a 1
SET @max_id = (SELECT MAX(passengerid) FROM passengers);
SET @sql = CONCAT('ALTER TABLE passengers AUTO_INCREMENT = ', @max_id + 1);
PREPARE stmt FROM @sql;
EXECUTE stmt;
DEALLOCATE PREPARE stmt;

# Insertar el nuevo pasajero

INSERT INTO passengers(survived, pclass, name, sex, age, sibsp)
VALUES (1, 1, 'Mr. Teddy Brooks', 'male', 42, 1);
```

## TABLAS TEMPORALES

### USOS COMUNES DE UNA TABLA TEMPORAL

Las tablas temporales en SQL Server tienen varios usos prácticos:

1. Almacenamiento de resultados intermedios:
   - En procesos complejos o procedimientos almacenados largos, puedes usar tablas temporales para guardar resultados intermedios.

2. Mejora del rendimiento:
   - Al trabajar con grandes conjuntos de datos, a veces es más eficiente insertar los resultados en una tabla temporal y luego realizar operaciones sobre ella.

3. Operaciones de ETL (Extract, Transform, Load):
   - Para almacenar datos temporalmente durante procesos de extracción, transformación y carga.

4. Eliminación de duplicados:
   - Puedes usar una tabla temporal para almacenar datos únicos extraídos de una tabla más grande.

5. Manipulación de datos antes de la inserción final:
   - Cuando necesitas realizar varias operaciones en los datos antes de insertarlos en una tabla permanente.

6. Debugging y pruebas:
   - Para verificar resultados intermedios en consultas o procedimientos complejos.

7. Manejo de datos de sesión:
   - Almacenar información específica de la sesión del usuario en aplicaciones web.

8. Operaciones de unión (JOIN) más eficientes:
   - A veces, unir una tabla temporal pequeña con una tabla grande es más rápido que unir dos tablas grandes.

9. Cálculos complejos:
   - Para almacenar resultados de cálculos que se utilizarán múltiples veces en una consulta.

10. Particionamiento lógico de datos:
    - Dividir grandes conjuntos de datos en partes más manejables para su procesamiento.
    
### TABLA TEMPORAL LOCAL (solo visible en la sesión actual):

```sql
CREATE TABLE #NombreTabla (
    Columna1 TipoDato,
    Columna2 TipoDato,
    ...
);
```

**EJEMPLO DE USO**

```SQL
CREATE TABLE #VentasTemporales (
    ID INT IDENTITY(1,1),
    Fecha DATE,
    Producto VARCHAR(50),
    Cantidad INT,
    Monto DECIMAL(10,2)
);

INSERT INTO #VentasTemporales (Fecha, Producto, Cantidad, Monto)
VALUES 
    ('2024-07-22', 'Laptop', 5, 3000.00),
    ('2024-07-22', 'Mouse', 10, 200.00);

SELECT * FROM #VentasTemporales;
```
### VARIABLE ALTERNATIVA

```SQL
DECLARE @NombreTabla TABLE (
    Columna1 TipoDato,
    Columna2 TipoDato,
    ...
);
```

**EJEMPLO DE USO**

```SQL
DECLARE @ProductosTop TABLE (
    ProductID INT,
    Nombre VARCHAR(50),
    TotalVentas DECIMAL(10,2)
);

INSERT INTO @ProductosTop (ProductID, Nombre, TotalVentas)
SELECT TOP 5 
    ProductID, 
    ProductName, 
    SUM(Quantity * UnitPrice) as TotalVentas
FROM Orders O
JOIN [Order Details] OD ON O.OrderID = OD.OrderID
JOIN Products P ON OD.ProductID = P.ProductID
GROUP BY ProductID, ProductName
ORDER BY TotalVentas DESC;

SELECT * FROM @ProductosTop;
```
### TABLA TEMPORAL GLOBAL (visible para todas las sesiones):

```sql
CREATE TABLE ##NombreTabla (
    Columna1 TipoDato,
    Columna2 TipoDato,
    ...
);
```

**EJEMPLO DE USO**

```SQL
CREATE TABLE ##UsuariosActivos (
    UserID INT,
    Nombre VARCHAR(50),
    UltimoAcceso DATETIME
);

INSERT INTO ##UsuariosActivos (UserID, Nombre, UltimoAcceso)
VALUES 
    (1, 'Juan Pérez', GETDATE()),
    (2, 'María García', GETDATE());

SELECT * FROM ##UsuariosActivos;
```


### METODO `SELECT`- `INTO`

El método SELECT INTO puede funcionar tanto con tablas locales como con tablas globales. 

**TABLAS TEMPORALES LOCALES**

   ```sql
   SELECT columnas
   INTO #TablaTempLocal
   FROM TablaOrigen;
   ```
   
   - Usa un solo '#' antes del nombre de la tabla.
   - Solo visible en la sesión actual.

**TABLAS TEMPORALES GLOBALES**

   ```sql
   SELECT columnas
   INTO ##TablaTempGlobal
   FROM TablaOrigen;
   ```
   
   - Usa '##' antes del nombre de la tabla.
   - Visible para todas las sesiones.

**TABLAS PERMANENTES**

   ```sql
   SELECT columnas
   INTO TablaPermanente
   FROM TablaOrigen;
   ```
   
   - Sin '#', crea una tabla permanente en la base de datos actual.

**PUNTOS IMPORTANTES**

- Si no especificas `#` o `##`, por defecto se crea una tabla permanente.
- Las tablas temporales se eliminan automáticamente al cerrar la sesión (locales) o cuando la última sesión que las usa se cierra (globales).
- Puedes usar esta sintaxis para crear cualquier tipo de tabla, incluyendo permanentes en otras bases de datos si especificas el nombre completo.

**EJEMPLO DE USO**

```SQL
SELECT 
    C.CustomerID,
    C.CompanyName,
    COUNT(O.OrderID) as TotalPedidos,
    SUM(OD.Quantity * OD.UnitPrice) as MontoTotal
INTO #ClientesVIP
FROM Customers C
JOIN Orders O ON C.CustomerID = O.CustomerID
JOIN [Order Details] OD ON O.OrderID = OD.OrderID
GROUP BY C.CustomerID, C.CompanyName
HAVING SUM(OD.Quantity * OD.UnitPrice) > 10000;

SELECT * FROM #ClientesVIP;
```
El método `SELECT INTO` es flexible y su uso depende de tus necesidades específicas y el alcance que quieras dar a los datos.

### TABLAS `CTE`(Common Table Expressions )

Las CTE (Common Table Expressions) son similares a las tablas temporales en algunos aspectos, pero tienen algunas diferencias importantes

   ```sql
   WITH NombreCTE AS (
       SELECT ...
       FROM ...
       WHERE ...
   )
   SELECT * FROM NombreCTE;
   ```

   - Son temporales, pero de una manera diferente a las tablas temporales.
   - Existen solo dentro del ámbito de una única instrucción SELECT, INSERT, UPDATE, DELETE o MERGE.
   - No se almacenan físicamente como las tablas temporales.
   - Se pueden considerar como vistas temporales definidas solo para una consulta.
   - Solo duran durante la ejecución de la consulta en la que están definidas.

 **USO**
   - Útiles para simplificar consultas complejas.
   - Permiten consultas recursivas.
   - Mejoran la legibilidad del código.
   - Muy útiles para TRASPASAR la información entre tablas. 

**DIFERENCIAS CON LAS TABLAS TEMPORALES:**
   - No requieren creación de estructura física.
   - No persisten después de la consulta.
   - No pueden ser indexadas directamente.

**EJEMPLO DE TABLA CTE**

```sql
WITH VentasPorCliente AS (
    SELECT CustomerID, SUM(TotalAmount) AS TotalVentas
    FROM Orders
    GROUP BY CustomerID
)
SELECT c.CustomerName, v.TotalVentas
FROM Customers c
JOIN VentasPorCliente v ON c.CustomerID = v.CustomerID
WHERE v.TotalVentas > 1000;
```

En este ejemplo, `"VentasPorCliente"` es una CTE que existe solo para esta consulta específica.

Las CTE son "temporales" en el sentido de que son efímeras y existen solo para la duración de la consulta, pero no son tablas temporales en el mismo sentido que `#TempTable` o `@TableVariable`. Son más como definiciones temporales de consultas que se pueden reutilizar dentro de una instrucción SQL más grande.

## CREACIÓN DE VARIABLES 

Las variables en SQL Server son contenedores temporales que almacenan datos durante la ejecución de un lote de instrucciones (batch). Son fundamentales para el manejo dinámico de datos y el control de flujo en consultas y procedimientos.

### 1. Variables Escalares
Son variables que almacenan un único valor de un tipo de dato específico.

#### Sintaxis básica:
```sql
DECLARE @NombreVariable TipoDeDato
```

#### Ejemplo de uso:
```sql
DECLARE @Promedio DECIMAL(10,2)
SELECT @Promedio = AVG(ListPrice)
FROM Production.Product

-- Uso de la variable
SELECT ProductID, ListPrice
FROM Production.Product
WHERE ListPrice < @Promedio
```

### 2. Variables Tipo Tabla
Son variables que pueden almacenar un conjunto de datos estructurados como una tabla temporal.

#### Sintaxis básica:
```sql
DECLARE @NombreTabla TABLE
(
    Columna1 TipoDato1,
    Columna2 TipoDato2,
    ...
)
```

#### Ejemplo de uso:
```sql
DECLARE @CategoriasProductos TABLE
(
    SubCategoria VARCHAR(50),
    Categoria    VARCHAR(50)
)

INSERT INTO @CategoriasProductos
SELECT pp.Name, ps.Name
FROM Production.ProductSubcategory pp
    INNER JOIN Production.ProductCategory ps 
    ON pp.ProductCategoryID = ps.ProductCategoryID

-- Consultar datos de la variable tabla
SELECT * FROM @CategoriasProductos
```

### Estructuras de Control

### IF-ELSE
Permite la ejecución condicional de código basada en una expresión booleana.

#### Sintaxis básica:
```sql
IF condición
    -- código si la condición es verdadera
ELSE
    -- código si la condición es falsa
```

#### Ejemplo de uso:
```sql
DECLARE @PromedioPrecios DECIMAL(10,2)
SELECT @PromedioPrecios = AVG(ListPrice)
FROM Production.Product

IF @PromedioPrecios < 500
    PRINT 'PROMEDIO BAJO'
ELSE 
    PRINT 'PROMEDIO ALTO'
```

### Alcance de Variables (Scope)
- Las variables tienen un alcance limitado al batch donde se declaran
- Para separar batches y reiniciar el alcance de las variables, se utiliza la sentencia GO
- Las variables no persisten entre diferentes batches

### Ejemplo de Scope:
```sql
-- Primer batch
DECLARE @Promedio INT
SELECT @Promedio = AVG(ListPrice)
FROM Production.Product
GO

-- Segundo batch (requiere nueva declaración)
DECLARE @Promedio INT
SELECT @Promedio = AVG(ListPrice)
FROM Production.Product
```

### Buenas Prácticas
1. Usar nombres descriptivos para las variables
2. Inicializar variables cuando sea necesario
3. Utilizar el tipo de dato más apropiado y específico
4. Documentar el propósito de variables complejas
5. Considerar el uso de variables tabla para operaciones complejas con conjuntos de datos
6. Manejar adecuadamente el scope usando GO cuando sea necesario

### Casos de Uso Comunes
1. Almacenar resultados intermedios de cálculos
2. Control de flujo en procedimientos almacenados
3. Almacenamiento temporal de conjuntos de datos para procesamiento
4. Parámetros dinámicos en consultas
5. Validaciones y comparaciones

### Limitaciones
- Las variables no persisten entre sesiones
- El alcance está limitado al batch donde se declaran
- Las variables tipo tabla son temporales y se eliminan al finalizar el batch

## CREACIÓN DE FUNCIONES 

#### SINTAXIS GENERAL

```SQL
CREATE FUNCTION nombre_funcion ([parámetros])
RETURNS tipo_retorno
AS
BEGIN
    -- Lógica de la función
    RETURN valor;
END;
```

- Reutilización de código: Si tienes cálculos o lógica que necesitas aplicar repetidamente en diferentes consultas, una función puede encapsular esa lógica.
- Complejidad: Algunas operaciones son demasiado complejas para una sola consulta SQL. Las funciones permiten dividir esa complejidad en pasos manejables.
- Rendimiento: En algunos casos, las funciones pueden mejorar el rendimiento al pre-calcular resultados comunes.
- Seguridad: Las funciones pueden usarse para controlar el acceso a los datos, permitiendo operaciones específicas sin dar acceso directo a las tablas.
- Abstracción: Puedes cambiar la lógica interna de una función sin afectar las consultas que la utilizan.
- Cálculos específicos del negocio: Por ejemplo, calcular descuentos, intereses, o aplicar reglas de negocio complejas.
- Mantenimiento: Centralizar la lógica en funciones facilita el mantenimiento y las actualizaciones.
- Integridad de datos: Las funciones pueden asegurar que ciertos cálculos o transformaciones se realicen de manera consistente.

#### VARIACIONES EN DIFERENTES PROGRAMAS

```SQL
# POSTGRESQL

CREATE [OR REPLACE] FUNCTION nombre_funcion([parámetros])
RETURNS tipo_retorno AS
$$
BEGIN
    -- Lógica de la función
    RETURN valor;
END;
$$
LANGUAGE plpgsql;

# EJEMPLO

CREATE OR REPLACE FUNCTION calcular_area_triangulo(base NUMERIC, altura NUMERIC)
RETURNS NUMERIC AS
$$
BEGIN
    RETURN (base * altura) / 2;
END;
$$
LANGUAGE plpgsql;

####################################

# SQL SERVER

CREATE FUNCTION dbo.nombre_funcion(@parametro1 tipo, @parametro2 tipo)
RETURNS tipo_retorno
AS
BEGIN
    DECLARE @resultado tipo_retorno;
    -- Lógica de la función
    RETURN @resultado;
END;

# EJEMPLO

CREATE FUNCTION dbo.calcular_impuesto(@salario DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @impuesto DECIMAL(10,2);
    SET @impuesto = CASE
        WHEN @salario <= 5000 THEN @salario * 0.05
        WHEN @salario <= 10000 THEN @salario * 0.1
        ELSE @salario * 0.15
    END;
    RETURN @impuesto;
END;

####################################

# MySQL

DELIMITER //
CREATE FUNCTION nombre_funcion(parametro1 tipo, parametro2 tipo)
RETURNS tipo_retorno
[DETERMINISTIC]
BEGIN
    DECLARE variable tipo;
    -- Lógica de la función
    RETURN valor;
END //
DELIMITER ;

# EJEMPLO

DELIMITER //
CREATE FUNCTION calcular_descuento(precio DECIMAL(10,2), porcentaje INT)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE descuento DECIMAL(10,2);
    SET descuento = precio * (porcentaje / 100);
    RETURN precio - descuento;
END //
DELIMITER ;
```

- PostgreSQL usa `$$` como delimitadores y requiere especificar el lenguaje (generalmente `plpgsql`).
- SQL Server utiliza `dbo.` para especificar el esquema y no requiere cambiar el delimitador.
- MySQL/MariaDB requiere cambiar el delimitador (usualmente a `//`) y volver a cambiarlo al final. También se puede usar `DETERMINISTIC` cuando sea apropiado.
- Todos los sistemas usan `BEGIN` y `END` para encapsular la lógica de la función.
- La forma de declarar variables y asignar valores puede variar ligeramente entre sistemas.
## PROCEDIMIENTOS ALMACENADOS

#### SINTAXIS GENERAL

```SQL
CREATE PROCEDURE nombre_procedimiento ([parámetros])
AS
BEGIN
    -- Lógica del procedimiento
END;
```

- Los procedimientos no retornan un valor directamente (aunque pueden tener parámetros de salida), mientras que las funciones sí.
- Los procedimientos se utilizan principalmente para realizar acciones (como insertar, actualizar o eliminar datos), mientras que las funciones se usan más para cálculos y retornar valores.
- Los procedimientos se llaman con `CALL` o `EXECUTE`, mientras que las funciones se usan en consultas SELECT o como parte de expresiones.

#### ¿Qué es?

Un procedimiento almacenado es un conjunto de instrucciones SQL precompiladas que se guardan en el servidor de base de datos. Es como una "función" que puedes llamar repetidamente, que puede aceptar parámetros y realizar operaciones en la base de datos.

#### Usos principales:

1. Ejecutar operaciones complejas que requieren múltiples consultas
2. Implementar lógica de negocio directamente en la base de datos
3. Realizar operaciones repetitivas
4. Gestionar la seguridad de la base de datos
5. Procesar transacciones

#### ¿Por qué es recomendable?

1. **Rendimiento:**
   - Se compilan una sola vez y se almacena el plan de ejecución
   - Reduce el tráfico de red al enviar solo los parámetros en lugar de toda la consulta
   - Mejor uso del caché del servidor

2. **Seguridad:**
   - Permite controlar quién tiene acceso a qué datos
   - Evita inyección SQL al usar parámetros
   - Puedes dar permisos para ejecutar el procedimiento sin dar acceso directo a las tablas

3. **Mantenimiento:**
   - Centraliza la lógica de negocio
   - Facilita las actualizaciones (solo modificas el procedimiento, no cada consulta)
   - Mejor control de versiones

4. **Reutilización:**
   - El mismo código puede ser usado por diferentes aplicaciones
   - Reduce la duplicación de código
   - Facilita la consistencia en las operaciones

#### ¿Cuándo NO es necesario usarlos?

1. **Consultas simples:**
   - Para SELECT básicos de una sola tabla
   - Cuando no hay lógica compleja involucrada
   - Operaciones CRUD básicas

2. **Operaciones poco frecuentes:**
   - Consultas que se ejecutan raramente
   - Operaciones únicas o de una sola vez

3. **Desarrollo rápido o prototipos:**
   - Cuando necesitas iterar rápidamente y cambiar consultas con frecuencia
   - En fases tempranas de desarrollo donde la estructura no está definida

4. **Aplicaciones pequeñas:**
   - Cuando la aplicación es simple y no requiere optimización
   - Cuando hay pocas consultas o usuarios

5. **Consultas dinámicas:**
   - Cuando necesitas generar consultas muy dinámicas
   - Cuando los criterios de búsqueda son muy variables

#### Ejemplo práctico de cuándo usar y no usar:

```sql
-- BUEN CASO PARA USAR PROCEDIMIENTO:
CREATE PROCEDURE dbo.ObtenerVentasPorRegion
(
    @Region VARCHAR(50),
    @FechaInicio DATE,
    @FechaFin DATE
)
AS
BEGIN
    -- Múltiples operaciones
    -- Cálculos complejos
    -- Lógica de negocio
    -- Validaciones
    -- Joins múltiples
END

-- NO NECESITA PROCEDIMIENTO:
SELECT Nombre, Email 
FROM Clientes 
WHERE Ciudad = 'Madrid';
```

En resumen, los procedimientos almacenados son muy útiles para operaciones complejas, repetitivas y que requieren seguridad, pero pueden ser innecesarios para operaciones simples o poco frecuentes. La decisión de usarlos debe basarse en los requerimientos específicos de tu aplicación.

#### VARIACIONES ENTRE PROGRAMAS:

```SQL

# PostgreSQL

CREATE [OR REPLACE] PROCEDURE nombre_procedimiento([parámetros])
LANGUAGE plpgsql
AS $$
BEGIN
    -- Lógica del procedimiento
END;
$$;

# Ejemplo (Insertar nuevo pasajero):

CREATE OR REPLACE PROCEDURE insertar_pasajero(
    p_nombre VARCHAR(100),
    p_edad INTEGER,
    p_genero CHAR(1)
)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO passengers (name, age, gender)
    VALUES (p_nombre, p_edad, p_genero);
END;
$$;

-- Llamada al procedimiento
CALL insertar_pasajero('Juan Pérez', 30, 'M');

#######################

# SQL Server

CREATE PROCEDURE nombre_procedimiento
    @parametro1 tipo,
    @parametro2 tipo
AS
BEGIN
    -- Lógica del procedimiento
END;

# Ejemplo (Insertar nuevo pasajero):

CREATE PROCEDURE insertar_pasajero
    @nombre VARCHAR(100),
    @edad INT,
    @genero CHAR(1)
AS
BEGIN
    INSERT INTO passengers (name, age, gender)
    VALUES (@nombre, @edad, @genero);
END;

-- Llamada al procedimiento
EXEC insertar_pasajero @nombre = 'Juan Pérez', @edad = 30, @genero = 'M';

#######################

# MySQL/MariaDB

DELIMITER //
CREATE PROCEDURE nombre_procedimiento(parametro1 tipo, parametro2 tipo)
BEGIN
    -- Lógica del procedimiento
END //
DELIMITER ;

# Ejemplo (Insertar nuevo pasajero):

DELIMITER //
CREATE PROCEDURE insertar_pasajero(
    IN p_nombre VARCHAR(100),
    IN p_edad INT,
    IN p_genero CHAR(1)
)

BEGIN
    INSERT INTO passengers (name, age, gender)
    VALUES (p_nombre, p_edad, p_genero);
END //
DELIMITER ;

-- Llamada al procedimiento
CALL insertar_pasajero('Juan Pérez', 30, 'M');
```

## TRIGGERS EN SQL

Los **triggers** (disparadores) en SQL son procedimientos almacenados que se ejecutan automáticamente cuando ocurre un evento específico en una tabla. Se usan para mantener la integridad de los datos, registrar cambios, prevenir operaciones no deseadas o ejecutar acciones automáticas.
### SINTAXIS GENERAL

```sql
CREATE TRIGGER nombre_del_trigger
{ BEFORE | AFTER } { INSERT | UPDATE | DELETE }
ON nombre_de_tabla
FOR EACH { ROW | STATEMENT }
BEGIN
    -- Código a ejecutar cuando se active el trigger
END;
```

- `BEFORE` o `AFTER`: Define si el trigger se ejecuta **antes** o **después** del evento.
- `INSERT | UPDATE | DELETE`: Especifica el tipo de evento que activa el trigger.
- `ON nombre_de_tabla`: Indica la tabla sobre la cual actúa el trigger.
- `FOR EACH ROW` o `FOR EACH STATEMENT`: Define si el trigger se ejecuta para **cada fila** afectada o solo **una vez por consulta**.
- El código dentro de `BEGIN ... END` ejecuta las acciones deseadas.

### DIFERENCIAS ENTRE MOTORES SQL

| Motor          | Sintaxis Destacada | Diferencias Principales                                                     |
| -------------- | ------------------ | --------------------------------------------------------------------------- |
| **MySQL**      | `CREATE TRIGGER`   | No permite `INSTEAD OF`. Solo `BEFORE` y `AFTER`.                           |
| **PostgreSQL** | Usa `PL/pgSQL`     | Se pueden usar funciones almacenadas en triggers.                           |
| **SQL Server** | `CREATE TRIGGER`   | Soporta `INSTEAD OF` triggers para interceptar eventos antes de ejecutarse. |

### EJEMPLO DE DIFERENCIA

En **SQL Server**, puedes hacer un trigger que reemplace una acción usando `INSTEAD OF`:

```sql
CREATE TRIGGER tr_eliminar_empleados
ON empleados
INSTEAD OF DELETE
AS
BEGIN
    PRINT 'No puedes eliminar empleados directamente.'
END;
```

Mientras que en **MySQL y PostgreSQL**, solo podrías prevenirlo con un `BEFORE DELETE` lanzando un error.

### TRIGGERS EN TABLAS vs. COLUMNAS/DATOS ESPECIFICOS

- **Triggers en Tablas**: Se activan cuando la tabla sufre cambios (`INSERT`, `UPDATE`, `DELETE`).
- **Triggers en Columnas/Datos**: Se implementan dentro del `UPDATE` con una condición para actuar solo si cambia un valor específico.

#### Ejemplo: Trigger solo si cambia un campo específico

```sql
CREATE TRIGGER verificar_cambio_salario
BEFORE UPDATE ON empleados
FOR EACH ROW
BEGIN
    IF OLD.salario <> NEW.salario THEN
        INSERT INTO auditoria_cambios (empleado_id, cambio)
        VALUES (OLD.id, 'Cambio de salario');
    END IF;
END;
```

**Explicación**: Se ejecuta **antes** de actualizar un empleado y solo si el salario cambia.

### EJEMPLO PRACTICO DE USO DE TRIGGERS

 **Objetivo**: Registrar automáticamente cada vez que un usuario es eliminado en una tabla de auditoría.

```sql
CREATE TRIGGER registrar_borrado_usuario
AFTER DELETE ON usuarios
FOR EACH ROW
BEGIN
    INSERT INTO auditoria (usuario_id, accion, fecha)
    VALUES (OLD.id, 'Usuario eliminado', NOW());
END;
```

 **Explicación**:
- `AFTER DELETE`: Se ejecuta después de borrar un usuario.
- `OLD.id`: Obtiene el ID del usuario eliminado.
- `NOW()`: Registra la fecha y hora del evento.

### CONCLUSION

Los triggers son herramientas poderosas para automatizar acciones en una base de datos. Pueden: ✅ Prevenir cambios no deseados.  
✅ Mantener registros de auditoría.  
✅ Automatizar procesos sin intervención manual.
## PALABRAS RESERVADAS EN LAS SUBCONSULTAS

### `EXISTS` vs. `NOT EXISTS`

Estas palabras clave verifican si una subconsulta devuelve o no resultados.

✅ **`EXISTS`** → Devuelve `TRUE` si la subconsulta retorna al menos una fila.  
❌ **`NOT EXISTS`** → Devuelve `TRUE` si la subconsulta **NO** devuelve filas.

**Ejemplo:** Listar comunidades que tienen territorios registrados.

```sql
SELECT nombre
FROM Comunidades C
WHERE EXISTS (
    SELECT 1 FROM Territorios T
    WHERE T.comunidad_id = C.id
);
```

Para las comunidades **sin** territorios registrados:

```sql
SELECT nombre
FROM Comunidades C
WHERE NOT EXISTS (
    SELECT 1 FROM Territorios T
    WHERE T.comunidad_id = C.id
);
```

### `IN` vs. `NOT IN`

Estas comparan si un valor está dentro de un conjunto de resultados.

✅ **`IN`** → Devuelve `TRUE` si el valor está en la lista de la subconsulta.  
❌ **`NOT IN`** → Devuelve `TRUE` si el valor **NO** está en la lista.

**Ejemplo:** Comunidades que tienen territorios.

```sql
SELECT nombre
FROM Comunidades
WHERE id IN (
    SELECT comunidad_id FROM Territorios
);
```

Comunidades **sin** territorios:

```sql
SELECT nombre
FROM Comunidades
WHERE id NOT IN (
    SELECT comunidad_id FROM Territorios
);
```

⚠️ **Precaución con `NULL` en `NOT IN`**, ya que puede provocar resultados inesperados. `EXISTS` es más seguro.

### `ALL` vs. `ANY`

Estas comparan un valor con **todos** o **al menos uno** de los resultados de una subconsulta.

✅ **`ALL`** → Compara un valor con **TODOS** los valores devueltos.  
✅ **`ANY`** → Compara un valor con **AL MENOS UNO** de los valores devueltos.

**Ejemplo con `ANY` (equivalente a `IN` en este caso):**

```sql
SELECT nombre
FROM Comunidades
WHERE id = ANY (
    SELECT comunidad_id FROM Territorios WHERE region = 'Amazonas'
);
```

**Ejemplo con `ALL`:**

```sql
SELECT nombre
FROM Comunidades
WHERE id = ALL (
    SELECT comunidad_id FROM Territorios WHERE region = 'Amazonas'
);
```

🔹 **Diferencia clave:**

- `ANY` → Se cumple si **al menos uno** de los registros coincide.
- `ALL` → Se cumple si **todos** los registros cumplen la condición.

### 🔥 Resumen rápido:

| Operador     | Devuelve `TRUE` si…                                      |
| ------------ | -------------------------------------------------------- |
| `EXISTS`     | La subconsulta devuelve al menos un registro.            |
| `NOT EXISTS` | La subconsulta NO devuelve registros.                    |
| `IN`         | El valor está en la lista de la subconsulta.             |
| `NOT IN`     | El valor **NO** está en la lista. (¡Cuidado con `NULL`!) |
| `ANY`        | Al menos un valor cumple la condición.                   |
| `ALL`        | **Todos** los valores cumplen la condición.              |

## TRANSACCIONES EN SQL SERVER

## Introducción

En SQL Server, una **transacción** es una secuencia de operaciones que se ejecutan como una unidad indivisible. Se utiliza para asegurar la integridad de los datos y garantizar que todas las operaciones dentro de la transacción se completen correctamente. Si ocurre algún error, los cambios pueden deshacerse mediante un **ROLLBACK**, o si todo es exitoso, se pueden confirmar con un **COMMIT**.

## Sintaxis General

```sql
BEGIN TRANSACTION;
-- Operaciones SQL
COMMIT; -- Confirma la transacción
-- o
ROLLBACK; -- Revierte la transacción
```

## Distinción entre COMMIT y ROLLBACK

| Comando      | Descripción                                                                                                               |
| ------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **COMMIT**   | Confirma los cambios realizados en la transacción, haciendo que sean permanentes en la base de datos.                     |
| **ROLLBACK** | Revierte todos los cambios realizados desde el inicio de la transacción, devolviendo la base de datos a su estado previo. |

---

### Usos de las Transacciones en SQL Server

#### 1. Uso en Operaciones DML (INSERT, UPDATE, DELETE)

Las transacciones son especialmente útiles al modificar datos para evitar inconsistencias.

#### Ejemplo:

```sql
BEGIN TRANSACTION;
DELETE FROM Productos WHERE Stock = 0;
-- Si algo sale mal
ROLLBACK;
-- Si todo está correcto
COMMIT;
```

#### 2. Uso en la Ejecución de Operaciones en Tablas Relacionadas

Al modificar datos en múltiples tablas, se debe garantizar que todas las modificaciones se realicen o ninguna de ellas.

#### Ejemplo:

```sql
BEGIN TRANSACTION;
UPDATE Productos SET Precio = Precio * 1.1 WHERE Categoria = 'Electrónica';
INSERT INTO Auditoria (Accion, Fecha) VALUES ('Aumento de precios', GETDATE());
-- Si todo es correcto
COMMIT;
-- Si ocurre un error
ROLLBACK;
```

#### 3. Uso con Variables

Las transacciones también pueden depender de valores calculados dentro de la consulta.

#### Ejemplo:

```sql
BEGIN TRANSACTION;
DECLARE @PromedioPrecio DECIMAL(10,2);
SELECT @PromedioPrecio = AVG(Precio) FROM Productos;
UPDATE Productos SET Precio = Precio * 1.15;
IF (SELECT MIN(Precio) FROM Productos) < @PromedioPrecio
    ROLLBACK;
ELSE
    COMMIT;
```


### Consideraciones

- Las transacciones ayudan a mantener la consistencia y confiabilidad de los datos.
- Un **COMMIT** hace que los cambios sean permanentes, mientras que un **ROLLBACK** los revierte.
- Se recomienda utilizar **SAVEPOINT** en transacciones largas para poder hacer un rollback parcial.

#### Uso de SAVEPOINT:

```sql
BEGIN TRANSACTION;
SAVE TRAN Punto1;
UPDATE Productos SET Precio = Precio * 1.05;
-- Si se necesita revertir solo hasta este punto
ROLLBACK TRAN Punto1;
COMMIT;
```

## MANEJO DE ERRORES EN SQL SERVER

### **1. Introducción**

El manejo de errores en SQL Server es una práctica fundamental para garantizar que los procedimientos almacenados, consultas y transacciones se ejecuten correctamente y permitan la recuperación ante posibles fallos.

SQL Server ofrece diversas herramientas para capturar y manejar errores, tales como:

- Variables de sistema (`@@ERROR`)
- Bloques `TRY...CATCH`
- Comandos `RAISERROR` y `THROW`

### **2. Uso de Variables de Sistema**

SQL Server proporciona la variable de sistema `@@ERROR`, que almacena el último código de error ocurrido en la sesión.

### **Sintaxis**

```sql
SELECT 1 / 0; -- Esto generará un error de división por cero

IF @@ERROR <> 0
BEGIN
    PRINT 'Se ha producido un error';
END
```

### **Ejemplo con Transacciones**

```sql
BEGIN TRANSACTION;
SELECT 1 / 0;
DECLARE @Error INT = @@ERROR;

IF @Error <> 0
BEGIN
    ROLLBACK TRANSACTION;
    PRINT 'Error detectado y transacción revertida';
    RETURN;
END

COMMIT TRANSACTION;
```

### **3. Uso de TRY...CATCH**

El bloque `TRY...CATCH` permite capturar errores de manera más estructurada y ejecutar acciones correctivas o de registro.

### **Sintaxis**

```sql
BEGIN TRY
    -- Código susceptible a error
END TRY
BEGIN CATCH
    -- Manejador de errores
END CATCH
```

### **Ejemplo con Transacciones**

```sql
BEGIN TRY
    BEGIN TRANSACTION;
    SELECT 1 / 0; -- Error intencional
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    PRINT 'Se detectó un error: ' + ERROR_MESSAGE();
END CATCH
```

### **4. Recuperación de Información sobre Errores**

Dentro de un `CATCH`, se pueden utilizar funciones del sistema para obtener información detallada del error:

- `ERROR_MESSAGE()`: Mensaje del error
- `ERROR_NUMBER()`: Número del error
- `ERROR_SEVERITY()`: Gravedad del error
- `ERROR_STATE()`: Estado del error
- `ERROR_LINE()`: Línea donde ocurrió el error
- `ERROR_PROCEDURE()`: Procedimiento en el que se generó el error

### **Ejemplo**

```sql
BEGIN TRY
    SELECT 1 / 0;
END TRY
BEGIN CATCH
    PRINT 'Error: ' + ERROR_MESSAGE();
    PRINT 'Número: ' + CAST(ERROR_NUMBER() AS NVARCHAR);
    PRINT 'Severidad: ' + CAST(ERROR_SEVERITY() AS NVARCHAR);
    PRINT 'Estado: ' + CAST(ERROR_STATE() AS NVARCHAR);
    PRINT 'Línea: ' + CAST(ERROR_LINE() AS NVARCHAR);
END CATCH
```

### **5. Uso de RAISERROR y THROW**

#### **RAISERROR**

`RAISERROR` permite generar errores personalizados con severidad y estado definidos.

#### **Sintaxis**

```sql
RAISERROR ('Mensaje de error', 16, 1);
```

#### **Ejemplo con TRY...CATCH**

```sql
BEGIN TRY
    BEGIN TRANSACTION;
    SELECT 1 / 0;
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    RAISERROR ('Error personalizado: %s', 16, 1, ERROR_MESSAGE());
END CATCH
```

#### **THROW**

`THROW` se usa para relanzar el error original en un bloque `CATCH`.

### **Ejemplo**

```sql
BEGIN TRY
    BEGIN TRANSACTION;
    SELECT 1 / 0;
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    THROW;
END CATCH
```

### **6. Conclusión**

El manejo de errores en SQL Server es esencial para el desarrollo de bases de datos robustas y confiables. Utilizar `@@ERROR`, `TRY...CATCH`, `RAISERROR` y `THROW` permite detectar, registrar y manejar errores de manera efectiva, asegurando la integridad de los datos y una mejor experiencia para los usuarios.