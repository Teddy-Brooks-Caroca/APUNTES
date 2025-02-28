
### CADENAS:

**Longitud de caracteres:**
```R
nchar(x)

# Devuelve la longitud (número de caracteres) de los elementos de un vector de caracteres.

nchar("Hola mundo") 
#devolverá 10.
```

**Extracción de subcadenas:**
```R
substr(x, start, stop) 

# Extrae subcadenas desde un vector de caracteres, comenzando en la posición `start` y terminando en la posición `stop`.

substr("Programación", 1, 5) 
#devolverá "Progr".
```

**Concatenación de vectores:**
```R
paste(..., sep = " ")
# Concatena vectores después de convertirlos a caracteres.

paste("Hola", "mundo", sep = " ")
#devolverá "Hola mundo".

```

**Convertir a mayúsculas:**
```R
toupper(x)
# Convierte los caracteres en un vector de caracteres a mayúsculas.

toupper("hola mundo") 
#devolverá "HOLA MUNDO".
```

**Convertir a minúsculas:**
```R
tolower(x)
# Convierte los caracteres en un vector de caracteres a minúsculas.

tolower("HOLA MUNDO")
#devolverá "hola mundo".
```

**Sustitución de patrones:**
```R
gsub(pattern, replacement, x)
# Realiza una sustitución de patrones en un vector de caracteres.

gsub("mundo", "R", "Hola mundo")
#devolverá "Hola R".
```

**División de cadenas:**
```R
strsplit(x, split)
# Divide los elementos de un vector de caracteres en substrings.

strsplit("Hola mundo", " ")
#devolverá una lista con dos elementos: "Hola" y "mundo".
```

**Búsqueda de patrones:**
```R
grep(pattern, x)
# Busca coincidencias de un patrón en un vector de caracteres.

grep("mundo", c("Hola mundo", "Adiós mundo"))
#devolverá 1 y 2 (las posiciones donde se encontró "mundo").
```

**Eliminar espacios en blanco:**
```R
trimws(x)
# Elimina los espacios en blanco iniciales y finales de un vector de caracteres.

trimws(" Hola mundo ")
# devolverá "Hola mundo".
```

**Reemplazo de patrones:**
```R
chartr(old, new, x)
# Reemplaza la coincidencia de patrones en un vector de caracteres.

chartr("mundo", "R", "Hola mundo")
# devolverá "Hola R".
```

### AGREGACIÓN:

**Suma de elementos:**
```R
sum(x)
#Suma todos los elementos de un vector.

sum(c(1, 2, 3, 4, 5))
# devolverá 15.
```

**Producto de elementos:**
```R
prod(x)
#Calcula el producto de todos los elementos de un vector.

prod(c(1, 2, 3, 4, 5)) 
# devolverá 120.
```

**Suma acumulativa:**
```R
cumsum(x)
#Devuelve una suma acumulativa de los elementos de un vector.

cumsum(c(1, 2, 3, 4, 5)) 
# devolverá 1, 3, 6, 10, 15.
```

**Producto acumulativo:**
```R
cumprod(x) 
#Devuelve un producto acumulativo de los elementos de un vector.

cumprod(c(1, 2, 3, 4, 5))
# devolverá 1, 2, 6, 24, 120.
```

**Valor mínimo:**
```R
min(x)
# Devuelve el valor mínimo de un vector.

min(c(5, 2, 8, 1, 3))
# devolverá 1.
```

**Valor máximo:**
```R
max(x)
# Devuelve el valor máximo de un vector.

max(c(5, 2, 8, 1, 3))
# devolverá 8.
```

**Rango de valores:**
```R
range(x)
# Devuelve un vector con el valor mínimo y máximo de un vector.

range(c(5, 2, 8, 1, 3))
# devolverá 1 y 8.
```

**Mediana:**
```R
median(x)
# Devuelve la mediana de un vector.

median(c(5, 2, 8, 1, 3))
# devolverá 3.
```

**Cuartil:**
```R
quantile(x, probs)
# Devuelve los cuantiles de un vector.

quantile(c(5, 2, 8, 1, 3), c(0.25, 0.75))
# devolverá 2 y 5.
```

**Any:**
```R
any(x)
# Devuelve `TRUE` si al menos uno de los elementos de un vector es `TRUE`.

any(c(FALSE, FALSE, TRUE, FALSE))
# devolverá `TRUE`.
```

### CONTROL DE FLUJOS Y CONDICIONALES:

**Condicional:**
```R
if(condición) {...} else {...}
# Ejecuta una sección de código si la condición es verdadera, y otra sección si es falsa.

x <- 5; if (x > 0) {print("Positivo")} else {print("Negativo")}`
```

**Bucle `for`:**
```R
for(valor in secuencia) {...}
# Ejecuta un ciclo para cada elemento de una secuencia.

for (i in 1:5) {print(i)}
# imprimirá 1, 2, 3, 4, 5.
```

**Bucle `while`:**
```R
while(condición) {...}
# Ejecuta un ciclo mientras la condición sea verdadera.

x <- 1; while (x <= 5) {print(x); x <- x + 1}
# imprimirá 1, 2, 3, 4, 5.
```

**Bucle infinito:**
```R
repeat {...}
# Ejecuta un ciclo infinito hasta que se encuentre una instrucción `break`.

x <- 1; repeat {print(x); x <- x + 1; if (x > 5) break}
```

**Saltar iteración:**
```R
next: 
# Sale de la iteración actual de un ciclo y continúa con la siguiente iteración.

for (i in 1:10) {if (i %% 2 == 0) next; print(i)}
# imprimirá 1, 3, 5, 7, 9.
```

**Salir bucle:**
```R
break 
# Sale de un ciclo completamente.

for (i in 1:10) {if (i > 5) break; print(i)}
# imprimirá 1, 2, 3, 4, 5.
```

**Evaluación de expresión:**
```R
switch(expr, ...)
# Evalúa una expresión y ejecuta el código correspondiente.

x <- 2; switch(x, "uno", "dos", "tres")
# devolverá "dos".
```

**Valor según condición:**
```R
ifelse(test, yes, no)
# Devuelve un valor según una condición.

x <- 5; ifelse(x > 0, "Positivo", "Negativo")
# devolverá "Positivo".
```

**Indices según condición:**
```R
which(condición)
# Devuelve los índices de los elementos que cumplen una condición.

x <- c(5, 2, 8, 1, 3); which(x > 3)
# devolverá 1 y 3.
```

**Existencia de valores TRUE/FALSE:**
```R
any(condición) y all(condición)

# Devuelven `TRUE` si al menos uno (any) o todos (all) los elementos de un vector cumplen una condición.

x <- c(5, 2, 8, 1, 3); any(x > 5)
# devolverá `TRUE`.
```

### FUNCIONES:

**Definición de función**
```R
nombre_funcion <- function(argumentos) {cuerpo_de_la_funcion}
# Define una función personalizada con los argumentos especificados y el cuerpo de la función que contiene las operaciones a realizar. 

suma <- function(a, b) {a + b}; suma(2, 3)
# devolverá 5.
```

**Retorno de valor**
```R
return(valor_a_devolver)
# Devuelve un valor desde una función. 

doblar <- function(x) {return(x * 2)}; doblar(5)
# devolverá 10.
```

 **Obtener argumentos de una función**
 ```R
 args(nombre_funcion)
# Devuelve una lista con los argumentos de la función especificada. 

args(sum)
# devolverá la lista de argumentos de la función `sum`.
```

 **Obtener el cuerpo de una función**
 ```R
 body(nombre_funcion)
 # Devuelve el cuerpo (código interno) de la función especificada. 
 
 body(sum)
 # devolverá el cuerpo de la función `sum`.
 ```
 
 **Obtener argumentos formales de una función**
 ```R
 formals(nombre_funcion)
 # Devuelve una lista con los argumentos formales de la función especificada. 
 
 formals(sum)
 # devolverá la lista de argumentos formales de la función `sum`.
 ```
 
 **Obtener el ambiente de una función**
 ```R
environment(nombre_funcion)
# Explicación: Devuelve el ambiente (entorno) asociado a la función especificada. 

environment(sum)
# devolverá el ambiente de la función `sum`.
```

 **Realizar sustituciones en una llamada a función** 
 ```R
 substitute(expresion)
 # Explicación: Realiza sustituciones en una expresión sin evaluarla. 
 
 substitute(x + y, list(x = 1, y = 2))
 # devolverá la expresión `1 + 2`.
 ```
 
 **Prevenir evaluación de una expresión**
 ```R
quote(expresion)
#Previene la evaluación de una expresión y la devuelve como un objeto de lenguaje. 

quote(x + y)
# devolverá la expresión `x + y` sin evaluarla.
```

 **Convertir expresiones R en caracteres** 
 ```R
deparse(expresion)
# Convierte expresiones R en caracteres, lo que puede ser útil para depuración y generación de código. 

deparse(expression(x + y))
# devolverá la cadena de caracteres `"x + y"`.
```

 **Obtener una función a partir de su nombre** 
 ```R
match.fun(nombre_funcion)
# Busca una función por su nombre y la devuelve como un objeto de función. 

match.fun("sum")
#devolverá la función `sum`
```

### ENTRADAS Y SALIDAS:

**Lectura de datos:**
```R
scan(file, what, nmax, sep, ...)
# Lee datos desde un archivo o la consola. 

x <- scan(what = double(), n = 5)
# leerá 5 números de la consola.
```

**Lectura de archivo de tabla**
```R
read.table(file, header, sep, ...)
# Lee un archivo de datos en formato de tabla. 

datos <- read.table("datos.csv", header = TRUE, sep = ",")
```

**Escritura de archivo de tabla**
```R. 
write.table(x, file, ...)
# Escribe un objeto (como un data frame) en un archivo de texto. 

write.table(datos, "datos.txt", row.names = FALSE)
```

**Escritura en consola/archivo**
```R
cat(...)
# Escribe los argumentos en la consola o un archivo. 

cat("Hola", "mundo", sep = " ")
# escribirá "Hola mundo" en la consola.
```

**Impresión de objeto**
```R
print(x)
# Imprime un objeto en la consola. 

print(datos)
# imprimirá el contenido del data frame `datos`.
```

**Redireccionamiento de salida** 
```R
sink(file)
# Redirige la salida a un archivo. 

sink("output.txt"); print(datos); sink()
# escribirá el contenido de `datos` en el archivo `output.txt`.
```

**Ejecución de código desde archivo**
```R
source(file)
# Ejecuta el código R desde un archivo. 

source("script.R")
# ejecutará el código en el archivo `script.R`.
```

**Lectura de líneas de texto** 
```R
readLines(con)
# Lee líneas de texto desde una conexión o archivo. 

lines <- readLines("archivo.txt")
# leerá las líneas del archivo `archivo.txt`.
```

**Selección de archivo** 
```R
file.choose()
# Abre un cuadro de diálogo para seleccionar un archivo. 

archivo <- file.choose()
# permitirá seleccionar un archivo a través de un cuadro de diálogo.
```

**Creación de menú interactivo**
```R
menu(choices, graphics)
# Crea un menú interactivo. 

opcion <- menu(c("Opción 1", "Opción 2", "Salir"))
# creará un menú interactivo.
```

### CONVERSION DE TIPOS:

**Conversión a caracteres**
```R
as.character(x)
# Convierte un objeto a un vector de caracteres. 

as.character(c(1, 2, 3))
# devolverá `"1"`, `"2"`, `"3"`.
```

**Conversión a numérico** 
```R
as.numeric(x)
# Convierte un objeto a un vector numérico. 

as.numeric(c("1", "2", "3"))
# devolverá `1`, `2`, `3`.
```

**Conversión a factor**
```R
as.factor(x)
# Convierte un objeto a un factor. 

as.factor(c("rojo", "verde", "azul"))
# creará un factor con niveles `"rojo"`, `"verde"`, `"azul"`.
```

**Conversión a lógico** 
```R
as.logical(x)
# Convierte un objeto a un vector lógico. 

as.logical(c(0, 1, 2))
# devolverá `FALSE`, `TRUE`, `TRUE`.
```

**Conversión a fecha**
```R
as.Date(x, format)
# Convierte una cadena de caracteres en un objeto de clase `Date`. 

as.Date("2023-05-01", "%Y-%m-%d")
# creará un objeto de clase `Date` con el valor `"2023-05-01"`.
```

**Conversión a fecha y hora** 
```R
as.POSIXct(x, tz)
# Convierte una cadena de caracteres en un objeto de clase `POSIXct` (fecha y hora). 

as.POSIXct("2023-05-01 12:00:00", tz = "UTC")
# creará un objeto de clase `POSIXct` con el valor `"2023-05-01 12:00:00"` en la zona horaria UTC.
```

**Conversión a lista**
```R
as.list(x)
# Convierte un objeto en una lista. 

as.list(c(1, 2, 3))
# devolverá una lista con tres elementos: `1`, `2`, `3`.
```

**Conversión a data frame** 
```R
as.data.frame(x)
# Convierte un objeto en un data frame. 

as.data.frame(matrix(1:6, nrow = 2))
# creará un data frame a partir de una matriz.
```

**Conversión a matriz** 
```R
as.matrix(x)
# Convierte un objeto en una matriz. 

as.matrix(1:6, nrow = 2)
# creará una matriz de 2 filas y 3 columnas a partir del vector `1:6`.
```

**Conversión a vector**
```R
as.vector(x)
# Convierte un objeto en un vector. 

as.vector(matrix(1:6, nrow = 2))
# devolverá un vector con los elementos `1`, `3`, `5`, `2`, `4`, `6`.
```

### PAQUETE BASE:

**Media aritmética:** 
```R
mean(x)
# Calcula la media aritmética de los elementos de un vector. 

mean(c(1, 2, 3, 4, 5))
# devolverá `3`.
```

**Desviación estándar:**
```R
sd(x)
# Calcula la desviación estándar de los elementos de un vector. 

sd(c(1, 2, 3, 4, 5))
# devolverá `1.58113883`.
```

**Varianza:**
```R
var(x)
# Calcula la varianza de los elementos de un vector. 

var(c(1, 2, 3, 4, 5))
# devolverá `2.5`.
```

**Longitud de objeto:**
```R
length(x)
# Devuelve la longitud de un objeto. 

length(c(1, 2, 3, 4, 5))
# devolverá `5`.
```

**Ordenamiento de elementos** 
```R
sort(x)
# Ordena los elementos de un vector. 

sort(c(3, 1, 5, 2, 4))
# devolverá `1`, `2`, `3`, `4`, `5`.
```

**Inversión de orden** 
```R
rev(x)
# Invierte el orden de los elementos de un vector. 

rev(c(1, 2, 3, 4, 5))
# devolverá `5`, `4`, `3`, `2`, `1`.
```

**Valores únicos** 
```R
unique(x)
# Devuelve los valores únicos de un vector. 

unique(c(1, 2, 3, 2, 1, 4))
# devolverá `1`, `2`, `3`, `4`.
```

**Muestra aleatoria**
```R
sample(x, size)
# Selecciona una muestra aleatoria de elementos de un vector. 

sample(1:10, 5)
# devolverá una muestra de 5 números aleatorios entre 1 y 10.
```

**Combinación por columnas/filas** 
```R
cbind(...) y rbind(...)
# Combina vectores o matrices por columnas o filas, respectivamente. 

cbind(c(1, 2), c(3, 4))
# devolverá una matriz con dos columnas: `1 3`, `2 4`.
```

**Secuencia de números** 
```R
seq(from, to, by)
# Genera una secuencia de números. 

seq(1, 10, by = 2)
# devolverá `1`, `3`, `5`, `7`, `9`.
