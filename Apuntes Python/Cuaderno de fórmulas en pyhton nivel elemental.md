
## OPERADORES ESPECIALES

### OPERADORES ARITMETICOS

**`+:` Suma dos operandos.**
```python
3 + 5  # Resultado: 8
```
**`-:` Resta el segundo operando del primero.**
```python
10 - 4  # Resultado: 6
```
**`*:` Multiplica dos operandos.**
```python
2 * 3  # Resultado: 6
```
**`/:` Divide el primer operando por el segundo (resultado como flotante).** 
```python
8 / 2  # Resultado: 4.0
``````
**`%:` Devuelve el resto de la división entre dos operandos.**
```python
10 % 3  # Resultado: 1
```
**`**:` Exponenciación, eleva el primer operando a la potencia del segundo.**
```python
2 ** 3  # Resultado: 8
```
**`//:` División entera, divide el primer operando por el segundo y devuelve el resultado truncado.**
```python
10 // 3  # Resultado: 3
```
### OPERADORES DE COMPARACION

**`==`: Comprueba si dos operandos son iguales.**
```python
5 == 5  # Resultado: True`
```    
**`!=`: Comprueba si dos operandos no son iguales.** 
```python
5 != 3  # Resultado: True`
```
**`>`: Comprueba si el primer operando es mayor que el segundo.**
```python
5 > 3  # Resultado: True`
```
**`<`: Comprueba si el primer operando es menor que el segundo.**
```python
5 < 3  # Resultado: False`
```
**`>=`: Comprueba si el primer operando es mayor o igual que el segundo.**
```python
5 >= 5  # Resultado: True`
```
**`<=`: Comprueba si el primer operando es menor o igual que el segundo.**
```python
5 <= 5  # Resultado: True`
```
### OPERADORES LÓGICOS

**`and`: Devuelve `True` si ambos operandos son `True`.**
```python
True and False  # Resultado: False`
```    
**`or`: Devuelve `True` si al menos uno de los operandos es `True`.**
```python
True or False  # Resultado: True`
```    
**`not`: Invierte el valor lógico del operando.**
```python
not True  # Resultado: False`
```    
### OPERADORES DE ASIGNACION

**`=`: Asigna un valor a una variable.**
```python
x = 5`
```    
**`+=`: Suma y asigna el valor al operando de la izquierda.**
```python
x += 3  # Equivalente a x = x + 3`
```    
**`-=`: Resta y asigna el valor al operando de la izquierda.**
```python
x -= 2  # Equivalente a x = x - 2`
```
**`*=`: Multiplica y asigna el valor al operando de la izquierda.**
```python
x *= 4  # Equivalente a x = x * 4`
```    
**`/=`: Divide y asigna el valor al operando de la izquierda.**
```python
x /= 2  # Equivalente a x = x / 2`
```
**`%=`: Calcula el módulo y asigna el valor al operando de la izquierda.**
```python
x %= 2  # Equivalente a x = x % 2`
```    
**`=`: Calcula la potencia y asigna el valor al operando de la izquierda.**
````python
x **= 3  # Equivalente a x = x ** 3`
`````
 **`//=`: Realiza la división entera y asigna el valor al operando de la izquierda.**
```python
x //= 2  # Equivalente a x = x // 2`
```

### OPERADORES DE CONJUNTO
**`|`: Unión de conjuntos.
```python
{1, 2} | {2, 3}  # Resultado: {1, 2, 3}`
```    
`&`: Intersección de conjuntos.
```python
{1, 2} & {2, 3}  # Resultado: {2}`
```    
`-`: Diferencia de conjuntos.
```python
{1, 2} - {2, 3}  # Resultado: {1}`
```    
`^`: Diferencia simétrica de conjuntos (elementos en cualquiera de los conjuntos pero no en ambos).
```python
{1, 2} ^ {2, 3}  # Resultado: {1, 3}`
```    

### OTROS OPERADORES COMUNES

**`in`: Comprueba si un valor está en una secuencia (lista, tupla, cadena, etc.).
 ```python
3 in [1, 2, 3]  # Resultado: True`
```
`not in`: Comprueba si un valor no está en una secuencia.**
```python
4 not in [1, 2, 3]  # Resultado: True`
```
**`is`: Comprueba si dos referencias son al mismo objeto.
```python
`x is y`
```    
`is not`: Comprueba si dos referencias no son al mismo objeto.
```python
`x is not y`
```

## DATOS SIMPLES

### OPERACIONES SIMPLES 

**FORMULA PARA NUMERO PAR:** 
```python 
 n % 2 = 0
```
Útil para cualquier operación donde se tenga que ocupar el divisor (por ejemplo si tal numero es multiplo de)
A considerar, se debe cambiar el resto en caso de modificaciones en realción con el divisor.

### FORMULAS DE CONTABILIDAD

**FORMULA INVERSIÓN OBTENIDA:**
```python
  CAPITAL_FINAL = CANTIDAD A INVERTIR * (1 + INTERES ANUAL * AÑOS)
  INVERSION = CAPITAL FINAL - CANTIDAD INVERTIDA
```
El interés se pone como número entero
El 1+ se usa para obtener el capital final, que es igual al capital inicial más el interés simple o compuesto. El representa el monto inicial

**FORMULA DECLARACION DE LA RENTA:** 
```python
  variable = renta anual (expresado en moneda) * tipo de renta(expresado en porcentaje) 
```
Sirve para toda operación de porcentaje.

**FORMULA APLICACION DE DESCUENTO:**
```python
  variable = (monto * descuento) / 100 
```
El descuento se pone como numero entero
Su lógica es multiplicación cruzada y división

**FORMULA DE DESGLOSE:**
```python
  variable_a = variable(input) // unidad a convertir
  variable_b = variable(input) % unidad a convertir
  variable_c = variable_b // unidad a convertir
```
La lógica del desgloce es usar la DIVISIÓN ENTERA y desde ahí hacer uso del RESTO
Aplicable a toda operación que necesite desgloce a unidades tanto mayores como menores 

### FORMULAS GEOMÉTRICAS

**FORMULA PERÍMETRO DE RECTANGULO:**
```python
  P = 2 * (ALTURA + LONGITUD)
```

**FORMULA PERÍMETRO DE CIRCULO:**
```python
  P = 2 * PI * RADIO
```

**FORMULA PERÍMETRO DE TRIANGULO:**
```python
  P = A + B + C
```

**FORMULA AREA DE RECTANGULO:**
```python
  A = BASE * ALTURA
```

**FORMULA AREA DE CIRCULO:** 
```python
  A = PI * RADIO**2
```

**FORMULA AREA DE TRIANGULO:**
```python
  A = (BASE * ALTURA) / 2
```

**FORMULA AREA DE HEXAGONO REGULAR:**
```python 
A = (LADO**2 * √3) / 2
```

**FORMULA AREA DE POLÍGONO REGULAR:**
```python 
 A = (PERIMETRO * APOTEMA) / 2
  APOTEMA = RADIO * COTANGENTE_ALFA
  RADIO = RADIO_CIRCUNSCRITO * COSENO(ALFA)
  COTAGENTE_ALFA = 1 / TANGENTE(ALFA)
  ALFA = PI / LADOS DEL POLÍGONO 
```

**FORMULA VOLUMEN ESFERA:**
```python
  V = 3/4 * PI * RADIO³
```

**FORMULA VOLUMEN DE CONO:**
```python
  V = PI * RADIO**2 * (ALTURA / 3) 
```

**FORMULA CONVERSION A RADIANES:**
```python
  RADIANES = grados * (PI / 180)
```

### FORMULAS FÍSICAS

**FORMULA DE VELOCIDAD:**
```python
  VELOCIDAD FINAL = VELOCIDAD INICIAL + ACELERACION * TIEMPO
```

**FORMULA ENERGÍA CINÉTICA:**
```python
  ENERGÍA CINETICA = (VELOCIDAD**2 * MASA) / 2
```

**FORMULA CAÍDA LIBRE (SIN VARIABLE TIEMPO):**
```python
  CAIDA LIBRE = VELOCIDAD FINAL**2 / (2 * ACELERACIÓN DE GRAVEDAD)
```

**FORMULA DE FUERZA (APLICADA EN JULES):**
```python
  TRABAJO APLICADO = MAGNITUD DE FUERZA * DISTANCIA * 1
```
La fuerza se aplica en NEWTON
El 1 representa el ángulo entre la fuerza aplicada y la dirección del desplazamiento (cos 0°)

### FORMULAS DE TRIGONOMETRÍA

**FORMULA ECUACIÓN DE SEGUNDO GRADO:**
```python
  X1 = (-B +(B**2 - 4AC)**0.5) / 2A
  X2 = (-B -(B**2 - 4AC)**0.5) / 2A
  AX**2 + BX + C = 0
```
### FORMULAS TEMPORALES

**MODULO datetime**
```python  
  año actual = datetime.now()year
  hora_actual = datetime.datetime.now()
  hora = hora_actual.hour
  minutos = hora_actual.minute
  segundos = hora_actual.second
```

**MODULO time**
```python
  hora = time.strftime("%H") # Devuelve la hora 
  minutos = time.strftime("%M") # Devuelve los minutos
  segundos = time.strftime("%S") # Devuelve los segundos
```  

## CADENAS 

**LÓGICA DEL OPERADOR  " : "  PARA *slicer*:** 
```python
 variable = variable [ aqui van los caracteres que se cortan : aqui van los caracteres que se muestran ] 
```
Con números negativos es al revés
 
**FORMULA PARA REEMPLAZAR:** 
```python
  variable.replace(caracter original, caracter reemplazo)
```

**FORMULA PARA REEMPLAZAR (sin `.replace`):**
```python
variable_nueva = re.sub(caracter original, caractero reemplazado, variable original)
```
Muy útil cuando quieres reemplazar varios caracteres de una misma naturaleza (por ejemplo varios números por una x)
`re.sub` viene del módulo `re` que se usa para expresiones regulare (regex)

**FORMULA PARA CORTAR UNA CADENA:** 
```python
variable = cadena.split()
 ```
De esta manera podemos dividir una cadena en una lista, sin importa el separador 

**FORMULA DE UNIÓN:**
```python
  variable = caracter.join(argumento)
 ```
De esta manera podemos unir lo que separamos con el `.split`	

**FORMULA PARA SACAR ESPACIOS:** 
```python
variable = cadena.strip()
 ```
De esta manera podemos eliminar los espacios en blanco entre caracteres 

**FORMULA PARA PERTINENCIA:**
```python
  if cadena1 in cadena2
```
La dupla `if - in` sirve tanto para cadenas como para caractéres
Es más "efectivo" que usar bucles `for` o `while`, su eficacia radica en que if es un CONDICIONAL
Usalo cuando necesites verificar si un elemento (cadena, carácter, etc) está contenido dentro de otro elemento (cadena, lista, tupla,   etc).

**FORMULA PARA COMPROBAR INICIO:**
```python
  variable = cadena.starwith(variable de comprobación como letra o numero)
```
Así sabemos si se comienza por letra o numero según lo que estamos buscando.

**FORMULA PARA COMPROBAR FINAL:**
```python
  variable = cadena.endwith(variable de comprobación como letra o numero)
```

**FORMULA DE CONTEO:**
```python  
variable = cadena.count(subcadena)
```
Útil para contar sub-cadenas, así también cualquier elemento contenido en una cadena que sea STRING.

## CONDICIONALES 

#### LOGICA DEL CONDICIONAL `if`:
```python 
if condición:
    # Código a ejecutar si la condición es True
    pass
elif otra_condición:
    # Código a ejecutar si la condición anterior es False y esta otra_condición es True
    pass
else:
    # Código a ejecutar si todas las condiciones anteriores son False
    pass
```

#### COMPARACION DE UN VALOR:
```python
if variable_1 in variable_2
```
Tal como está expuesto en el apartado de las cadenas.
El `in` lo usamos para comparar con mas de un valor. A diferencia del `==` que es para un valor.
#### CUANDO USAR `if` Y CUANDO `elif`

**USAR `if`**:
- **Inicio de una cadena de condiciones**: Siempre comienzas con `if` para evaluar la primera condición.
- **Condiciones independientes**: Si las condiciones no dependen unas de otras y deben evaluarse por separado, usa múltiples `if`. Por ejemplo:
```python
    if condicion_1:
        # Hacer algo
    if condicion_2:
        # Hacer otra cosa
```

**USAR `elif`**:
- **Condiciones mutuamente excluyentes**: Si tienes múltiples condiciones donde solo una puede ser verdadera, usa `elif`. Esto asegura que solo una rama de la cadena de condiciones se ejecute. Por ejemplo:
    ```python
    if condicion_1:
        # Hacer algo si condicion_1 es verdadera
    elif condicion_2:
        # Hacer algo diferente si condicion_2 es verdadera
    elif condicion_3:
        # Hacer otra cosa si condicion_3 es verdadera
    else:
        # Hacer algo si ninguna de las condiciones anteriores es verdadera
    ```
    Aquí, solo una de las condiciones `if`, `elif` o `else` se ejecutará.


 **EJEMPLO DE USO**

Supongamos que estás verificando la temperatura y quieres mostrar mensajes diferentes según el rango de temperatura:

```python
temperatura = int(input("Ingrese la temperatura: "))

if temperatura > 30:
    print("Hace mucho calor.")
elif temperatura > 20:
    print("Hace calorcito.")
elif temperatura > 10:
    print("Hace fresco.")
else:
    print("Hace frío.")
```

En este ejemplo:
- `if` verifica si la temperatura es mayor que 30.
- `elif` verifica si la temperatura es mayor que 20 y menor o igual a 30.
- Otro `elif` verifica si la temperatura es mayor que 10 y menor o igual a 20.
- `else` se ejecuta si ninguna de las condiciones anteriores es verdadera (es decir, si la temperatura es menor o igual a 10).

## BUCLES 

#### LOGICA DEL BUCLE `for`

```python
for i in range(stop) o (star,stop) o (star,stop,step)
```
Los argumentos `()` respetan un orden que se compone del rango de lo que se pide (rango)
OJO el argumento del () puede ser o contener una o más variables configuradas por el usuario por ejemplo range(año)
La `i` es la variable de ITERACION que toma los valores generados en el () 
Es con la i que podemos hacer las operatorias matemáticas de lo generado en el ()

#### USOS DEL BUCLE `for` 
El bucle `for` en Python se puede utilizar de varias formas diferentes:

Iterar sobre un rango de números con `range()`:
```python
for i in range(5):  # Itera del 0 al 4
    print(i)
```

Iterar sobre una secuencia (lista, tupla, cadena, etc.):
```python
frutas = ['manzana', 'banana', 'naranja']
for fruta in frutas:
    print(fruta)
```

Iterar sobre los caracteres de una cadena:
```python
palabra = "Python"
for letra in palabra:
    print(letra)
```

Iterar sobre los elementos de una lista y sus índices:
```python
colores = ['rojo', 'verde', 'azul']
for i, color in enumerate(colores):
    print(f"El color en el índice {i} es {color}")
```

#### LÓGICA DEL BUCLE `while`

```python
while condición:
    # Código a ejecutar mientras la condición sea True
    pass
else:
    # Código a ejecutar después de que la condición sea False
    pass
```

Este bucle se utiliza cuando se desea repetir un bloque de código mientras se cumpla una determinada condición. Es muy útil cuando se desconoce de antemano el número de iteraciones necesarias para completar una tarea.

```python
contador = 0
maximo = 5

while contador < maximo:
    print(f"Iteración {contador}")
    contador += 1

print("Bucle terminado")
```

#### LÓGICA DEL `while True`

```python
while True:
    # Código a ejecutar en cada iteración del bucle infinito
    pass
    # Incluir una condición de salida dentro del bucle
    # para evitar un bucle infinito no deseado
```

La palabra clave `while` seguida de `True`, lo que crea un bucle infinito.
El bloque de código indentado debajo de `while True` se ejecutará repetidamente.
Es necesario incluir una condición de salida dentro del bucle para poder detenerlo en algún momento, de lo contrario, se convertiría en un bucle infinito no deseado.

```python
while True:
    respuesta = input("¿Deseas continuar? (s/n): ")
    if respuesta.lower() == "n":
        break
    print("Continuando...")

print("Bucle terminado")
```

#### EJEMPLO DE UN BUCLE `while`con una tríada simple de `while`- `if` - `for`

```python
seguir = True
    
while seguir:
    lista_argumentos = []
    argumentos = input("Ingrese los argumentos que quiera (o 'salir' para terminar): ")  
    contador = 0
    if argumentos.lower() == 'salir':
        seguir = False
    else:
        argumentos = argumentos.split()
        for argumento in argumentos:
            lista_argumentos.append(argumento)
            contador = contador + 1  
            if contador == 0:
                print("No se agregaron nuevos argumentos")
            else:
                print(lista_argumentos)
```

Nótese que pusimos un variable `True` antes del bucle para generar una condición para su uso
La condición la ponemos en el mismo input
Iteramos con un `for`dentro del `if`

## LISTAS,DICCIONARIOS Y TUPLAS 

#### DIFERENCIAS ENTRE LLAVES

```python
[] = lista

{} = diccionario

() = tupla

set() = conjunto caractéres 

{} = conjunto numérico
```

### LÓGICA DE UNA LISTA

```python
temperaturas = [21,24,27,30,[2,3,5]]
```                                    
 Esto es una lista, y puede contener diferentes elementos y llamarlos en cualquier orden
Una lista puede contener otras listas

#### EXTENSIÓN DE UNA LISTA

```python
len(temperaturas)    # Cuenta la cantidad de elementos contenidos en una lista
```

#### EXTRACCIÓN MEDIANTE INDICES

```python
temperaturas[2]                   # Recordar que se extrae en el orden en se ponen los elementos, partiendo de 0. 

temperaturas[-1]                 # Recordar que conteo negativo es util para listas largas en donde no sabemos cuantos elementos tiene la lista.

temperaturas[1] = 34        # Así modificamos un elemento.

temperaturas[2][1]            # Asi invocamos un elemento de una lista inserto en otra lista
```

####  INSERCIÓN DE ELEMENTOS
 
```python
temperaturas.append(34)           # Insertamos un elemento AL FINAL de la lista.

temperaturas.insert(2,29)        # Insertamos un elemento en una posición determinada.
```

#### BORRADO DE ELEMENTOS

```python
del temperaturas[1]                  # Así borramos un elemnto de la lista, según la posición que ocupa el elemento

temperaturas.pop()       # Se borra el ULTIMO elemento de la lista.

temperaturas.remove(21)  # Aquí borra el elemento según el contenido,no por posición( si hay dos 21, borra el primero)
```

#### ORDENAMIENTO DE ELEMENTOS

```python
temperaturas.sort()        # Se ordenan los elementos. CUIDADO QUE PYTHON ES CASE SENSITIVE

temperaturas.sort(reverse = True)            # Ordena al REVÉS, pero su criterio de uso es de mayor a menor (como DESC)

temperatura.reverse() #Ordena al revés, CAMBIANDO permanentemente el orden
```

#### AGRUPAMIENTO DE ELEMENTOS

```python
min(temperaturas))                  # El mínimo

max(temperaturas))                  # El máximo
```

#### UNION DE CONJUNTOS

```python
conjunto_1.union(conjunto_2) # Alternativo a "|"
```

### LÓGICA DE LA TUPLA

```python
  lista = [1, 2, 3]
  tupla = tuple(lista)  # tupla contiene (1, 2, 3)
     tupla = (1, 2, 3)
     tupla[0] = 5 # Esto da error
```

`tuple()` es una función que convierte otro tipo de dato a una tupla.
Las tuplas son similares a las listas, pero son inmutables (no se pueden modificar después de su creación).
Se definen encerrando los elementos entre paréntesis, por ejemplo: (1, 2, 3)

#### TUPLA CONFIGURADA DESDE UNA FUNCIÓN

```python
def funcion_tupla( *args):
    print(args)  # Tupla con argumentos adicionales
   
funcion_tupla(1,2,3,4,5)
```
```python
def sumar_numeros(*args):
    total = 0
    for num in args:
        total += num
    return total

resultado = sumar_numeros(1, 2, 3, 4, 5)
print(resultado)  # Salida: 15
```

`*args` es otra forma de pasar un número variable de argumentos a una función en Python, pero en este caso se trata de argumentos sin nombre (también conocidos como argumentos posicionales).
Dentro de la función, `args` será una tupla que contiene todos los argumentos posicionales pasados.

### LÓGICA DE UN DICCIONARIO

```python
diccionario = {clave : valor}
```

Para ver sus elementos se puede usar la manera de índices

```python
diccionario = {"Nombre":"Pedro","Edad":"32","Ciudad":"La Serena","Profesión":"Ingeniero"}

print(diccionario["Nombre"])
print(diccionario["Edad"])
print(diccionario["Ciudad"])
print(diccionario["Profesión"])
diccionario["Recomandado"] = "Si" #Se agrega un nuevo elemento
print(diccionario)
```

#### DICCIONARIO CONFIGURADO DESDE UNA FUNCION

```python
def funcion_diccionario( **kwargs):
    print(kwargs)  # Diccionario con argumentos clave=valor

funcion_diccionario(nombre = 'Juan', apellido='20', ciudad ='La Serena')
```
```python
def mi_funcion(**kwargs):
    print(kwargs)
    print(type(kwargs))

mi_funcion(frutas=['manzana', 'naranja'], numeros=[1, 2, 3], nombre='Juan')

{'frutas': ['manzana', 'naranja'], 'numeros': [1, 2, 3], 'nombre': 'Juan'}
<class 'dict'>
```

Diccionario con argumentos `clave`=`valor`
Cuando defines una función con `**kwargs`, puedes pasar un número arbitrario de argumentos con nombre a la función, y estos se empaquetarán en un diccionario dentro de la función.
En el ejemplo, se pasa `frutas=['manzana', 'naranja']`, lo que en `kwargs` se convierte en la clave `'frutas'` con el valor `['manzana', 'naranja']`. Lo mismo ocurre con números y nombre.
Entonces, `**kwargs` te permite crear un diccionario dinámicamente a partir de los argumentos con nombre pasados a la función. Puedes acceder a los valores usando la sintaxis de diccionarios regular, como `kwargs['nombre']`, por ejemplo.
Esto es muy útil cuando no sabes de antemano cuántos argumentos con nombre se pasarán a la función, o cuando deseas permitir que la función acepte un conjunto flexible de argumentos con nombre.

#### FORMULA PARA EXTRAER ELEMENTOS DE UNA VARIABLE

```python
variable.get(elemento)   
```

Muy útil para trabajar en diccionarios donde podemos usarlo con índices

### LÓGICA DE LAS LISTAS POR COMPRENSIÓN

Las listas por comprensión son una forma concisa y elegante de crear nuevas listas a partir de otras secuencias (listas, tuplas, cadenas, etc.) en Python. 

```python
[expresión for elemento in secuencia [if condición]]
```

- `expresión`: Es la operación que se realizará con cada elemento de la secuencia. Puede ser tan simple como el mismo elemento o una operación más compleja.
- `elemento`: Es el nombre que se le asigna a cada elemento de la secuencia durante la iteración.
- `secuencia`: Es la secuencia (lista, tupla, cadena, etc.) sobre la cual se itera.
- `if condición` (opcional): Es una condición que determina si el elemento se incluye o no en la nueva lista.

#### EJEMPLO DE LISTAS DE COMPRENSIÓN

```python
# Crear una lista con los cuadrados de los números del 1 al 10
cuadrados = [x**2 for x in range(1, 11)]
print(cuadrados)  # Salida: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# Crear una lista con las palabras que tienen más de 5 caracteres
palabras = ["Python", "es", "un", "lenguaje", "poderoso"]
palabras_largas = [palabra for palabra in palabras if len(palabra) > 5]
print(palabras_largas)  # Salida: ['Python', 'lenguaje', 'poderoso']

# Crear una lista de tuplas (x, y) donde x e y son los elementos de dos listas
numeros1 = [1, 2, 3]
numeros2 = [10, 20, 30]
pares = [(x, y) for x in numeros1 for y in numeros2]
print(pares)  # Salida: [(1, 10), (1, 20), (1, 30), (2, 10), (2, 20), (2, 30), (3, 10), (3, 20), (3, 30)]
```

Las listas por comprensión son muy útiles cuando necesitas crear nuevas listas a partir de otras secuencias, realizando operaciones o filtrando elementos según ciertas condiciones. Además, suelen ser más concisas y legibles que los bucles tradicionales.
 
## FUNCIONES 

### LÓGICA DE LAS FUNCIONES

```python
print("------------ RETORNO EN FUNCIONES ------------")
print("------ FUNCION SIN ARGUMENTOS ------")

def sum():
    a = int(input("Ingrese el primer número: "))
    b = int(input("Ingrese el segundo número: "))
    return a + b

# Llamada a la función
result = sum()
print(result)

print("------------------------------------")

print("------ FUNCION CON ARGUMENTOS ------")

print("------ PRIMERA VARIACION ------")

def suma(numero_1,numero_2):
    return numero_1 + numero_2

numero_1 = int(input("Ingrese primer número: "))
numero_2 = int(input("Ingrese segundo número: "))

print(suma(numero_1,numero_2))

print("-------------------------------")

print("------ SEGUNDA VARIACION ------")

def suma(numero_1, numero_2):
    return numero_1 + numero_2

resultado = suma(3, 5) # Con argumento hardcodeado
print(resultado)  

print("------------ ------------ ------------")
```

### EJEMPLO DE FUNCIONES

```python 
# Definición de la función para calcular el área de un rectángulo
def calcular_area_rectangulo(ancho, alto):
    return ancho * alto

# Definición de la función para calcular el área de un triángulo
def calcular_area_triangulo(base, alto):
    return 0.5 * base * alto

# Código principal
ancho = float(input("Ingrese el ancho del rectángulo: "))
alto = float(input("Ingrese la altura: "))
base_triangulo = float(input("Ingrese la base del triángulo: "))

area_rectangulo = calcular_area_rectangulo(ancho, alto)
area_triangulo = calcular_area_triangulo(base_triangulo, alto)

print(f"El área del rectángulo es: {area_rectangulo}")
print(f"El área del triángulo es: {area_triangulo}")

```

### EJEMPLO DE FUNCIÓN con triada simple de `while` - `if` - `for`

```python
def mostrar_argumentos():
    argumentos = []  # Creamos una lista vacía para almacenar los argumentos
    
    while True:
        argumento = input("Ingrese un argumento (o escriba 'salir' para terminar): ")
        
        if argumento.lower() == 'salir':
            break  # Salimos del bucle si el usuario escribe 'salir'
        else:
            argumentos.append(argumento)  # Agregamos el argumento a la lista
    
    print("Argumentos ingresados:")
    for arg in argumentos:
        print(arg)  # Mostramos cada argumento en la consola

mostrar_argumentos()  # Llamamos a la función para ejecutarla
```

## BIBLIOTECAS

#### SINTAXIS DE LOS MÓDULOS
```python
# Se invoca al modulo
import [módulo] as [alias]

# Sintaxis general para usar un modulo
variable = modulo.funcion(argumento)
```

- `modulo` es el nombre del módulo importado o su alias
- `funcion` es una función específica del módulo
- `argumento` son los parámetros que la función requiere

#### EJEMPLOS DE USO
```python
# Usando un módulo importado sin alias
import math
resultado = math.sqrt(16)

# Usando un módulo con alias
import numpy as np
array = np.array([1, 2, 3, 4, 5])

# Importando una función específica de un módulo
from random import randint
numero_aleatorio = randint(1, 10)
```

#### MODULO `math`:

El módulo `math` de la biblioteca estándar de Python proporciona funciones y constantes matemáticas avanzadas para realizar operaciones matemáticas más complejas que las operaciones aritméticas básicas.

Algunas de las principales características y operaciones que puedes realizar con el módulo `math` son:

- Constantes matemáticas: Proporciona constantes matemáticas como `math.pi` (valor de pi),` math.e` (número de Euler), entre otras.
- Funciones trigonométricas: Incluye funciones como `math.sin()`, `math.cos()`, `math.tan()` para calcular senos, cosenos y tangentes de ángulos dados en radianes.
- Funciones exponenciales y logarítmicas: Ofrece funciones como `math.exp()`,` math.log()`,` math.log10()` para cálculos con exponenciales y logaritmos.
- Funciones de redondeo: Provee funciones como `math.ceil()` (redondear hacia arriba), `math.floor()` (redondear hacia abajo), `math.trunc()` (truncar un número).
- Funciones de valor absoluto y signo: Incluye `math.fabs()` para obtener el valor absoluto y `math.copysign()` para copiar el signo de un número.
- Funciones de potencia y raíz: Contiene `math.pow()` para calcular potencias y `math.sqrt()` para calcular raíces cuadradas.
- Funciones especiales: Ofrece funciones más avanzadas como `math.gamma()` (función gamma), `math.erf()` (función de error), entre otras.

#### EJEMPLOS DE  `math`

```python
import math

# Calcular el valor de pi
print(math.pi)  # Salida: 3.141592653589793

# Calcular la raíz cuadrada de un número
num = 16
raiz = math.sqrt(num)
print(f"La raíz cuadrada de {num} es: {raiz}")  # Salida: La raíz cuadrada de 16 es: 4.0

# Calcular el valor absoluto de un número
num = -5
valor_absoluto = math.fabs(num)
print(f"El valor absoluto de {num} es: {valor_absoluto}")  # Salida: El valor absoluto de -5 es: 5.0

# Calcular el logaritmo base 10 de un número
num = 100
log10 = math.log10(num)
print(f"El logaritmo base 10 de {num} es: {log10}")  # Salida: El logaritmo base 10 de 100 es: 2.0

# Calcular el seno de un ángulo en radianes
angulo_radianes = math.pi / 4  # 45 grados
seno = math.sin(angulo_radianes)
print(f"El seno de {angulo_radianes} radianes es: {seno}")  # Salida: El seno de 0.7853981633974483 radianes es: 0.7071067811865476

# Redondear un número hacia arriba
num = 5.3
num_redondeado = math.ceil(num)
print(f"{num} redondeado hacia arriba es: {num_redondeado}")  # Salida: 5.3 redondeado hacia arriba es: 6

# Redondear un número hacia abajo
num = 5.8
num_redondeado = math.floor(num)
print(f"{num} redondeado hacia abajo es: {num_redondeado}")  # Salida: 5.8 redondeado hacia abajo es: 5
```

#### MODULO `datetime`

El módulo `datetime` en Python es una biblioteca estándar que proporciona clases para manipular fechas y horas. Es muy útil para realizar operaciones con datos de fecha y hora, como calcular diferencias entre fechas, formatear fechas, realizar operaciones aritméticas con fechas, entre otras funcionalidades.

Algunas de las clases y funciones más importantes del módulo `datetime` son:

- Clase `datetime`: Representa una fecha y hora específicas. Permite acceder y modificar los componentes de fecha y hora (año, mes, día, hora, minuto, segundo, microsegundo).
- Clase `date`: Representa solo una fecha (año, mes y día), sin información de hora.
- Clase `time`: Representa solo una hora (hora, minuto, segundo, microsegundo), sin información de fecha.
- Clase `timedelta`: Representa una duración de tiempo, que se puede usar para realizar operaciones aritméticas con fechas y horas.
- Función `datetime.now()`: Devuelve la fecha y hora actuales.
- Función `datetime.strptime()`: Analiza una cadena de texto y crea un objeto datetime a partir de ella.
- Función `datetime.strftime()`: Convierte un objeto datetime en una cadena de texto formateada según un patrón específico.

#### EJMEPLOS DE `datetime`

```python
import datetime

# Crear una fecha y hora específicas
fecha_hora = datetime.datetime(2023, 5, 15, 12, 30, 0)
print(fecha_hora)  # Salida: 2023-05-15 12:30:00

# Obtener la fecha actual
fecha_actual = datetime.date.today()
print(fecha_actual)  # Salida: 2023-04-27 (la fecha actual en la que se ejecuta el código)

# Calcular la diferencia entre dos fechas
fecha_futura = datetime.date(2023, 6, 1)
diferencia = fecha_futura - fecha_actual
print(diferencia)  # Salida: 34 days, 0:00:00 (un objeto timedelta)

# Formatear una fecha y hora
formato = "%Y-%m-%d %H:%M:%S"
cadena_fecha = fecha_hora.strftime(formato)
print(cadena_fecha)  # Salida: 2023-05-15 12:30:00
```

#### MODULO random

El módulo `random` en Python es una biblioteca estándar que proporciona funciones para generar números aleatorios. Es muy útil en diversos escenarios, como simulaciones, juegos, criptografía, muestreo estadístico, entre otros.

Algunas de las funciones más importantes del módulo `random` son:

- `random.random()`: Devuelve un número flotante aleatorio en el rango [0.0, 1.0).
- `random.uniform(a, b)`: Devuelve un número flotante aleatorio en el rango [a, b).
- `random.randint(a, b)`: Devuelve un número entero aleatorio en el rango [a, b].
- `random.choice(secuencia)`: Devuelve un elemento aleatorio de una secuencia no vacía (lista, tupla, cadena, etc.).
- `random.shuffle(secuencia)`: Reordena los elementos de una secuencia mutable (lista) de forma aleatoria.
- `random.sample(población, k)`: Devuelve una lista con k elementos únicos aleatorios de una población (secuencia o conjunto).
- `random.seed(semilla)`: Inicializa el generador de números aleatorios con una semilla específica. Esto permite reproducir secuencias de números aleatorios.

#### EJEMPLOS DE `random`

```python
import random

# Generar un número flotante aleatorio entre 0 y 1
num_aleatorio = random.random()
print(num_aleatorio)  # Salida: 0.6543216789098765

# Generar un número entero aleatorio entre 1 y 10
num_entero = random.randint(1, 10)
print(num_entero)  # Salida: 7

# Seleccionar un elemento aleatorio de una lista
frutas = ['manzana', 'naranja', 'plátano', 'pera']
fruta_aleatoria = random.choice(frutas)
print(fruta_aleatoria)  # Salida: 'naranja'

# Mezclar aleatoriamente una lista
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
random.shuffle(numeros)
print(numeros)  # Salida: [7, 2, 9, 5, 4, 10, 1, 8, 6, 3]

# Generar una muestra aleatoria de una población
poblacion = range(1, 101)
muestra = random.sample(poblacion, k=5)
print(muestra)  # Salida: [42, 63, 7, 22, 91]
```

## USOS AVANZADOS

#### SCRIPTS CONFIGURADOS DESDE VARIOS MODULOS

```python
# utils.py

def cuadrado(numero):
    """ Devuelve el cuadrado de un número """
    return numero ** 2

# main.py
import utils

def main():
    numero = 5
    resultado = utils.cuadrado(numero)
    print(f"El cuadrado de {numero} es {resultado}")

if __name__ == "__main__":
    main() 
```

RECORDAR que  `utils.py`(puede tener el nombre que quieras) es un archivo diferente de `main.py` 
Nótese que creamos una variable `resultado`para llamar la función `def cuadrado`, y lo hacemos 
poniéndola como primer argumento, tal como si fuese una `string`

```python
# archivo volumen.py

import math

def volumen_cono(radio,altura):
    return math.pi * radio**2 *(altura / 3)

#  archivo main.py

import volumen

radio = int(input("Ingrese radio de cono: "))
altura = int(input("Ingrese altura de cono: "))

resultado_volumen_cono = volumen.volumen_cono(radio,altura)
print("El volumen del cono es: {}".format(resultado_volumen_cono))
```

En este caso las variables las pedimos como `input`en el archivo `main.py` y usamos
la variable resultado en `.format`

## CREACIÓN DE APLICACIONES

#### MÓDULO `tkinter`

Creamos una ventana

```python
import tkinter as tk

ventana = tk.Tk()

ventana.config(width=800,height=600)                # Medimos la ventana desde su enmallado en pixeles
                                    
ventana.title("Bienvenido a la aplicacion")   # Agregamos un titulo

ventana.iconbitmap("icono2.ico")                           # Le agregamos un ícono
                                      
ventana.config(bg="#97704C")                                  # Configuramos su color

ventana.resizable(1,1)                                                   # Cambiamos sus dimensiones         

ventana.mainloop()                                                          # Le damos fin a la ventana
```

Creamos botones

```python
boton = tk.Button(text="Aceptar", command=boton_presionado)  # Le ponemos nombre al botón y un comando

boton.place(x=20, y=150, width=150,height=50)                                    # Dimensionamos el o los botones
```

Considerar que para crear un botón llamamos a la función `Button` del módulo `tkinter`(`tk`)
Ese es el comando para un solo botón, si se tiene otro más hay que repetir esta operación (botón_1)

Creamos cajas de texto

```python
caja = tk.Entry()

caja.place(x=180, y=150, width=150, height=50)
```

Creamos etiquetas

```python
etiqueta_nombre = tk.Label (text= "Ingrese su nombre",bg="#ADD5E9")

etiqueta_nombre.place(x=250, y=100)
```