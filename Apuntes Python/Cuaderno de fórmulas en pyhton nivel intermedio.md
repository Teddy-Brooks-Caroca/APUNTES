## MANEJO DE ARCHIVOS (lectura, escritura)

### LECTURA:

#### LÓGICA PARA LEER ARCHIVOS

```python
import [módulo_necesario]

with open('archivo.extensión', 'modo_apertura') as archivo:
    contenido = [módulo_necesario].función_lectura(archivo)
    print(contenido)
```

Donde:
- `[módulo_necesario]` se reemplaza por el módulo específico si es necesario (como csv, json, etc.)
- `modo_apertura` puede ser 'r' para texto o 'rb' para binario
- `función_lectura` depende del tipo de archivo y módulo usado

#### FORMULAS DE LECTURAS SEGÚN TIPO

```python
# Texto plano (.txt)
with open('archivo.txt', 'r') as archivo:
    contenido = archivo.read()
    print(contenido)

# CSV
import csv
with open('archivo.csv', 'r') as archivo:
    contenido = csv.reader(archivo)
    for fila in contenido:
        print(fila)

# JSON
import json
with open('archivo.json', 'r') as archivo:
    contenido = json.load(archivo)
    print(contenido)

# XML
import xml.etree.ElementTree as ET

tree = ET.parse('datos.xml')
root = tree.getroot()
for elemento in root:
    print(elemento.tag, elemento.text)

# Excel (desde PANDAS)
import pandas as pd

df = pd.read_excel('datos.xlsx')
print(df)

# Archivo binario
with open('archivo.bin', 'rb') as archivo:
    contenido = archivo.read()
    print(contenido)

```

Aspectos a considerar:
- La estructura básica con `with` y `open()` es consistente.
- El modo de apertura y la función de lectura varían según el tipo de archivo.
- Algunos formatos requieren módulos específicos.
- La forma de procesar el contenido (como imprimir) puede variar según el formato y las necesidades.

### ESCRITURA:

#### METODO`write()`
```python
with open('archivo.txt', 'w') as f:
    f.write("Hola, mundo!")
```

Escribe una cadena de texto en el archivo.

#### METODO `writelines()`
```python
lineas = ["Línea 1\n", "Línea 2\n", "Línea 3\n"]
with open('archivo.txt', 'w') as f:
    f.writelines(lineas)
```

Escribe una lista de cadenas en el archivo.
No añade automáticamente saltos de línea.

#### ESCRITURA CON `print()`
```python
with open('archivo.txt', 'w') as f:
    print("Hola, mundo!", file=f)
    print("Nueva línea", file=f)
```

Puedes redirigir la salida de `print()` a un archivo.
Útil para formatear fácilmente la salida.

#### ESCRITURA EN MODO  `append` ('a')
```python
with open('archivo.txt', 'a') as f:
    f.write("Texto añadido al final\n")
```

Añade contenido al final del archivo sin borrar lo existente.

#### ESCRITURA EN MODO BINARIO ('wb')
```python
datos = bytes([0, 1, 2, 3])
with open('archivo.bin', 'wb') as f:
    f.write(datos)
```

Para escribir datos no textuales.

Puntos importantes:
- `write()` no añade automáticamente saltos de línea.
- Para formatos específicos (CSV, JSON), se usan módulos dedicados.
- Siempre cierra los archivos después de escribir (el bloque `with` lo hace automáticamente).
- Ten cuidado con el modo 'w', ya que sobrescribe el contenido existente.
- Para simplificar, se pueden crear funciones "helper" para los tipos de escritura más comunes en tu trabajo. Por ejemplo:
```python
def escribir_texto(nombre_archivo, contenido):
    with open(nombre_archivo, 'w') as f:
        f.write(contenido)

def añadir_texto(nombre_archivo, contenido):
    with open(nombre_archivo, 'a') as f:
        f.write(contenido)

def escribir_lineas(nombre_archivo, lineas):
    with open(nombre_archivo, 'w') as f:
        f.writelines(linea + '\n' for linea in lineas)
```

#### FORMULAS DE ESCRITURA SEGÚN TIPO (VARÍA SEGÚN TIPO DE ESCRITURA)

```python
# Archivo de texto (.txt)
with open('archivo.txt', 'w') as f:
    f.write("Contenido del archivo")
```
```python
# CSV
import csv

datos = [['Nombre', 'Edad'], ['Ana', 25], ['Juan', 30]]
with open('archivo.csv', 'w', newline='') as f:
    escritor = csv.writer(f)
    escritor.writerows(datos)
```
```python
# JSON
import json

datos = {'nombre': 'Ana', 'edad': 25}
with open('archivo.json', 'w') as f:
    json.dump(datos, f)
```
```python
# XML
import xml.etree.ElementTree as ET

root = ET.Element("raiz")
ET.SubElement(root, "hijo").text = "Contenido"
tree = ET.ElementTree(root)
tree.write("archivo.xml")
```
```python
# Excel (usando pandas)
import pandas as pd

df = pd.DataFrame({'Nombre': ['Ana', 'Juan'], 'Edad': [25, 30]})
df.to_excel('archivo.xlsx', index=False)
```
```python
# Archivo binario
datos = bytes([0, 1, 2, 3])
with open('archivo.bin', 'wb') as f:
    f.write(datos)
```
```python
# YAML
import yaml

datos = {'nombre': 'Ana', 'edad': 25}
with open('archivo.yaml', 'w') as f:
    yaml.dump(datos, f)
```

Puntos clave para tu cuaderno:
- La sintaxis básica con `open()` es similar para la mayoría de los archivos de texto.
- Formatos como CSV, JSON, XML y YAML requieren módulos específicos.
- Para Excel, se recomienda usar bibliotecas como pandas.
- El modo de apertura 'w' es para escritura en texto, 'wb' para binario.
- Algunos formatos pueden requerir parámetros adicionales (como `newline=''` en CSV).

### MODOS DE APERTURA:

1. 'r' - Lectura (por defecto):
   - Abre el archivo para lectura.
   - Error si el archivo no existe.

2. 'w' - Escritura:
   - Abre el archivo para escritura.
   - Crea el archivo si no existe.
   - Sobrescribe el contenido si el archivo ya existe.

3. 'a' - Append (Añadir):
   - Abre el archivo para añadir contenido al final.
   - Crea el archivo si no existe.

4. 'x' - Creación exclusiva:
   - Crea un nuevo archivo y lo abre para escritura.
   - Error si el archivo ya existe.

5. 'b' - Modo binario:
   - Se usa en combinación con otros modos (ej. 'rb', 'wb').
   - Para trabajar con datos no textuales.

6. 't' - Modo texto (por defecto):
   - Se usa en combinación con otros modos (ej. 'rt', 'wt').
   - Para trabajar con archivos de texto.

7. '+' - Actualización (lectura y escritura):
   - Se usa en combinación con otros modos (ej. 'r+', 'w+', 'a+').
   - Permite lectura y escritura en el archivo.

**EJEMPLOS DE MODOS DE APERTURA:**
```python
# Lectura
with open('archivo.txt', 'r') as f:
    contenido = f.read()

# Escritura (sobrescribe)
with open('archivo.txt', 'w') as f:
    f.write('Nuevo contenido')

# Añadir al final
with open('archivo.txt', 'a') as f:
    f.write('Contenido adicional')

# Lectura y escritura
with open('archivo.txt', 'r+') as f:
    contenido = f.read()
    f.write('Nuevo contenido')

# Modo binario (para imágenes, por ejemplo)
with open('imagen.jpg', 'rb') as f:
    datos_imagen = f.read()
```

Es importante elegir el modo correcto según lo que necesites hacer con el archivo. El uso inadecuado puede resultar en pérdida de datos o errores inesperados.

## MANEJO DE EXCEPCIONES

### LOGICA DE LAS EXCEPCIONES
```python
try:
    # Código que puede generar una excepción
except ExcepcionEspecifica:
    # Código que se ejecuta si ocurre ExcepcionEspecifica
```

Las excepciones sirven para manejar errores o situaciones inesperadas en tu código, permitiendo que el programa continúe ejecutándose de manera controlada en lugar de detenerse abruptamente.

### EJEMPLO DE EXCEPCION
```python
try:
    numero = int(input("Ingrese un número: "))
    resultado = 10 / numero
    print(f"El resultado es: {resultado}")
except ValueError:
    print("Error: Debe ingresar un número válido.")
except ZeroDivisionError:
    print("Error: No se puede dividir por cero.")
```

### ESTRUCTURAS DE MANEJOS DE EXCEPCIONES

1. Capturando múltiples excepciones:
```python
try:
    # Código
except (ValueError, TypeError):
    print("Error de tipo de dato")
```

2. Cláusula `else`:
```python
try:
    # Código que puede fallar
except Exception:
    # Manejo de error
else:
    # Se ejecuta si no hubo excepciones
```

3. Cláusula `finally`:
```python
try:
    # Código
except Exception:
    # Manejo de error
finally:
    # Se ejecuta siempre, haya o no excepciones
```

4. Capturando todas las excepciones (no recomendado en general):
```python
try:
    # Código
except Exception as e:
    print(f"Ocurrió un error: {e}")
```

5. Lanzar excepciones:
```python
def dividir(a, b):
    if b == 0:
        raise ValueError("No se puede dividir por cero")
    return a / b
```

### TIPOS DE EXCEPCIONES

1. ValueError:
   - Se produce cuando una función recibe un argumento del tipo correcto pero con un valor inapropiado.
   - Ejemplo: Intentar convertir una cadena no numérica a un entero.

```python
try:
    numero = int("abc")
except ValueError:
    print("No se puede convertir 'abc' a un número.")
```

2. ZeroDivisionError:
   - Ocurre al intentar dividir por cero.

```python
try:
    resultado = 10 / 0
except ZeroDivisionError:
    print("No se puede dividir por cero.")
```

3. TypeError:
   - Surge cuando se realiza una operación en un objeto de tipo inapropiado.

```python
try:
    resultado = "5" + 5
except TypeError:
    print("No se puede sumar una cadena y un número.")
```

4. Exception:
   - Es la clase base para la mayoría de las excepciones incorporadas.
   - Capturar Exception capturará casi todos los errores, pero es mejor ser específico cuando sea posible.

```python
try:
    # Algún código que podría generar varios tipos de errores
except Exception as e:
    print(f"Ocurrió un error: {type(e).__name__}")
```

5. Excepciones personalizadas:
   - Puedes crear tus propias excepciones para manejar errores específicos de tu aplicación.

```python
class MiErrorPersonalizado(Exception):
    pass

try:
    raise MiErrorPersonalizado("Este es un error personalizado")
except MiErrorPersonalizado as e:
    print(f"Capturado error personalizado: {e}")
```

Las cláusulas adicionales:

- `else`: Se ejecuta si no ocurre ninguna excepción en el bloque `try`.
- `finally`: Se ejecuta siempre, haya ocurrido una excepción o no. Útil para limpieza o cierre de recursos.

El manejo de excepciones permite:
1. Prevenir que tu programa se detenga abruptamente.
2. Proporcionar mensajes de error útiles.
3. Ejecutar código de recuperación cuando ocurren errores.
4. Realizar limpieza de recursos incluso si ocurren errores.


### EJEMPLOS PRACTICOS DE EXCEPCIONES

1. Estructura básica y tipos de excepciones:

```python
try:
    # Intentamos realizar operaciones que pueden causar errores
    numero = int(input("Ingrese un número: "))
    resultado = 10 / numero
    
    with open("archivo.txt", "r") as archivo:
        contenido = archivo.read()

except ValueError:
    # Se ejecuta si el usuario no ingresa un número válido
    print("Error: Debe ingresar un número válido.")

except ZeroDivisionError:
    # Se ejecuta si el usuario ingresa cero
    print("Error: No se puede dividir por cero.")

except FileNotFoundError:
    # Se ejecuta si el archivo no existe
    print("Error: El archivo no se encontró.")

except Exception as e:
    # Captura cualquier otra excepción no prevista
    print(f"Ocurrió un error inesperado: {e}")

else:
    # Se ejecuta si no hubo excepciones
    print(f"El resultado es: {resultado}")
    print(f"Contenido del archivo: {contenido}")

finally:
    # Se ejecuta siempre, haya o no excepciones
    print("Proceso finalizado.")
```

2. Lanzar excepciones personalizadas:

```python
class ValorNegativoError(Exception):
    pass

def calcular_raiz_cuadrada(numero):
    if numero < 0:
        raise ValorNegativoError("No se puede calcular la raíz cuadrada de un número negativo")
    return numero ** 0.5

try:
    resultado = calcular_raiz_cuadrada(-4)
except ValorNegativoError as e:
    print(f"Error: {e}")
```

Este ejemplo combina:
- La estructura básica de manejo de excepciones (try, except, else, finally).
- Diferentes tipos de excepciones específicas (ValueError, ZeroDivisionError, etc.).
- El uso de Exception para capturar errores no previstos.
- Cómo lanzar y manejar excepciones personalizadas.

Puntos clave:
1. Las excepciones te permiten manejar errores de forma controlada.
2. Puedes tener múltiples bloques `except` para manejar diferentes tipos de errores.
3. `else` se ejecuta si no hay excepciones, y `finally` se ejecuta siempre.
4. Puedes crear y lanzar tus propias excepciones para situaciones específicas.




- Trabajo con rutas de archivos y directorios
- Funciones más avanzadas (lambdas, decoradores)
- Programación orientada a objetos
- Módulos y paquetes más avanzados
- Expresiones regulares
- Trabajo con fechas y tiempo
- Conexiones a bases de datos
- Requests y APIs
- Proyectos más complejos con Tkinter