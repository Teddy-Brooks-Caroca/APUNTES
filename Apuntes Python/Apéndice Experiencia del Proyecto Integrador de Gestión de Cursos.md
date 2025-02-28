
## Etapa 1: Aplicación de Consola

En esta etapa, se desarrolló una aplicación de consola que permitía al usuario ingresar el nombre de un alumno y la cantidad de cursos en los que estaba inscrito. Los datos se almacenaban en una lista de listas llamada `lista_de_alumnos`.

```python
lista_de_alumnos = []

while True:                                    
      print("Ingrese el número de la operación que desea ejecutar:")
      print("1 - Ver la lista de alumnos.")
      print("2 - Añadir un alumno a la lista.")
      print("3 - Salir.")
      operacion = input(">> ")
      
      # ...
```

Se utilizó un bucle `while True` para mantener el programa en ejecución hasta que el usuario seleccionara la opción de salir. Dentro del bucle, se presentaba un menú con tres opciones: ver la lista de alumnos, añadir un alumno a la lista y salir.

Si el usuario seleccionaba la opción 1, se ejecutaba el siguiente código:

```python
if operacion == "1":
    print("Lista de alumnos:")
    for alumno in lista_de_alumnos:            
        nombre = alumno[0]
        curso = alumno[1]
        print("{} - {} cursos".format(nombre,str(curso)))
```

Este código itera sobre la lista `lista_de_alumnos` utilizando un bucle `for`. Para cada alumno (sublista) en la lista, se extraen el nombre (`alumno[0]`) y la cantidad de cursos (`alumno[1]`), y se imprimen en la consola.

Si el usuario seleccionaba la opción 2, se ejecutaba el siguiente código:

```python
elif operacion == "2":
    nuevo_alumno = input("Ingrese nuevo alumno: ")
    if nuevo_alumno == "":
        print("Error, debe agregar un nombre válido")
    else:
        cantidad_de_cursos = int(input("Ingrese cantidad de cursos: "))
        lista_de_alumnos.append([nuevo_alumno,cantidad_de_cursos])
        print("¡El alumno fue añadido a la lista!")
```

Primero, se solicita al usuario ingresar el nombre del nuevo alumno. Si el nombre está vacío, se muestra un mensaje de error. De lo contrario, se solicita la cantidad de cursos y se crea una nueva sublista con el nombre y la cantidad de cursos utilizando `[nuevo_alumno, cantidad_de_cursos]`. Esta sublista se agrega a la lista `lista_de_alumnos` utilizando el método `append`.

Si el usuario seleccionaba la opción 3, se ejecutaba el siguiente código:

```python
elif operacion == "3":
    print("¡Gracias por utilizar el programa!")
    break
```

Este código simplemente imprime un mensaje de despedida y sale del bucle `while True` utilizando la instrucción `break`.

## Etapa 2: Uso de Diccionarios

En esta etapa, se migró la estructura de datos de una lista de listas a un diccionario llamado `lista_de_alumnos`, donde las claves eran los nombres de los alumnos y los valores eran la cantidad de cursos correspondiente.

```python
lista_de_alumnos = {}

while True:                                 
      print("Ingrese el número de la operación que desea ejecutar:")
      print("1 - Añadir un alumno a la lista.")
      print("2 - Ver la lista de alumnos.")
      print("3 - Ver la cantidad de cursos de un alumno.")
      print("4 - Salir.")
      operacion = input(">> ")
      
      # ...
```

En esta etapa, el menú se actualizó para incluir una nueva opción: "Ver la cantidad de cursos de un alumno".

Si el usuario seleccionaba la opción 1, se ejecutaba el siguiente código:

```python
if operacion == "1":
    nuevo_alumno = input("Ingrese nuevo alumno: ")
    nuevo_alumno = verificar(nuevo_alumno)
    cantidad_de_cursos = input("Ingrese cantidad de cursos: ")
    cantidad_de_cursos = convertir(cantidad_de_cursos)
    lista_de_alumnos[nuevo_alumno] = cantidad_de_cursos
    print("¡El alumno fue añadido a la lista!")
```

Primero, se solicita al usuario ingresar el nombre del nuevo alumno y la cantidad de cursos. Luego, se utilizan las funciones `verificar` y `convertir` para validar los datos ingresados.

```python
def verificar(dato):
    while dato == "":
        print("Error")
        dato = input("Ingrese el dato nuevamente: ")
    return dato

def convertir(valor):
    while valor.isdecimal() == False:
        print("Error")
        valor = input("Ingrese valor nuevamente: ")
    valor= int(valor)    
    return valor
```

La función `verificar` verifica que el dato ingresado no esté vacío. Si está vacío, muestra un mensaje de error y solicita al usuario ingresar el dato nuevamente.

La función `convertir` verifica que el valor ingresado sea un número entero válido. Si no lo es, muestra un mensaje de error y solicita al usuario ingresar el valor nuevamente.

Después de validar los datos, se agrega una nueva entrada al diccionario `lista_de_alumnos` utilizando el nombre del alumno como clave y la cantidad de cursos como valor.

Si el usuario seleccionaba la opción 2, se ejecutaba el siguiente código:

```python
elif operacion == "2":
    mostrar(lista_de_alumnos)

def mostrar(estudiantes):
    for n in estudiantes:
        print(n,"-",estudiantes[n],"cursos")
```

Este código llama a la función `mostrar`, que itera sobre las claves del diccionario `lista_de_alumnos` y muestra el nombre del alumno y la cantidad de cursos correspondiente.

Si el usuario seleccionaba la opción 3, se ejecutaba el siguiente código:

```python
elif operacion == "3":
    nombre = input("Ingrese el nombre del alumno: ")
    if nombre in lista_de_alumnos:
        print(nombre +" tiene "+ str(lista_de_alumnos[nombre])+" cursos.")
    else:
        print("Ese alumno no tiene cursos asignados")
```

Primero, se solicita al usuario ingresar el nombre del alumno. Luego, se verifica si el nombre existe como clave en el diccionario `lista_de_alumnos`. Si existe, se imprime la cantidad de cursos correspondiente. De lo contrario, se muestra un mensaje indicando que el alumno no tiene cursos asignados.

Si el usuario seleccionaba la opción 4, se ejecutaba el mismo código que en la etapa anterior para salir del programa.

## Etapa 3: Interfaz Gráfica de Usuario (GUI)

En esta etapa, se migró la aplicación a una interfaz gráfica de usuario (GUI) utilizando la biblioteca Tkinter de Python.

```python
import tkinter as tk

# ...

ventana = tk.Tk()
ventana.config(width=400, height=300)
ventana.title("Proyecto integrador")
```

Primero, se importa la biblioteca Tkinter y se crea una instancia de la clase `Tk`, que representa la ventana principal de la aplicación. Se configura el ancho y el alto de la ventana, y se establece el título.

Luego, se crean varios widgets y se posicionan en la ventana:

```python
boton_lista = tk.Button(text="Ver lista de alumnos", command=ver)
boton_lista.place(x=10, y=10)

etiqueta_nombre = tk.Label(text="Nombre alumno:")
etiqueta_nombre.place(x=10, y=60)

caja_nombre = tk.Entry()
caja_nombre.place(x=110, y=60, width=150, height=20)

etiqueta_cursos = tk.Label(text="Cursos:")
etiqueta_cursos.place(x=10, y=100)

caja_cursos = tk.Entry()
caja_cursos.place(x=110, y=100, width=50, height=20)

boton_agregar = tk.Button(text="Agregar a la lista", command=agregar)
boton_agregar.place(x=10, y=150)

boton_cursos = tk.Button(text="Ver cantidad de cursos", command=ver_alumno)
boton_cursos.place(x=115, y=150)
```

Se crea un botón `boton_lista` con el texto "Ver lista de alumnos" y se asocia a la función `ver` (que se explicará más adelante). Luego, se posiciona el botón en la ventana utilizando el método `place`.

Se crea una etiqueta `etiqueta_nombre` con el texto "Nombre alumno:" y se posiciona en la ventana.

Se crea una caja de entrada `caja_nombre` para ingresar el nombre del alumno y se posiciona en la ventana.

Se crean una etiqueta `etiqueta_cursos` y una caja de entrada `caja_cursos` para ingresar la cantidad de cursos, y se posicionan en la ventana.

Se crea un botón `boton_agregar` con el texto "Agregar a la lista" y se asocia a la función `agregar`. Se posiciona en la ventana.

Se crea un botón `boton_cursos` con el texto "Ver cantidad de cursos" y se asocia a la función `ver_alumno`. Se posiciona en la ventana.

A continuación, se definen las funciones asociadas a los botones:

```python
def ver():
    print("Lista de alumnos:")
    for nombre in alumnos:
        cursos = alumnos[nombre]
        print(nombre + " - " + str(cursos) + " cursos")
```

La función `ver` imprime la lista de alumnos y sus cursos correspondientes en la consola. Itera sobre las claves del diccionario `alumnos` y muestra el nombre del alumno y la cantidad de cursos.

```python
def agregar():
    nombre_alumno = caja_nombre.get()
    nombre_alumno = verificar(nombre_alumno)
    cursos = caja_cursos.get()
    cursos = convertir(cursos)
    if nombre_alumno != "error" and cursos != "error":
        alumnos[nombre_alumno] = cursos
        print("Has ingresado un alumno correctamente.")
```

La función `agregar` obtiene el nombre del alumno y la cantidad de cursos ingresados en las cajas de texto utilizando el método `get`. Luego, utiliza las funciones `verificar` y `convertir` (definidas en la Etapa 2) para validar los datos ingresados. Si los datos son válidos, agrega una nueva entrada al diccionario `alumnos` con el nombre del alumno como clave y la cantidad de cursos como valor, e imprime un mensaje de confirmación.

```python
def ver_alumno():
    nombre = caja_nombre.get()
    if nombre in alumnos:
        print(nombre + " tiene " + str(alumnos[nombre]) + " cursos")
    else:
        print("Ese alumno no tiene cursos")
```

La función `ver_alumno` obtiene el nombre del alumno ingresado en la caja de texto. Si el nombre existe como clave en el diccionario `alumnos`, imprime la cantidad de cursos correspondiente. De lo contrario, muestra un mensaje indicando que el alumno no tiene cursos asignados.

Finalmente, se inicializa el diccionario `alumnos` vacío y se ejecuta el bucle principal de la GUI:

```python
alumnos = {}

ventana.mainloop()
```

El método `mainloop` inicia el bucle de eventos de la interfaz gráfica de usuario, lo que permite que la ventana se mantenga abierta y responda a las interacciones del usuario.

En esta etapa, se recomienda mejorar la experiencia de usuario agregando más widgets y funcionalidades, como una tabla para mostrar la lista de alumnos de manera más organizada. Además, se podría implementar una función para editar o eliminar alumnos de la lista.

# Observaciones y Recomendaciones

## Observaciones

1. **Estructura del Código**: Si bien el código estuvo estructurado en etapas y funciones, se podría haber mejorado la modularidad separando aún más las funcionalidades en módulos/archivos diferentes. Esto habría facilitado la legibilidad y mantenibilidad del código.

2. **Manejo de Errores**: Aunque se implementaron algunas validaciones para los datos de entrada, se podrían haber considerado casos adicionales de manejo de errores, como entradas no válidas (letras en lugar de números) o intentos de ingresar alumnos duplicados.

3. **Documentación**: El código careció de comentarios explicativos adecuados. Agregar comentarios detallados sobre el propósito y funcionamiento de cada sección del código habría facilitado su comprensión y mantenimiento futuro.

4. **Experiencia de Usuario**: La interfaz gráfica de usuario (GUI) en la Etapa 3 fue básica y podría mejorarse significativamente. Una GUI más intuitiva y atractiva mejoraría la experiencia del usuario final.

## Recomendaciones

1. **Principios de Diseño de Software**: Se recomienda estudiar y aplicar los principios de diseño de software, como el Principio de Responsabilidad Única (SRP), el Principio Abierto/Cerrado (OCP), y el Principio de Inversión de Dependencias (DIP). Esto ayudará a escribir código más modular, mantenible y extensible.

2. **Pruebas Unitarias**: Implementar pruebas unitarias desde el inicio del proyecto habría facilitado la detección temprana de errores y asegurado el correcto funcionamiento del código a medida que se agregaban nuevas funcionalidades.

3. **Patrones de Diseño**: Explorar y aplicar patrones de diseño adecuados, como el Patrón Singleton, el Patrón Observador o el Patrón Estrategia, podría haber mejorado la estructura y flexibilidad del código.

4. **Mejora de la GUI**: Invertir tiempo en aprender a fondo la biblioteca Tkinter o explorar otras bibliotecas de GUI como PyQt o wxPython podría haber resultado en una interfaz de usuario más atractiva y funcional.

5. **Implementar Persistencia de Datos**: Agregar la capacidad de almacenar y cargar los datos de los alumnos y sus cursos desde un archivo o una base de datos habría brindado una solución más robusta y escalable.

6. **Refactorización Continua**: A medida que se avanza en un proyecto, es importante refactorizar continuamente el código para mantenerlo limpio, legible y eficiente. Esto facilitará futuras modificaciones y extensiones.

7. **Documentación Completa**: Mantener una documentación detallada del proyecto, incluyendo diagramas, casos de uso y especificaciones técnicas, facilitará la comprensión del sistema por parte de otros desarrolladores y su propio mantenimiento a largo plazo.

Estas observaciones y recomendaciones tienen como objetivo destacar áreas de mejora y buenas prácticas que pueden aplicarse en futuros proyectos para lograr un código más robusto, mantenible y escalable, así como una mejor experiencia de usuario.

Con gusto ejemplificaré cómo se podría modificar y mejorar el código del proyecto integrador siguiendo algunas de las recomendaciones mencionadas.

1. **Modularidad y Separación de Preocupaciones (SoC):**

En lugar de tener todo el código en un solo archivo, se podría separar en múltiples módulos o archivos, cada uno encargado de una tarea específica. Por ejemplo:

`main.py` (archivo principal):

```python
import tkinter as tk
from gui import GUI
from backend import Backend

def main():
    backend = Backend()
    root = tk.Tk()
    app = GUI(root, backend)
    app.run()

if __name__ == "__main__":
    main()
```

`backend.py` (lógica de negocio):

```python
class Backend:
    def __init__(self):
        self.alumnos = {}

    def agregar_alumno(self, nombre, cursos):
        # Validar entrada
        if not nombre or not cursos.isdigit():
            return False
        self.alumnos[nombre] = int(cursos)
        return True

    def obtener_cursos_alumno(self, nombre):
        return self.alumnos.get(nombre, "No encontrado")

    def obtener_lista_alumnos(self):
        return self.alumnos
```

`gui.py` (interfaz gráfica de usuario):

```python
import tkinter as tk

class GUI:
    def __init__(self, root, backend):
        self.root = root
        self.backend = backend
        # Configurar widgets aquí

    def agregar_alumno(self):
        nombre = self.entry_nombre.get()
        cursos = self.entry_cursos.get()
        if self.backend.agregar_alumno(nombre, cursos):
            print("Alumno agregado correctamente.")
        else:
            print("Error al agregar alumno.")

    def ver_cursos_alumno(self):
        nombre = self.entry_nombre.get()
        cursos = self.backend.obtener_cursos_alumno(nombre)
        print(f"{nombre} tiene {cursos} cursos.")

    def ver_lista_alumnos(self):
        alumnos = self.backend.obtener_lista_alumnos()
        for nombre, cursos in alumnos.items():
            print(f"{nombre} - {cursos} cursos")

    def run(self):
        self.root.mainloop()
```

Esta separación sigue el principio de Separación de Preocupaciones (SoC), donde cada módulo se encarga de una tarea específica: `main.py` para iniciar la aplicación, `backend.py` para la lógica de negocio, y `gui.py` para la interfaz gráfica de usuario.

2. **Manejo de Errores y Validación de Entrada:**

En el módulo `backend.py`, se pueden agregar validaciones adicionales para los datos de entrada y manejar los errores de manera más robusta. Por ejemplo:

```python
class Backend:
    def __init__(self):
        self.alumnos = {}

    def agregar_alumno(self, nombre, cursos):
        # Validar nombre
        if not nombre or not isinstance(nombre, str):
            print("Error: El nombre del alumno no es válido.")
            return False

        # Validar cursos
        if not cursos.isdigit():
            print("Error: La cantidad de cursos debe ser un número entero.")
            return False

        # Verificar si el alumno ya existe
        if nombre in self.alumnos:
            print("Error: El alumno ya existe en la lista.")
            return False

        self.alumnos[nombre] = int(cursos)
        return True
```

En este ejemplo, se valida que el nombre del alumno sea una cadena no vacía y que la cantidad de cursos sea un número entero. Además, se verifica si el alumno ya existe en el diccionario `alumnos` para evitar duplicados.

3. **Documentación y Comentarios:**

Es una buena práctica agregar comentarios explicativos en el código para facilitar su comprensión y mantenimiento futuro. Por ejemplo:

```python
class Backend:
    """
    Clase que maneja la lógica de negocio de la aplicación de gestión de cursos.
    """

    def __init__(self):
        """
        Inicializa el diccionario de alumnos vacío.
        """
        self.alumnos = {}

    def agregar_alumno(self, nombre, cursos):
        """
        Agrega un nuevo alumno al diccionario de alumnos.

        Args:
            nombre (str): Nombre del alumno.
            cursos (str): Cantidad de cursos en los que está inscrito el alumno.

        Returns:
            bool: True si el alumno se agregó correctamente, False en caso contrario.
        """
        # Validaciones y lógica de agregar alumno
        ...

    def obtener_cursos_alumno(self, nombre):
        """
        Obtiene la cantidad de cursos de un alumno.

        Args:
            nombre (str): Nombre del alumno.

        Returns:
            str: Cantidad de cursos del alumno o "No encontrado" si el alumno no existe.
        """
        # Lógica para obtener cursos del alumno
        ...
```

Estos comentarios, conocidos como "docstrings", describen el propósito y funcionamiento de cada clase, método y sus parámetros de entrada y salida.

4. **Mejora de la Interfaz Gráfica de Usuario (GUI):**

Para mejorar la experiencia de usuario, se podría utilizar una biblioteca de GUI más avanzada como PyQt o wxPython, o explorar en profundidad las capacidades de Tkinter. Por ejemplo, se podría agregar una tabla para mostrar la lista de alumnos de manera más organizada:

```python
import tkinter as tk
from tkinter import ttk

class GUI:
    def __init__(self, root, backend):
        self.root = root
        self.backend = backend

        # Crear tabla para mostrar alumnos
        self.tabla_alumnos = ttk.Treeview(self.root)
        self.tabla_alumnos["columns"] = ("Nombre", "Cursos")
        self.tabla_alumnos.heading("#0", text="", anchor=tk.W)
        self.tabla_alumnos.column("#0", width=0, stretch=tk.NO)
        self.tabla_alumnos.heading("Nombre", text="Nombre", anchor=tk.W)
        self.tabla_alumnos.heading("Cursos", text="Cursos", anchor=tk.W)
        self.tabla_alumnos.pack(pady=20)

        # Otros widgets aquí

    def ver_lista_alumnos(self):
        # Limpiar tabla antes de mostrar nuevos datos
        for item in self.tabla_alumnos.get_children():
            self.tabla_alumnos.delete(item)

        alumnos = self.backend.obtener_lista_alumnos()
        for nombre, cursos in alumnos.items():
            self.tabla_alumnos.insert("", tk.END, values=(nombre, cursos))
```

En este ejemplo, se utiliza la clase `ttk.Treeview` de Tkinter para crear una tabla y mostrar la lista de alumnos de manera más organizada. La tabla se configura con dos columnas: "Nombre" y "Cursos". Al hacer clic en el botón "Ver lista de alumnos", se llama al método `ver_lista_alumnos`, el cual limpia la tabla y luego inserta las filas con los nombres de los alumnos y sus respectivas cantidades de cursos.

Estas son solo algunas sugerencias de cómo se podría mejorar el código del proyecto integrador. Es importante tener en cuenta que estas modificaciones son ejemplos y podrían requerir ajustes adicionales para adaptarse al código existente y a los requisitos específicos del proyecto.