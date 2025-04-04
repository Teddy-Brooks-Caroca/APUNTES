# Numpy: Guía de uso
## 1. Introducción a NumPy

NumPy (Numerical Python) es una biblioteca fundamental para el cálculo numérico en Python. Proporciona soporte para arreglos multidimensionales (arrays) y funciones matemáticas de alto rendimiento, optimizadas para operar sobre estos arreglos de manera eficiente.

**Características principales:**

- Creación y manipulación de arreglos (arrays) multidimensionales
- Operaciones matemáticas y estadísticas sobre datos numéricos
- Generación de números aleatorios
- Álgebra lineal y transformaciones matriciales
- Manejo eficiente de datos en análisis numérico y científico

## 2. Arrays en NumPy y Funciones Principales

### 2.1 Creación de Arrays

Un array en NumPy es una estructura de datos similar a una lista en Python, pero optimizada para operaciones matemáticas y de álgebra lineal. Es más eficiente en términos de almacenamiento y velocidad, ya que almacena datos en bloques de memoria contiguos y permite realizar operaciones vectorizadas.

```python
import numpy as np  # Importar la librería NumPy

# Crear un array unidimensional (vector)
arr1 = np.array([1, 2, 3, 4, 5])

# Crear un array bidimensional (matriz)
arr2 = np.array([[1, 2, 3], [4, 5, 6]])

# Crear un array tridimensional
arr3 = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])

print(arr1)
print(arr2)
print(arr3)
```

### 2.2 Función np.arange()

La función `np.arange()` genera un array con valores dentro de un rango específico, similar a la función `range()` de Python, pero devolviendo un array de NumPy.

**Sintaxis:**

```python
np.arange(inicio, fin, paso, dtype)
```

- inicio (opcional): valor inicial (por defecto es 0)
- fin: valor final (no se incluye en el array)
- paso (opcional): intervalo entre valores (por defecto es 1)
- dtype (opcional): tipo de dato del array

**Ejemplo:**

```python
import numpy as np

# Crear un array desde 0 hasta 9 (sin incluir 10)
arr = np.arange(10)
print(arr)  # Salida: [0 1 2 3 4 5 6 7 8 9]

# Crear un array de 1 a 10 con paso de 2
arr2 = np.arange(1, 10, 2)
print(arr2)  # Salida: [1 3 5 7 9]
```

### 2.3 Función np.reshape()

La función `np.reshape()` reorganiza los elementos de un array en una nueva forma sin alterar sus datos.

**Sintaxis:**

```python
np.reshape(array, nueva_forma)
```

- array: array original que se quiere cambiar
- nueva_forma: tupla con las nuevas dimensiones (deben ser compatibles con el número total de elementos)

**Ejemplo:**

```python
# Crear un array de 1D y transformarlo en 2D (matriz 3x3)
arr = np.arange(9)  # [0 1 2 3 4 5 6 7 8]
arr_reshaped = np.reshape(arr, (3, 3))
print(arr_reshaped)
# Salida:
# [[0 1 2]
#  [3 4 5]
#  [6 7 8]]
```

Si intentas darle una forma incompatible con el número total de elementos, NumPy generará un error.

### 2.4 Funciones argmin() y argmax()

Las funciones `np.argmin()` y `np.argmax()` devuelven la posición (índice) del valor mínimo y máximo en un array, respectivamente.

#### 2.4.1 np.argmin(): Índice del Valor Mínimo

```python
import numpy as np
arr = np.array([10, 5, 2, 8, 3])
indice_min = np.argmin(arr)
print("Índice del valor mínimo:", indice_min)  # 2 (corresponde al valor 2)
print("Valor mínimo:", arr[indice_min])  # 2
```

#### 2.4.2 np.argmax(): Índice del Valor Máximo

```python
indice_max = np.argmax(arr)
print("Índice del valor máximo:", indice_max)  # 0 (corresponde al valor 10)
print("Valor máximo:", arr[indice_max])  # 10
```

#### 2.4.3 Uso en Matrices con axis

Podemos encontrar los índices de los valores mínimo y máximo por filas o columnas en una matriz.

```python
matriz = np.array([[10, 5, 2],
                   [8, 3, 9]])
# Índices del mínimo por columna (axis=0)
print("Índices del mínimo por columna:", np.argmin(matriz, axis=0))
# Salida: [1 1 0] → Min en cada columna está en la fila 1, 1 y 0.

# Índices del máximo por fila (axis=1)
print("Índices del máximo por fila:", np.argmax(matriz, axis=1))
# Salida: [0 2] → Max en la primera fila está en col 0, en la segunda fila en col 2.
```

### 2.5 Función transpose()

La función `transpose()` en NumPy se utiliza para cambiar las dimensiones de un array, es decir, invertir las filas y columnas en una matriz. Esta función es especialmente útil cuando se trabaja con matrices de 2 dimensiones, pero también se puede aplicar a arrays de más dimensiones.

**Sintaxis:**

```python
numpy.transpose(a, axes=None)
```

- a: Array que se desea transponer
- axes (opcional): Especifica el orden de los ejes. Si no se proporciona, se invierte el orden por defecto

**Ejemplo:**

```python
import numpy as np
# Crear una matriz 2D
arr = np.array([[1, 2, 3],
                [4, 5, 6]])
# Transponer la matriz
arr_transpose = np.transpose(arr)
print("Matriz original:")
print(arr)
print("Matriz transpuesta:")
print(arr_transpose)
```

**Salida esperada:**

```
Matriz original:
[[1 2 3]
 [4 5 6]]
Matriz transpuesta:
[[1 4]
 [2 5]
 [3 6]]
```

### 2.6 El Operador @ (Producto Matricial)

El operador `@` se utiliza para realizar el producto matricial entre dos arrays de 2 dimensiones (matrices). Este operador fue introducido en Python 3.5 como una forma más limpia y eficiente de realizar multiplicaciones de matrices, reemplazando la función `np.dot()` o `np.matmul()`.

**Sintaxis:**

```python
result = a @ b
```

- a: Primer array (matriz)
- b: Segundo array (matriz)

**Ejemplo:**

```python
import numpy as np
# Crear dos matrices 2D
A = np.array([[1, 2],
              [3, 4]])
B = np.array([[5, 6],
              [7, 8]])
# Producto matricial
C = A @ B
print("Matriz A:")
print(A)
print("Matriz B:")
print(B)
print("Producto matricial (A @ B):")
print(C)
```

**Salida esperada:**

```
Matriz A:
[[1 2]
 [3 4]]
Matriz B:
[[5 6]
 [7 8]]
Producto matricial (A @ B):
[[19 22]
 [43 50]]
```

### 2.7 Función np.zeros()

La función `np.zeros()` crea un array lleno de ceros con las dimensiones especificadas.

**Sintaxis:**

```python
np.zeros(shape, dtype=float, order='C')
```

- shape: Dimensiones del array resultante (entero o tupla de enteros)
- dtype (opcional): Tipo de datos (por defecto es float)
- order (opcional): Orden de almacenamiento en memoria ('C' para orden de C, 'F' para orden de Fortran)

**Ejemplo:**

```python
import numpy as np

# Crear un array 1D de 5 elementos con ceros
zeros_1d = np.zeros(5)
print("Array 1D de ceros:")
print(zeros_1d)  # [0. 0. 0. 0. 0.]

# Crear un array 2D (matriz 3x4) con ceros
zeros_2d = np.zeros((3, 4))
print("Matriz de ceros:")
print(zeros_2d)
# Salida:
# [[0. 0. 0. 0.]
#  [0. 0. 0. 0.]
#  [0. 0. 0. 0.]]

# Crear un array de ceros con tipo de datos entero
zeros_int = np.zeros((2, 3), dtype=int)
print("Matriz de ceros (enteros):")
print(zeros_int)
# Salida:
# [[0 0 0]
#  [0 0 0]]
```

### 2.8 Funciones random en NumPy

NumPy proporciona varias funciones para generar números aleatorios, lo que es fundamental para simulaciones, inicialización de algoritmos y muestreo estadístico.

#### 2.8.1 np.random.rand(): Números aleatorios uniformes [0,1)

Genera números aleatorios con distribución uniforme entre 0 (inclusive) y 1 (exclusivo).

```python
import numpy as np

# Generar un único número aleatorio
random_num = np.random.rand()
print("Número aleatorio:", random_num)

# Generar un array 1D de 5 números aleatorios
random_1d = np.random.rand(5)
print("Array 1D de números aleatorios:")
print(random_1d)

# Generar una matriz 2x3 de números aleatorios
random_2d = np.random.rand(2, 3)
print("Matriz de números aleatorios:")
print(random_2d)
```

#### 2.8.2 np.random.randn(): Números aleatorios con distribución normal

Genera números aleatorios con distribución normal (media 0, varianza 1).

```python
# Generar números aleatorios con distribución normal
normal_nums = np.random.randn(3, 3)
print("Matriz de distribución normal:")
print(normal_nums)
```

#### 2.8.3 np.random.randint(): Enteros aleatorios

Genera enteros aleatorios dentro de un rango especificado.

```python
# Generar enteros aleatorios entre 1 y 10 (inclusive)
random_ints = np.random.randint(1, 11, size=(3, 4))
print("Matriz de enteros aleatorios:")
print(random_ints)
```

#### 2.8.4 np.random.choice(): Muestreo aleatorio

Selecciona elementos aleatorios de un array.

```python
# Seleccionar elementos aleatorios de un array
elementos = np.array([1, 3, 5, 7, 9])
seleccion = np.random.choice(elementos, size=4, replace=True)
print("Selección aleatoria:", seleccion)

# Muestreo con probabilidades personalizadas
prob = [0.1, 0.2, 0.4, 0.2, 0.1]  # Probabilidades para cada elemento
seleccion_ponderada = np.random.choice(elementos, size=10, p=prob)
print("Selección ponderada:", seleccion_ponderada)
```

#### 2.8.5 np.random.shuffle(): Mezclar un array

Mezcla aleatoriamente los elementos de un array (modifica el array original).

```python
# Crear un array ordenado
arr = np.arange(10)
print("Array original:", arr)

# Mezclar el array
np.random.shuffle(arr)
print("Array mezclado:", arr)
```

#### 2.8.6 Establecer semilla aleatoria

Para hacer reproducibles los resultados, se puede establecer una semilla:

```python
# Establecer semilla para reproducibilidad
np.random.seed(42)
print("Con semilla 42:", np.random.rand(3))

np.random.seed(42)
print("Con la misma semilla:", np.random.rand(3))  # Mismo resultado
```

## 3. Vectores en NumPy

### 3.1 Definición y Tipos

Un vector en NumPy es un array unidimensional que puede representar una serie de valores numéricos. Se usa en cálculos matemáticos, estadísticas, aprendizaje automático y álgebra lineal.

Existen dos tipos de vectores en NumPy:

1. Vector fila: Tiene una sola fila y múltiples columnas
2. Vector columna: Tiene múltiples filas y una sola columna

**Sintaxis para Crear un Vector:**

```python
import numpy as np
# Vector fila (1D)
vector_fila = np.array([1, 2, 3, 4, 5])
# Vector columna (usando reshape)
vector_columna = np.array([1, 2, 3, 4, 5]).reshape(5, 1)
print("Vector fila:", vector_fila)
print("Vector columna:\n", vector_columna)
```

**Salida:**

```
Vector fila: [1 2 3 4 5]
Vector columna:
[[1]
 [2]
 [3]
 [4]
 [5]]
```

Los vectores son esenciales para operaciones algebraicas como producto punto, norma, y transformaciones en el análisis de datos.

### 3.2 Operaciones con Vectores

#### 3.2.1 Suma y Resta de Vectores

Las operaciones se realizan elemento a elemento.

```python
import numpy as np
v1 = np.array([1, 2, 3])
v2 = np.array([4, 5, 6])
# Suma
suma = v1 + v2  # [1+4, 2+5, 3+6]
print("Suma:", suma)  # [5 7 9]
# Resta
resta = v1 - v2
print("Resta:", resta)  # [-3 -3 -3]
```

#### 3.2.2 Multiplicación y División Elemento a Elemento

Cada elemento del primer vector se multiplica o divide con su correspondiente en el segundo.

```python
# Multiplicación
multiplicacion = v1 * v2
print("Multiplicación:", multiplicacion)  # [4 10 18]
# División
division = v1 / v2
print("División:", division)  # [0.25 0.4 0.5]
```

#### 3.2.3 Producto Punto entre Vectores

El producto punto es la suma de los productos de los elementos correspondientes.

```python
# Producto punto
producto_punto = np.dot(v1, v2)  # 1*4 + 2*5 + 3*6 = 32
print("Producto punto:", producto_punto)  # 32
```

Otra forma de calcularlo es con el operador @ :

```python
print("Producto punto con @:", v1 @ v2)  # 32
```

#### 3.2.4 Norma de un Vector

La norma de un vector mide su magnitud o longitud en el espacio. Se calcula con `np.linalg.norm()`.

```python
norma_v1 = np.linalg.norm(v1)
print("Norma del vector v1:", norma_v1)  # √(1² + 2² + 3²) = 3.741
```

#### 3.2.5 Normalización de un Vector

La normalización convierte un vector en un vector unitario (de longitud 1).

```python
vector_normalizado = v1 / np.linalg.norm(v1)
print("Vector normalizado:", vector_normalizado)
```

## 4. Métodos de Agregación en NumPy

Los métodos de agregación en NumPy permiten calcular valores resumidos de un array, como sumas, promedios, valores mínimos y máximos. Estas funciones son fundamentales en análisis de datos y estadística.

### 4.1 np.sum() : Suma de Elementos

Calcula la suma de todos los elementos del array o a lo largo de un eje específico.

```python
import numpy as np
arr = np.array([[1, 2, 3], [4, 5, 6]])
# Suma total del array
print("Suma total:", np.sum(arr))  # 1+2+3+4+5+6 = 21
# Suma por filas (axis=1 → fila)
print("Suma por filas:", np.sum(arr, axis=1))  # [6, 15]
# Suma por columnas (axis=0 → columna)
print("Suma por columnas:", np.sum(arr, axis=0))  # [5, 7, 9]
```

### 4.2 np.min() y np.max() : Valor Mínimo y Máximo

Encuentran el menor y el mayor valor en un array.

```python
print("Mínimo:", np.min(arr))  # 1
print("Máximo:", np.max(arr))  # 6
# Mínimo por columnas
print("Mínimo por columnas:", np.min(arr, axis=0))  # [1 2 3]
```

### 4.3 np.mean() : Promedio (Media Aritmética)

Calcula el promedio de los valores del array.

```python
print("Promedio:", np.mean(arr))  # (1+2+3+4+5+6)/6 = 3.5
```

### 4.4 np.median() : Mediana

La mediana es el valor central de un conjunto de datos ordenados.

```python
print("Mediana:", np.median(arr))  # 3.5
```

### 4.5 np.std() y np.var() : Desviación Estándar y Varianza

Miden la dispersión de los datos.

```python
print("Desviación estándar:", np.std(arr))  # ≈ 1.7078
print("Varianza:", np.var(arr))  # ≈ 2.9166
```

Estos métodos se pueden aplicar sobre matrices y en diferentes ejes.

## 5. Medidas de Dispersión y Tendencia Central

NumPy proporciona varias funciones para calcular medidas de tendencia central (como la media y la mediana) y medidas de dispersión (como la varianza y la desviación estándar), fundamentales en estadística y análisis de datos.

### 5.1 Medidas de Tendencia Central

#### 5.1.1 np.mean() : Media Aritmética

La media es el promedio de los valores del array.

```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9])
# Media total
print("Media:", np.mean(arr))  # (1+2+...+9)/9 = 5.0
```

También se puede calcular la media por filas o columnas en matrices.

```python
matriz = np.array([[1, 2, 3], [4, 5, 6]])
print("Media por columnas:", np.mean(matriz, axis=0))  # [2.5 3.5 4.5]
print("Media por filas:", np.mean(matriz, axis=1))  # [2.0 5.0]
```

#### 5.1.2 np.median() : Mediana

La mediana es el valor central cuando los datos están ordenados. Si hay un número par de elementos, se promedia los dos valores centrales.

```python
print("Mediana:", np.median(arr))  # 5.0
arr_par = np.array([1, 2, 3, 4, 5, 6])
print("Mediana (par):", np.median(arr_par))  # (3+4)/2 = 3.5
```

### 5.2 Medidas de Dispersión

#### 5.2.1 np.var() : Varianza

La varianza mide cuánto se dispersan los datos respecto a la media.

```python
print("Varianza:", np.var(arr))  # ≈ 6.6667
```

Para una matriz:

```python
print("Varianza por columnas:", np.var(matriz, axis=0))  # [2.25 2.25 2.25]
print("Varianza por filas:", np.var(matriz, axis=1))  # [0.666 0.666]
```

#### 5.2.2 np.std() : Desviación Estándar

La desviación estándar es la raíz cuadrada de la varianza, representando la dispersión de los datos.

```python
print("Desviación estándar:", np.std(arr))  # ≈ 2.58
```

Para matrices:

```python
print("Desviación estándar por columnas:", np.std(matriz, axis=0))
print("Desviación estándar por filas:", np.std(matriz, axis=1))
```

#### 5.2.3 np.ptp() : Rango (Diferencia Máximo - Mínimo)

El rango es la diferencia entre el valor máximo y el mínimo del array.

```python
print("Rango:", np.ptp(arr))  # 9 - 1 = 8
```

Estas funciones son esenciales para describir conjuntos de datos y entender su distribución.

## 6. Tratamiento de Missing Values en NumPy

En análisis de datos, los missing values (valores faltantes) pueden generar errores en cálculos estadísticos y deben ser manejados adecuadamente. En NumPy, los valores faltantes se representan con `np.nan` (Not a Number).

### 6.1 Identificar Valores Faltantes

Podemos detectar los valores NaN con `np.isnan()`.

```python
import numpy as np
arr = np.array([1, 2, np.nan, 4, 5])
# Identificar valores NaN
print("Valores NaN en el array:", np.isnan(arr))
# Salida: [False False True False False]
```

### 6.2 Remover Missing Values (np.nan)

Si queremos eliminar los valores NaN y trabajar solo con los datos disponibles, usamos `arr[~np.isnan(arr)]`.

```python
arr_sin_nan = arr[~np.isnan(arr)]
print("Array sin NaN:", arr_sin_nan)
# Salida: [1. 2. 4. 5.]
```

### 6.3 Reemplazar Missing Values (np.nan)

Podemos rellenar los valores NaN con un valor específico, como 0 o la media del conjunto de datos.

```python
# Reemplazar NaN por 0
arr_reemplazado = np.where(np.isnan(arr), 0, arr)
print("Reemplazar NaN con 0:", arr_reemplazado)
# Salida: [1. 2. 0. 4. 5.]

# Reemplazar NaN por la media
media = np.nanmean(arr)  # np.nanmean() calcula la media ignorando NaN
arr_reemplazado_media = np.where(np.isnan(arr), media, arr)
print("Reemplazar NaN con la media:", arr_reemplazado_media)
```

### 6.4 Operaciones Ignorando Missing Values

NumPy proporciona versiones especiales de funciones estadísticas que ignoran los NaN:

- `np.nanmean(arr)`: Media ignorando NaN
- `np.nanmedian(arr)`: Mediana ignorando NaN
- `np.nanstd(arr)`: Desviación estándar ignorando NaN

```python
print("Media ignorando NaN:", np.nanmean(arr))
print("Mediana ignorando NaN:", np.nanmedian(arr))
print("Desviación estándar ignorando NaN:", np.nanstd(arr))
```

Este enfoque permite tratar datos incompletos sin sesgar los resultados.

## 7. Operaciones en NumPy con axis (Ejes)

NumPy permite operar sobre ejes específicos en arrays multidimensionales. El parámetro `axis` indica en qué dirección se aplicará la operación dentro del array.

### 7.1 Concepto de Ejes en NumPy

Para una matriz 2D:

- `axis=0` → Operación columna por columna (vertical)
- `axis=1` → Operación fila por fila (horizontal)

### 7.2 Ejemplo con np.sum()

```python
import numpy as np
matriz = np.array([[1, 2, 3],
                   [4, 5, 6]])

# Sin `axis`: suma todos los elementos del array
print("Suma total:", np.sum(matriz))  # 1+2+3+4+5+6 = 21

# Con `axis=0`: suma los valores de cada columna
print("Suma por columna:", np.sum(matriz, axis=0))  # [5 7 9]

# Con `axis=1`: suma los valores de cada fila
print("Suma por fila:", np.sum(matriz, axis=1))  # [6 15]
```

### 7.3 Ejemplo con np.mean() (Promedio)

```python
print("Promedio por columna:", np.mean(matriz, axis=0))  # [2.5 3.5 4.5]
print("Promedio por fila:", np.mean(matriz, axis=1))  # [2.0 5.0]
```

### 7.4 Ejemplo con np.min() y np.max()

```python
print("Mínimo por columna:", np.min(matriz, axis=0))  # [1 2 3]
print("Máximo por fila:", np.max(matriz, axis=1))  # [3 6]
```

### 7.5 Aplicación en Arrays 3D

Para un array tridimensional, hay tres ejes:

- `axis=0`: Operación sobre profundidad (agregando en la primera dimensión)
- `axis=1`: Operación sobre filas
- `axis=2`: Operación sobre columnas

```python
arr_3d = np.array([[[1, 2], [3, 4]],
                   [[5, 6], [7, 8]]])
print("Suma sobre el eje 0 (profundidad):", np.sum(arr_3d, axis=0))
# [[1+5, 2+6], [3+7, 4+8]] → [[6 8] [10 12]]
```

El uso de `axis` en NumPy permite controlar la dirección de los cálculos en arrays multidimensionales, lo que es clave en análisis de datos y machine learning.

## 8. Función linspace

La función `numpy.linspace()` se usa para generar un conjunto de valores equiespaciados entre un rango definido.

---

### **Sintaxis:**


```python
`numpy.linspace(inicio, fin, num=50, endpoint=True, retstep=False, dtype=None)`
```

### **Parámetros:**

1. **`inicio`** → Valor inicial de la secuencia.
    
2. **`fin`** → Valor final de la secuencia.
    
3. **`num`** _(opcional, por defecto 50)_ → Cantidad de elementos en la secuencia.
    
4. **`endpoint`** _(opcional, por defecto `True`)_ → Si `True`, el `fin` estará incluido en la secuencia; si `False`, no.
    
5. **`retstep`** _(opcional, por defecto `False`)_ → Si `True`, devuelve también el tamaño del paso entre valores.
    
6. **`dtype`** _(opcional)_ → Especifica el tipo de dato de los valores generados.
    

---

### **Ejemplos de Uso:**

#### **1. Generar 5 valores entre 0 y 10**

python

CopiarEditar

`import numpy as np  arr = np.linspace(0, 10, 5) print(arr)`

🔹 **Salida:**

python

CopiarEditar

`[  0.   2.5  5.   7.5 10. ]`

Se generan 5 valores equiespaciados entre 0 y 10.

---

#### **2. Excluir el valor final (`endpoint=False`)**

python

CopiarEditar

`arr = np.linspace(0, 10, 5, endpoint=False) print(arr)`

🔹 **Salida:**

python

CopiarEditar

`[0. 2. 4. 6. 8.]`

El `10` no se incluye, y los valores se distribuyen uniformemente en 4 intervalos en lugar de 5.

---

#### **3. Obtener el tamaño del paso (`retstep=True`)**

python

CopiarEditar

`arr, step = np.linspace(0, 10, 5, retstep=True) print(f"Array: {arr}") print(f"Paso entre valores: {step}")`

🔹 **Salida:**

python

CopiarEditar

`Array: [  0.   2.5  5.   7.5 10. ] Paso entre valores: 2.5`

Nos devuelve el array y el paso (`2.5` en este caso).

---

### **Casos de Uso Común**

- Generar puntos para gráficos (`matplotlib`).
    
- Crear intervalos uniformes en análisis numérico.
    
- Simular datos en análisis de señales o series temporales.
# Pandas: Guía Completa

## 1. Introducción a Pandas

### ¿Qué es Pandas?

Pandas es una biblioteca de Python que proporciona estructuras de datos y herramientas para la manipulación y análisis de datos. Está construida sobre NumPy y permite trabajar con datos estructurados de manera eficiente.

### Características principales de Pandas:

✅ Facilita la manipulación de datos estructurados (tablas, series de tiempo, etc.). 
✅ Basado en DataFrames y Series, estructuras de datos optimizadas para análisis. 
✅ Soporta operaciones como filtrado, agregaciones, fusiones y más. 
✅ Permite leer y escribir datos desde múltiples fuentes (CSV, Excel, SQL, JSON, etc.).

### Instalación y Uso

Si no tienes instalada la librería Pandas, puedes hacerlo con el siguiente comando:

```python
pip install pandas
```

Para usar Pandas en tu código, debes importarlo:

```python
import pandas as pd
```

## 2. Estructuras de Datos en Pandas

### 2.1 Series

Una Serie es un arreglo unidimensional con etiquetas en los índices.

**Ejemplo:**

```python
import pandas as pd
# Crear una Serie
serie = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])
print(serie)
```

**Salida:**

```
a    10
b    20
c    30
d    40
dtype: int64
```

### 2.2 DataFrames

Un DataFrame es una estructura bidimensional (como una hoja de cálculo de Excel o una tabla SQL).

**Ejemplo:**

```python
import pandas as pd
# Crear un DataFrame
datos = {
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 35],
    "Ciudad": ["Santiago", "Lima", "Buenos Aires"]
}
df = pd.DataFrame(datos)
print(df)
```

**Salida:**

```
   Nombre  Edad        Ciudad
0     Ana    25      Santiago
1    Juan    30          Lima
2   Pedro    35  Buenos Aires
```

## 3. Indexación en Pandas

El indexing en Pandas es la forma en que accedemos a elementos dentro de un DataFrame o Series. Existen diferentes métodos para seleccionar datos:

### 3.1 Label Indexing (.loc[])

El label indexing permite seleccionar datos usando el nombre del índice o el nombre de la columna.

**Ejemplo: Crear un DataFrame con etiquetas personalizadas**

```python
import pandas as pd
# Crear un DataFrame con etiquetas personalizadas
df = pd.DataFrame({
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 35],
    "Ciudad": ["Santiago", "Lima", "Buenos Aires"]
}, index=["A", "B", "C"])
print(df)
```

**Salida:**

```
  Nombre  Edad        Ciudad
A    Ana    25      Santiago
B   Juan    30          Lima
C  Pedro    35  Buenos Aires
```

**Ejemplo: Acceder a una fila por su etiqueta (.loc[])**

```python
print(df.loc["B"])
```

**Salida:**

```
Nombre    Juan
Edad        30
Ciudad     Lima
Name: B, dtype: object
```

**Ejemplo: Seleccionar múltiples filas**

```python
print(df.loc[["A", "C"]])
```

**Salida:**

```
  Nombre  Edad        Ciudad
A    Ana    25      Santiago
C  Pedro    35  Buenos Aires
```

**Ejemplo: Seleccionar una columna por nombre (.loc[])**

```python
print(df.loc[:, "Edad"])  # Selecciona solo la columna "Edad"
```

**Salida:**

```
A    25
B    30
C    35
Name: Edad, dtype: int64
```

**Ejemplo: Seleccionar varias columnas**

```python
print(df.loc[:, ["Nombre", "Ciudad"]])
```

**Salida:**

```
  Nombre      Ciudad
A    Ana    Santiago
B   Juan        Lima
C  Pedro  Buenos Aires
```

### 3.2 Integer Indexing (.iloc[])

El integer indexing permite acceder a datos usando la posición numérica en lugar del nombre del índice o la columna.

**Ejemplo: Seleccionar una fila por su posición (.iloc[])**

```python
print(df.iloc[1])  # Selecciona la segunda fila (índice 1)
```

**Salida:**

```
Nombre    Juan
Edad        30
Ciudad     Lima
Name: B, dtype: object
```

**Ejemplo: Seleccionar un valor específico**

```python
print(df.iloc[1, 2])  # Fila 1, Columna 2
```

**Salida:**

```
Lima
```

**Ejemplo: Seleccionar un rango de filas**

```python
print(df.iloc[0:2])  # Selecciona las dos primeras filas
```

**Salida:**

```
  Nombre  Edad    Ciudad
A    Ana    25  Santiago
B   Juan    30      Lima
```

### 3.3 Filtrado de Datos

Los filtros en Pandas permiten seleccionar filas que cumplen con ciertas condiciones.

**Ejemplo: Filtrar por una condición**

```python
print(df[df["Edad"] > 25])  # Filtrar personas con edad mayor a 25
```

**Salida:**

```
  Nombre  Edad        Ciudad
B   Juan    30          Lima
C  Pedro    35  Buenos Aires
```

**Ejemplo: Filtrar por múltiples condiciones**

```python
print(df[(df["Edad"] > 25) & (df["Ciudad"] == "Lima")])
```

**Salida:**

```
  Nombre  Edad Ciudad
B   Juan    30   Lima
```

## 4. Índices en Pandas

Los índices en Pandas son etiquetas que identifican de manera única cada fila o columna en un DataFrame o una Serie. Son esenciales para acceder, filtrar y manipular datos de manera eficiente.

### Características de los índices:

✅ Se pueden asignar de forma manual o automática. 
✅ Pueden ser numéricos o alfanuméricos. 
✅ Se pueden modificar o resetear.

### 4.1 Índices en una Serie

**Ejemplo de Serie con índice automático:**

```python
import pandas as pd
serie = pd.Series([100, 200, 300, 400])
print(serie)
```

**Salida:**

```
0    100
1    200
2    300
3    400
dtype: int64
```

**Ejemplo de Serie con índice personalizado:**

```python
serie = pd.Series([100, 200, 300, 400], index=['A', 'B', 'C', 'D'])
print(serie)
```

**Salida:**

```
A    100
B    200
C    300
D    400
dtype: int64
```

### 4.2 Índices en un DataFrame

**Ejemplo de DataFrame con índice automático:**

```python
datos = {
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 35],
    "Ciudad": ["Santiago", "Lima", "Buenos Aires"]
}
df = pd.DataFrame(datos)
print(df)
```

**Salida:**

```
   Nombre  Edad        Ciudad
0     Ana    25      Santiago
1    Juan    30          Lima
2   Pedro    35  Buenos Aires
```

**Ejemplo de DataFrame con un índice personalizado:**

```python
df.index = ["A", "B", "C"]
print(df)
```

**Salida:**

```
  Nombre  Edad        Ciudad
A    Ana    25      Santiago
B   Juan    30          Lima
C  Pedro    35  Buenos Aires
```

### 4.3 Modificación y Reseteo del Índice

**Modificar el índice con una columna existente**

```python
df = df.set_index("Nombre")
print(df)
```

**Salida:**

```
       Edad        Ciudad
Nombre                  
Ana      25      Santiago
Juan     30          Lima
Pedro    35  Buenos Aires
```

**Resetear el índice a valores numéricos**

```python
df = df.reset_index()
print(df)
```

**Salida:**

```
  Nombre  Edad        Ciudad
0    Ana    25      Santiago
1   Juan    30          Lima
2  Pedro    35  Buenos Aires
```

## 5. Reindexación (reindex())

La función `reindex()` en Pandas se utiliza para reordenar o modificar los índices de un DataFrame o una Series. Si se proporcionan nuevos índices que no existen en los datos originales, se rellenarán con valores NaN por defecto.

### 5.1 reindex() en Series

**Ejemplo: Cambiar el orden del índice**

```python
import pandas as pd
# Crear una Serie con índices personalizados
serie = pd.Series([100, 200, 300], index=['A', 'B', 'C'])
print("Serie original:")
print(serie)
# Reordenar los índices
serie_reindexada = serie.reindex(['C', 'A', 'B'])
print("\nSerie reindexada:")
print(serie_reindexada)
```

**Salida:**

```
Serie original:
A    100
B    200
C    300
dtype: int64

Serie reindexada:
C    300
A    100
B    200
dtype: int64
```

**Ejemplo: Añadir nuevos índices con valores faltantes (NaN)**

```python
serie_nueva = serie.reindex(['A', 'B', 'C', 'D', 'E'])
print(serie_nueva)
```

**Salida:**

```
A    100.0
B    200.0
C    300.0
D      NaN
E      NaN
dtype: float64
```

### 5.2 reindex() en DataFrames

**Ejemplo: Reordenar las filas de un DataFrame**

```python
# Crear un DataFrame
datos = {
    "Nombre": ["Ana", "Juan", "Pedro"],
    "Edad": [25, 30, 35]
}
df = pd.DataFrame(datos, index=['A', 'B', 'C'])
print("DataFrame original:")
print(df)
# Reordenar los índices
df_reindexado = df.reindex(['C', 'A', 'B'])
print("\nDataFrame reindexado:")
print(df_reindexado)
```

**Salida:**

```
DataFrame original:
  Nombre  Edad
A    Ana    25
B   Juan    30
C  Pedro    35

DataFrame reindexado:
  Nombre  Edad
C  Pedro    35
A    Ana    25
B   Juan    30
```

**Ejemplo: Añadir índices faltantes con valores NaN**

```python
df_nuevo = df.reindex(['A', 'B', 'C', 'D'])
print(df_nuevo)
```

**Salida:**

```
  Nombre  Edad
A    Ana  25.0
B   Juan  30.0
C  Pedro  35.0
D    NaN   NaN
```

### 5.3 Rellenar valores al usar reindex()

**Para evitar valores NaN, podemos usar el parámetro fill_value:**

```python
df_nuevo = df.reindex(['A', 'B', 'C', 'D'], fill_value="Desconocido")
print(df_nuevo)
```

**Salida:**

```
    Nombre        Edad
A      Ana        25.0
B     Juan        30.0
C    Pedro        35.0
D  Desconocido  Desconocido
```

**reindex() es útil cuando necesitas:** 
✅ Reordenar los datos en un orden específico. 
✅ Agregar nuevas filas o columnas con valores predeterminados. 
✅ Alinear diferentes conjuntos de datos con los mismos índices.

## 6. Operaciones en Pandas

En Pandas, podemos realizar operaciones matemáticas y lógicas en Series y DataFrames de manera eficiente.

### 6.1 Operaciones Aritméticas en Pandas

Las operaciones aritméticas (`+`, `-`, `*`, `/`, `**`, etc.) se aplican directamente a Series y DataFrames. Si los índices coinciden, se realizan las operaciones elemento a elemento.

**Ejemplo: Operaciones con Series**

```python
import pandas as pd
serie1 = pd.Series([10, 20, 30], index=["A", "B", "C"])
serie2 = pd.Series([1, 2, 3], index=["A", "B", "C"])
suma = serie1 + serie2
resta = serie1 - serie2
multiplicacion = serie1 * serie2
division = serie1 / serie2
print("Suma:\n", suma)
print("\nResta:\n", resta)
print("\nMultiplicación:\n", multiplicacion)
print("\nDivisión:\n", division)
```

**Salida:**

```
Suma:
 A    11
B    22
C    33
dtype: int64

Resta:
 A     9
B    18
C    27
dtype: int64

Multiplicación:
 A    10
B    40
C    90
dtype: int64

División:
 A    10.0
B    10.0
C    10.0
dtype: float64
```

### 6.2 Alineación en Operaciones

Si las Series o DataFrames tienen índices diferentes, Pandas intenta alinear los datos. Si un índice no está presente en ambos, el resultado será NaN.

**Ejemplo: Alineación automática**

```python
serie3 = pd.Series([100, 200, 300], index=["A", "B", "D"])
resultado = serie1 + serie3
print(resultado)
```

**Salida:**

```
A    110.0
B    220.0
C      NaN
D      NaN
dtype: float64
```

### 6.3 Operaciones Lógicas en Pandas

Podemos aplicar operadores lógicos (`&`, `|`, `~`) para filtrar datos.

**Ejemplo: Operaciones lógicas en un DataFrame**

```python
df = pd.DataFrame({
    "Nombre": ["Ana", "Juan", "Pedro", "Sofía"],
    "Edad": [25, 30, 35, 40],
    "Ciudad": ["Santiago", "Lima", "Buenos Aires", "Bogotá"]
})
# Filtrar personas mayores de 30 años
filtro_edad = df[df["Edad"] > 30]
print(filtro_edad)
```

**Salida:**

```
   Nombre  Edad        Ciudad
2   Pedro    35  Buenos Aires
3   Sofía    40        Bogotá
```

**Ejemplo: Combinar condiciones con & y |**

```python
# Personas mayores de 30 y que viven en Buenos Aires
filtro_combinado = df[(df["Edad"] > 30) & (df["Ciudad"] == "Buenos Aires")]
print(filtro_combinado)
```

**Salida:**

```
  Nombre  Edad        Ciudad
2  Pedro    35  Buenos Aires
```

### 6.4 Métodos Asociados a Operaciones

Pandas ofrece métodos que facilitan operaciones matemáticas:

|Método|Descripción|
|---|---|
|`sum()`|Suma de los valores|
|`mean()`|Media (promedio)|
|`median()`|Mediana|
|`std()`|Desviación estándar|
|`min()`|Mínimo|
|`max()`|Máximo|
|`abs()`|Valor absoluto|
|`round(n)`|Redondeo a n decimales|

**Ejemplo: Aplicando métodos matemáticos en un DataFrame**

```python
df["Edad"].sum()  # Suma total de edades
df["Edad"].mean()  # Promedio de edad
df["Edad"].max()  # Edad máxima
df["Edad"].min()  # Edad mínima
df["Edad"].std()  # Desviación estándar
```

### 6.5 Comparaciones en Pandas

Podemos comparar valores con operadores como `==`, `!=`, `>`, `<`, `>=`, `<=`.

**Ejemplo: Comparaciones en Series**

```python
serie = pd.Series([10, 20, 30, 40])
comparacion = serie > 25
print(comparacion)
```

**Salida:**

```
0    False
1    False
2     True
3     True
dtype: bool
```

**Ejemplo: Comparaciones en un DataFrame**

```python
df["Mayor de 30"] = df["Edad"] > 30
print(df)
```

**Salida:**

```
   Nombre  Edad        Ciudad  Mayor de 30
0     Ana    25      Santiago       False
1    Juan    30          Lima       False
2   Pedro    35  Buenos Aires        True
3   Sofía    40        Bogotá        True
```

## Resumen de Conceptos Clave

- **Series y DataFrames**: Estructuras principales de Pandas para almacenar datos.
- **Indexación**:
    - `.loc[]` → Usa nombres de índices y columnas.
    - `.iloc[]` → Usa posiciones numéricas.
- **Filtrado de datos**: Permite seleccionar filas según condiciones.
- **Índices**: Etiquetas que identifican filas y columnas.
- **Reindexación**: Método para reordenar o modificar índices.
- **Operaciones**:
    - Aritméticas → Suma, resta, multiplicación, etc.
    - Lógicas → Filtrado con `&`, `|`, `~`
    - Métodos asociados → `sum()`, `mean()`, `max()`, etc.
    - Comparaciones → Operadores `>`, `<`, `==`, etc.

## **1️⃣ `groupby()` en Pandas**

El método `groupby()` permite **agrupar datos** en un `DataFrame` en función de una o más columnas, aplicando funciones agregadas.

### **Ejemplo:** Agrupar por categoría y calcular la media

```python
import pandas as pd

# Crear un DataFrame
datos = {
    "Categoria": ["A", "A", "B", "B", "C", "C"],
    "Valor": [10, 20, 30, 40, 50, 60]
}
df = pd.DataFrame(datos)

# Agrupar por "Categoria" y calcular la media
grupo = df.groupby("Categoria")["Valor"].mean()

print(grupo)
```

**Salida:**

```
Categoria
A    15.0
B    35.0
C    55.0
Name: Valor, dtype: float64
```

📌 **Funciones comunes con `groupby()`**  
✔ `sum()` → Suma de valores en cada grupo  
✔ `mean()` → Promedio de cada grupo  
✔ `count()` → Cantidad de elementos en cada grupo  
✔ `max()` / `min()` → Máximo y mínimo de cada grupo

---

## **2️⃣ Manejo de Missing Values (Valores Faltantes)**

En Pandas, los valores faltantes se representan como `NaN`. Hay varias formas de **tratarlos**.

### **Ejemplo:** Identificar y eliminar valores faltantes

```python
import numpy as np

# Crear un DataFrame con valores faltantes
df = pd.DataFrame({
    "Nombre": ["Ana", "Juan", "Pedro", np.nan],
    "Edad": [25, np.nan, 35, 40]
})

print(df)  # Mostrar datos originales

# Identificar valores faltantes
print(df.isna())  

# Eliminar filas con valores NaN
df_sin_na = df.dropna()
print(df_sin_na)
```

📌 **Métodos útiles:**  
✔ `isna()` / `isnull()` → Identificar valores NaN  
✔ `dropna()` → Eliminar filas con NaN  
✔ `fillna(valor)` → Reemplazar NaN con un valor

---

## **3️⃣ Manejo de Strings (`str`)**

Pandas permite **manipular cadenas de texto** dentro de los `DataFrame`.

### **Ejemplo:** Convertir a mayúsculas y eliminar espacios

```python
df = pd.DataFrame({"Nombres": [" ana ", "JUAN", "Pedro "]})

df["Nombres"] = df["Nombres"].str.strip().str.upper()
print(df)
```

**Salida:**

```
  Nombres
0     ANA
1    JUAN
2   PEDRO
```

📌 **Métodos útiles con `.str`**  
✔ `.str.upper()` → Convertir a mayúsculas  
✔ `.str.lower()` → Convertir a minúsculas  
✔ `.str.strip()` → Eliminar espacios en blanco  
✔ `.str.contains("x")` → Buscar texto

---

## **4️⃣ Manejo de Fechas y Horas**

Pandas maneja **fechas y tiempos** con `pd.to_datetime()`.

### **Ejemplo:** Convertir texto a fecha y calcular diferencia

```python
df = pd.DataFrame({"Fecha": ["2024-01-01", "2024-02-15", "2024-03-10"]})

df["Fecha"] = pd.to_datetime(df["Fecha"])
df["Días transcurridos"] = df["Fecha"] - df["Fecha"].min()

print(df)
```

**Salida:**

```
       Fecha Días transcurridos
0 2024-01-01      0 days
1 2024-02-15     45 days
2 2024-03-10     69 days
```

📌 **Funciones clave con fechas**  
✔ `pd.to_datetime()` → Convertir a fecha  
✔ `.dt.day`, `.dt.month`, `.dt.year` → Extraer día, mes y año  
✔ `df["Fecha"].max() - df["Fecha"].min()` → Diferencia de tiempo

---

## **5️⃣ Graficar con Pandas (`plot()`)**

Podemos generar gráficos con Pandas usando `.plot()`, basado en Matplotlib.

### **Ejemplo:** Graficar datos

```python
import matplotlib.pyplot as plt

# Crear un DataFrame
df = pd.DataFrame({
    "Día": [1, 2, 3, 4, 5],
    "Ventas": [100, 200, 150, 300, 250]
})

# Crear el gráfico
df.plot(x="Día", y="Ventas", kind="line", marker="o")
plt.title("Ventas Diarias")
plt.xlabel("Día")
plt.ylabel("Ventas")
plt.show()
```

📌 **Tipos de gráficos comunes**  
✔ `kind="line"` → Gráfico de líneas  
✔ `kind="bar"` → Barras  
✔ `kind="hist"` → Histograma  
✔ `kind="pie"` → Pastel

---

### **📌 Resumen de lo aprendido**

✔ **`groupby()`** → Agrupa datos y aplica funciones.  
✔ **Missing values** → Detectar, eliminar y rellenar valores NaN.  
✔ **Manejo de Strings** → `.str.upper()`, `.str.strip()`, `.str.contains()`.  
✔ **Fechas y Horas** → `pd.to_datetime()`, `.dt.year`, `.dt.month`, `.dt.day`.  
✔ **Gráficos con Pandas** → `.plot(kind="...")` con Matplotlib.


## IDXMIN Y IDXMAX
En **Pandas**, las funciones `idxmin()` e `idxmax()` se utilizan para encontrar el **índice** del valor mínimo y máximo de una columna o Serie.

---

## **📌 `idxmin()` y `idxmax()` en Pandas**

- `idxmin()` → Devuelve el índice donde se encuentra el **valor mínimo** de la Serie o columna del DataFrame.
    
- `idxmax()` → Devuelve el índice donde se encuentra el **valor máximo** de la Serie o columna del DataFrame.
    

---

### **Ejemplo de uso**

python

CopiarEditar

`import pandas as pd  # Crear un DataFrame df = pd.DataFrame({     "Producto": ["A", "B", "C", "D"],     "Precio": [150, 200, 120, 300] })  # Encontrar el índice del valor mínimo y máximo en la columna "Precio" indice_min = df["Precio"].idxmin() indice_max = df["Precio"].idxmax()  print(f"Índice del precio mínimo: {indice_min}")  # Devuelve el índice de "C" print(f"Índice del precio máximo: {indice_max}")  # Devuelve el índice de "D"`

**Salida esperada:**

less

CopiarEditar

`Índice del precio mínimo: 2 Índice del precio máximo: 3`

---

### **📌 Notas importantes**

✔ `idxmin()` y `idxmax()` **devuelven el índice, no el valor**.  
✔ Se pueden usar en columnas numéricas de un DataFrame o en Series.  
✔ Si hay valores `NaN`, se pueden manejar con `dropna()` antes de aplicar la función.

---

# MATPLOTLIB
## **📌 Introducción a Matplotlib**

Matplotlib permite crear gráficos como **líneas, barras, histogramas, dispersión, torta (pie), entre otros**. Su módulo más usado es `pyplot`.

**📌 Importación de la librería**

python

CopiarEditar

`import matplotlib.pyplot as plt`

---

## **1️⃣ Gráfico de Líneas**

Se usa para visualizar la evolución de datos en función de otra variable, generalmente el tiempo.

python

CopiarEditar

`import matplotlib.pyplot as plt  # Datos de ejemplo x = [1, 2, 3, 4, 5] y = [10, 20, 15, 25, 30]  # Crear el gráfico plt.plot(x, y, marker="o", linestyle="-", color="b", label="Ventas")  # Personalizar el gráfico plt.xlabel("Día") plt.ylabel("Ventas") plt.title("Ventas Diarias") plt.legend() plt.grid()  # Mostrar el gráfico plt.show()`

📌 **Elementos clave**  
✔ `plt.plot(x, y, marker="o", linestyle="-", color="b")` → Personaliza el gráfico.  
✔ `plt.xlabel()` / `plt.ylabel()` → Etiquetas de ejes.  
✔ `plt.title()` → Título del gráfico.  
✔ `plt.legend()` → Agrega leyenda.  
✔ `plt.grid()` → Agrega una cuadrícula.

---

## **2️⃣ Gráfico de Barras**

Se usa para comparar **valores categóricos**.

python

CopiarEditar

`categorias = ["A", "B", "C", "D"] valores = [15, 30, 25, 10]  plt.bar(categorias, valores, color="purple")  plt.xlabel("Categorías") plt.ylabel("Valores") plt.title("Gráfico de Barras") plt.show()`

📌 También se puede hacer **barras horizontales** con `plt.barh()`.

---

## **3️⃣ Histograma**

Se usa para representar **distribuciones de datos**.

python

CopiarEditar

`import numpy as np  datos = np.random.randn(1000)  # Genera 1000 datos aleatorios  plt.hist(datos, bins=30, color="green", edgecolor="black") plt.xlabel("Valores") plt.ylabel("Frecuencia") plt.title("Histograma") plt.show()`

📌 `bins=30` define el número de barras o clases en el histograma.

---

## **4️⃣ Gráfico de Dispersión (Scatter Plot)**

Se usa para analizar la relación entre dos variables.

python

CopiarEditar

`x = np.random.rand(50) y = np.random.rand(50)  plt.scatter(x, y, color="red", marker="x") plt.xlabel("Variable X") plt.ylabel("Variable Y") plt.title("Gráfico de Dispersión") plt.show()`

📌 Se usa para encontrar **correlaciones** entre dos variables.

---

## **5️⃣ Gráfico de Torta (Pie Chart)**

Se usa para representar proporciones.

python

CopiarEditar

`etiquetas = ["A", "B", "C", "D"] valores = [30, 20, 35, 15]  plt.pie(valores, labels=etiquetas, autopct="%1.1f%%", colors=["blue", "green", "red", "yellow"]) plt.title("Distribución de Categorías") plt.show()`

📌 `autopct="%1.1f%%"` muestra el porcentaje en cada sector.

---

### **📌 Resumen**

✔ `plt.plot()` → **Líneas**  
✔ `plt.bar()` → **Barras**  
✔ `plt.hist()` → **Histogramas**  
✔ `plt.scatter()` → **Dispersión**  
✔ `plt.pie()` → **Torta**

### **📌 `.plot()` en Pandas y Matplotlib**

La función `.plot()` en **Pandas** es una interfaz simplificada para graficar datos utilizando **Matplotlib**. Permite crear rápidamente diferentes tipos de gráficos sin necesidad de escribir muchas líneas de código.

---

## **1️⃣ Sintaxis General**

python

CopiarEditar

`df.plot(kind="tipo_de_gráfico", x="columna_x", y="columna_y", ...)`

📌 **Argumentos principales**:  
✔ `kind` → Tipo de gráfico (**line**, **bar**, **hist**, **scatter**, etc.).  
✔ `x` → Columna del eje X.  
✔ `y` → Columna del eje Y.

> **Nota**: Para que `df.plot()` funcione, el DataFrame debe contener datos numéricos.

---

## **2️⃣ Gráfico de Líneas**

Es el tipo por defecto si no se especifica `kind`.

python

CopiarEditar

`import pandas as pd import matplotlib.pyplot as plt  # Crear DataFrame datos = {     "Día": [1, 2, 3, 4, 5],     "Ventas": [100, 200, 150, 300, 250] } df = pd.DataFrame(datos)  # Graficar df.plot(x="Día", y="Ventas", kind="line", marker="o", color="b", title="Ventas Diarias") plt.show()`

📌 **Elementos clave**:  
✔ `marker="o"` → Agrega puntos en la línea.  
✔ `color="b"` → Color azul.  
✔ `title="Ventas Diarias"` → Agrega título al gráfico.

---

## **3️⃣ Gráfico de Barras**

python

CopiarEditar

`df.plot(x="Día", y="Ventas", kind="bar", color="green", title="Ventas por Día") plt.show()`

📌 **Para barras horizontales**, usa `kind="barh"`.

---

## **4️⃣ Histograma**

python

CopiarEditar

`df["Ventas"].plot(kind="hist", bins=5, color="red", edgecolor="black") plt.show()`

📌 `bins=5` define el número de intervalos.

---

## **5️⃣ Gráfico de Dispersión**

python

CopiarEditar

`df.plot(x="Día", y="Ventas", kind="scatter", color="purple") plt.show()`

📌 Se usa para analizar correlaciones entre dos variables.

---

## **6️⃣ Gráfico de Torta**

python

CopiarEditar

`df.plot(y="Ventas", kind="pie", labels=df["Día"], autopct="%1.1f%%") plt.show()`

📌 `autopct="%1.1f%%"` muestra los porcentajes en cada sector.

---

### **📌 Resumen de `.plot()`**

✔ `.plot(kind="line")` → **Líneas** (por defecto).  
✔ `.plot(kind="bar")` → **Barras verticales**.  
✔ `.plot(kind="barh")` → **Barras horizontales**.  
✔ `.plot(kind="hist")` → **Histogramas**.  
✔ `.plot(kind="scatter")` → **Dispersión**.  
✔ `.plot(kind="pie")` → **Torta**.

### **📌 Format Strings en Matplotlib**

En **Matplotlib**, los **format strings** (cadenas de formato) son atajos que permiten definir rápidamente el **color**, **estilo de línea** y **marcador** en los gráficos de líneas con `plt.plot()`.

---

## **📌 Sintaxis General**

python

CopiarEditar

`plt.plot(x, y, "formato")`

Donde `"formato"` es una combinación de:  
✔ **Color** (ej. `"r"` para rojo).  
✔ **Estilo de línea** (ej. `"-"` para línea continua).  
✔ **Marcador** (ej. `"o"` para círculos).

---

## **1️⃣ Definir solo el color**

python

CopiarEditar

`import matplotlib.pyplot as plt  x = [1, 2, 3, 4, 5] y = [10, 15, 7, 20, 18]  plt.plot(x, y, "g")  # Gráfico verde plt.show()`

📌 `"g"` significa **verde** (green).

---

## **2️⃣ Definir color y tipo de línea**

python

CopiarEditar

`plt.plot(x, y, "r--")  # Línea roja discontinua plt.show()`

📌 `"r--"` → **Rojo (`r`) + Línea discontinua (`--`)**.

---

## **3️⃣ Agregar marcadores**

python

CopiarEditar

`plt.plot(x, y, "bo-")  # Línea azul con círculos en cada punto plt.show()`

📌 `"bo-"` → **Azul (`b`) + Línea sólida (`-`) + Círculos (`o`)**.

---

## **📌 Tabla de Formatos**

|Tipo|Código|Ejemplo|
|---|---|---|
|**Colores**|`"r"`, `"g"`, `"b"`, `"c"`, `"m"`, `"y"`, `"k"`, `"w"`|`"r-"` (rojo sólido)|
|**Líneas**|`"-"`, `"--"`, `"-."`, `":"`|`"g--"` (verde discontinua)|
|**Marcadores**|`"o"`, `"s"`, `"D"`, `"x"`, `"+"`, `"*"`, `"v"`, `"^"`|`"mD-"` (magenta con rombos)|

📌 **Ejemplo con varios formatos**:

python

CopiarEditar

`plt.plot(x, y, "mD-.")  # Magenta con rombos y línea punteada plt.show()`

---

### **📌 Resumen**

✔ `"r-"` → **Rojo con línea continua**  
✔ `"b--"` → **Azul con línea discontinua**  
✔ `"g*-"` → **Verde con línea y estrellas como marcadores**  
✔ `"kD:"` → **Negro con rombos y línea punteada**

### **📌 Anatomía de un Gráfico en Matplotlib**

Cuando creamos gráficos en **Matplotlib**, estos tienen diferentes **componentes** que se pueden personalizar. Es importante conocerlos para modificar y mejorar la presentación de nuestros gráficos.

---

## **1️⃣ Estructura General de un Gráfico**

En **Matplotlib**, un gráfico está compuesto por:

1. **Figure** → Es la ventana o área donde se dibuja el gráfico.
    
2. **Axes** → Representa los ejes del gráfico (puede haber más de uno en una Figure).
    
3. **Axis** → Los ejes individuales (`x` e `y`).
    
4. **Ticks** → Marcas en los ejes (`x` y `y`) para indicar valores.
    
5. **Labels** → Nombres de los ejes.
    
6. **Title** → Título del gráfico.
    
7. **Legend** → Leyenda para identificar los datos.
    
8. **Grid** → Cuadrícula de fondo.
    

---

## **2️⃣ Ejemplo Visual de la Anatomía**

python

CopiarEditar

`import matplotlib.pyplot as plt import numpy as np  # Datos de ejemplo x = np.linspace(0, 10, 100) y = np.sin(x)  # Crear la figura y los ejes fig, ax = plt.subplots()  # Dibujar la línea ax.plot(x, y, label="Seno(x)", color="b", linestyle="--", marker="o")  # Agregar títulos y etiquetas ax.set_title("Ejemplo de Anatomía de un Gráfico") ax.set_xlabel("Eje X") ax.set_ylabel("Eje Y")  # Configurar ticks (marcas en los ejes) ax.set_xticks([0, 2, 4, 6, 8, 10]) ax.set_yticks([-1, -0.5, 0, 0.5, 1])  # Agregar leyenda ax.legend()  # Agregar una cuadrícula ax.grid(True, linestyle=":", linewidth=0.7)  # Mostrar el gráfico plt.show()`

---

## **3️⃣ Explicación del Código**

✔ `fig, ax = plt.subplots()` → Crea una figura y un conjunto de ejes.  
✔ `ax.plot(x, y, label="Seno(x)", color="b", linestyle="--", marker="o")` → Dibuja la función seno con formato.  
✔ `ax.set_title("Ejemplo de Anatomía de un Gráfico")` → Agrega un título.  
✔ `ax.set_xlabel("Eje X")` y `ax.set_ylabel("Eje Y")` → Etiquetas de los ejes.  
✔ `ax.set_xticks([...])` y `ax.set_yticks([...])` → Personaliza los ticks.  
✔ `ax.legend()` → Agrega una leyenda.  
✔ `ax.grid(True, linestyle=":", linewidth=0.7)` → Activa la cuadrícula.

---

## **4️⃣ Estructura Jerárquica de Matplotlib**

📌 **Figura (`Figure`)**: Es el contenedor principal.  
📌 **Ejes (`Axes`)**: Representan el área donde se dibujan los gráficos.  
📌 **Ejes individuales (`Axis`)**: `x-axis` y `y-axis`.  
📌 **Elementos visuales**: Ticks, labels, leyenda, cuadrícula.

---

### **📌 Resumen**

✔ Un gráfico en **Matplotlib** se compone de una **Figura (`Figure`)** y al menos un conjunto de **Ejes (`Axes`)**.  
✔ Podemos personalizar **ticks, labels, título, leyenda y cuadrícula** para mejorar la visualización.  
✔ Se recomienda trabajar con `fig, ax = plt.subplots()` para mayor control sobre los gráficos

### **📌 Tipos de Gráficos en Matplotlib**

Matplotlib permite crear distintos tipos de gráficos según la necesidad del análisis de datos. Aquí te explico los principales junto con ejemplos prácticos.

---

## **1️⃣ Gráfico de Líneas (`line plot`)**

📌 Útil para representar tendencias a lo largo del tiempo o cambios continuos.

python

CopiarEditar

`import matplotlib.pyplot as plt import numpy as np  x = np.linspace(0, 10, 100) y = np.sin(x)  plt.plot(x, y, label="Seno(x)", color="b", linestyle="--", marker="o") plt.title("Gráfico de Líneas") plt.xlabel("Eje X") plt.ylabel("Eje Y") plt.legend() plt.grid(True) plt.show()`

---

## **2️⃣ Gráfico de Barras (`bar plot`)**

📌 Se usa para comparar categorías o valores discretos.

python

CopiarEditar

`categorias = ["A", "B", "C", "D"] valores = [5, 7, 3, 8]  plt.bar(categorias, valores, color="purple") plt.title("Gráfico de Barras") plt.xlabel("Categorías") plt.ylabel("Valores") plt.show()`

📌 **Para barras horizontales**, usa `plt.barh()`:

python

CopiarEditar

`plt.barh(categorias, valores, color="orange") plt.show()`

---

## **3️⃣ Histograma (`histogram`)**

📌 Representa la distribución de datos dividiéndolos en intervalos (bins).

python

CopiarEditar

`datos = np.random.randn(1000)  # 1000 valores aleatorios con distribución normal  plt.hist(datos, bins=30, color="skyblue", edgecolor="black") plt.title("Histograma de Datos") plt.xlabel("Valores") plt.ylabel("Frecuencia") plt.show()`

---

## **4️⃣ Gráfico de Dispersión (`scatter plot`)**

📌 Útil para visualizar correlaciones entre dos variables.

python

CopiarEditar

`x = np.random.rand(100) y = np.random.rand(100)  plt.scatter(x, y, color="red", alpha=0.5) plt.title("Gráfico de Dispersión") plt.xlabel("Variable X") plt.ylabel("Variable Y") plt.show()`

📌 **Personalización**:

- `alpha=0.5` → Transparencia de los puntos.
    
- `color="red"` → Color de los puntos.
    

---

## **5️⃣ Gráfico de Torta (`pie chart`)**

📌 Representa proporciones de un todo.

python

CopiarEditar

`etiquetas = ["A", "B", "C", "D"] valores = [25, 35, 20, 20]  plt.pie(valores, labels=etiquetas, autopct="%1.1f%%", colors=["blue", "green", "red", "yellow"]) plt.title("Gráfico de Torta") plt.show()`

📌 **Personalización**:

- `autopct="%1.1f%%"` → Muestra los porcentajes en cada sector.
    

---

## **6️⃣ Gráfico de Caja y Bigotes (`box plot`)**

📌 Se usa para visualizar la distribución de datos y detectar outliers.

python

CopiarEditar

`data = [np.random.randn(100), np.random.randn(100) * 1.5 + 1]  plt.boxplot(data, labels=["Conjunto 1", "Conjunto 2"]) plt.title("Gráfico de Caja") plt.show()`

---

## **7️⃣ Gráfico de Área (`area plot`)**

📌 Similar al gráfico de líneas, pero con el área debajo de la curva rellenada.

python

CopiarEditar

`x = np.linspace(0, 10, 100) y = np.sin(x)  plt.fill_between(x, y, color="cyan", alpha=0.5) plt.title("Gráfico de Área") plt.xlabel("Eje X") plt.ylabel("Eje Y") plt.show()`

📌 **Personalización**:

- `fill_between(x, y, color="cyan", alpha=0.5)` → Rellena el área bajo la curva con color.
    

---

## **8️⃣ Gráfico de Barras Apiladas**

📌 Útil para visualizar partes de un todo.

python

CopiarEditar

`categorias = ["A", "B", "C"] valores1 = [3, 5, 2] valores2 = [4, 6, 3]  plt.bar(categorias, valores1, color="blue", label="Grupo 1") plt.bar(categorias, valores2, bottom=valores1, color="orange", label="Grupo 2") plt.title("Gráfico de Barras Apiladas") plt.legend() plt.show()`

---

### **📌 Resumen de Tipos de Gráficos en Matplotlib**

✔ **Líneas (`plt.plot()`)** → Tendencias y evolución.  
✔ **Barras (`plt.bar()`)** → Comparaciones entre categorías.  
✔ **Histogramas (`plt.hist()`)** → Distribución de datos.  
✔ **Dispersión (`plt.scatter()`)** → Correlación entre variables.  
✔ **Torta (`plt.pie()`)** → Proporciones.  
✔ **Caja y Bigotes (`plt.boxplot()`)** → Distribución y valores atípicos.  
✔ **Área (`plt.fill_between()`)** → Representación acumulativa.  
✔ **Barras Apiladas (`plt.bar()` con `bottom=`)** → Comparación entre grupos.

### **📌 ¿Qué es un Subplot en Matplotlib?**

Un **subplot** en Matplotlib es una forma de mostrar **múltiples gráficos en una sola figura**. Se usa para comparar visualizaciones sin necesidad de abrir varias ventanas o imágenes separadas.

---

## **1️⃣ Métodos para Crear Subplots**

### **Método 1: `plt.subplot()`**

📌 Divide la figura en una cuadrícula (`nrows x ncols`) y selecciona la celda activa.

python

CopiarEditar

`import matplotlib.pyplot as plt import numpy as np  x = np.linspace(0, 10, 100) y1, y2 = np.sin(x), np.cos(x)  plt.figure(figsize=(8, 6))  # Tamaño de la figura  # Primer subplot (1 fila, 2 columnas, primer gráfico) plt.subplot(1, 2, 1) plt.plot(x, y1, color="blue") plt.title("Seno")  # Segundo subplot (1 fila, 2 columnas, segundo gráfico) plt.subplot(1, 2, 2) plt.plot(x, y2, color="red") plt.title("Coseno")  plt.tight_layout()  # Ajusta los espacios plt.show()`

📌 **Explicación**:

- `plt.subplot(1, 2, 1)` → Primer gráfico (1 fila, 2 columnas, celda 1).
    
- `plt.subplot(1, 2, 2)` → Segundo gráfico (1 fila, 2 columnas, celda 2).
    
- `plt.tight_layout()` → Evita que los gráficos se solapen.
    

---

### **Método 2: `plt.subplots()` (Más Recomendado)**

📌 Crea la figura y una matriz de **ejes (`Axes`)** de manera más estructurada.

python

CopiarEditar

`fig, axes = plt.subplots(2, 2, figsize=(8, 6))  # 2 filas, 2 columnas  x = np.linspace(0, 10, 100) y1, y2, y3, y4 = np.sin(x), np.cos(x), np.tan(x), np.exp(-x)  # Asignar gráficos a cada subplot axes[0, 0].plot(x, y1, color="blue") axes[0, 0].set_title("Seno")  axes[0, 1].plot(x, y2, color="red") axes[0, 1].set_title("Coseno")  axes[1, 0].plot(x, y3, color="green") axes[1, 0].set_title("Tangente")  axes[1, 1].plot(x, y4, color="purple") axes[1, 1].set_title("Exponencial")  plt.tight_layout()  # Ajusta espacios plt.show()`

📌 **Ventajas de `plt.subplots()`**: ✔ Retorna una matriz de ejes (`Axes`), facilitando la manipulación.  
✔ Acceso directo a cada gráfico con `axes[row, col]`.  
✔ Compatible con `fig.suptitle("Título General")` para un título global.

---

### **Método 3: `add_subplot()` con `fig`**

📌 Alternativa para agregar subplots de forma manual.

python

CopiarEditar

`fig = plt.figure(figsize=(8, 6))  ax1 = fig.add_subplot(2, 2, 1) ax1.plot(x, np.sin(x)) ax1.set_title("Seno")  ax2 = fig.add_subplot(2, 2, 2) ax2.plot(x, np.cos(x)) ax2.set_title("Coseno")  plt.tight_layout() plt.show()`

---

## **📌 Resumen**

✔ **`plt.subplot()`** → Divide en una cuadrícula y asigna cada gráfico.  
✔ **`plt.subplots()`** → Método más recomendado, usa una matriz de ejes (`Axes`).  
✔ **`add_subplot()`** → Permite agregar gráficos manualmente a una figura (`fig`).  
✔ **Usar `plt.tight_layout()`** → Para mejorar la distribución de gráficos.