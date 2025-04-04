
### **1. Funciones de Configuración en Consola e IDE**  

Este apartado cubre comandos esenciales para configurar y diagnosticar bases de datos en diferentes motores SQL (SQL Server, MySQL, PostgreSQL). Incluye fórmulas para buscar tablas, deshabilitar restricciones, reparar estructuras y reiniciar secuencias.  

---

#### **1.1 Búsqueda de tablas a través de columnas conocidas**  
**Objetivo:** Encontrar el nombre de una tabla cuando solo se conoce el nombre de una columna.  

- **SQL Server:**  
  ```sql
  SELECT OBJECT_NAME(object_id) 
  FROM sys.columns 
  WHERE name = 'nombre_columna';
  ```  
  **Explicación:**  
  - `sys.columns` almacena metadatos de columnas.  
  - `OBJECT_NAME()` devuelve el nombre de la tabla asociada al `object_id`.  

  **Ejemplo:**  
  ```sql
  SELECT OBJECT_NAME(object_id) AS Tabla
  FROM sys.columns 
  WHERE name = 'customer_id';  -- Devuelve 'customers' si existe.
  ```  

- **MySQL:**  
  ```sql
  SELECT table_name 
  FROM information_schema.columns 
  WHERE column_name = 'nombre_columna';
  ```  
  **Ejemplo:**  
  ```sql
  SELECT table_name 
  FROM information_schema.columns 
  WHERE column_name = 'email';  -- Devuelve 'users' si existe.
  ```  

- **PostgreSQL:**  
  ```sql
  SELECT table_name, column_name, data_type 
  FROM information_schema.columns 
  WHERE table_name = 'nombre_tabla';
  ```  
  **Explicación:**  
  - Equivalente a `DESCRIBE tabla` en otros sistemas.  
  **Ejemplo:**  
  ```sql
  SELECT column_name, data_type 
  FROM information_schema.columns 
  WHERE table_name = 'orders';  -- Lista todas las columnas de 'orders'.
  ```  

---

#### **1.2 Deshabilitar verificaciones de llaves foráneas**  
**Objetivo:** Permitir operaciones que violen restricciones temporalmente (ej. borrar registros referenciados).  

- **MySQL:**  
  ```sql
  SET FOREIGN_KEY_CHECKS = 0;  -- Deshabilita verificaciones
  -- Operaciones (ej. DELETE o TRUNCATE)
  SET FOREIGN_KEY_CHECKS = 1;  -- Reactiva verificaciones
  ```  
  **Ejemplo:**  
  ```sql
  SET FOREIGN_KEY_CHECKS = 0;
  TRUNCATE TABLE orders;  -- Borra datos aunque haya referencias
  SET FOREIGN_KEY_CHECKS = 1;
  ```  

- **SQL Server:**  
  ```sql
  ALTER TABLE tabla NOCHECK CONSTRAINT ALL;  -- Deshabilita todas las FK
  -- Operaciones
  ALTER TABLE tabla CHECK CONSTRAINT ALL;    -- Reactiva
  ```  

---

#### **1.3 Modo de actualizaciones seguras**  
**Objetivo:** Permitir actualizaciones sin cláusula `WHERE` (útil en desarrollo).  

- **MySQL:**  
  ```sql
  SET SQL_SAFE_UPDATES = 0;  -- Permite UPDATE/DELETE sin WHERE
  UPDATE productos SET precio = 10;  -- Actualiza toda la tabla
  SET SQL_SAFE_UPDATES = 1;  -- Vuelve al modo seguro
  ```  

---

#### **1.4 Reparación de columnas o tablas**  
**Objetivo:** Corregir errores en estructuras de tablas (ej. después de un crash).  

- **MySQL:**  
  ```sql
  REPAIR TABLE mysql.proc;  -- Repara la tabla de procedimientos
  ```  

---

#### **1.5 Visualización de bases de datos y tablas**  
- **Listar bases de datos:**  
  ```sql
  SHOW DATABASES;  -- MySQL
  SELECT name FROM sys.databases;  -- SQL Server
  ```  

- **Listar tablas de una base de datos:**  
  ```sql
  SHOW TABLES IN nombre_bd;  -- MySQL
  SELECT table_name FROM information_schema.tables WHERE table_schema = 'nombre_bd';  -- PostgreSQL/SQL Server
  ```  

---

#### **1.6 Reinicio de secuencias (Auto-incrementales)**  
**Objetivo:** Corregir saltos en IDs después de inserciones fallidas.  

- **PostgreSQL:**  
  ```sql
  -- Diagnóstico:
  SELECT last_value FROM tabla_columna_seq;
  
  -- Reinicio:
  SELECT setval('tabla_columna_seq', (SELECT MAX(id) FROM tabla));
  ```  
  **Ejemplo:**  
  ```sql
  SELECT setval('products_id_seq', (SELECT MAX(id) FROM products));  -- Sincroniza la secuencia con el máximo ID.
  ```  

- **MySQL:**  
  ```sql
  -- Ver valor actual:
  SELECT AUTO_INCREMENT 
  FROM information_schema.tables 
  WHERE table_name = 'tabla' AND table_schema = 'bd';
  
  -- Reiniciar:
  ALTER TABLE tabla AUTO_INCREMENT = 1;
  ```  
  **Ejemplo:**  
  ```sql
  ALTER TABLE users AUTO_INCREMENT = 100;  -- El próximo ID será 100.
  ```  

---

### **Resumen de comandos clave**  
| **Función**               | **SQL Server**                          | **MySQL**                                | **PostgreSQL**                          |
|---------------------------|----------------------------------------|------------------------------------------|----------------------------------------|
| Buscar tabla por columna  | `OBJECT_NAME()` + `sys.columns`        | `information_schema.columns`             | `information_schema.columns`           |
| Deshabilitar FKs          | `ALTER TABLE ... NOCHECK CONSTRAINT`   | `SET FOREIGN_KEY_CHECKS = 0`             | `ALTER TABLE ... DISABLE TRIGGER ALL`  |
| Reiniciar secuencias      | `DBCC CHECKIDENT('tabla', RESEED, n)`  | `ALTER TABLE ... AUTO_INCREMENT = n`     | `setval('secuencia', n)`               |

### **2. Tablas Temporales en SQL**  

Las tablas temporales son estructuras que permiten almacenar datos de forma **transitoria** durante una sesión o una consulta. Son útiles para:  
- **Optimizar consultas complejas** (almacenar resultados intermedios).  
- **Procesar grandes volúmenes de datos** en etapas.  
- **Debuggear** o validar datos antes de operaciones definitivas.  

---

## **2.1 Tipos de Tablas Temporales**  

### **A. Tablas Temporales Locales (`#NombreTabla`)**  
**Alcance:** Solo visible en la sesión actual. Se eliminan al cerrar la sesión.  

**Sintaxis:**  
```sql
CREATE TABLE #NombreTabla (
    Columna1 TipoDato,
    Columna2 TipoDato,
    ...
);
```

**Ejemplo:**  
```sql
CREATE TABLE #VentasTemp (
    ID INT IDENTITY(1,1),
    Fecha DATE,
    Producto VARCHAR(50),
    Cantidad INT,
    Monto DECIMAL(10,2)
);

-- Insertar datos
INSERT INTO #VentasTemp (Fecha, Producto, Cantidad, Monto)
VALUES 
    ('2024-07-22', 'Laptop', 5, 3000.00),
    ('2024-07-22', 'Mouse', 10, 200.00);

-- Consultar
SELECT * FROM #VentasTemp;
```

**Caso de uso:**  
Almacenar resultados intermedios de un reporte mensual antes de consolidarlos en una tabla permanente.

---

### **B. Tablas Temporales Globales (`##NombreTabla`)**  
**Alcance:** Visible para **todas las sesiones**. Se eliminan cuando la última sesión que las usa se cierra.  

**Sintaxis:**  
```sql
CREATE TABLE ##NombreTabla (
    Columna1 TipoDato,
    Columna2 TipoDato,
    ...
);
```

**Ejemplo:**  
```sql
CREATE TABLE ##UsuariosActivos (
    UserID INT,
    Nombre VARCHAR(50),
    UltimoAcceso DATETIME
);

-- Insertar datos desde múltiples sesiones
INSERT INTO ##UsuariosActivos (UserID, Nombre, UltimoAcceso)
VALUES 
    (1, 'Juan Pérez', GETDATE()),
    (2, 'María García', GETDATE());

-- Consultar desde otra sesión
SELECT * FROM ##UsuariosActivos;
```

**Caso de uso:**  
Compartir datos entre conexiones simultáneas (ej.: monitoreo de usuarios activos en una app).

---

### **C. Variables de Tabla (`@NombreTabla`)**  
**Alcance:** Solo en el **batch actual** (no persisten después de `GO` en SQL Server).  

**Sintaxis:**  
```sql
DECLARE @NombreTabla TABLE (
    Columna1 TipoDato,
    Columna2 TipoDato,
    ...
);
```

**Ejemplo:**  
```sql
DECLARE @ProductosTop TABLE (
    ProductID INT,
    Nombre VARCHAR(50),
    TotalVentas DECIMAL(10,2)
);

-- Insertar datos con una consulta
INSERT INTO @ProductosTop (ProductID, Nombre, TotalVentas)
SELECT TOP 5
    P.ProductID,
    P.ProductName,
    SUM(OD.Quantity * OD.UnitPrice) AS TotalVentas
FROM 
    Orders O
    JOIN [Order Details] OD ON O.OrderID = OD.OrderID
    JOIN Products P ON OD.ProductID = P.ProductID
GROUP BY 
    P.ProductID, P.ProductName
ORDER BY 
    TotalVentas DESC;

-- Consultar
SELECT * FROM @ProductosTop;
```

**Caso de uso:**  
Almacenar resultados de subconsultas para reutilizarlos en operaciones posteriores (ej.: filtrar clientes VIP).

---

## **2.2 Método `SELECT INTO` para Crear Tablas Temporales**  
Permite crear tablas temporales **copiando la estructura y datos** de una consulta.  

### **A. Tabla Temporal Local (`#TempTable`)**  
```sql
SELECT columnas
INTO #TempTable
FROM TablaOrigen
WHERE condición;
```

**Ejemplo:**  
```sql
-- Crear tabla temporal con clientes VIP
SELECT 
    C.CustomerID, 
    C.CompanyName, 
    COUNT(O.OrderID) AS TotalPedidos,
    SUM(OD.Quantity * OD.UnitPrice) AS MontoTotal
INTO #ClientesVIP
FROM 
    Customers C
    JOIN Orders O ON C.CustomerID = O.CustomerID
    JOIN [Order Details] OD ON O.OrderID = OD.OrderID
GROUP BY 
    C.CustomerID, C.CompanyName
HAVING 
    SUM(OD.Quantity * OD.UnitPrice) > 10000;

-- Consultar
SELECT * FROM #ClientesVIP;
```

### **B. Tabla Temporal Global (`##TempTable`)**  
```sql
SELECT columnas
INTO ##TempTable
FROM TablaOrigen;
```

### **C. Tabla Permanente**  
```sql
SELECT columnas
INTO NuevaTablaPermanente
FROM TablaOrigen;
```

**Diferencias clave:**  
| Tipo                | Sintaxis       | Alcance               | Persistencia          |  
|---------------------|---------------|-----------------------|-----------------------|  
| Local               | `INTO #Temp`  | Sesión actual         | Hasta cierre de sesión |  
| Global              | `INTO ##Temp` | Todas las sesiones    | Hasta última sesión    |  
| Permanente          | `INTO Tabla`  | Base de datos         | Hasta ser eliminada    |  

---

## **2.3 Tablas CTE (Common Table Expressions)**  
**Definición:** Consultas temporales que existen solo dentro de una instrucción SQL.  

**Sintaxis:**  
```sql
WITH NombreCTE AS (
    SELECT columnas
    FROM Tabla
    WHERE condición
)
SELECT * FROM NombreCTE;
```

**Ejemplo:**  
```sql
-- CTE para calcular ventas por región
WITH VentasPorRegion AS (
    SELECT 
        R.RegionID,
        R.RegionName,
        SUM(O.TotalAmount) AS TotalVentas
    FROM 
        Orders O
        JOIN Customers C ON O.CustomerID = C.CustomerID
        JOIN Region R ON C.RegionID = R.RegionID
    GROUP BY 
        R.RegionID, R.RegionName
)
-- Consulta principal usando la CTE
SELECT 
    RegionName,
    TotalVentas
FROM 
    VentasPorRegion
WHERE 
    TotalVentas > 100000
ORDER BY 
    TotalVentas DESC;
```

**Diferencias con Tablas Temporales:**  
| Característica      | CTE                          | Tabla Temporal (`#Temp`)       |  
|---------------------|-----------------------------|-------------------------------|  
| Persistencia        | Solo durante la consulta    | Hasta fin de sesión           |  
| Reutilización       | Solo en la misma consulta   | Múltiples consultas           |  
| Índices             | No soportados              | Sí (se pueden crear)          |  

---

## **2.4 Casos de Uso Comunes**  
1. **ETL (Extraer, Transformar, Cargar):**  
   ```sql
   SELECT * INTO #TempData FROM RawData WHERE Year = 2024;
   -- Limpieza y transformación
   UPDATE #TempData SET Category = UPPER(Category);
   -- Carga final
   INSERT INTO CleanData SELECT * FROM #TempData;
   ```

2. **Debugging de consultas complejas:**  
   ```sql
   SELECT * INTO #DebugResults FROM LargeTable WHERE Condition = 'X';
   -- Verificar datos intermedios
   SELECT COUNT(*) FROM #DebugResults;
   ```

3. **Particionamiento de datos:**  
   ```sql
   SELECT * INTO #HighPriority FROM Orders WHERE Priority = 'High';
   SELECT * INTO #LowPriority FROM Orders WHERE Priority = 'Low';
   ```

---

### **Resumen de Comandos Clave**  
| **Operación**               | **Sintaxis**                                     |     |
| --------------------------- | ------------------------------------------------ | --- |
| Crear tabla temporal local  | `CREATE TABLE #Temp (...)` o `SELECT INTO #Temp` |     |
| Crear tabla temporal global | `CREATE TABLE ##Temp (...)`                      |     |
| Variable de tabla           | `DECLARE @Temp TABLE (...)`                      |     |
| CTE                         | `WITH CTE AS (SELECT ...)`                       |     |
### **3. Common Table Expressions (CTE)**  

Las **CTE (Common Table Expressions)** son consultas temporales que existen solo dentro del ámbito de una instrucción SQL. Se utilizan para simplificar consultas complejas, mejorar la legibilidad y permitir operaciones recursivas.  

---

## **3.1 Definición y Sintaxis**  

### **Sintaxis Básica**  
```sql
WITH NombreCTE AS (
    -- Consulta SQL que define la CTE
    SELECT columnas
    FROM tabla
    WHERE condición
)
-- Consulta principal que usa la CTE
SELECT * FROM NombreCTE;
```

### **Ejemplo Básico**  
```sql
-- CTE para obtener productos con ventas superiores a $1000
WITH ProductosDestacados AS (
    SELECT 
        ProductID,
        ProductName,
        UnitPrice * Quantity AS TotalVentas
    FROM 
        OrderDetails
    WHERE 
        UnitPrice * Quantity > 1000
)
-- Consulta principal
SELECT * FROM ProductosDestacados
ORDER BY TotalVentas DESC;
```

**Explicación:**  
- La CTE `ProductosDestacados` filtra productos con ventas altas.  
- La consulta principal usa esta CTE como si fuera una tabla temporal.  

---

## **3.2 Diferencias con Tablas Temporales**  

| **Característica**       | **CTE**                                      | **Tabla Temporal (`#Temp`)**                |  
|--------------------------|---------------------------------------------|--------------------------------------------|  
| **Persistencia**         | Solo dura durante la ejecución de la consulta | Persiste hasta que la sesión se cierra     |  
| **Reutilización**        | Solo se puede usar en la misma consulta      | Se puede usar en múltiples consultas       |  
| **Índices**              | No soporta índices                          | Soporta índices (se pueden crear)          |  
| **Almacenamiento**       | No se almacena físicamente                  | Se almacena en `tempdb` (SQL Server)       |  
| **Rendimiento**          | Ideal para consultas anidadas               | Mejor para datos reutilizables             |  

**Ejemplo Comparativo:**  
```sql
-- Usando CTE (no persiste después de la consulta)
WITH Ventas2024 AS (
    SELECT * FROM Orders WHERE YEAR(OrderDate) = 2024
)
SELECT * FROM Ventas2024;

-- Usando Tabla Temporal (persiste en la sesión)
SELECT * INTO #Ventas2024 FROM Orders WHERE YEAR(OrderDate) = 2024;
SELECT * FROM #Ventas2024;  -- Reutilizable en otras consultas
```

---

## **3.3 Ejemplos de Uso Avanzados**  

### **A. CTE Recursivas**  
Útiles para jerarquías (ej.: organigramas, árboles de categorías).  

**Ejemplo: Jerarquía de Empleados**  
```sql
WITH JerarquiaEmpleados AS (
    -- Caso base: CEO (no tiene manager)
    SELECT 
        EmployeeID,
        Name,
        ManagerID,
        0 AS Nivel
    FROM 
        Employees
    WHERE 
        ManagerID IS NULL

    UNION ALL

    -- Caso recursivo: Subordinados
    SELECT 
        e.EmployeeID,
        e.Name,
        e.ManagerID,
        j.Nivel + 1
    FROM 
        Employees e
    JOIN 
        JerarquiaEmpleados j ON e.ManagerID = j.EmployeeID
)
SELECT * FROM JerarquiaEmpleados
ORDER BY Nivel;
```

**Resultado:**  
| EmployeeID | Name       | ManagerID | Nivel |  
|------------|------------|-----------|-------|  
| 1          | Ana (CEO)  | NULL      | 0     |  
| 2          | Carlos     | 1         | 1     |  
| 3          | María      | 2         | 2     |  

---

### **B. CTE para Dividir Consultas Complejas**  
**Ejemplo: Cálculo de Ventas por Categoría con Filtros**  
```sql
WITH VentasPorCategoria AS (
    SELECT 
        c.CategoryName,
        SUM(od.Quantity * od.UnitPrice) AS TotalVentas
    FROM 
        OrderDetails od
        JOIN Products p ON od.ProductID = p.ProductID
        JOIN Categories c ON p.CategoryID = c.CategoryID
    GROUP BY 
        c.CategoryName
),
-- Segunda CTE para filtrar
CategoriasDestacadas AS (
    SELECT * 
    FROM VentasPorCategoria 
    WHERE TotalVentas > 10000
)
-- Consulta final
SELECT * FROM CategoriasDestacadas
ORDER BY TotalVentas DESC;
```

---

## **3.4 Ventajas y Limitaciones**  

### **Ventajas**  
✔ **Legibilidad:** Divide consultas largas en partes lógicas.  
✔ **Recursión:** Única forma nativa de hacer consultas recursivas en SQL.  
✔ **Sin sobrecargar `tempdb`:** No ocupa espacio físico como las tablas temporales.  

### **Limitaciones**  
✖ **No reutilizable:** No se puede referenciar fuera de su consulta principal.  
✖ **Sin índices:** No se pueden optimizar con índices como las tablas temporales.  
✖ **Ámbito limitado:** Solo existe en la consulta donde se define.  

**Ejemplo de Limitación:**  
```sql
WITH CTE_Ejemplo AS (SELECT 1 AS Valor);
-- Error: La CTE no existe fuera de su ámbito
SELECT * FROM CTE_Ejemplo;  
```

---

## **3.5 Comparación entre Motores de Bases de Datos**  

| **Operación**          | **SQL Server**       | **PostgreSQL**       | **MySQL**            |  
|------------------------|----------------------|----------------------|----------------------|  
| **Sintaxis CTE**       | `WITH CTE AS (...)`  | `WITH CTE AS (...)`  | `WITH CTE AS (...)`  |  
| **CTE Recursivas**     | Sí                   | Sí                   | Sí (v8.0+)           |  
| **Materialización**    | No                   | Opcional (`MATERIALIZED`)| No                |  

**Ejemplo en PostgreSQL con `MATERIALIZED`:**  
```sql
WITH MATERIALIZED Ventas AS (
    SELECT * FROM Orders WHERE Total > 1000
)
SELECT * FROM Ventas;  -- Fuerza la materialización para mejorar rendimiento
```

---

### **Resumen de Comandos Clave**  
| **Propósito**               | **Sintaxis**                                  |  
|----------------------------|----------------------------------------------|  
| CTE básica                 | `WITH CTE AS (SELECT ...)`                  |  
| CTE recursiva              | `WITH RECURSIVE CTE AS (... UNION ALL ...)` |  
| Múltiples CTEs             | `WITH CTE1 AS (...), CTE2 AS (...)`         |  

Las CTE son ideales para consultas complejas pero anidadas, mientras que las tablas temporales son mejores para datos reutilizables. 

### **4. Variables en SQL**  

Las variables en SQL permiten almacenar valores temporales durante la ejecución de consultas, procedimientos almacenados o scripts. Se clasifican en **escalares** (un solo valor) y **tipo tabla** (conjuntos de datos).  

---

## **4.1 Variables Escalares**  
Almacenan un único valor de un tipo de dato específico.  

### **Sintaxis Básica**  
```sql
DECLARE @NombreVariable TipoDato [ = ValorInicial ];
SET @NombreVariable = Valor;  -- Asignación explícita
-- o
SELECT @NombreVariable = Valor FROM Tabla;  -- Asignación desde consulta
```

### **Ejemplos**  

#### **Ejemplo 1: Asignación Directa**  
```sql
DECLARE @PrecioMaximo DECIMAL(10,2) = 1000.00;
DECLARE @Descuento INT = 15;

-- Calcular precio con descuento
SET @PrecioMaximo = @PrecioMaximo * (1 - @Descuento / 100.0);
PRINT 'Precio con descuento: ' + CAST(@PrecioMaximo AS VARCHAR);
```
**Salida:**  
```
Precio con descuento: 850.00
```

#### **Ejemplo 2: Asignación desde Consulta**  
```sql
DECLARE @TotalClientes INT;

SELECT @TotalClientes = COUNT(*) 
FROM Clientes 
WHERE Activo = 1;

PRINT 'Clientes activos: ' + CAST(@TotalClientes AS VARCHAR);
```

#### **Ejemplo 3: Uso en Condiciones**  
```sql
DECLARE @PromedioVentas DECIMAL(10,2);

SELECT @PromedioVentas = AVG(Total) 
FROM Ventas;

IF @PromedioVentas > 5000
    PRINT 'Rendimiento alto';
ELSE
    PRINT 'Rendimiento bajo';
```

---

## **4.2 Variables Tipo Tabla**  
Almacenan conjuntos de datos estructurados como una tabla temporal.  

### **Sintaxis Básica**  
```sql
DECLARE @NombreTabla TABLE (
    Columna1 TipoDato1 [PRIMARY KEY],
    Columna2 TipoDato2,
    ...
);
```

### **Ejemplos**  

#### **Ejemplo 1: Almacenar Resultados de Consulta**  
```sql
DECLARE @ClientesVIP TABLE (
    ClienteID INT,
    Nombre VARCHAR(100),
    TotalCompras DECIMAL(10,2)
);

INSERT INTO @ClientesVIP
SELECT 
    c.ClienteID, 
    c.Nombre, 
    SUM(v.Total) AS TotalCompras
FROM 
    Clientes c
    JOIN Ventas v ON c.ClienteID = v.ClienteID
GROUP BY 
    c.ClienteID, c.Nombre
HAVING 
    SUM(v.Total) > 10000;

-- Consultar la variable
SELECT * FROM @ClientesVIP;
```

#### **Ejemplo 2: Filtrar Datos**  
```sql
DECLARE @ProductosAgotados TABLE (
    ProductoID INT,
    Nombre VARCHAR(100)
);

INSERT INTO @ProductosAgotados
SELECT 
    ProductoID, 
    Nombre 
FROM 
    Productos 
WHERE 
    Stock = 0;

-- Actualizar productos agotados
UPDATE Productos
SET Estado = 'Agotado'
WHERE ProductoID IN (SELECT ProductoID FROM @ProductosAgotados);
```

---

## **4.3 Alcance (Scope) de Variables**  
- **Variables escalares y tipo tabla:**  
  - Solo existen en el **batch** donde se declaran.  
  - Se pierden después de ejecutar `GO` (en SQL Server) o al finalizar el script.  

### **Ejemplo de Scope**  
```sql
-- Batch 1
DECLARE @Contador INT = 0;
SET @Contador = 10;
PRINT 'Batch 1: ' + CAST(@Contador AS VARCHAR);  -- Output: 10
GO

-- Batch 2
-- Error: @Contador no existe aquí
PRINT 'Batch 2: ' + CAST(@Contador AS VARCHAR);  -- Error
```

### **Solución para Persistencia**  
Usar **tablas temporales** (`#Temp`) si necesitas datos entre batches:  
```sql
CREATE TABLE #TempContador (Valor INT);
INSERT INTO #TempContador VALUES (10);
GO

-- Batch 2
SELECT * FROM #TempContador;  -- Funciona
```

---

## **4.4 Comparación entre Tipos de Variables**  

| **Característica**       | **Variables Escalares**            | **Variables Tipo Tabla**          |  
|--------------------------|-----------------------------------|-----------------------------------|  
| **Almacenamiento**       | Un único valor                    | Múltiples filas y columnas        |  
| **Uso típico**           | Contadores, cálculos simples      | Almacenar resultados intermedios  |  
| **Persistencia**         | Solo en el batch actual           | Solo en el batch actual           |  
| **Índices**              | No aplica                        | No soportados                     |  

---

## **4.5 Buenas Prácticas**  
1. **Nombres descriptivos:**  
   ```sql
   DECLARE @FechaInicio DATE;  -- Mejor que @F1
   ```  
2. **Inicialización:**  
   ```sql
   DECLARE @Total INT = 0;  -- Evitar valores NULL
   ```  
3. **Tipo de dato adecuado:**  
   ```sql
   DECLARE @Precio DECIMAL(10,2);  -- Para valores monetarios
   ```  

---

### **Resumen de Comandos**  
| **Propósito**               | **Sintaxis**                                  |  
|----------------------------|----------------------------------------------|  
| Declarar variable escalar  | `DECLARE @Variable TipoDato [= Valor];`      |  
| Declarar variable tabla    | `DECLARE @Tabla TABLE (Columna TipoDato);`   |  
| Asignar valor              | `SET @Variable = Valor;` o `SELECT @Variable = Columna FROM Tabla;` |  

Las variables son esenciales para dinamizar consultas y procedimientos. 

### **5. Estructuras de Control en SQL**  

Las estructuras de control permiten manejar el flujo de ejecución en scripts SQL, procedimientos almacenados y bloques de código. Incluyen condicionales (`IF-ELSE`) y bucles (`WHILE`), que son fundamentales para implementar lógica compleja en bases de datos.  

---

## **5.1 Condicionales (`IF-ELSE`)**  
Evalúan una condición y ejecutan bloques de código según el resultado (`TRUE`/`FALSE`).  

### **Sintaxis Básica**  
```sql
IF condición
BEGIN
    -- Código si la condición es TRUE
END
ELSE
BEGIN
    -- Código si la condición es FALSE
END
```

### **Ejemplos Prácticos**  

#### **Ejemplo 1: Validación Simple**  
```sql
DECLARE @Edad INT = 25;

IF @Edad >= 18
BEGIN
    PRINT 'Mayor de edad';
END
ELSE
BEGIN
    PRINT 'Menor de edad';
END
```
**Salida:**  
```
Mayor de edad
```

#### **Ejemplo 2: Con Consulta a Tabla**  
```sql
DECLARE @PromedioVentas DECIMAL(10,2);

SELECT @PromedioVentas = AVG(Total) 
FROM Ventas;

IF @PromedioVentas > 5000
BEGIN
    PRINT 'Rendimiento alto: ' + CAST(@PromedioVentas AS VARCHAR);
    -- Insertar en tabla de log
    INSERT INTO LogRendimiento (Mensaje, Fecha)
    VALUES ('Rendimiento alto', GETDATE());
END
ELSE
BEGIN
    PRINT 'Rendimiento bajo: ' + CAST(@PromedioVentas AS VARCHAR);
END
```

#### **Ejemplo 3: Anidado (`IF` dentro de `IF`)**  
```sql
DECLARE @Stock INT = 10;
DECLARE @UmbralCritico INT = 5;

IF @Stock <= @UmbralCritico
BEGIN
    PRINT 'Stock CRÍTICO!';
    -- Enviar alerta
    EXEC sp_enviar_alerta 'Stock bajo en producto ID:123';
END
ELSE IF @Stock <= 20
BEGIN
    PRINT 'Stock bajo, reordenar pronto';
END
ELSE
BEGIN
    PRINT 'Stock suficiente';
END
```

---

## **5.2 Bucles (`WHILE`)**  
Ejecutan un bloque de código **mientras** se cumpla una condición.  

### **Sintaxis Básica**  
```sql
WHILE condición
BEGIN
    -- Código a repetir
    -- Importante: Modificar la condición para evitar loops infinitos!
END
```

### **Ejemplos Prácticos**  

#### **Ejemplo 1: Contador Básico**  
```sql
DECLARE @Contador INT = 1;

WHILE @Contador <= 5
BEGIN
    PRINT 'Iteración: ' + CAST(@Contador AS VARCHAR);
    SET @Contador = @Contador + 1;
END
```
**Salida:**  
```
Iteración: 1  
Iteración: 2  
Iteración: 3  
Iteración: 4  
Iteración: 5
```

#### **Ejemplo 2: Procesamiento por Lotes**  
```sql
DECLARE @Lote INT = 1;
DECLARE @TotalRegistros INT;

SELECT @TotalRegistros = COUNT(*) FROM Productos;

WHILE @Lote <= @TotalRegistros
BEGIN
    -- Actualizar 100 registros por lote
    UPDATE TOP (100) Productos
    SET Precio = Precio * 1.05
    WHERE ProductoID BETWEEN @Lote AND @Lote + 99;

    PRINT 'Actualizados registros: ' + CAST(@Lote AS VARCHAR) + ' a ' + CAST(@Lote + 99 AS VARCHAR);
    SET @Lote = @Lote + 100;
END
```

#### **Ejemplo 3: Con `BREAK` y `CONTINUE`**  
```sql
DECLARE @Numero INT = 1;

WHILE @Numero <= 10
BEGIN
    IF @Numero = 5
    BEGIN
        PRINT 'Saltando el 5';
        SET @Numero = @Numero + 1;
        CONTINUE;  -- Salta a la siguiente iteración
    END

    IF @Numero = 8
    BEGIN
        PRINT 'Bucle detenido en 8';
        BREAK;  -- Termina el bucle
    END

    PRINT 'Número: ' + CAST(@Numero AS VARCHAR);
    SET @Numero = @Numero + 1;
END
```
**Salida:**  
```
Número: 1  
Número: 2  
Número: 3  
Número: 4  
Saltando el 5  
Número: 6  
Número: 7  
Bucle detenido en 8
```

---

## **5.3 Buenas Prácticas y Casos de Uso**  

### **Buenas Prácticas**  
1. **Evitar bucles infinitos:**  
   - Asegurarse de que la condición del `WHILE` eventualmente sea `FALSE`.  
   ```sql
   -- Peligroso (sin incremento)
   DECLARE @i INT = 1;
   WHILE @i <= 10
   BEGIN
       PRINT @i;
       -- Falta: SET @i = @i + 1;
   END
   ```

2. **Usar `BEGIN/END` para bloques múltiples:**  
   ```sql
   -- Correcto
   IF @Condicion
   BEGIN
       PRINT 'Mensaje 1';
       PRINT 'Mensaje 2';
   END
   ```

3. **Optimizar con operaciones basadas en conjuntos:**  
   - En SQL, los bucles son menos eficientes que operaciones masivas (`UPDATE`, `INSERT SELECT`).  

### **Casos de Uso Típicos**  
- **Validación de datos antes de operaciones:**  
  ```sql
  IF EXISTS (SELECT 1 FROM Clientes WHERE Email = 'cliente@example.com')
  BEGIN
      PRINT 'El cliente ya existe';
  END
  ```

- **Procesamiento por lotes en tablas grandes:**  
  ```sql
  WHILE @Offset < @TotalRegistros
  BEGIN
      -- Procesar 1000 registros por iteración
      SELECT * FROM Productos
      ORDER BY ProductoID
      OFFSET @Offset ROWS
      FETCH NEXT 1000 ROWS ONLY;
      
      SET @Offset = @Offset + 1000;
  END
  ```

- **Generación de datos de prueba:**  
  ```sql
  DECLARE @i INT = 1;
  WHILE @i <= 100
  BEGIN
      INSERT INTO Pruebas (Valor) VALUES ('Test ' + CAST(@i AS VARCHAR));
      SET @i = @i + 1;
  END
  ```

---

### **Resumen de Comandos**  
| **Estructura**       | **Sintaxis**                                  | **Uso Principal**                |  
|----------------------|----------------------------------------------|----------------------------------|  
| **IF-ELSE**         | `IF cond BEGIN... END ELSE BEGIN... END`     | Validaciones y bifurcaciones     |  
| **WHILE**          | `WHILE cond BEGIN... END`                   | Bucles con condición             |  
| **BREAK**          | `BREAK;`                                    | Salir del bucle inmediatamente   |  
| **CONTINUE**       | `CONTINUE;`                                 | Saltar a la siguiente iteración  |  

--- 

### **6. Funciones en SQL**  

Las funciones en SQL permiten encapsular lógica reusable para cálculos, transformaciones de datos y operaciones complejas. Se definen una vez y se pueden llamar múltiples veces en consultas, procedimientos o triggers.  

---

## **6.1 Sintaxis General**  
```sql
CREATE FUNCTION nombre_funcion ([parámetros])
RETURNS tipo_retorno
AS
BEGIN
    -- Lógica de la función
    RETURN valor;
END;
```

**Partes Clave:**  
- **Parámetros:** Pueden ser de entrada (`IN`), salida (`OUT`), o ambos.  
- **RETURNS:** Define el tipo de dato que devuelve (ej: `INT`, `VARCHAR`, `TABLE`).  
- **Cuerpo:** Contiene la lógica, con `RETURN` obligatorio en funciones escalares.  

---

## **6.2 Variaciones entre Motores de Bases de Datos**  

### **A. PostgreSQL**  
**Características:**  
- Soporta funciones en múltiples lenguajes (`plpgsql`, `Python`, etc.).  
- Permite sobrecargar funciones (mismo nombre, distintos parámetros).  

**Sintaxis:**  
```sql
CREATE OR REPLACE FUNCTION nombre_funcion(param1 tipo, param2 tipo)
RETURNS tipo_retorno AS $$
BEGIN
    -- Lógica
    RETURN valor;
END;
$$ LANGUAGE plpgsql;
```

**Ejemplo: Calcular IVA**  
```sql
CREATE OR REPLACE FUNCTION calcular_iva(precio NUMERIC, iva NUMERIC DEFAULT 21)
RETURNS NUMERIC AS $$
BEGIN
    RETURN precio * (iva / 100);
END;
$$ LANGUAGE plpgsql;

-- Llamada:
SELECT nombre, precio, calcular_iva(precio) AS iva FROM productos;
```

---

### **B. SQL Server**  
**Características:**  
- Requiere esquema (ej: `dbo.`).  
- Diferencias entre funciones escalares y en tabla.  

**Sintaxis:**  
```sql
CREATE FUNCTION dbo.nombre_funcion (@param1 tipo, @param2 tipo)
RETURNS tipo_retorno
AS
BEGIN
    DECLARE @resultado tipo_retorno;
    -- Lógica
    RETURN @resultado;
END;
```

**Ejemplo: Clasificar Clientes por Compra**  
```sql
CREATE FUNCTION dbo.clasificar_cliente(@total_compras DECIMAL(10,2))
RETURNS VARCHAR(20)
AS
BEGIN
    DECLARE @categoria VARCHAR(20);
    SET @categoria = CASE 
        WHEN @total_compras > 10000 THEN 'Premium'
        WHEN @total_compras > 5000 THEN 'Gold'
        ELSE 'Standard'
    END;
    RETURN @categoria;
END;

-- Llamada:
SELECT nombre, dbo.clasificar_cliente(SUM(total)) AS categoria FROM ventas GROUP BY nombre;
```

---

### **C. MySQL / MariaDB**  
**Características:**  
- Requiere cambiar delimitadores con `DELIMITER //`.  
- Opción `DETERMINISTIC` para funciones que siempre devuelven lo mismo con mismos inputs.  

**Sintaxis:**  
```sql
DELIMITER //
CREATE FUNCTION nombre_funcion(param1 tipo, param2 tipo)
RETURNS tipo_retorno
DETERMINISTIC
BEGIN
    DECLARE resultado tipo_retorno;
    -- Lógica
    RETURN resultado;
END //
DELIMITER ;
```

**Ejemplo: Formatear Fecha**  
```sql
DELIMITER //
CREATE FUNCTION formatear_fecha(fecha DATE)
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
    RETURN DATE_FORMAT(fecha, '%d/%m/%Y');
END //
DELIMITER ;

-- Llamada:
SELECT formatear_fecha(fecha_registro) AS fecha_legible FROM usuarios;
```

---

## **6.3 Tipos de Funciones**  

### **1. Funciones Escalares**  
Devuelven un único valor.  
**Ejemplo en SQL Server:**  
```sql
CREATE FUNCTION dbo.sumar(@a INT, @b INT)
RETURNS INT
AS
BEGIN
    RETURN @a + @b;
END;
```

### **2. Funciones en Tabla (RETURNS TABLE)**  
Devuelven un conjunto de filas.  
**Ejemplo en PostgreSQL:**  
```sql
CREATE OR REPLACE FUNCTION obtener_clientes_activos()
RETURNS TABLE (id INT, nombre VARCHAR) AS $$
BEGIN
    RETURN QUERY SELECT cliente_id, nombre FROM clientes WHERE activo = true;
END;
$$ LANGUAGE plpgsql;

-- Llamada:
SELECT * FROM obtener_clientes_activos();
```

### **3. Funciones con Parámetros de Tabla**  
**Ejemplo en SQL Server:**  
```sql
CREATE FUNCTION dbo.filtrar_productos(@precio_max DECIMAL)
RETURNS @resultado TABLE (id INT, nombre VARCHAR(100), precio DECIMAL)
AS
BEGIN
    INSERT INTO @resultado
    SELECT producto_id, nombre, precio FROM productos WHERE precio <= @precio_max;
    RETURN;
END;
```

---

## **6.4 Usos Recomendados**  

### **Cuándo Usar Funciones**  
✔ **Cálculos repetitivos:**  
   ```sql
   SELECT nombre, calcular_descuento(precio, 10) AS precio_final FROM productos;
   ```  
✔ **Validación de datos:**  
   ```sql
   CREATE FUNCTION es_email_valido(@email VARCHAR(100)) RETURNS BIT AS ...;
   ```  
✔ **Simplificar consultas complejas:**  
   ```sql
   SELECT * FROM dbo.obtener_ventas_por_region('Norte');
   ```  

### **Cuándo Evitarlas**  
✖ **En consultas que procesan millones de filas** (pueden ser lentas).  
✖ **Para operaciones que modifican datos** (usar procedimientos almacenados).  

---

## **6.5 Ejemplo Integrado (PostgreSQL)**  
**Función: Top N Productos por Categoría**  
```sql
CREATE OR REPLACE FUNCTION top_productos_por_categoria(categoria_id INT, limite INT)
RETURNS TABLE (id INT, nombre VARCHAR, ventas NUMERIC) AS $$
BEGIN
    RETURN QUERY
    SELECT p.producto_id, p.nombre, SUM(v.cantidad * v.precio) AS ventas
    FROM productos p
    JOIN ventas v ON p.producto_id = v.producto_id
    WHERE p.categoria_id = top_productos_por_categoria.categoria_id
    GROUP BY p.producto_id, p.nombre
    ORDER BY ventas DESC
    LIMIT top_productos_por_categoria.limite;
END;
$$ LANGUAGE plpgsql;

-- Llamada:
SELECT * FROM top_productos_por_categoria(1, 5);  -- Top 5 de categoría 1
```

---

### **Resumen por Motor**  
| **Operación**           | **PostgreSQL**            | **SQL Server**           | **MySQL**               |  
|-------------------------|---------------------------|--------------------------|-------------------------|  
| **Crear función**       | `CREATE OR REPLACE FUNCTION` | `CREATE FUNCTION dbo.`   | `DELIMITER // CREATE FUNCTION` |  
| **Lenguaje**            | `LANGUAGE plpgsql`        | No requiere              | `DETERMINISTIC` opcional |  
| **Devolver tabla**      | `RETURNS TABLE`           | `RETURNS @tabla TABLE`   | No soportado            |  

--- 

### **7. Procedimientos Almacenados**  

Los procedimientos almacenados (**stored procedures**) son bloques de código SQL precompilados que se ejecutan en el servidor de bases de datos. Permiten encapsular lógica compleja, mejorar el rendimiento y centralizar reglas de negocio.  

---

## **7.1 Definición y Sintaxis**  

### **Sintaxis General**  
```sql
CREATE PROCEDURE nombre_procedimiento (
    [@parámetro1 tipo [= valor_predeterminado], ...]
)
AS
BEGIN
    -- Código SQL (INSERT, UPDATE, DELETE, SELECT, etc.)
    -- Puede incluir transacciones, manejo de errores, etc.
END;
```

### **Ejemplo Básico (SQL Server)**  
```sql
CREATE PROCEDURE dbo.actualizar_precios
    @porcentaje DECIMAL(5,2),
    @categoria VARCHAR(50)
AS
BEGIN
    UPDATE Productos
    SET Precio = Precio * (1 + @porcentaje / 100)
    WHERE Categoria = @categoria;
    
    PRINT 'Precios actualizados para la categoría: ' + @categoria;
END;
```

**Llamada:**  
```sql
EXEC dbo.actualizar_precios @porcentaje = 10, @categoria = 'Electrónicos';
```

---

## **7.2 Diferencias con Funciones**  

| **Característica**       | **Procedimientos Almacenados**      | **Funciones**                      |  
|--------------------------|------------------------------------|------------------------------------|  
| **Retorno**              | No devuelven valor (solo parámetros `OUT`) | Devuelven un valor o tabla.       |  
| **Uso en consultas**     | No se pueden usar en `SELECT`      | Sí (`SELECT dbo.funcion()`).      |  
| **Modificación de datos**| Permiten DML (INSERT, UPDATE, etc.)| Solo consultas (en la mayoría de DBMS). |  
| **Transacciones**        | Soporte completo (`BEGIN TRAN`)    | No soportadas.                     |  

---

## **7.3 Usos Principales**  

### **1. Operaciones Complejas**  
**Ejemplo:** Procesar pedidos con validaciones y transacciones.  
```sql
CREATE PROCEDURE dbo.procesar_pedido
    @cliente_id INT,
    @producto_id INT,
    @cantidad INT
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION;
        
        -- Validar stock
        DECLARE @stock INT;
        SELECT @stock = Stock FROM Productos WHERE ProductoID = @producto_id;
        
        IF @stock < @cantidad
            RAISERROR('Stock insuficiente', 16, 1);
        
        -- Registrar pedido
        INSERT INTO Pedidos (ClienteID, ProductoID, Cantidad, Fecha)
        VALUES (@cliente_id, @producto_id, @cantidad, GETDATE());
        
        -- Actualizar stock
        UPDATE Productos SET Stock = Stock - @cantidad 
        WHERE ProductoID = @producto_id;
        
        COMMIT TRANSACTION;
        PRINT 'Pedido procesado correctamente';
    END TRY
    BEGIN CATCH
        ROLLBACK TRANSACTION;
        PRINT 'Error: ' + ERROR_MESSAGE();
    END CATCH
END;
```

### **2. Seguridad y Mantenimiento**  
- **Ventaja:** Los usuarios pueden ejecutar procedimientos sin acceso directo a las tablas.  
```sql
-- Otorgar permisos sin exponer tablas:
GRANT EXECUTE ON dbo.procesar_pedido TO usuario_ventas;
```

---

## **7.4 Ejemplos por Motor de Base de Datos**  

### **A. PostgreSQL**  
```sql
CREATE OR REPLACE PROCEDURE insertar_usuario(
    p_nombre VARCHAR(100),
    p_email VARCHAR(100)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO Usuarios (Nombre, Email) VALUES (p_nombre, p_email);
    RAISE NOTICE 'Usuario % insertado', p_nombre;
END;
$$;

-- Llamada:
CALL insertar_usuario('Juan Pérez', 'juan@example.com');
```

### **B. SQL Server**  
```sql
CREATE PROCEDURE dbo.buscar_clientes
    @filtro_nombre VARCHAR(100) = NULL,
    @filtro_pais VARCHAR(50) = NULL
AS
BEGIN
    SELECT * FROM Clientes
    WHERE 
        (Nombre LIKE '%' + @filtro_nombre + '%' OR @filtro_nombre IS NULL)
        AND (Pais = @filtro_pais OR @filtro_pais IS NULL);
END;

-- Llamada con parámetros opcionales:
EXEC dbo.buscar_clientes @filtro_pais = 'México';
```

### **C. MySQL**  
```sql
DELIMITER //
CREATE PROCEDURE calcular_estadisticas_ventas(IN anio INT)
BEGIN
    SELECT 
        COUNT(*) AS TotalVentas,
        SUM(Monto) AS IngresosTotales
    FROM Ventas
    WHERE YEAR(Fecha) = anio;
END //
DELIMITER ;

-- Llamada:
CALL calcular_estadisticas_ventas(2023);
```

---

## **7.5 Cuándo Usarlos y Cuándo Evitarlos**  

### **✅ Cuándo Usarlos**  
1. **Lógica de negocio compleja** (ej: validaciones multicapa).  
2. **Procesos batch** (ej: generación de reportes mensuales).  
3. **Seguridad** (evitar acceso directo a tablas).  
4. **Rendimiento en operaciones repetitivas** (plan de ejecución cacheado).  

### **❌ Cuándo Evitarlos**  
1. **Consultas simples** (ej: `SELECT * FROM Clientes`).  
2. **Operaciones únicas o ad-hoc** (mejor usar queries directos).  
3. **Entornos con cambios frecuentes** (el código SP es más difícil de versionar que el código de aplicación).  

---

### **Resumen de Comandos Clave**  
| **Acción**               | **SQL Server**           | **PostgreSQL**       | **MySQL**            |  
|--------------------------|--------------------------|----------------------|----------------------|  
| **Crear procedimiento**  | `CREATE PROCEDURE dbo.`  | `CREATE PROCEDURE`   | `DELIMITER // CREATE PROCEDURE` |  
| **Llamar**               | `EXEC dbo.proc`          | `CALL proc()`        | `CALL proc()`        |  
| **Parámetros opcionales**| `@param tipo = default`  | `param tipo DEFAULT` | `IN param tipo`      |  

--- 

**Conclusión:**  
Los procedimientos almacenados son ideales para centralizar lógica crítica, mejorar seguridad y optimizar operaciones repetitivas. Sin embargo, en entornos ágiles o con consultas simples, pueden añadir complejidad innecesaria.  

### **8. Triggers (Disparadores) en SQL**

Los triggers (disparadores) son procedimientos automáticos que se ejecutan en respuesta a eventos específicos (INSERT, UPDATE, DELETE) en una tabla. Se utilizan para mantener la integridad de los datos, auditoría y automatización de procesos.

---

## **8.1 Definición y Sintaxis Básica**

### **Sintaxis General**
```sql
CREATE TRIGGER nombre_trigger
{BEFORE | AFTER | INSTEAD OF} {INSERT | UPDATE | DELETE}
ON nombre_tabla
[FOR EACH ROW | FOR EACH STATEMENT]
BEGIN
    -- Código a ejecutar
END;
```

**Partes Clave:**
- **BEFORE/AFTER:** Ejecuta el trigger antes o después del evento.
- **INSTEAD OF:** Reemplaza la operación original (útil en vistas).
- **FOR EACH ROW:** Actúa por cada fila afectada.
- **FOR EACH STATEMENT:** Actúa una vez por sentencia (default en SQL Server).

---

## **8.2 Tipos de Triggers**

### **A. Triggers BEFORE**
Se ejecutan **antes** de la operación. Ideales para validaciones.

**Ejemplo (MySQL): Validar stock antes de una venta**
```sql
DELIMITER //
CREATE TRIGGER before_venta_insert
BEFORE INSERT ON Ventas
FOR EACH ROW
BEGIN
    DECLARE stock_actual INT;
    SELECT Stock INTO stock_actual FROM Productos WHERE ProductoID = NEW.ProductoID;
    
    IF stock_actual < NEW.Cantidad THEN
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Error: Stock insuficiente';
    END IF;
END //
DELIMITER ;
```

### **B. Triggers AFTER**
Se ejecutan **después** de la operación. Usados para auditoría.

**Ejemplo (SQL Server): Registrar cambios en una tabla de log**
```sql
CREATE TRIGGER after_empleado_update
ON Empleados
AFTER UPDATE
AS
BEGIN
    INSERT INTO Auditoria (Tabla, Accion, ID_Registro, Fecha)
    SELECT 'Empleados', 'UPDATE', deleted.EmpleadoID, GETDATE()
    FROM deleted; -- Tabla especial que almacena los valores antiguos
END;
```

### **C. Triggers INSTEAD OF**
Reemplazan la operación original. Comunes en vistas.

**Ejemplo (PostgreSQL): Insertar en una vista compleja**
```sql
CREATE TRIGGER instead_of_insert_view
INSTEAD OF INSERT ON VistaClientes
FOR EACH ROW
EXECUTE FUNCTION insertar_en_tablas_reales(); -- Llama a una función
```

---

## **8.3 Diferencias entre Motores SQL**

| **Característica**       | **SQL Server**               | **MySQL**                     | **PostgreSQL**              |
|--------------------------|------------------------------|-------------------------------|-----------------------------|
| **Soporte INSTEAD OF**   | Sí (para vistas)             | No                            | Sí                          |
| **Tablas especiales**    | `inserted`, `deleted`        | `NEW`, `OLD`                  | `NEW`, `OLD`                |
| **Lenguaje**             | T-SQL                        | SQL estándar                  | PL/pgSQL                    |
| **Ejecución por defecto**| Por sentencia (`STATEMENT`)  | Por fila (`ROW`)              | Por fila (`ROW`)            |

---

## **8.4 Ejemplos Prácticos**

### **A. Registro de Auditoría (SQL Server)**
```sql
CREATE TRIGGER tr_auditoria_clientes
ON Clientes
AFTER INSERT, UPDATE, DELETE
AS
BEGIN
    DECLARE @accion CHAR(6);
    SET @accion = CASE
        WHEN EXISTS (SELECT * FROM inserted) AND EXISTS (SELECT * FROM deleted) THEN 'UPDATE'
        WHEN EXISTS (SELECT * FROM inserted) THEN 'INSERT'
        ELSE 'DELETE'
    END;
    
    INSERT INTO Log_Auditoria (Tabla, Accion, Usuario, Fecha)
    VALUES ('Clientes', @accion, SYSTEM_USER, GETDATE());
END;
```

### **B. Validación de Cambios (MySQL)**
```sql
DELIMITER //
CREATE TRIGGER before_empleado_salario
BEFORE UPDATE ON Empleados
FOR EACH ROW
BEGIN
    IF NEW.Salario < OLD.Salario THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Error: El salario no puede disminuir';
    END IF;
END //
DELIMITER ;
```

### **C. Trigger en Columna Específica (PostgreSQL)**
```sql
CREATE TRIGGER after_email_update
AFTER UPDATE OF Email ON Usuarios
FOR EACH ROW
EXECUTE FUNCTION registrar_cambio_email();
```

**Función asociada:**
```sql
CREATE OR REPLACE FUNCTION registrar_cambio_email()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO Log_Cambios_Email (UsuarioID, Email_Anterior, Email_Nuevo, Fecha)
    VALUES (OLD.UsuarioID, OLD.Email, NEW.Email, NOW());
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

---

## **8.5 Triggers en Tablas vs. Columnas Específicas**

| **Enfoque**             | **Ejemplo**                                  | **Uso Típico**                |
|-------------------------|---------------------------------------------|-------------------------------|
| **Tabla completa**      | `AFTER UPDATE ON Productos`                 | Auditoría general             |
| **Columna específica**  | `AFTER UPDATE OF Precio ON Productos`       | Validación de campos críticos |

**Ejemplo para columna (SQL Server):**
```sql
CREATE TRIGGER tr_precio_update
ON Productos
AFTER UPDATE
AS
IF UPDATE(Precio) -- Solo se activa si cambia la columna Precio
BEGIN
    INSERT INTO Precio_Historial (ProductoID, Precio_Anterior, Precio_Nuevo)
    SELECT d.ProductoID, d.Precio, i.Precio
    FROM deleted d
    JOIN inserted i ON d.ProductoID = i.ProductoID;
END;
```

---

### **Resumen de Comandos Clave**
| **Acción**               | **SQL Server**            | **MySQL/PostgreSQL**        |
|--------------------------|---------------------------|-----------------------------|
| **Crear trigger**        | `CREATE TRIGGER`          | `CREATE TRIGGER`            |
| **Valores antiguos**     | `deleted`                 | `OLD`                       |
| **Valores nuevos**       | `inserted`                | `NEW`                       |
| **Validación**           | `IF UPDATE(columna)`      | `IF NEW.columna <> OLD.columna` |

**Conclusión:**  
Los triggers son herramientas poderosas para garantizar integridad de datos y automatizar procesos, pero deben usarse con cuidado para no afectar el rendimiento. 

### **9. Subconsultas y Palabras Reservadas en SQL**

Las subconsultas y operadores especiales permiten crear consultas más dinámicas y potentes. Aquí te muestro cómo dominarlas con ejemplos prácticos y explicaciones claras.

---

## **9.1 Operadores Clave**

### **A. EXISTS vs NOT EXISTS**
Verifican si una subconsulta devuelve algún resultado.

#### **EXISTS (¿Existe?)**
```sql
SELECT nombre
FROM Productos p
WHERE EXISTS (
    SELECT 1 
    FROM Ventas v 
    WHERE v.producto_id = p.id
);
```
**Explicación:**  
- Devuelve productos **que tienen al menos una venta**.  
- `SELECT 1` es una optimización (no importa qué columna se seleccione).  

#### **NOT EXISTS (¿No existe?)**
```sql
SELECT nombre
FROM Productos p
WHERE NOT EXISTS (
    SELECT 1 
    FROM Ventas v 
    WHERE v.producto_id = p.id
);
```
**Explicación:**  
- Devuelve productos **que no tienen ninguna venta**.  

---

### **B. IN vs NOT IN**
Comparan un valor con una lista de resultados.

#### **IN (¿Está en la lista?)**
```sql
SELECT nombre
FROM Empleados
WHERE departamento_id IN (
    SELECT id 
    FROM Departamentos 
    WHERE ubicacion = 'Nueva York'
);
```
**Explicación:**  
- Devuelve empleados en departamentos de Nueva York.  

#### **NOT IN (¿No está en la lista?)**
```sql
SELECT nombre
FROM Clientes
WHERE id NOT IN (
    SELECT cliente_id 
    FROM Pedidos
);
```
**⚠️ Precaución:**  
- Si la subconsulta devuelve `NULL`, `NOT IN` **falla silenciosamente**.  
- Alternativa segura: Usar `NOT EXISTS`.  

---

### **C. ALL vs ANY/SOME**
Comparan un valor con **todos** o **algunos** resultados de una subconsulta.

#### **ALL (¿Cumple con todos?)**
```sql
SELECT nombre
FROM Productos
WHERE precio > ALL (
    SELECT precio 
    FROM Productos 
    WHERE categoria = 'Económico'
);
```
**Explicación:**  
- Productos más caros que **todos** los económicos.  

#### **ANY/SOME (¿Cumple con alguno?)**
```sql
SELECT nombre
FROM Empleados
WHERE salario > ANY (
    SELECT salario 
    FROM Empleados 
    WHERE departamento = 'Ventas'
);
```
**Explicación:**  
- Empleados que ganan más que **al menos uno** en Ventas.  

---

## **9.2 Ejemplos Prácticos Avanzados**

### **Ejemplo 1: EXISTS con JOIN implícito**
```sql
-- Clientes con pedidos en 2023
SELECT c.nombre
FROM Clientes c
WHERE EXISTS (
    SELECT 1
    FROM Pedidos p
    WHERE p.cliente_id = c.id
    AND YEAR(p.fecha) = 2023
);
```

### **Ejemplo 2: IN con múltiples columnas**
```sql
-- Productos vendidos en combinación específica
SELECT nombre
FROM Productos
WHERE (id, categoria) IN (
    SELECT producto_id, categoria
    FROM Ventas
    WHERE cantidad > 10
);
```

### **Ejemplo 3: ALL para comparación agregada**
```sql
-- Empleados que superan el promedio de su departamento
SELECT e.nombre
FROM Empleados e
WHERE e.salario > ALL (
    SELECT AVG(salario)
    FROM Empleados
    WHERE departamento = e.departamento
);
```

---

## **9.3 Precauciones Clave**

1. **Rendimiento de NOT IN:**  
   ```sql
   -- ❌ Riesgoso
   SELECT * FROM tabla1 WHERE columna NOT IN (SELECT columna FROM tabla2);
   
   -- ✅ Mejor alternativa
   SELECT * FROM tabla1 t1 
   WHERE NOT EXISTS (SELECT 1 FROM tabla2 t2 WHERE t2.columna = t1.columna);
   ```

2. **NULL en subconsultas:**  
   - `IN` y `NOT IN` pueden dar resultados inesperados si hay `NULL`s.  
   - `EXISTS/NOT EXISTS` son inmunes a este problema.

3. **Optimización:**  
   - Las subconsultas en el `WHERE` pueden ser lentas con grandes volúmenes de datos.  
   - Alternativas: Usar `JOIN` o tablas temporales.

---

## **9.4 Resumen Visual**

| **Operador** | **Descripción**                  | **Ejemplo Típico**                     | **Alternativa Recomendada**       |
|--------------|----------------------------------|----------------------------------------|-----------------------------------|
| `EXISTS`     | Verifica existencia              | `WHERE EXISTS (SELECT 1 FROM ...)`     | -                                 |
| `NOT EXISTS` | Verifica no existencia           | `WHERE NOT EXISTS (...)`               | Reemplaza a `NOT IN` seguro       |
| `IN`         | Compara con lista                | `WHERE id IN (1, 2, 3)`                | `JOIN` para rendimiento           |
| `NOT IN`     | Exclusión de lista               | `WHERE id NOT IN (SELECT ...)`         | Usar `NOT EXISTS`                 |
| `ALL`        | Compara con todos los resultados | `WHERE precio > ALL (SELECT ...)`      | -                                 |
| `ANY/SOME`   | Compara con algún resultado      | `WHERE salario > ANY (SELECT ...)`     | `WHERE salario > (SELECT MIN...)` |

---

**Conclusión:**  
Estos operadores son esenciales para consultas complejas. Dominarlos te permitirá:  
✅ Escribir consultas más legibles.  
✅ Evitar errores comunes con `NULL`.  
✅ Optimizar el rendimiento.  

### **10. Transacciones en SQL Server**

Las transacciones son bloques de operaciones SQL que se ejecutan como una unidad indivisible. Garantizan la **integridad de los datos** mediante el principio **ACID** (Atomicidad, Consistencia, Aislamiento, Durabilidad).

---

## **10.1 Sintaxis Básica**
```sql
BEGIN TRANSACTION; -- Inicia la transacción
    -- Operaciones SQL (INSERT, UPDATE, DELETE)
    
    -- Confirmar cambios (éxito)
    COMMIT TRANSACTION;
    
    -- O revertir cambios (fallo)
    -- ROLLBACK TRANSACTION;
```

---

## **10.2 Usos Prácticos con Ejemplos**

### **A. Operaciones DML (INSERT/UPDATE/DELETE)**
**Escenario:** Transferencia bancaria entre cuentas (atomicidad).  
```sql
BEGIN TRANSACTION;
    -- Retirar de cuenta origen
    UPDATE Cuentas 
    SET Saldo = Saldo - 1000 
    WHERE CuentaID = 123;
    
    -- Depositar en cuenta destino
    UPDATE Cuentas 
    SET Saldo = Saldo + 1000 
    WHERE CuentaID = 456;
    
    -- Verificar saldo negativo (validación)
    IF EXISTS (SELECT 1 FROM Cuentas WHERE CuentaID = 123 AND Saldo < 0)
    BEGIN
        ROLLBACK TRANSACTION;
        PRINT 'Error: Saldo insuficiente';
    END
    ELSE
    BEGIN
        COMMIT TRANSACTION;
        PRINT 'Transferencia exitosa';
    END
```

---

### **B. Operaciones en Tablas Relacionadas**  
**Escenario:** Registrar un pedido y actualizar el stock.  
```sql
BEGIN TRANSACTION;
    -- Insertar pedido
    INSERT INTO Pedidos (ClienteID, Fecha, Total)
    VALUES (1, GETDATE(), 500);
    
    -- Obtener el ID del nuevo pedido
    DECLARE @PedidoID INT = SCOPE_IDENTITY();
    
    -- Insertar detalles del pedido
    INSERT INTO DetallesPedido (PedidoID, ProductoID, Cantidad)
    VALUES (@PedidoID, 101, 2);
    
    -- Actualizar stock
    UPDATE Productos 
    SET Stock = Stock - 2 
    WHERE ProductoID = 101;
    
    -- Validar stock negativo
    IF (SELECT Stock FROM Productos WHERE ProductoID = 101) < 0
    BEGIN
        ROLLBACK TRANSACTION;
        PRINT 'Error: Stock insuficiente';
    END
    ELSE
        COMMIT TRANSACTION;
```

---

### **C. Uso con Variables**  
**Escenario:** Ajuste de precios basado en condiciones.  
```sql
BEGIN TRANSACTION;
    DECLARE @Aumento DECIMAL(5,2) = 10; -- 10%
    DECLARE @ProductosAfectados INT = 0;
    
    -- Aplicar aumento
    UPDATE Productos 
    SET Precio = Precio * (1 + @Aumento/100) 
    WHERE Categoria = 'Electrónicos';
    
    -- Contar productos afectados
    SET @ProductosAfectados = @@ROWCOUNT;
    
    -- Validar impacto
    IF @ProductosAfectados = 0
    BEGIN
        ROLLBACK TRANSACTION;
        PRINT 'Error: No hay productos en la categoría';
    END
    ELSE
    BEGIN
        COMMIT TRANSACTION;
        PRINT CONCAT('Actualizados ', @ProductosAfectados, ' productos');
    END
```

---

### **D. Puntos de Guardado (SAVEPOINT)**  
Permiten revertir parcialmente una transacción.  

**Escenario:** Procesamiento por lotes con posible rollback parcial.  
```sql
BEGIN TRANSACTION;
    -- Lote 1
    UPDATE Productos SET Precio = Precio * 1.05 WHERE Categoria = 'Ropa';
    SAVE TRANSACTION Lote1; -- Punto de guardado
    
    -- Lote 2
    UPDATE Productos SET Precio = Precio * 1.10 WHERE Categoria = 'Electrónicos';
    
    -- Si falla el Lote 2, revertir solo ese lote
    IF @@ERROR <> 0
    BEGIN
        ROLLBACK TRANSACTION Lote1; -- Revierte solo el Lote 2
        PRINT 'Error en Lote 2. Lote 1 confirmado';
    END
    ELSE
        COMMIT TRANSACTION;
```

---

## **10.3 Buenas Prácticas**

1. **Manejo de Errores:**  
   Usar `TRY...CATCH` para mayor claridad:  
   ```sql
   BEGIN TRY
       BEGIN TRANSACTION;
           -- Operaciones
       COMMIT TRANSACTION;
   END TRY
   BEGIN CATCH
       ROLLBACK TRANSACTION;
       PRINT 'Error: ' + ERROR_MESSAGE();
   END CATCH
   ```

2. **Duración Corta:**  
   Evitar transacciones largas que bloqueen recursos.

3. **Niveles de Aislamiento:**  
   Configurar según necesidad:  
   ```sql
   SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
   ```

---

## **10.4 Resumen de Comandos**

| **Comando**              | **Descripción**                                  | **Ejemplo**                          |
|--------------------------|------------------------------------------------|--------------------------------------|
| `BEGIN TRANSACTION`      | Inicia la transacción.                         | `BEGIN TRANSACTION;`                |
| `COMMIT TRANSACTION`     | Confirma todos los cambios.                    | `COMMIT;`                           |
| `ROLLBACK TRANSACTION`   | Revierte todos los cambios.                    | `ROLLBACK;`                         |
| `SAVE TRANSACTION`       | Establece un punto de guardado.                | `SAVE TRANSACTION Punto1;`          |
| `@@ERROR`               | Verifica errores después de una operación.     | `IF @@ERROR <> 0 ROLLBACK;`         |

---

**Conclusión:**  
Las transacciones son esenciales para operaciones críticas. Combinadas con puntos de guardado y manejo de errores, garantizan la consistencia de los datos incluso en escenarios complejos.  

### **11. Manejo de Errores en SQL Server**  

El manejo de errores es fundamental para garantizar la robustez de tus scripts y procedimientos almacenados. SQL Server ofrece varias herramientas para capturar y gestionar errores de manera estructurada.

---

## **11.1 Variables de Sistema (`@@ERROR`)**  

### **Descripción**  
- `@@ERROR` devuelve el código del último error ocurrido en la sesión actual.  
- **Código 0**: Sin errores.  
- **Código ≠ 0**: Error detectado.  

### **Ejemplo Práctico**  
```sql
BEGIN TRANSACTION;
    -- Intentar una división por cero (error intencional)
    SELECT 1 / 0;

    -- Verificar si hubo error
    IF @@ERROR <> 0
    BEGIN
        ROLLBACK TRANSACTION;
        PRINT 'Error: División por cero detectada. Transacción revertida.';
    END
    ELSE
        COMMIT TRANSACTION;
```
**Salida:**  
```
Error: División por cero detectada. Transacción revertida.
```

**Limitación:**  
- `@@ERROR` se reinicia después de cada sentencia. Usar `TRY...CATCH` para manejo más robusto.

---

## **11.2 Bloques `TRY...CATCH`**  

### **Estructura Básica**  
```sql
BEGIN TRY
    -- Código que puede generar errores
END TRY
BEGIN CATCH
    -- Manejo del error
END CATCH
```

### **Ejemplo con Transacción**  
```sql
BEGIN TRY
    BEGIN TRANSACTION;
        -- Operación 1
        UPDATE Cuentas SET Saldo = Saldo - 100 WHERE CuentaID = 1;
        
        -- Operación 2 (generará error si el saldo es insuficiente)
        IF (SELECT Saldo FROM Cuentas WHERE CuentaID = 1) < 0
            RAISERROR('Saldo insuficiente', 16, 1);
            
        COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    PRINT 'Error: ' + ERROR_MESSAGE();
END CATCH
```
**Salida si hay error:**  
```
Error: Saldo insuficiente
```

---

## **11.3 Funciones para Recuperar Información de Errores**  

Dentro de un bloque `CATCH`, usa estas funciones para obtener detalles del error:  

| **Función**            | **Descripción**                          | **Ejemplo**                          |
|------------------------|-----------------------------------------|--------------------------------------|
| `ERROR_MESSAGE()`      | Mensaje descriptivo del error.          | `PRINT ERROR_MESSAGE();`             |
| `ERROR_NUMBER()`       | Número del error.                       | `PRINT ERROR_NUMBER();`              |
| `ERROR_SEVERITY()`     | Gravedad (1-25).                        | `PRINT ERROR_SEVERITY();`            |
| `ERROR_STATE()`        | Estado del error (0-255).               | `PRINT ERROR_STATE();`               |
| `ERROR_LINE()`         | Línea donde ocurrió el error.           | `PRINT ERROR_LINE();`                |
| `ERROR_PROCEDURE()`    | Nombre del procedimiento que falló.     | `PRINT ERROR_PROCEDURE();`           |

### **Ejemplo Completo**  
```sql
BEGIN TRY
    SELECT 1 / 0;
END TRY
BEGIN CATCH
    PRINT 'Mensaje: ' + ERROR_MESSAGE();
    PRINT 'Número: ' + CAST(ERROR_NUMBER() AS VARCHAR);
    PRINT 'Severidad: ' + CAST(ERROR_SEVERITY() AS VARCHAR);
    PRINT 'Línea: ' + CAST(ERROR_LINE() AS VARCHAR);
END CATCH
```
**Salida:**  
```
Mensaje: Divide by zero error encountered.
Número: 8134
Severidad: 16
Línea: 2
```

---

## **11.4 Comandos `RAISERROR` y `THROW`**  

### **A. `RAISERROR`**  
Genera errores personalizados con severidad y estado.  

**Sintaxis:**  
```sql
RAISERROR('Mensaje', Severidad, Estado);
```

**Ejemplo:**  
```sql
BEGIN TRY
    DECLARE @Saldo DECIMAL(10,2) = -100;
    IF @Saldo < 0
        RAISERROR('El saldo no puede ser negativo', 16, 1);
END TRY
BEGIN CATCH
    PRINT 'Error: ' + ERROR_MESSAGE();
END CATCH
```
**Salida:**  
```
Error: El saldo no puede ser negativo
```

### **B. `THROW`**  
Relanza el error original o genera uno nuevo (SQL Server 2012+).  

**Sintaxis:**  
```sql
THROW [ErrorNumber, 'Mensaje', Estado];
```

**Ejemplo 1: Relanzar Error**  
```sql
BEGIN TRY
    SELECT 1 / 0;
END TRY
BEGIN CATCH
    PRINT 'Error capturado: ' + ERROR_MESSAGE();
    THROW; -- Relanza el error original
END CATCH
```

**Ejemplo 2: Error Personalizado**  
```sql
BEGIN TRY
    THROW 50001, 'Error personalizado: Datos inválidos', 1;
END TRY
BEGIN CATCH
    PRINT 'Error: ' + ERROR_MESSAGE();
END CATCH
```
**Salida:**  
```
Error: Error personalizado: Datos inválidos
```

---

## **11.5 Comparación: `RAISERROR` vs `THROW`**  

| **Característica**       | `RAISERROR`                          | `THROW`                              |
|--------------------------|--------------------------------------|--------------------------------------|
| **Versión**              | SQL Server 2000+                     | SQL Server 2012+                     |
| **Relanzar errores**     | No                                   | Sí (`THROW;` sin parámetros)         |
| **Severidad**            | Personalizable (1-25)                | Siempre 16                           |
| **Formato de mensaje**   | Soporta parámetros estilo `printf`   | Mensaje plano                        |

---

### **Resumen de Buenas Prácticas**  
1. **Usa `TRY...CATCH`** para manejo estructurado.  
2. **Prefiere `THROW`** en SQL Server moderno (más simple y claro).  
3. **Registra errores** en tablas de log para auditoría:  
   ```sql
   BEGIN CATCH
       INSERT INTO ErrorLog (Mensaje, Fecha, Usuario)
       VALUES (ERROR_MESSAGE(), GETDATE(), SYSTEM_USER);
       THROW;
   END CATCH
   ```

---

**Conclusión:**  
El manejo adecuado de errores evita fallos silenciosos y mejora la mantenibilidad. Combina `TRY...CATCH` con `THROW` para un flujo claro y profesional.  

### **12. Cursores en SQL Server**

Los cursores son herramientas que permiten procesar filas de un conjunto de resultados **una por una**. Aunque suelen evitarse por impacto en el rendimiento, son útiles para operaciones fila por fila complejas.

---

## **12.1 Introducción y Sintaxis Básica**

### **Flujo de Trabajo de un Cursor**
1. **Declarar**: Definir el cursor y su consulta asociada.
2. **Abrir**: Ejecutar la consulta y cargar los resultados.
3. **Recorrer**: Obtener filas secuencialmente con `FETCH`.
4. **Cerrar/Liberar**: Liberar recursos.

### **Sintaxis Completa**
```sql
DECLARE cursor_nombre CURSOR 
    [LOCAL | GLOBAL] 
    [FORWARD_ONLY | SCROLL] 
    [STATIC | KEYSET | DYNAMIC | FAST_FORWARD] 
    FOR select_statement;

OPEN cursor_nombre;
FETCH NEXT FROM cursor_nombre INTO @variables;

WHILE @@FETCH_STATUS = 0
BEGIN
    -- Procesar fila actual
    FETCH NEXT FROM cursor_nombre INTO @variables;
END

CLOSE cursor_nombre;
DEALLOCATE cursor_nombre;
```

---

## **12.2 Tipos de Cursor**

| **Tipo**          | **Descripción**                                                                 | **Uso Típico**                     |
|--------------------|-------------------------------------------------------------------------------|-----------------------------------|
| **STATIC**         | Copia los datos en `tempdb`. No refleja cambios posteriores.                   | Cuando se necesita consistencia.  |
| **DYNAMIC**        | Refleja cambios en los datos subyacentes en tiempo real.                       | Datos volátiles.                  |
| **KEYSET**         | Bloquea las filas iniciales pero permite ver actualizaciones a datos no clave. | Balance entre rendimiento y frescura. |
| **FAST_FORWARD**   | Cursor optimizado de solo lectura y avance rápido.                             | Solo lectura eficiente.           |

---

## **12.3 Ejemplos Prácticos**

### **A. Ejemplo Básico (Recorrer Empleados)**
```sql
DECLARE @id INT, @nombre VARCHAR(100);

-- Declarar cursor
DECLARE empleado_cursor CURSOR FOR 
    SELECT EmpleadoID, Nombre FROM Empleados WHERE Departamento = 'Ventas';

OPEN empleado_cursor;
FETCH NEXT FROM empleado_cursor INTO @id, @nombre;

WHILE @@FETCH_STATUS = 0
BEGIN
    PRINT CONCAT('ID: ', @id, ' - Nombre: ', @nombre);
    FETCH NEXT FROM empleado_cursor INTO @id, @nombre;
END

CLOSE empleado_cursor;
DEALLOCATE empleado_cursor;
```

### **B. Ejemplo con Actualización (Aumento Salarial)**
```sql
DECLARE @emp_id INT, @salario DECIMAL(10,2);

DECLARE salario_cursor CURSOR FOR 
    SELECT EmpleadoID, Salario FROM Empleados 
    WHERE Puesto = 'Gerente' FOR UPDATE OF Salario;

OPEN salario_cursor;
FETCH NEXT FROM salario_cursor INTO @emp_id, @salario;

WHILE @@FETCH_STATUS = 0
BEGIN
    -- Aumento del 10%
    UPDATE Empleados 
    SET Salario = @salario * 1.10 
    WHERE CURRENT OF salario_cursor;
    
    FETCH NEXT FROM salario_cursor INTO @emp_id, @salario;
END

CLOSE salario_cursor;
DEALLOCATE salario_cursor;
```
**Clave:**  
- `FOR UPDATE OF` permite modificar la fila actual.  
- `WHERE CURRENT OF` apunta a la fila en la que está el cursor.

---

## **12.4 Procedimientos Almacenados del Sistema**

SQL Server ofrece procedimientos para manejo dinámico de cursores:

### **`sp_cursoropen`**
Abre un cursor dinámico desde T-SQL dinámico.
```sql
DECLARE @cursor INT;
DECLARE @sql NVARCHAR(100) = 'SELECT * FROM Empleados';

EXEC sp_cursoropen 
    @cursor OUTPUT, 
    @sql,
    @scrollopt = 1, -- KEYSET
    @ccopt = 1;     -- Optimización para lectura
```

### **`sp_cursorfetch`**
Recupera filas desde un cursor abierto.
```sql
DECLARE @rowcount INT;
EXEC sp_cursorfetch @cursor, 2, 1, 5, @rowcount OUTPUT; -- Fetch 5 filas
```

### **`sp_cursorclose`**
Cierra el cursor.
```sql
EXEC sp_cursorclose @cursor;
```

---

## **12.5 Consideraciones de Rendimiento**

### **Problemas Comunes**
1. **Alto consumo de memoria**: Cada cursor mantiene un conjunto de resultados en `tempdb` (especialmente `STATIC`).  
2. **Bloqueos prolongados**: Cursores `DYNAMIC` pueden bloquear tablas.  
3. **Lentitud**: Procesar filas una por una es más lento que operaciones basadas en conjuntos.

### **Alternativas Recomendadas**
- **Operaciones por conjuntos**: Usar `UPDATE`, `INSERT SELECT`, etc.  
- **Tablas temporales**: Para almacenar resultados intermedios.  
- **WHILE con TOP**: Procesamiento por lotes.  
  ```sql
  DECLARE @batch_size INT = 1000;
  WHILE EXISTS (SELECT 1 FROM Productos WHERE Procesado = 0)
  BEGIN
      UPDATE TOP (@batch_size) Productos
      SET Procesado = 1
      WHERE Procesado = 0;
  END
  ```

---

## **12.6 Cuándo Usar Cursores**

✅ **Casos válidos**:  
- Migración de datos con lógica compleja fila por fila.  
- Validaciones que requieren acceso secuencial.  
- Integración con código procedural (ej: CLR).  

❌ **Evitar cuando**:  
- Se pueden usar operaciones basadas en conjuntos.  
- Se procesan grandes volúmenes de datos.  

---

### **Resumen de Comandos Clave**
| **Acción**               | **Comando**                                  |
|--------------------------|---------------------------------------------|
| Declarar cursor          | `DECLARE cursor_name CURSOR FOR SELECT...` |
| Abrir                    | `OPEN cursor_name`                         |
| Obtener fila             | `FETCH NEXT FROM cursor INTO @vars`        |
| Verificar estado         | `WHILE @@FETCH_STATUS = 0`                 |
| Cerrar/Liberar           | `CLOSE cursor_name; DEALLOCATE cursor_name`|

**Conclusión:**  
Los cursores son herramientas poderosas pero costosas. Úsalos solo cuando no exista alternativa basada en conjuntos. Siempre libera recursos con `CLOSE` y `DEALLOCATE`.  

### **13. Operadores PIVOT y UNPIVOT en SQL Server**

Estos operadores permiten **transformar datos entre formatos de filas y columnas**, facilitando el análisis y presentación de información. Aquí te muestro su uso con ejemplos prácticos y claros.

---

## **13.1 Operador PIVOT**  
Convierte **valores únicos de una columna** en **múltiples columnas**, agregando datos.

### **Sintaxis Básica**
```sql
SELECT [columnas_fijas], [valores_pivoteados]
FROM (
    SELECT [columna_fija], [columna_a_pivotear], [valor_a_mostrar]
    FROM tabla
) AS SourceTable
PIVOT (
    FUNCIÓN_AGREGACIÓN(valor_a_mostrar)
    FOR [columna_a_pivotear] IN ([lista_de_valores_pivoteados])
) AS PivotTable;
```

### **Ejemplo 1: Ventas por Producto y Mes**  
**Tabla Original (`Ventas`):**
| ProductoID | Mes   | TotalVentas |
|------------|-------|-------------|
| 1          | Enero | 1000        |
| 2          | Enero | 1500        |
| 1          | Feb   | 2000        |

**Consulta PIVOT:**
```sql
SELECT ProductoID, [Enero], [Febrero]
FROM (
    SELECT ProductoID, Mes, TotalVentas
    FROM Ventas
) AS SourceTable
PIVOT (
    SUM(TotalVentas)
    FOR Mes IN ([Enero], [Febrero])
) AS PivotTable;
```

**Resultado:**
| ProductoID | Enero | Febrero |
|------------|-------|---------|
| 1          | 1000  | 2000    |
| 2          | 1500  | NULL    |

---

### **Ejemplo 2: PIVOT Dinámico (Cuando no conoces los valores de antemano)**  
```sql
DECLARE @columnas NVARCHAR(MAX) = '';
DECLARE @sql NVARCHAR(MAX);

-- Obtener meses únicos para crear las columnas
SELECT @columnas = @columnas + '[' + Mes + '],'
FROM (SELECT DISTINCT Mes FROM Ventas) AS m;

SET @columnas = LEFT(@columnas, LEN(@columnas) - 1); -- Eliminar última coma

-- Construir consulta dinámica
SET @sql = '
SELECT ProductoID, ' + @columnas + '
FROM (
    SELECT ProductoID, Mes, TotalVentas
    FROM Ventas
) AS SourceTable
PIVOT (
    SUM(TotalVentas)
    FOR Mes IN (' + @columnas + ')
) AS PivotTable;';

EXEC sp_executesql @sql;
```

---

## **13.2 Operador UNPIVOT**  
Convierte **columnas en filas**, útil para normalizar datos.

### **Sintaxis Básica**
```sql
SELECT [columnas_fijas], [nombre_columna], [valor]
FROM (
    SELECT [columna_fija], [col1], [col2], ...
    FROM tabla
) AS SourceTable
UNPIVOT (
    [valor] FOR [nombre_columna] IN ([col1], [col2], ...)
) AS UnpivotTable;
```

### **Ejemplo: Transformar Columnas de Meses a Filas**  
**Tabla Original (`VentasPivotadas`):**
| ProductoID | Enero | Febrero |
|------------|-------|---------|
| 1          | 1000  | 2000    |
| 2          | 1500  | NULL    |

**Consulta UNPIVOT:**
```sql
SELECT ProductoID, Mes, TotalVentas
FROM (
    SELECT ProductoID, Enero, Febrero
    FROM VentasPivotadas
) AS SourceTable
UNPIVOT (
    TotalVentas FOR Mes IN (Enero, Febrero)
) AS UnpivotTable;
```

**Resultado:**
| ProductoID | Mes     | TotalVentas |
|------------|---------|-------------|
| 1          | Enero   | 1000        |
| 1          | Febrero | 2000        |
| 2          | Enero   | 1500        |
| 2          | Febrero | NULL        |

---

## **13.3 Diferencias Clave y Casos de Uso**

| **Operador** | **Propósito**                          | **Ejemplo Típico**                     |
|--------------|----------------------------------------|----------------------------------------|
| **PIVOT**    | Convertir filas en columnas (agregación). | Reportes de ventas por mes/producto.  |
| **UNPIVOT**  | Convertir columnas en filas (normalización). | Preparar datos para ETL o análisis.   |

---

## **13.4 Consideraciones Importantes**

1. **PIVOT requiere funciones de agregación** (`SUM`, `AVG`, etc.).
2. **UNPIVOT excluye NULLs** por defecto (usa `INCLUDE NULLS` si es necesario).
3. **Rendimiento**: 
   - PIVOT/UNPIVOT pueden ser costosos en grandes volúmenes de datos.
   - Alternativas: Usar `CASE` o consultas dinámicas para mayor control.

### **Alternativa con `CASE` (Similar a PIVOT)**
```sql
SELECT 
    ProductoID,
    SUM(CASE WHEN Mes = 'Enero' THEN TotalVentas ELSE 0 END) AS Enero,
    SUM(CASE WHEN Mes = 'Febrero' THEN TotalVentas ELSE 0 END) AS Febrero
FROM Ventas
GROUP BY ProductoID;
```

---

### **Resumen de Comandos**
| **Operación**       | **Sintaxis SQL**                                                                 |
|----------------------|----------------------------------------------------------------------------------|
| **PIVOT Estático**   | `PIVOT (SUM(valor) FOR columna IN ([Enero], [Febrero]))`                        |
| **PIVOT Dinámico**   | Usar `sp_executesql` con columnas generadas.                                     |
| **UNPIVOT**          | `UNPIVOT (valor FOR nombre_columna IN (Enero, Febrero))`                        |

**Conclusión:**  
Estos operadores son ideales para transformar datos entre formatos horizontales (columnas) y verticales (filas), pero deben usarse con cuidado en datasets grandes.  

