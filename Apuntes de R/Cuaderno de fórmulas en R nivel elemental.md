
## ESTRUCTURAS DE DATOS EN R

#### CREAR UNA VARIABLE
```R
nombre_variable <- valor

nombre_variable = valor
```

En R, se recomienda usar `<-` en lugar de `=` para asignar valores a variables, ya que es una convención de estilo más común en la comunidad.
#### EJEMPLOS DE VARIABLES
```R
# Asignando números
x <- 10
y = 20

# Asignando texto (caracteres deben ir entre comillas)
nombre <- "Juan"

# Asignando un vector
numeros <- c(1, 2, 3, 4, 5)

# Asignando un valor lógico (TRUE o FALSE)
es_mayor <- TRUE

```

#### CREAR UN VECTOR:
```R
vector_nombre <- c(elemento1, elemento2, elemento3, ...)
```

- `vector_nombre` es el nombre que le quieres dar a tu vector.
- `c()` es la función que combina los elementos para crear el vector.
- `elemento1`, `elemento2`, `elemento3`, etc. son los valores que quieres almacenar en el vector. Pueden ser números, cadenas de texto, valores lógicos, etc.

#### EJEMPLOS DE VECTORES:
```R
# Vector numérico
mi_vector <- c(1, 2, 3, 4, 5)

# Vector de caracteres
nombres <- c("Juan", "María", "Pedro", "Ana")

# Vector lógico
logicos <- c(TRUE, FALSE, TRUE, FALSE)

#Se puede acceder a los elementos del vector utilizando los índices numéricos:

mi_vector[1]  # Devuelve el primer elemento
mi_vector[2:4]  # Devuelve un vector con los elementos del 2 al 4
```

#### CREAR UNA MATRIZ:
```R
matriz_nombre <- matrix(vector, nrow = filas, ncol = columnas, byrow = FALSE)
```

- `matriz_nombre` es el nombre que le quieres dar a tu matriz.
- `vector` es un vector que contiene los elementos que quieres incluir en la matriz.
- `nrow` es el número de filas que tendrá la matriz.
- `ncol` es el número de columnas que tendrá la matriz.
- `byrow` es un argumento lógico que indica si el vector debe ser rellenado por filas (`byrow = TRUE`) o por columnas (`byrow = FALSE`, que es el valor por defecto).

#### EJEMPLOS DE MATRICES:
```R
# Matriz 2x3 rellenada por columnas
mi_matriz <- matrix(c(1, 2, 3, 4, 5, 6), nrow = 2, ncol = 3)
#      [,1] [,2] [,3]
# [1,]    1    3    5
# [2,]    2    4    6

# Matriz 3x2 rellenada por filas
otra_matriz <- matrix(c(1, 2, 3, 4, 5, 6), nrow = 3, ncol = 2, byrow = TRUE)
#      [,1] [,2]
# [1,]    1    2
# [2,]    3    4
# [3,]    5    6

# Se puede acceder a los elementos de una matriz utilizando índices de fila y columna:

mi_matriz[1, 2]  # Devuelve el elemento en la fila 1, columna 2
otra_matriz[2, ]  # Devuelve la fila 2 como un vector
```

#### CREAR UNA LISTA:
```R
lista_nombre <- list(elemento1, elemento2, elemento3, ...)
````

- `lista_nombre` es el nombre que le quieres dar a tu lista.
- `elemento1`, `elemento2`, `elemento3`, etc. son los elementos que quieres incluir en la lista. Estos elementos pueden ser de diferentes tipos de datos (numéricos, caracteres, vectores, matrices, incluso otras listas).

#### EJEMPLOS DE LISTAS:
```R
# Lista con elementos de diferentes tipos
mi_lista <- list(1, "dos", c(3, 4, 5), TRUE)

# Lista con nombres para los elementos
otra_lista <- list(numeros = 1:5, caracteres = c("a", "b", "c"), logico = FALSE)

# Lista anidada (con otra lista dentro)
lista_anidada <- list(1, 2, lista_interna = lista(3, 4, 5))

# Se puede acceder a los elementos de una lista utilizando corchetes `[ ]` y los nombres o índices numéricos de los elementos:

mi_lista[1]  # Devuelve el primer elemento
otra_lista["caracteres"]  # Devuelve el elemento con nombre "caracteres"
lista_anidada[[3]]  # Devuelve la lista interna
```
Las listas en R son muy versátiles y permiten almacenar diferentes tipos de datos en una sola estructura.

#### CREAR UN DATA FRAME:
```R
nuevo_conjunto <- data.frame( nombre_columna_1 = c(dato, dato, dato),
                              nombre_columna_2 = c(dato, dato, dato))

print(nuevo_conjunto)

```

- `data.frame()` es la función que se utiliza para crear un data frame en R.
- Dentro de los paréntesis, se definen las columnas del data frame. Cada columna se asigna con un `nombre_columna = vector_de_datos`.
- `c(dato, dato, dato)` es la forma de crear un vector en R, donde `dato` representa los valores que quieres almacenar en esa columna.
- Puedes agregar tantas columnas como necesites, separándolas por comas.
- `nuevo_conjunto` es el nombre que le asignas a tu data frame recién creado.
- `print(nuevo_conjunto)` simplemente imprime el contenido del data frame en la consola.

#### EJEMPLO DE DATA FRAME:
```R
# Crear el DataFrame con valores de ejemplo
df <- data.frame(
  nombre = c('Juan', 'María', 'Pedro', 'Ana', 'Luis'),
  edad = c(25, 32, 45, 28, 34),
  ciudad = c('Madrid', 'Barcelona', 'Valencia', 'Sevilla', 'Bilbao'),
  salario = c(30000, 40000, 50000, 35000, 45000)
)

# Mostrar el DataFrame completo
print("DataFrame completo:")
print(df)

# Seleccionar las filas donde la edad es mayor a 30 años
df_mayor_30 <- df[df$edad > 30, ]

# Mostrar las filas seleccionadas
print("Filas donde la edad es mayor a 30 años:")
print(df_mayor_30)

# Ordenar el DataFrame por la columna "salario" de forma descendente
df_ordenado <- df[order(-df$salario), ]

# Mostrar el DataFrame ordenado
print("DataFrame ordenado por salario de forma descendente:")
print(df_ordenado)

# Calcular el salario promedio
salario_promedio <- mean(df$salario)

# Calcular la desviación estándar del salario
desviacion_estandar <- sd(df$salario)

# Mostrar los resultados
print(paste("Salario promedio:", salario_promedio))
print(paste("Desviación estándar del salario:", desviacion_estandar))
```

#### INGRESAR UNA VARIABLE (Input a usuario)

```R
variable <- readline(prompt = "Texto que debe mostrar al usuario: ")
```

- `readline` es la línea que debe leer R para crear la variable.
- `prompt` es la entrada que recibe el usuario.

#### TIPOS DE CONVERSIONES DE VARIABLES

```r
# Ejemplo de conversiones de entrada en R

# 1. Cadena de texto (character)
texto <- readline(prompt = "Ingresa un texto: ")
cat("Texto ingresado:", texto, "\n")

# 2. Número entero (integer)
entero <- as.integer(readline(prompt = "Ingresa un número entero: "))
cat("Número entero ingresado:", entero, "\n")

# 3. Número de punto flotante (numeric)
flotante <- as.numeric(readline(prompt = "Ingresa un número decimal: "))
cat("Número decimal ingresado:", flotante, "\n")

# 4. Valor lógico (logical)
entrada_logico <- readline(prompt = "Ingresa un valor (true/false): ")
logico <- tolower(entrada_logico) %in% c("true", "1", "yes")
cat("Valor lógico ingresado:", logico, "\n")

# 5. Fecha (Date)
fecha <- as.Date(readline(prompt = "Ingresa una fecha (YYYY-MM-DD): "), format = "%Y-%m-%d")
cat("Fecha ingresada:", fecha, "\n")

# 6. Factor
categoria <- readline(prompt = "Ingresa una categoría: ")
factor_variable <- factor(categoria)
cat("Categoría como factor:", factor_variable, "\n")

# 7. Lista
cadena_lista <- readline(prompt = "Ingresa valores separados por comas: ")
lista <- strsplit(cadena_lista, ",")[[1]]
cat("Lista de valores ingresados:", paste(lista, collapse = ", "), "\n")

# 8. Matriz
cadena_matriz <- readline(prompt = "Ingresa valores separados por comas para una fila: ")
valores_matriz <- as.numeric(strsplit(cadena_matriz, ",")[[1]])
matriz <- matrix(valores_matriz, nrow = 1)
cat("Matriz de valores ingresados:\n")
print(matriz)
```
## EXTRAER ELEMENTOS 

#### MÉTODO SLICING O SUBSET:
```R
objeto[índices]
```

- objeto: es el vector, lista, matriz, data frame, etc. del que quieres extraer elementos.
- índices: especifica qué elementos quieres. Puede ser uno o una secuencia de índices numéricos, nombres (para listas y data frames), o una expresión lógica.

#### EJEMPLOS DE SLICING:
```R
mi_vector <- c(1, 2, 3, 4, 5)
mi_vector[2]  # Devuelve 2
mi_vector[c(1, 3, 5)]  # Devuelve 1 3 5

mi_df <- data.frame(nombre=c("Ana", "Juan", "Pedro"), edad=c(25, 32, 18))
mi_df[2, ]  # Devuelve la segunda fila
mi_df[mi_df$edad > 25, ]  # Filas donde edad > 25
````

#### MÉTODO CON OPERADOR `$` :
```R
dataframe$nombre_columna
```

Esta sintaxis sólo se puede usar con data frames para acceder a columnas por su nombre.
Es simplemente una forma abreviada y más concisa de extraer columnas de un data frame por su nombre, en lugar de usar los corchetes `[ ]`.

#### EJEMPLOS DE `$`:
```R
mi_df <- data.frame(nombre=c("Ana", "Juan", "Pedro"), edad=c(25, 32, 18))
mi_df$nombre  # Devuelve la columna "nombre"
mi_df$edad  # Devuelve la columna "edad"
```

Cada método tiene su propia sintaxis específica. Los corchetes `[ ]` son más generales y flexibles, mientras que el operador `$` es una forma abreviada para acceder a columnas de data frames por nombre.
Ambas sintaxis son muy utilizadas en R y es importante conocerlas y saber cuándo aplicar cada una.
Por ejemplo, si tenemos un data frame `df` con columnas "nombre" y "edad":
```R
df <- data.frame(nombre = c("Ana", "Juan", "Pedro"), 
                 edad = c(25, 32, 18))

#Usando corchetes:
df[, "nombre"]

#Usando $:
df$nombre
```

## CONTROL DE FLUJOS Y CONDICIONALES

#### CONDICIONAL `if`:
```R
if (condición) {
  # Código a ejecutar si la condición es TRUE
} else if (otra_condición) {
  # Código a ejecutar si la primera condición es FALSE y la otra_condición es TRUE
} else {
  # Código a ejecutar si todas las condiciones anteriores son FALSE
}
```

- `condición` y `otra_condición` son expresiones lógicas (TRUE o FALSE) que determinan qué bloque de código se ejecutará.
- Las llaves `{ }` encierran el código que se ejecutará si la condición correspondiente es TRUE.
- La cláusula `else if` es opcional y puedes tener tantas como necesites.
- La cláusula `else` final es también opcional y se ejecutará si todas las condiciones anteriores son FALSE.

#### EJEMPLOS DE `if`:
```R
# Ejemplo 1
x <- 5
if (x > 0) {
  print("x es positivo")
} else {
  print("x es negativo o cero")
}

# Ejemplo 2
edad <- 18
if (edad < 18) {
  print("Eres menor de edad")
} else if (edad >= 18 & edad <= 65) {
  print("Eres adulto")
} else {
  print("Eres de la tercera edad")
}
```

#### CONDICIONAL `ifelse`:
```R
resultado <- ifelse(condición, valor_si_verdadero, valor_si_falso)
```
 Es una forma más compacta de escribir condicionales `if` en R
 Esta construcción evalúa la `condición` y devuelve `valor_si_verdadero` si la condición es TRUE, o `valor_si_falso` en caso contrario.

#### BUCLE `for`:
```R
for (valor in vector) {
  # Código a ejecutar en cada iteración
}
```

- `valor` es el nombre de la variable que tomará los valores del `vector` en cada iteración.
- `vector` es un objeto iterable, como un vector numérico, un vector de caracteres, una lista, etc.
- Las llaves `{ }` encierran el código que se ejecutará en cada iteración del bucle.

#### EJEMPLOS DE `for`:
```R
# Imprimir los números del 1 al 5
for (i in 1:5) {
  print(i)
}

# Salida:
# [1] 1
# [1] 2
# [1] 3
# [1] 4
# [1] 5

#También se puede iterar desde un vector

frutas <- c("manzana", "naranja", "plátano")

for (fruta in frutas) {
  print(paste("Me gusta la", fruta))
}

# Salida:
# [1] "Me gusta la manzana"
# [1] "Me gusta la naranja" 
# [1] "Me gusta la plátano"

# Puedes anidar bucles `for` dentro de otros bucles `for` para iterar sobre múltiples estructuras de datos:

matriz <- matrix(1:9, nrow = 3)

for (fila in 1:nrow(matriz)) {
  for (columna in 1:ncol(matriz)) {
    print(matriz[fila, columna])
  }
}
```

#### FUNCION `seq()` para bucle `for`:
```R
seq(inicio,fin,paso)

for (i in seq(inicio,fin,paso))
```

En R, no hay una sintaxis tan directa como en Python para iterar sobre un rango de números con un paso específico. La función `seq(from, to, by)` genera una secuencia de números desde `from` hasta `to` con un incremento de `by`.

#### EJEMPLO DE  `seq()`:
```R
for (i in seq(1, 10, by = 2)) {
  print(i)
}
```

#### BUCLE `while`:
```R
while (condición) {
  # Código a ejecutar mientras la condición sea TRUE
}
```

- `condición` es una expresión lógica que se evalúa antes de cada iteración del bucle.
- Las llaves `{ }` encierran el código que se ejecutará repetidamente mientras la `condición` sea `TRUE`.

El bucle `while` se utiliza cuando no se conoce de antemano el número de iteraciones necesarias, sino que depende de una condición que se debe cumplir.

#### EJEMPLOS DE `while`:
```R
# Imprimir los números del 1 al 5
i <- 1
while (i <= 5) {
  print(i)
  i <- i + 1  # Incrementar el contador
}

# Salida:
# [1] 1
# [1] 2
# [1] 3
# [1] 4
# [1] 5

# Calcular la suma de los números del 1 al 10
suma <- 0
i <- 1
while (i <= 10) {
  suma <- suma + i
  i <- i + 1
}
print(suma)

# Salida:
# [1] 55
```

Es importante asegurarse de que la condición del bucle `while` eventualmente se vuelva `FALSE`, de lo contrario, se producirá un bucle infinito que puede bloquear o agotar los recursos del sistema.

En general, se recomienda utilizar el bucle `for` cuando se conoce de antemano el número de iteraciones necesarias, y el bucle `while` cuando se debe repetir un bloque de código hasta que se cumpla una determinada condición.

## FUNCIONES EN R

#### SINTAXIS PARA CREAR FUNCIONES EN R:
```R
nombre_funcion <- function(argumento1, argumento2, ...) {
  # Código de la función
  ...
  return(valor_a_retornar)
}
```

- `nombre_funcion` es el nombre que le das a tu función.
- `function` es la palabra clave que indica que estás definiendo una función.
- `argumento1`, `argumento2`, etc. son los parámetros o argumentos que recibirá la función. Son opcionales, puedes tener tantos como necesites o ninguno.
- Las llaves `{ }` encierran el código que se ejecutará cuando se llame a la función.
- `return(valor_a_retornar)` es la instrucción que especifica el valor que devolverá la función. Es opcional si la función no necesita devolver un valor.

#### EJEMPLO DE FUNCIONES:
```R
# Función que calcula el área de un rectángulo
calc_area_rectangulo <- function(base, altura) {
  area <- base * altura
  return(area)
}

# Llamar a la función
resultado <- calc_area_rectangulo(5, 3)
print(resultado)  # Salida: 15
```

En este ejemplo, definimos una función llamada `calc_area_rectangulo` que toma dos argumentos `base` y `altura`, calcula el área de un rectángulo y devuelve el resultado.

```R
# Función que imprime un saludo
saludar <- function(nombre) {
  mensaje <- paste("Hola", nombre, "!")
  print(mensaje)
}

# Llamar a la función
saludar("Juan")  # Salida: "Hola Juan!"
```

Aquí, la función `saludar` recibe un argumento `nombre`, construye un mensaje de saludo y lo imprime en la consola.

```R

# Función que calcula el factorial de número pedido al usuario
n <- as.integer(readline(prompt = "Ingrese un número entero no negativo: "))

factorial_func <- function(n) {
  if (n < 0) {
    stop("El factorial no está definido para números negativos")
  } else if (n == 0) {
    return(1)
  } else {
    fact <- 1
    for (i in 1:n) {
      fact <- fact * i
    }
    return(fact)
  }
}

factorial_n <- factorial_func(n)

cat("El factorial de", n, "es:", factorial_n)
```
Las funciones en R pueden tener argumentos opcionales con valores predeterminados, utilizar la recursividad, y mucho más. Son fundamentales para escribir código modular y reutilizable.
## IMPORTAR DATOS

#### LEER DIVERSAS FUENTES:
```R
variable <- read.funcion_según_tipo(archivo)
```

#### EJEMPLOS DE DIVERSOS FORMATOS:
```R
# Leer archivo CSV
datos <- read.csv("nombre_archivo.csv")

# Leer archivo Excel
library(readxl)
datos <- read_excel("nombre_archivo.xlsx")

# Leer archivo de texto
datos <- read.table("nombre_archivo.txt", header = TRUE, sep = ",")
```

## EXPORTAR DATOS

#### ESCRIBIR DIVERSAS FUENTES:
```R
write.función_según_tipo(archivo)
```

#### EJEMPLOS DE DIVERSOS FORMATOS:
```R
# Para archivos CSV:
write.csv(datos, "archivo.csv", row.names = FALSE)

# Para archivos de Excel:
library(writexl)
write_xlsx(datos, "archivo.xlsx")

# Para archivos RDS (formato nativo de R):
saveRDS(datos, "archivo.rds")

# Para archivos de texto:
write.table(datos, "archivo.txt", sep = "\t", row.names = FALSE)

# Para archivos SPSS:
library(haven)
write_sav(datos, "archivo.sav")
```

## MANIPULANDO DATOS CON DPLYR:

#### FILTER:
```R
filter(dataframe, condición)

# Con pipe
dataframe %>% filter(condición)

# Ejemplo
filter(datos_personales, edad < 30)

# Para crear una nueva variable
menores_de_30 <- datos_personales %>% 
filter(edad < 30)
```

Puedes combinar múltiples condiciones en `filter()` usando operadores lógicos como `&` (y) o `|` (o).

#### SELECT:
```R
select(dataframe, columna1, columna2, ...)

# Con pipe
dataframe %>% select(columna1, columna2, ...)

# Ejemplo
select(datos_personales, nombre, salario)

# Para crear una nueva variable
nombre_salario <- datos_personales %>% 
select(nombre, salario)
```

En `select()`, puedes usar `-` para excluir columnas.

#### RENAME:
```R
rename(dataframe, nuevo_nombre = viejo_nombre)

# Con pipe
dataframe %>% rename(nuevo_nombre = viejo_nombre)

# Renombrar la columna 'salario' a 'sueldo'
datos_personales %>%
  rename(sueldo = salario)
```

Renombra columnas en un dataframe.

#### MUTATE:
```R
mutate(dataframe, nueva_columna = expresión)

# Con pipe
dataframe %>% mutate(nueva_columna = expresión)

# Ejemplo
mutate(datos_personales, edad_en_cinco_años = edad + 5)

# Para crear una nueva variable
edad_en_5_años <- datos_personales %>% 
select(nombre, edad) %>% 
mutate(edad_en_cinco_años = edad + 5)
```

`mutate()` puede crear múltiples columnas en una sola llamada.

#### SUMMARIZE/SUMMARISE:
```R
summarize(dataframe, nueva_columna = función_resumen())

# Con pipe
dataframe %>% summarize(nueva_columna = función_resumen())

# Ejemplo sin pipe
summarise(group_by(datos_personales,ciudad),promedio_edad = mean(edad))

# Ejemplo con pipe
datos_personales %>% 
group_by(ciudad) %>%
summarise(promedio_edad = mean(edad))

# Para crear una nueva variable
promedio_edades <- summarise(group_by(datos_personales,ciudad),promedio_edad = mean(edad))

```

`summarize()` se usa a menudo con `group_by()` para cálculos por grupo.

#### ARRANGE:
```R
arrange(dataframe, columna)

# Con pipe
dataframe %>% arrange(columna)

# Ejemplo
arrange(datos_personales, salario)
```

`arrange()` ordena de forma ascendente por defecto. Usa `desc()` para orden descendente.

#### GROUP_BY:
```R
group_by(dataframe, columna)

# Con pipe
dataframe %>% group_by(columna)

# Agrupar por ciudad y calcular el salario promedio
datos_personales %>%
  group_by(ciudad) %>%
  summarise(salario_promedio = mean(salario))
```

Esta función agrupa el dataframe por una o más variables, lo que es útil para realizar operaciones por grupo.

#### JOIN:
```R
left_join(x, y, by = "columna_clave")

# Con pipe
x %>% left_join(y, by = "columna_clave")

# Primero, creemos un nuevo dataframe con información adicional
info_adicional <- data.frame(
  nombre = c("Juan Altamirano", "Pedro Henriquez", "Antonia Bravo"),
  departamento = c("Ventas", "Marketing", "Finanzas")
)

# Ahora, unimos este nuevo dataframe con datos_personales
datos_personales %>%
  left_join(info_adicional, by = "nombre")
```

Estas funciones combinan dos dataframes basándose en una columna clave común.

#### SLICE:
```R
slice(dataframe, n:m)

# Con pipe
dataframe %>% slice(n:m)

# Seleccionar las primeras 3 filas del dataframe
datos_personales %>%
  slice(1:3)
```

Selecciona filas por su posición.

#### DISTINCT:
```R
distinct(dataframe, columna1, columna2, ...)

# Con pipe
dataframe %>% distinct(columna1, columna2, ...)

# Obtener las ciudades únicas
datos_personales %>%
  distinct(ciudad)
```

Elimina filas duplicadas basándose en las columnas especificadas.


#### EJEMPLOS ADICIONALES DE FUNCIONES COMBIANADAS:
```R
# Encontrar el empleado más joven de cada ciudad
datos_personales %>%
  group_by(ciudad) %>%
  slice(which.min(edad))

# Calcular el salario promedio por ciudad, solo para personas mayores de 30 años
datos_personales %>%
  filter(edad > 30) %>%
  group_by(ciudad) %>%
  summarise(salario_promedio = mean(salario))

# Renombrar columnas y seleccionar solo algunas
datos_personales %>%
  rename(nombre_completo = nombre, sueldo = salario) %>%
  select(nombre_completo, sueldo, ciudad)
```

#### IMPORTANCIA DEL PIPE (`%>`):
En ambos casos (con y sin pipe) el resultado debería ser exactamente el mismo. La diferencia está en la sintaxis y la legibilidad del código, no en el resultado final.

Por ejemplo:

1. Sin pipe:
```R
filter(datos_personales, edad < 30)
```

2. Con pipe:
```R
datos_personales %>% filter(edad < 30)
```

Ambas expresiones producirán el mismo resultado: un dataframe filtrado con las personas menores de 30 años.

La principal ventaja del pipe es que permite encadenar múltiples operaciones de una manera que muchos consideran más legible y fácil de seguir, especialmente cuando se realizan varias operaciones consecutivas. Por ejemplo:

```R
datos_personales %>%
  filter(edad < 30) %>%
  select(nombre, salario) %>%
  arrange(salario)
```

Este código es equivalente a:

```R
arrange(select(filter(datos_personales, edad < 30), nombre, salario), salario)
```

Ambos producen el mismo resultado, pero muchos encuentran la versión con pipe más fácil de leer y entender.

En resumen, el uso del pipe es una cuestión de estilo y preferencia en la escritura del código, pero no afecta el resultado final de las operaciones. Es una herramienta que facilita la lectura y escritura de código, especialmente cuando se realizan múltiples operaciones consecutivas sobre un conjunto de datos.

## MANIPULANDO DATOS CON TIDYR:

**PIVOT_LONGER:**
```R
pivot_longer(data, cols, names_to, values_to)

# Ejemplo de pivot_longer
data <- data.frame(
  id = 1:3,
  var1_2020 = c(10, 15, 20),
  var1_2021 = c(12, 18, 22),
  var2_2020 = c(25, 30, 35),
  var2_2021 = c(28, 32, 38)
)

data_long <- pivot_longer(data, cols = starts_with("var"), 
                          names_to = c(".value", "year"), 
                          names_pattern = "(var\\d+)_(\\d+)")
print(data_long)

```

Convierte datos de formato ancho a formato largo.

**GATHER:**
```R
gather(data, key, value, ..., na.rm = FALSE, convert = FALSE)

# Ejemplo de gather
data <- data.frame(
  id = 1:3,
  var1_2020 = c(10, 15, 20),
  var1_2021 = c(12, 18, 22),
  var2_2020 = c(25, 30, 35),
  var2_2021 = c(28, 32, 38)
)

data_gathered <- gather(data, key = "variable", value = "value", -id)
print(data_gathered)

```

Se usa para convertir datos de formato ancho a formato largo, donde `key` especifica el nombre de la columna para las claves y `value` especifica el nombre de la columna para los valores.

**PIVOT_WIDER:**
```R
pivot_wider(data, names_from, values_from)

# Ejemplo de pivot_wider
data_wide <- pivot_wider(data_long, names_from = year, values_from = value)
print(data_wide)

```

Convierte datos de formato largo a formato ancho.

**SPREAD:**
```R
spread(data, key, value, fill = NA)

# Ejemplo de spread
data <- data.frame(
  id = c(1, 2, 3, 1, 2, 3),
  variable = c("var1", "var1", "var1", "var2", "var2", "var2"),
  value = c(10, 15, 20, 25, 30, 35)
)

data_spread <- spread(data, key = variable, value = value)
print(data_spread)

```

Se usa para convertir datos de formato largo a formato ancho, donde `key` especifica la columna que contiene los nombres de las nuevas columnas y `value` especifica la columna que contiene los valores para esas columnas.

**SEPARATE:**
```R
separate(data, col, into, sep, remove = TRUE)

# Ejemplo de separate
data <- data.frame(
  col1 = c("A_1", "B_2", "C_3"),
  col2 = c("X_4", "Y_5", "Z_6")
)

data_sep <- separate(data, col = col1, into = c("letter", "number"), sep = "_")
print(data_sep)
```

Divide una columna en varias columnas.

**UNITE:**
```R
unite(data, col, ..., sep = "_", remove = TRUE)

# Ejemplo de unite
data <- data.frame(
  letter = c("A", "B", "C"),
  number = c(1, 2, 3)
)

data_unite <- unite(data, col = "combined", letter, number, sep = "_")
print(data_unite)

```

Une varias columnas en una sola.

**DROP_NA:**
```R
drop_na(data, ...)

# Ejemplo de drop_na
data <- data.frame(
  col1 = c(1, NA, 3),
  col2 = c("A", "B", NA)
)

data_drop <- drop_na(data)
print(data_drop)

```

Elimina filas con valores faltantes.

**REPLACE_NA:**
```R
replace_na(data, replace = list(...))

# Ejemplo de replace_na
data <- data.frame(
  col1 = c(1, NA, 3),
  col2 = c("A", "B", NA)
)

data_replace <- replace_na(data, replace = list(col1 = 0, col2 = "N/A"))
print(data_replace)

```

Reemplaza valores faltantes con un valor específico.

**FILL:**
```R
fill(data, ..., .direction = c("down", "up"))

# Ejemplo de fill
data <- data.frame(
  col1 = c(1, NA, NA, 4),
  col2 = c("A", "B", NA, "D")
)

data_fill <- fill(data, col1, .direction = "down")
print(data_fill)

```

Rellena valores faltantes con el valor previo o siguiente en una columna.

**SEPARATE_ROWS:**
```R
separate_rows(data, ..., sep = "[^[:alnum:]]+")

# Ejemplo de separate_rows
data <- data.frame(
  id = 1:3,
  categories = c("A,B,C", "D,E", "F")
)

data_separate <- separate_rows(data, categories, sep = ",")
print(data_separate)

```

Divide filas que contienen valores separados por comas u otros delimitadores en múltiples filas.

**DROP_DUPLICATES:**
```R
drop_duplicates(data)

# Ejemplo de drop_duplicates 
data <- data.frame( id = c(1, 2, 3, 1, 2), value = c("A", "B", "C", "A", "B") ) data_unique <- drop_duplicates(data) 
print(data_unique)
```

Elimina filas duplicadas de un dataframe.

**NESTING:**
```R
nesting(data)

# Ejemplo de nesting
data <- data.frame(
  id = 1:2,
  values = list(c(1, 2, 3), c("A", "B"))
)

data_nested <- nesting(data)
print(data_nested)

```

Una función útil cuando se trabaja con datos anidados o listas dentro de columnas.

## TYDYR Y DPLYR

`tidyr` y `dplyr` son dos paquetes fundamentales dentro del conjunto `tidyverse` de herramientas para manipulación y análisis de datos en R. Las características principales de cada uno y la secuencia recomendada para su uso:

### Características y diferencias entre `tidyr` y `dplyr`:

#### `tidyr`:
- **Reestructuración de datos**: Se especializa en la reorganización y transformación de la estructura de los datos.
- **Funciones clave**: `pivot_longer`, `pivot_wider`, `gather`, `spread`, `separate`, `unite`.
- **Trabajo con datos largos y anchos**: Facilita la conversión entre formatos de datos anchos y largos.
- **Limpieza de datos**: Ayuda a manejar datos desordenados o que necesitan ser reorganizados para un análisis más efectivo.
- **Preparación para análisis**: Ideal para preparar datos para análisis posteriores con `dplyr`.

#### `dplyr`:
- **Manipulación de datos**: Se centra en la manipulación, filtrado, agregación y transformación de datos.
- **Funciones clave**: `filter`, `select`, `mutate`, `summarize`, `arrange`, `group_by`, `join`.
- **Operaciones por grupo**: Permite realizar operaciones estadísticas y de resumen por grupos de datos.
- **Selección y renombrado de columnas**: Facilita la selección de columnas específicas y el renombrado de estas.
- **Integración con `tidyr`**: Combinando con `tidyr`, se logra una manipulación y preparación completa de datos antes del análisis.

### Secuencia recomendada de uso:

1. **`tidyr`**: Es recomendable usar `tidyr` primero cuando necesitas reestructurar la forma en que los datos están organizados. Por ejemplo, si tienes datos en formato ancho que necesitas convertir a formato largo (o viceversa), `tidyr` es la elección adecuada.

2. **`dplyr`**: Una vez que los datos están en el formato adecuado (gracias a `tidyr`), puedes usar `dplyr` para realizar operaciones más avanzadas de manipulación y análisis. Esto incluye filtrar filas, seleccionar columnas específicas, crear nuevas variables (`mutate`), agrupar datos para cálculos por grupo (`group_by` y `summarize`), ordenar filas (`arrange`) y combinar datasets (`join`).

### Integración y flujo de trabajo:

- **Integración**: Ambos paquetes están diseñados para trabajar bien juntos. `tidyr` te ayuda a preparar y limpiar los datos, mientras que `dplyr` te permite realizar análisis y manipulación detallada después de la preparación inicial.
  
- **Flujo de trabajo**: Por lo tanto, el flujo de trabajo típico implicaría comenzar con `tidyr` para preparar y reestructurar los datos según sea necesario, y luego pasar a `dplyr` para realizar análisis más específicos y detallados.

En resumen, `tidyr` y `dplyr` son complementarios en el flujo de trabajo de análisis de datos en R, donde `tidyr` se usa principalmente para la preparación inicial y reestructuración de datos, seguido por `dplyr` para manipulaciones más avanzadas y análisis detallados.
## GRAFICAR DATOS

### USANDO RBASE

En R base, el enfoque para crear gráficos es diferente y generalmente menos modular comparado con `ggplot2`.

**ORDEN TÍPICO DE LAS CAPAS CON RBASE:**

1. **Preparar los datos**:
   - Prepara y limpia tus datos antes de graficar. Este paso no es una capa del gráfico, pero es fundamental.

2. **Abrir el dispositivo gráfico** (opcional):
   - Si necesitas guardar el gráfico en un archivo, abre el dispositivo gráfico con funciones como `png()`, `jpeg()`, `pdf()`, etc.

3. **Crear el gráfico principal**:
   - Usa funciones como `plot()`, `barplot()`, `pie()`, etc., para crear el gráfico principal.

4. **Añadir elementos adicionales**:
   - Usa funciones como `points()`, `lines()`, `text()`, `legend()`, etc., para añadir elementos adicionales al gráfico.

5. **Cerrar el dispositivo gráfico** (opcional):
   - Si abriste un dispositivo gráfico para guardar el gráfico, ciérralo con `dev.off()`.

#### Ejemplo con diferentes tipos de gráficos en R base

#### Gráfico de puntos

```r
# Datos de ejemplo
x <- 1:10
y <- rnorm(10)

# Crear el gráfico principal
plot(x, y, main = "Gráfico de Puntos", xlab = "Eje X", ylab = "Eje Y", pch = 19, col = "blue")

# Añadir una línea
lines(x, y, col = "red")

# Añadir una leyenda
legend("topright", legend = c("Puntos", "Línea"), col = c("blue", "red"), pch = c(19, NA), lty = c(NA, 1))
```

#### Gráfico de barras

```r
# Datos de ejemplo
valores <- c(5, 10, 15, 20)
nombres <- c("A", "B", "C", "D")

# Crear el gráfico de barras
barplot(valores, names.arg = nombres, main = "Gráfico de Barras", col = "lightblue")

# Añadir etiquetas a las barras
text(x = seq_along(valores), y = valores, label = valores, pos = 3, cex = 0.8, col = "red")
```

#### Gráfico circular

```r
# Datos de ejemplo
categorias <- c("A", "B", "C", "D")
valores <- c(40, 30, 20, 10)

# Crear el gráfico circular
pie(valores, labels = paste0(categorias, " - ", valores, "%"), main = "Gráfico Circular", col = rainbow(length(valores)))
```

### Gráfico de caja (boxplot)

```R
# Sintaxis general para un box plot con rbase
boxplot(numeric_variable ~ factor_variable, data = dataframe,
        main = "Título del Gráfico",
        xlab = "Etiqueta del Eje X",
        ylab = "Etiqueta del Eje Y")

# Crear el grafico usando el db "iris"

boxplot(Sepal.Length ~ Species, data = iris, main = "Box Plot de Sepal Length por Species", xlab = "Species", ylab = "Sepal Length")
```

#### Gráfico de violín

```R
# Instalar y cargar el paquete vioplot
install.packages("vioplot")
library(vioplot)

# Sintaxis general para un violin plot con rbase
vioplot(numeric_variable ~ factor_variable, data = dataframe,
        main = "Título del Gráfico",
        xlab = "Etiqueta del Eje X",
        ylab = "Etiqueta del Eje Y")

# Crear el gráfico usando el db "iris"

vioplot(Sepal.Length ~ Species, data = iris,
        main = "Violin Plot de Sepal Length por Species",
        xlab = "Species",
        ylab = "Sepal Length")

```

#### Grafico de densidad

```R
# Sintaxis general para un gráfico de densidad con rbase
plot(density(dataframe$numeric_variable[dataframe$factor_variable == "nivel1"]),
     main = "Título del Gráfico",
     xlab = "Etiqueta del Eje X",
     ylab = "Densidad",
     col = "color1")
lines(density(dataframe$numeric_variable[dataframe$factor_variable == "nivel2"]),
      col = "color2")
lines(density(dataframe$numeric_variable[dataframe$factor_variable == "nivel3"]),
      col = "color3")
legend("topright", legend = c("nivel1", "nivel2", "nivel3"), col = c("color1", "color2", "color3"), lty = 1)

# Crear el grafico usando el db "iris"

plot(density(iris$Sepal.Length[iris$Species == "setosa"]),
     main = "Gráfico de Densidad de Sepal Length por Species",
     xlab = "Sepal Length",
     ylab = "Densidad",
     col = "red")
lines(density(iris$Sepal.Length[iris$Species == "versicolor"]),
      col = "green")
lines(density(iris$Sepal.Length[iris$Species == "virginica"]),
      col = "blue")
legend("topright", legend = levels(iris$Species), col = c("red", "green", "blue"), lty = 1)

```
#### Resumen del orden de las capas en R base

1. **Preparar los datos**.
2. **Abrir el dispositivo gráfico (opcional)**.
3. **Crear el gráfico principal** usando funciones como `plot()`, `barplot()`, `pie()`, etc.
4. **Añadir elementos adicionales** como puntos, líneas, texto, leyendas, etc.
5. **Cerrar el dispositivo gráfico (opcional)**.

Este enfoque proporciona una estructura para crear gráficos en R base, permitiendo añadir múltiples elementos y personalizar el gráfico en cada paso.
### USUANDO GGPLOT

#### ORDEN DE LAS CAPAS

En `ggplot2`, el orden de las capas es importante y puede afectar cómo se renderiza el gráfico. Aquí te explico el orden típico de las capas en `ggplot2` y cómo se construyen:

1. **Cargar el paquete y los datos**:
   - Primero, carga `ggplot2` y tus datos. Este paso no es una capa en el gráfico, pero es fundamental para preparar el entorno.

2. **Inicializar el gráfico con `ggplot()`**:
   - Esta función establece el marco del gráfico y define los mapeos estéticos globales que se aplicarán a todas las capas subsiguientes.

3. **Agregar capas geométricas (`geom_*`)**:
   - Las capas geométricas (`geom_*`) definen qué tipo de gráfico se dibuja, como puntos, líneas, barras, etc. Estas capas pueden incluir mapeos estéticos locales si es necesario.

4. **Transformaciones estadísticas (`stat_*`)** (si es necesario):
   - Las transformaciones estadísticas aplican cálculos a los datos antes de que se dibuje la geometría. A menudo, esto se combina directamente en las capas geométricas, pero puede ser explícito.

5. **Ajustes de coordenadas (`coord_*`)**:
   - Los ajustes de coordenadas transforman el sistema de coordenadas del gráfico, como `coord_flip()` para girar los ejes o `coord_polar()` para gráficos circulares.

6. **Escalas (`scale_*`)**:
   - Las escalas controlan cómo se mapean los datos a las propiedades estéticas del gráfico, como colores, tamaños, y etiquetas de los ejes.

7. **Facetas (`facet_*`)**:
   - Las facetas permiten dividir el gráfico en múltiples paneles según las variables de los datos.

8. **Temas (`theme_*`) y etiquetas**:
   - Los temas y etiquetas personalizan la apariencia del gráfico, incluyendo títulos, etiquetas de ejes, leyendas, y otros elementos estéticos.

```r
# Cargar el paquete ggplot2
library(ggplot2)

# Datos de ejemplo
datos <- data.frame(variable_x = 1:10, variable_y = rnorm(10), grupo = rep(letters[1:2], each = 5))

# Crear el gráfico
ggplot(datos, aes(x = variable_x, y = variable_y, color = grupo)) +  # Inicializar el gráfico y mapeos estéticos globales
  geom_point() +  # Agregar capa geométrica de puntos
  geom_line() +  # Agregar capa geométrica de líneas
  stat_smooth(method = "lm") +  # Agregar transformación estadística (opcional)
  coord_cartesian() +  # Ajustes de coordenadas (opcional)
  scale_color_manual(values = c("red", "blue")) +  # Ajustes de escalas (opcional)
  facet_wrap(~ grupo) +  # Agregar facetas (opcional)
  theme_minimal() +  # Aplicar tema
  labs(title = "Título del gráfico", x = "Etiqueta del eje X", y = "Etiqueta del eje Y")  # Etiquetas
```


1. Inicializar el gráfico con `ggplot()` y `aes()` globales.
2. Agregar capas geométricas (`geom_*`).
3. Aplicar transformaciones estadísticas (`stat_*`) si es necesario.
4. Ajustar coordenadas (`coord_*`).
5. Definir escalas (`scale_*`).
6. Agregar facetas (`facet_*`).
7. Personalizar con temas (`theme_*`) y etiquetas (`labs()`).

Este orden ayuda a estructurar y entender mejor cómo se construyen los gráficos en `ggplot2`.

#### DOS SINTAXIS DE ELABORACION

```R
# Dentro de ggplot
ggplot(datos, aes(x = variable_x, y = variable_y))

# Dentro de geom_*
ggplot(datos) + 
  geom_punto(aes(x = variable_x, y = variable_y))
```
La primera forma es más común y recomendada, ya que los mapeos estéticos se establecen a nivel del gráfico completo. La segunda forma es útil cuando se necesita especificar mapeos diferentes para cada capa geométrica.
Algunas razones por las que algunos usuarios prefieren separar `aes()`  de `ggplot()` son:

Claridad: Separa la especificación de datos de los mapeos estéticos, lo que puede hacer que el código sea más legible y fácil de mantener.
Flexibilidad: Permite anular o agregar mapeos estéticos por capa geométrica, lo que puede ser útil en ciertos casos.
Herencia: Cuando se usa `aes()` dentro de `geom_*()`, los mapeos estéticos heredan los mapeos globales establecidos en `ggplot()`, lo que puede ser conveniente.
Estilo personal o de equipo: Algunos equipos o desarrolladores prefieren este estilo por convención.

#### ESPECIFICANDO `aes()` DENTRO DE `ggplot()`

```R
# Cargar el paquete ggplot2
library(ggplot2)

# Crear un gráfico básico de puntos
ggplot(datos, aes(x = variable_x, y = variable_y)) +
  geom_point()

# Gráfico de líneas con color por grupo
ggplot(datos, aes(x = variable_x, y = variable_y, color = grupo)) +
  geom_line()

# Gráfico de barras apiladas
ggplot(datos, aes(x = variable_x, y = variable_y, fill = grupo)) +
  geom_bar(stat = "identity", position = "stack")

# Gráfico circular
ggplot(datos, aes(x = "", y = variable_y, fill = grupo)) + 
	geom_bar(stat = "identity", width = 1) +                                           coord_polar("y", start = 0) +                                                      theme_void() +                                                                     ggtitle("Título del gráfico") +                                                    geom_text(aes(label = paste0(variable_y, "%")), position =position_stack(vjust = 0.5))

# Gráfico de caja
ggplot(data, aes(x = factor_variable, y = numeric_variable)) +
  geom_boxplot() +
  theme_minimal() +
  labs(title = "Título del Gráfico", x = "Etiqueta del Eje X", y = "Etiqueta del Eje Y")

# Gráfico de violin
ggplot(data, aes(x = factor_variable, y = numeric_variable)) +
  geom_violin(trim = FALSE) +
  theme_minimal() +
  labs(title = "Título del Gráfico", x = "Etiqueta del Eje X", y = "Etiqueta del Eje Y")

# Gráfico de densidad
ggplot(data, aes(x = numeric_variable, fill = factor_variable)) +
  geom_density(alpha = 0.5) +
  theme_minimal() +
  labs(title = "Título del Gráfico", x = "Etiqueta del Eje X", y = "Etiqueta del Eje Y")

```

En este enfoque, los mapeos estéticos se definen dentro de `ggplot()` y se aplican a todas las capas geométricas del gráfico.

#### ESPECIFICANDO `aes()` DENTRO DE `geom_*`:

```R
# Cargar el paquete ggplot2
library(ggplot2)

# Crear un gráfico básico de puntos
ggplot(datos) +
  geom_point(aes(x = variable_x, y = variable_y))

# Gráfico de líneas con color por grupo
ggplot(datos) +
  geom_line(aes(x = variable_x, y = variable_y, color = grupo))

# Gráfico de barras apiladas
ggplot(datos) +
  geom_bar(aes(x = variable_x, y = variable_y, fill = grupo),
           stat = "identity", position = "stack")

# Gráfico circular
ggplot(datos) +                                                         geom_bar(aes(x = "", y = variable_y, fill = grupo), stat = "identity", width = 1) + coord_polar("y", start = 0) + theme_void() + ggtitle("Título del gráfico") + geom_text(aes(label = paste0(variable_y, "%")), position = position_stack(vjust = 0.5))

# Gráfico de caja
ggplot(data)+
geom_boxplot(aes(x = factor_variable, y = numeric_variable)) +
  theme_minimal() +
  labs(title = "Título del Gráfico", x = "Etiqueta del Eje X", y = "Etiqueta del Eje Y")

# Gráfico de violin
ggplot(data)+
geom_violin(aes(x = factor_variable, y = numeric_variable,trim = FALSE)) +
  theme_minimal() +
  labs(title = "Título del Gráfico", x = "Etiqueta del Eje X", y = "Etiqueta del Eje Y")

# Gráfico de densidad
ggplot(data)+
geom_density(aes(x = numeric_variable, fill = factor_variable,alpha = 0.5)) +
  theme_minimal() +
  labs(title = "Título del Gráfico", x = "Etiqueta del Eje X", y = "Etiqueta del Eje Y")
```

En este enfoque, los mapeos estéticos se definen dentro de cada capa geométrica `(geom_*())`. Esto permite anular o agregar mapeos estéticos específicos para cada capa.
Ambas formas producen gráficos idénticos, pero la primera forma `(aes() dentro de ggplot())` es más común y recomendada, a menos que necesites anular o agregar mapeos estéticos por capa geométrica.
Es importante tener en cuenta que al usar `aes()` dentro de `geom_*()`, los mapeos estéticos heredan los mapeos globales establecidos en `ggplot()`. Por ejemplo:
```r 
# Mapeo global en ggplot()
ggplot(datos, aes(x = variable_x, y = variable_y)) +
  geom_point(aes(color = grupo)) # Hereda x y y, agrega mapeo de color
```  
En este caso, `geom_point()` hereda los mapeos x y y de `ggplot()`, y agrega el mapeo de color a grupo.