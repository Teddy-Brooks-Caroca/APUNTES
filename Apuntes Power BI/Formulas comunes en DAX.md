
## Estadísticas

**Promedio:**
Calcula el promedio de una columna numérica.
```d
// DAX
AVERAGE(Tabla[Columna])

// M
List.Average(Tabla[Columna]) 

// Ejemplo 
Promedio_Ventas = AVERAGE(Ventas[Monto])
```

**Suma**
Suma todos los valores de una columna numérica.
```d
   // DAX 
   SUM(Tabla[Columna])
   
   // M 
   List.Sum(Tabla[Columna])
   
   //Ejemplo: 
   Total_Ventas = SUM(Ventas[Monto])
```

**Contar**
Cuenta el número de filas en una columna.
```d
// DAX 
COUNT(Tabla[Columna])

// M: 
List.Count(Tabla[Columna])

// Ejemplo: 
Num_Transacciones = COUNT(Ventas[ID])
```

**Máximo**
Encuentra el valor máximo en una columna.
```d
//DAX 
MAX(Tabla[Columna])
   
//M
List.Max(Tabla[Columna])

//Ejemplo: 
Venta_Maxima = MAX(Ventas[Monto])
```

**Mínimo**
Encuentra el valor mínimo en una columna.
```D
//DAX: 
MIN(Tabla[Columna])

//M: 
List.Min(Tabla[Columna])

//Ejemplo: 
Venta_Minima = MIN(Ventas[Monto])
```


**Mediana**
Calcula la mediana de una columna numérica.
```D
//DAX: 
MEDIAN(Tabla[Columna])

//M: 
List.Median(Tabla[Columna])
   
//Ejemplo: 
Mediana_Ventas = MEDIAN(Ventas[Monto])
```

**Desviación Estándar**
Calcula la desviación estándar poblacional.
```D
//DAX: 
STDEV.P(Tabla[Columna])
   
//M:
List.StandardDeviation(Tabla[Columna])

//Ejemplo: 
Desv_Est_Ventas = STDEV.P(Ventas[Monto])
```

**Varianza**
Calcula la varianza poblacional.
```D
//DAX: 
VAR.P(Tabla[Columna])

//M: 
List.Variance(Tabla[Columna])

//Ejemplo: 
Varianza_Ventas = VAR.P(Ventas[Monto])
```

**Percentil**
Calcula el percentil 90 de una columna numérica.
```D
//DAX: 
PERCENTILE.EXC(Tabla[Columna], 0.9)
   
//M: 
List.Percentile(Tabla[Columna], 0.9)

//Ejemplo:
Percentil90_Ventas = PERCENTILE.EXC(Ventas[Monto], 0.9)
```

**Moda**
Encuentra el valor más frecuente en una columna.
```D
//DAX: 
CALCULATE(MAX(Tabla[Columna]), GROUPBY(Tabla, Tabla[Columna], "Count", COUNTROWS()))
    
//M: 
List.Mode(Tabla[Columna])

//Ejemplo: 
Moda_Ventas = CALCULATE(MAX(Ventas[Monto]), GROUPBY(Ventas, Ventas[Monto], "Count", COUNTROWS()))
```

Categoría 2: Texto

1. Mayúsculas
   DAX: `UPPER(Tabla[Columna])`
   M: `Text.Upper(Tabla[Columna])`
   Ejemplo: `Nombre_Mayusculas = UPPER(Clientes[Nombre])`
   Explicación: Convierte el texto a mayúsculas.

2. Minúsculas
   DAX: `LOWER(Tabla[Columna])`
   M: `Text.Lower(Tabla[Columna])`
   Ejemplo: `Email_Minusculas = LOWER(Clientes[Email])`
   Explicación: Convierte el texto a minúsculas.

3. Longitud
   DAX: `LEN(Tabla[Columna])`
   M: `Text.Length(Tabla[Columna])`
   Ejemplo: `Longitud_Nombre = LEN(Clientes[Nombre])`
   Explicación: Cuenta el número de caracteres en una cadena de texto.

4. Concatenar
   DAX: `CONCATENATE(Tabla[Columna1], " ", Tabla[Columna2])`
   M: `Text.Combine({Tabla[Columna1], " ", Tabla[Columna2]})`
   Ejemplo: `Nombre_Completo = CONCATENATE(Clientes[Nombre], " ", Clientes[Apellido])`
   Explicación: Une dos o más cadenas de texto.

5. Extraer
   DAX: `LEFT(Tabla[Columna], 3)`
   M: `Text.Start(Tabla[Columna], 3)`
   Ejemplo: `Codigo_Pais = LEFT(Clientes[Telefono], 3)`
   Explicación: Extrae los primeros n caracteres de una cadena.

6. Reemplazar
   DAX: `SUBSTITUTE(Tabla[Columna], "viejo", "nuevo")`
   M: `Text.Replace(Tabla[Columna], "viejo", "nuevo")`
   Ejemplo: `Texto_Corregido = SUBSTITUTE(Productos[Descripcion], "color", "Color")`
   Explicación: Reemplaza una subcadena por otra en el texto.

7. Recortar espacios
   DAX: `TRIM(Tabla[Columna])`
   M: `Text.Trim(Tabla[Columna])`
   Ejemplo: `Nombre_Limpio = TRIM(Clientes[Nombre])`
   Explicación: Elimina espacios al inicio y al final del texto.

8. Encontrar posición
   DAX: `FIND("@", Tabla[Columna], 1, -1)`
   M: `Text.PositionOf(Tabla[Columna], "@")`
   Ejemplo: `Posicion_Arroba = FIND("@", Clientes[Email], 1, -1)`
   Explicación: Encuentra la posición de una subcadena en el texto.

9. Dividir
   DAX: `PATHITEM(SUBSTITUTE(Tabla[Columna], "@", "|"), 1)`
   M: `Text.Split(Tabla[Columna], "@"){0}`
   Ejemplo: `Nombre_Usuario = PATHITEM(SUBSTITUTE(Clientes[Email], "@", "|"), 1)`
   Explicación: Divide una cadena en base a un delimitador y selecciona una parte.

10. Contiene
    DAX: `CONTAINS(LOWER(Tabla[Columna]), "texto")`
    M: `Text.Contains(Text.Lower(Tabla[Columna]), "texto")`
    Ejemplo: `Tiene_Promocion = CONTAINS(LOWER(Productos[Nombre]), "oferta")`
    Explicación: Verifica si una cadena contiene una subcadena específica.

Categoría 3: Fecha y Hora

1. Año
   DAX: `YEAR(Tabla[Fecha])`
   M: `Date.Year(Tabla[Fecha])`
   Ejemplo: `Año_Venta = YEAR(Ventas[Fecha])`
   Explicación: Extrae el año de una fecha.

2. Mes
   DAX: `MONTH(Tabla[Fecha])`
   M: `Date.Month(Tabla[Fecha])`
   Ejemplo: `Mes_Venta = MONTH(Ventas[Fecha])`
   Explicación: Extrae el mes de una fecha.

3. Día
   DAX: `DAY(Tabla[Fecha])`
   M: `Date.Day(Tabla[Fecha])`
   Ejemplo: `Dia_Venta = DAY(Ventas[Fecha])`
   Explicación: Extrae el día de una fecha.

4. Nombre del mes
   DAX: `FORMAT(Tabla[Fecha], "mmmm")`
   M: `Date.MonthName(Tabla[Fecha])`
   Ejemplo: `Nombre_Mes = FORMAT(Ventas[Fecha], "mmmm")`
   Explicación: Obtiene el nombre del mes de una fecha.

5. Día de la semana
   DAX: `WEEKDAY(Tabla[Fecha])`
   M: `Date.DayOfWeek(Tabla[Fecha])`
   Ejemplo: `Dia_Semana = WEEKDAY(Ventas[Fecha])`
   Explicación: Obtiene el día de la semana (1-7) de una fecha.

6. Primer día del mes
   DAX: `EOMONTH(Tabla[Fecha], -1) + 1`
   M: `Date.StartOfMonth(Tabla[Fecha])`
   Ejemplo: `Inicio_Mes = EOMONTH(Ventas[Fecha], -1) + 1`
   Explicación: Obtiene el primer día del mes de una fecha dada.

7. Último día del mes
   DAX: `EOMONTH(Tabla[Fecha], 0)`
   M: `Date.EndOfMonth(Tabla[Fecha])`
   Ejemplo: `Fin_Mes = EOMONTH(Ventas[Fecha], 0)`
   Explicación: Obtiene el último día del mes de una fecha dada.

8. Diferencia en días
   DAX: `DATEDIFF(Tabla[Fecha1], Tabla[Fecha2], DAY)`
   M: `Duration.Days(Tabla[Fecha2] - Tabla[Fecha1])`
   Ejemplo: `Dias_Entrega = DATEDIFF(Pedidos[Fecha_Pedido], Pedidos[Fecha_Entrega], DAY)`
   Explicación: Calcula la diferencia en días entre dos fechas.

9. Sumar días
   DAX: `Tabla[Fecha] + 7`
   M: `Date.AddDays(Tabla[Fecha], 7)`
   Ejemplo: `Fecha_Vencimiento = Facturas[Fecha_Emision] + 30`
   Explicación: Suma un número específico de días a una fecha.

10. Es fin de semana
    DAX: `IF(WEEKDAY(Tabla[Fecha]) IN {1,7}, TRUE, FALSE)`
    M: `Date.DayOfWeek(Tabla[Fecha]) >= 5`
    Ejemplo: `Es_FinDeSemana = IF(WEEKDAY(Calendario[Fecha]) IN {1,7}, TRUE, FALSE)`
    Explicación: Determina si una fecha cae en fin de semana.
Por supuesto, continuaré con las siguientes categorías.

Categoría 4: Lógica y Condicionales

1. Si...entonces
   DAX: `IF(Tabla[Columna] > 100, "Alto", "Bajo")`
   M: `if [Columna] > 100 then "Alto" else "Bajo"`
   Ejemplo: `Categoria_Ventas = IF(Ventas[Monto] > 1000, "Alta", "Baja")`
   Explicación: Evalúa una condición y devuelve un valor según sea verdadera o falsa.

2. Y lógico
   DAX: `AND(Tabla[Columna1] > 0, Tabla[Columna2] < 100)`
   M: `[Columna1] > 0 and [Columna2] < 100`
   Ejemplo: `Producto_Valido = AND(Productos[Precio] > 0, Productos[Stock] > 0)`
   Explicación: Devuelve verdadero si todas las condiciones son verdaderas.

3. O lógico
   DAX: `OR(Tabla[Columna1] = "A", Tabla[Columna1] = "B")`
   M: `[Columna1] = "A" or [Columna1] = "B"`
   Ejemplo: `Es_Prioridad = OR(Clientes[Tipo] = "VIP", Clientes[Compras] > 10000)`
   Explicación: Devuelve verdadero si al menos una condición es verdadera.

4. No lógico
   DAX: `NOT(Tabla[Columna] = "Inactivo")`
   M: `not ([Columna] = "Inactivo")`
   Ejemplo: `Cliente_Activo = NOT(Clientes[Estado] = "Inactivo")`
   Explicación: Invierte el valor de una expresión booleana.

5. Conmutador (Switch)
   DAX: `SWITCH(Tabla[Columna], 1, "Bajo", 2, "Medio", 3, "Alto", "Desconocido")`
   M: `Table.AddColumn(Tabla, "Nueva_Columna", each 
        if [Columna] = 1 then "Bajo"
        else if [Columna] = 2 then "Medio"
        else if [Columna] = 3 then "Alto"
        else "Desconocido")`
   Ejemplo: `Categoria_Producto = SWITCH(Productos[ID_Categoria], 1, "Electrónica", 2, "Ropa", 3, "Hogar", "Otro")`
   Explicación: Evalúa una expresión contra una lista de valores y devuelve uno de múltiples resultados posibles.

6. Es nulo
   DAX: `ISBLANK(Tabla[Columna])`
   M: `[Columna] = null`
   Ejemplo: `Tiene_Telefono = NOT(ISBLANK(Clientes[Telefono]))`
   Explicación: Comprueba si un valor es nulo o está en blanco.

7. Si es error
   DAX: `IFERROR(Tabla[Columna1] / Tabla[Columna2], 0)`
   M: `try [Columna1] / [Columna2] otherwise 0`
   Ejemplo: `Precio_Unitario_Seguro = IFERROR(Ventas[Total] / Ventas[Cantidad], 0)`
   Explicación: Evalúa una expresión y devuelve un valor alternativo si se produce un error.

8. Valor si nulo
   DAX: `COALESCE(Tabla[Columna], "No disponible")`
   M: `if [Columna] = null then "No disponible" else [Columna]`
   Ejemplo: `Direccion_Completa = COALESCE(Clientes[Direccion], "Dirección no proporcionada")`
   Explicación: Devuelve el primer valor no nulo de una lista de expresiones.

9. Entre (Between)
   DAX: `Tabla[Columna] >= 10 && Tabla[Columna] <= 20`
   M: `[Columna] >= 10 and [Columna] <= 20`
   Ejemplo: `Precio_Medio = Productos[Precio] >= 50 && Productos[Precio] <= 100`
   Explicación: Comprueba si un valor está dentro de un rango específico.

10. Caso cuando (Case When)
    DAX: `SWITCH(TRUE(),
                 Tabla[Columna] < 0, "Negativo",
                 Tabla[Columna] = 0, "Cero",
                 Tabla[Columna] > 0, "Positivo")`
    M: `if [Columna] < 0 then "Negativo"
        else if [Columna] = 0 then "Cero"
        else if [Columna] > 0 then "Positivo"
        else null`
    Ejemplo: `Estado_Cuenta = SWITCH(TRUE(),
                                     Clientes[Saldo] < 0, "Deudor",
                                     Clientes[Saldo] = 0, "Al día",
                                     Clientes[Saldo] > 0, "Con crédito")`
    Explicación: Permite múltiples condiciones y resultados, similar a un CASE WHEN en SQL.
Ciertamente. Continuaré con la última categoría.

Categoría 5: Matemáticas

1. Suma
   DAX: `SUM(Tabla[Columna])`
   M: `List.Sum(Tabla[Columna])`
   Ejemplo: `Total_Ventas = SUM(Ventas[Monto])`
   Explicación: Suma todos los números en una columna.

2. Redondear
   DAX: `ROUND(Tabla[Columna], 2)`
   M: `Number.Round(Tabla[Columna], 2)`
   Ejemplo: `Precio_Redondeado = ROUND(Productos[Precio], 2)`
   Explicación: Redondea un número al número especificado de decimales.

3. Potencia
   DAX: `POWER(Tabla[Columna], 2)`
   M: `Number.Power(Tabla[Columna], 2)`
   Ejemplo: `Area = POWER(Terrenos[Lado], 2)`
   Explicación: Eleva un número a una potencia especificada.

4. Raíz cuadrada
   DAX: `SQRT(Tabla[Columna])`
   M: `Number.Sqrt(Tabla[Columna])`
   Ejemplo: `Raiz_Cuadrada = SQRT(Datos[Valor])`
   Explicación: Calcula la raíz cuadrada de un número.

5. Valor absoluto
   DAX: `ABS(Tabla[Columna])`
   M: `Number.Abs(Tabla[Columna])`
   Ejemplo: `Diferencia_Absoluta = ABS(Inventario[Stock_Actual] - Inventario[Stock_Mínimo])`
   Explicación: Devuelve el valor absoluto de un número.

6. Logaritmo
   DAX: `LOG(Tabla[Columna])`
   M: `Number.Ln(Tabla[Columna])`
   Ejemplo: `Log_Ventas = LOG(Ventas[Monto])`
   Explicación: Calcula el logaritmo natural de un número.

7. Exponencial
   DAX: `EXP(Tabla[Columna])`
   M: `Number.Exp(Tabla[Columna])`
   Ejemplo: `Crecimiento_Exponencial = EXP(Datos[Tasa] * Datos[Tiempo])`
   Explicación: Calcula e elevado a la potencia de un número.

8. Módulo (Resto)
   DAX: `MOD(Tabla[Columna], 2)`
   M: `Number.Mod(Tabla[Columna], 2)`
   Ejemplo: `Es_Par = MOD(Productos[ID], 2) = 0`
   Explicación: Devuelve el resto de una división.

9. Máximo común divisor
   DAX: `No hay función nativa, se requiere una función personalizada`
   M: `Number.Gcd(Tabla[Columna1], Tabla[Columna2])`
   Ejemplo: `MCD = Number.Gcd(Datos[Valor1], Datos[Valor2])`
   Explicación: Calcula el máximo común divisor de dos números.

10. Truncar
    DAX: `TRUNC(Tabla[Columna], 2)`
    M: `Number.RoundDown(Tabla[Columna], 2)`
    Ejemplo: `Precio_Truncado = TRUNC(Productos[Precio], 2)`
    Explicación: Trunca un número al número especificado de decimales sin redondear.

 Recuerda que DAX se usa principalmente para crear medidas y columnas calculadas en el modelo de datos, mientras que M se usa en Power Query para transformar y preparar datos antes de cargarlos en el modelo.

Es importante notar que algunas funciones pueden tener ligeras diferencias en su implementación o sintaxis entre DAX y M, y que DAX está más orientado al análisis de datos, mientras que M es más versátil en la manipulación y transformación de datos.

