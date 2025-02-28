# 1. Introducción, conceptos y condicionales

## Programación y estructura de un programa

La programación es el proceso de escribir instrucciones en un lenguaje de programación, como Python, que le indican a una computadora qué hacer. Un programa es un conjunto de instrucciones que resuelve un problema específico. La estructura básica de un programa en Python consta de:

1. **Declaraciones de importación**: Permiten utilizar código de bibliotecas externas.
2. **Definiciones de funciones**: Bloques de código reutilizables.
3. **Declaraciones de variables**: Almacenan valores que pueden cambiar durante la ejecución del programa.
4. **Estructuras de control de flujo**: Determinan qué partes del código se ejecutan, como condicionales e iteraciones.
5. **Entrada y salida de datos**: Interacción con el usuario o archivos.

```python
# Ejemplo de programa básico
nombre = input("Ingresa tu nombre: ") # Entrada de datos
edad = int(input("Ingresa tu edad: ")) # Conversión de tipo

if edad >= 18: # Condicional
    print(f"Bienvenido {nombre}, eres mayor de edad.") # Salida de datos
else:
    print(f"{nombre}, eres menor de edad.")
```

## Preparación del entorno

Para comenzar a programar en Python, necesitarás:

1. **Instalar Python**: Puedes descargarlo desde el sitio web oficial (python.org).
2. **Elegir un IDE (Entorno de Desarrollo Integrado)** o un editor de código: Estos son programas que facilitan la escritura, ejecución y depuración de código. Algunos populares son PyCharm, Visual Studio Code y IDLE (este último viene incluido con Python).

## Concepto de IDE, editor de código y otras herramientas

- **IDE (Entorno de Desarrollo Integrado)**: Es una aplicación que combina varias herramientas para facilitar el desarrollo de software, como un editor de código, un compilador o intérprete, un depurador, etc. Ejemplos: PyCharm, Visual Studio.
- **Editor de código**: Es un programa diseñado específicamente para editar código fuente. Algunos son más simples, mientras que otros ofrecen características adicionales como resaltado de sintaxis, autocompletado, etc. Ejemplos: Visual Studio Code, Sublime Text, Atom.
- **Otras herramientas**: Además del IDE o editor de código, puedes utilizar herramientas adicionales como sistemas de control de versiones (Git), herramientas de pruebas unitarias, entornos virtuales, etc.

## Fundamentos del lenguaje

### Tipos de datos

Python tiene varios tipos de datos integrados:

- **Números**: Enteros (int), flotantes (float), complejos.
- **Cadenas de texto** (str): Secuencias de caracteres.
- **Booleanos** (bool): Valores Verdadero (True) o Falso (False).
- **Listas**: Colecciones ordenadas de elementos.
- **Tuplas**: Colecciones ordenadas e inmutables de elementos.
- **Diccionarios**: Colecciones desordenadas de pares clave-valor.
- **Conjuntos**: Colecciones desordenadas de elementos únicos.

```python
entero = 42
flotante = 3.14
cadena = "Hola, mundo"
booleano = True
lista = [1, 2, 3, 4]
tupla = (1, 2, 3, 4)
diccionario = {"clave": "valor", "edad": 30}
conjunto = {1, 2, 3, 4}
```

### Operaciones básicas

Python admite operaciones aritméticas, de comparación, lógicas y de asignación:

```python
# Operaciones aritméticas
suma = 2 + 3
resta = 5 - 2
multiplicacion = 4 * 6
division = 10 / 2

# Operaciones de comparación
es_igual = 5 == 5  # True
es_distinto = 4 != 3  # True
es_mayor = 7 > 5  # True
es_menor = 2 < 10  # True

# Operaciones lógicas
and_logico = True and False  # False
or_logico = True or False  # True
not_logico = not False  # True

# Operaciones de asignación
x = 5
x += 3  # x = x + 3 = 8
```

### Condicionales

Las estructuras condicionales permiten ejecutar diferentes bloques de código según una condición. La más común es `if`/`elif`/`else`:

```python
edad = 17

if edad < 18:
    print("Eres menor de edad.")
elif edad < 21:
    print("Eres mayor de edad, pero menor de 21 años.")
else:
    print("Eres mayor de 21 años.")
```

También existe la estructura condicional `match`/`case` (nueva en Python 3.10):

```python
opcion = "b"

match opcion:
    case "a":
        print("Elegiste la opción a")
    case "b":
        print("Elegiste la opción b")
    case _:
        print("Opción no válida")
```

# 2. Entrada de datos, bucles y listas

## Conversión entre tipos de datos

A menudo, necesitarás convertir un tipo de dato a otro. Python proporciona funciones integradas para esto:

```python
# Convertir a entero
x = int("42")  # x = 42

# Convertir a flotante
y = float("3.14")  # y = 3.14

# Convertir a cadena
z = str(100)  # z = "100"

# Convertir a booleano
a = bool(0)  # a = False
b = bool(1)  # b = True
```

## Sintaxis y operaciones de acceso a elementos

Las cadenas de texto, listas y tuplas son secuencias de elementos a las que puedes acceder mediante índices:

```python
cadena = "Hola, mundo"
lista = [1, 2, 3, 4, 5]
tupla = (6, 7, 8, 9, 10)

# Acceder a un elemento
print(cadena[0])  # "H"
print(lista[2])  # 3
print(tupla[4])  # 10

# Rebanadas (slicing)
subcadena = cadena[0:5]  # "Hola,"
sublista = lista[1:4]  # [2, 3, 4]
subtupla = tupla[2:]  # (8, 9, 10)
```

## Bucle while

El bucle `while` se utiliza para repetir un bloque de código mientras una condición sea verdadera:

```python
contador = 0
while contador < 5:
    print(f"Contador: {contador}")
    contador += 1  # contador = contador + 1

# Salida:
# Contador: 0
# Contador: 1
# Contador: 2
# Contador: 3
# Contador: 4
```

## Listas: concepto y propósito

Las listas son colecciones ordenadas de elementos. Puedes almacenar diferentes tipos de datos en una lista y acceder a sus elementos por índice:

```python
frutas = ["manzana", "banana", "naranja", "kiwi"]
numeros = [1, 2, 3, 4, 5]
mixta = [1, "dos", 3.14, True]

print(frutas[0])  # "manzana"
print(numeros[-1])  # 5
```

## Bucle for

El bucle `for` se utiliza para iterar sobre una secuencia (como una lista, tupla o cadena de texto):

```python
frutas = ["manzana", "banana", "naranja", "kiwi"]

for fruta in frutas:
    print(f"Fruta: {fruta}")

# Salida:
# Fruta: manzana
# Fruta: banana
# Fruta: naranja
# Fruta: kiwi
```

También puedes iterar sobre un rango de números usando la función `range()`:

```python
for i in range(5):
    print(i)

# Salida:
# 0
# 1
# 2
# 3
# 4
```

## Matrices con listas

Puedes crear matrices (arreglos bidimensionales) utilizando listas anidadas:

```python
matriz = [[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]]

print(matriz[1][2])  # 6
```

# 3. Colecciones, diccionarios y funciones

## Colecciones

Python tiene varios tipos de colecciones integradas, además de listas:

- **Tuplas**: Son colecciones ordenadas e inmutables de elementos.
- **Conjuntos** (sets): Son colecciones desordenadas de elementos únicos.

```python
# Tupla
punto = (3, 4)
print(punto[0])  # 3

# Conjunto
numeros = {1, 2, 3, 4, 4, 4}  # {1, 2, 3, 4}
letras = set("hola")  # {"h", "o", "l", "a"}
```

## Diccionarios

Los diccionarios son colecciones desordenadas de pares clave-valor:

```python
persona = {"nombre": "Juan", "edad": 30, "ciudad": "Madrid"}

print(persona["nombre"])  # "Juan"
persona["edad"] = 31  # Modificar un valor
persona["profesion"] = "Ingeniero"  # Agregar un nuevo par clave-valor
```

## Rango

La función `range()` se utiliza para generar secuencias de números:

```python
# range(start, stop, step)
numeros = list(range(1, 11))  # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numeros_pares = list(range(2, 11, 2))  # [2, 4, 6, 8, 10]
```

## Funciones: conceptos básicos

Las funciones son bloques de código reutilizables que pueden tomar argumentos y devolver un valor:

```python
def saludar(nombre):
    """Esta función imprime un saludo."""
    print(f"¡Hola, {nombre}!")

saludar("Juan")  # ¡Hola, Juan!
```

## Argumentos y Retorno

Las funciones pueden tener argumentos (valores de entrada) y pueden devolver un valor usando la instrucción `return`:

```python
def suma(a, b):
    """Suma dos números."""
    return a + b

resultado = suma(3, 4)
print(resultado)  # 7
```

# 4. Bibliotecas y aplicaciones de escritorio

## Más sobre funciones

Las funciones también pueden tener argumentos opcionales (con valores predeterminados) y argumentos arbitrarios (empaquetados en tuplas o diccionarios):

```python
def funcion_args(a, b, c=0, *args, **kwargs):
    print(a, b, c)
    print(args)  # Tupla con argumentos adicionales
    print(kwargs)  # Diccionario con argumentos clave=valor

funcion_args(1, 2, 3, 4, 5, x=10, y=20)
# 1 2 3
# (4, 5)
# {'x': 10, 'y': 20}
```

## Bibliotecas, la librería estándar

Python viene con una extensa biblioteca estándar que proporciona módulos para tareas comunes, como matemáticas, manejo de archivos, expresiones regulares, etc.

```python
import math

print(math.pi)  # 3.141592653589793
print(math.sqrt(16))  # 4.0
```

## Sintaxis para incorporar módulos

Puedes importar módulos completos o partes específicas de ellos:

```python
import math  # Importar el módulo completo
from math import pi, sqrt  # Importar solo ciertas funciones

print(math.pi)  # 3.141592653589793
print(sqrt(16))  # 4.0
```

## Scripts con varios módulos

Tus propios archivos Python son módulos que puedes importar en otros scripts:

```python
# archivo calculadora.py
def suma(a, b):
    return a + b

def resta(a, b):
    return a - b

# archivo main.py
import calculadora

resultado = calculadora.suma(3, 4)
print(resultado)  # 7
```

## Módulo `tkinter`

`tkinter` es un módulo integrado que permite crear interfaces gráficas de usuario (GUIs) en Python:

```python
import tkinter as tk

root = tk.Tk()  # Crear la ventana principal
label = tk.Label(root, text="¡Hola, mundo!")
label.pack()
root.mainloop()  # Iniciar el bucle de eventos
```

## Primera aplicación

Aquí hay un ejemplo de una aplicación de escritorio simple con `tkinter`:

```python
import tkinter as tk

def saludar():
    nombre = entry_nombre.get()
    label_saludo.config(text=f"¡Hola, {nombre}!")

root = tk.Tk()
root.title("Mi aplicación")

label_nombre = tk.Label(root, text="Ingresa tu nombre:")
label_nombre.pack()

entry_nombre = tk.Entry(root)
entry_nombre.pack()

boton_saludar = tk.Button(root, text="Saludar", command=saludar)
boton_saludar.pack()

label_saludo = tk.Label(root, text="")
label_saludo.pack()

root.mainloop()
```

Este programa crea una ventana con un campo de entrada de texto, un botón "Saludar" y una etiqueta para mostrar el saludo. Al hacer clic en el botón, se ejecuta la función `saludar()`, que toma el texto del campo de entrada y lo muestra en la etiqueta de saludo.