
## ETL (Extracción, Transformación, Carga)

### Obtención de Datos

#### Conectarse a fuentes: Excel, CSV, Access, Carpetas, Web, OData

**Importar datos desde Excel**
```
Pasos: Inicio > Obtener Datos > Excel
Ejemplo: Inicio > Obtener Datos > Excel > Seleccionar archivo "Ventas2022.xlsx"
```

**Importar datos desde CSV**
```
Pasos: Inicio > Obtener Datos > Texto/CSV
Ejemplo: Inicio > Obtener Datos > Texto/CSV > Seleccionar archivo "Ventas2022.csv"
```

**Importar datos desde Access**
```
Pasos: Inicio > Obtener Datos > Base de Datos de Access
Ejemplo: Inicio > Obtener Datos > Base de Datos de Access > Seleccionar archivo "Neptuno.accdb"
```

**Importar datos desde una carpeta**
```
Pasos: Inicio > Obtener Datos > Más... > Carpeta
Ejemplo: Inicio > Obtener Datos > Más... > Carpeta > Seleccionar carpeta con archivos ".txt"
```

**Importar datos desde la web**
```
Pasos: Inicio > Obtener Datos > Web
Ejemplo: Inicio > Obtener Datos > Web > Ingresar URL > Conectar
```

**Importar datos desde OData**
```
Pasos: Inicio > Obtener Datos > Fuente OData
Ejemplo: Inicio > Obtener Datos > Fuente OData > Ingresar URL
```

### Vista de Power Query

**Explorar datos cargados**
```
Pasos: Seleccionar tabla > Transformar datos
Ejemplo: Tabla "Ventas2022" cargada > Ver vista previa de datos
```

### Limpiar y Transformar Datos

**Remover filas/columnas innecesarias**
```
Pasos: Inicio > Quitar Filas > Quitar Filas Superiores
Ejemplo: Quitar las primeras 2 filas de la tabla "Ventas2022"
```

**Recortar espacios en texto**
```
Pasos: Transformar > Formato > Recortar
Ejemplo: Recortar espacios en blanco en la columna "NombreCliente"
```

**Reemplazar valores nulos/erróneos**
```
Pasos: Transformar > Reemplazar Valores
Ejemplo: Reemplazar valores nulos en la columna "CódigoPostal" por "00000"
```

**Dividir columnas combinadas**
```
Pasos: Transformar > Dividir Columna > Por delimitador
Ejemplo: Dividir la columna "NombreCompleto" en "Nombre" y "Apellido" usando el delimitador espacio (" ")
```

**Corregir tipos de datos**
```
Pasos: Seleccionar columna > Cambiar tipo de dato
Ejemplo: Cambiar el tipo de dato de la columna "Fecha" a "Fecha"
```

**Anular dinamización de columnas**
```
Pasos: Transformar > Anular Dinamización
Ejemplo: Anular la dinamización de las columnas "Enero", "Febrero", "Marzo" en la tabla "VentasMensuales"
```

### Transformaciones Avanzadas

**Columnas calculadas/índice**
```
Pasos: Agregar Columna > Índice de fila
Ejemplo: Crear una columna de índice empezando en 1 e incrementando en 1
```

**Editor Avanzado (código M)**
```
Pasos: Inicio > Editor Avanzado
Ejemplo: Agregar una columna calculada "NombreEdad" que combine "Nombre" y "Edad":
let
    Origen = Excel.Workbook(File.Contents("C:\ruta\archivo.xlsx"), null, true),
    Datos = Origen{[Nombre= "Hoja1"]}[Data],
    ColumnasCambiadas = Table.TransformColumnTypes(Datos,{{"Nombre", type text}, {"Edad", Int64.Type}}),
    ColumnaNueva = Table.AddColumn(ColumnasCambiadas, "NombreEdad", each [Nombre] & " - " & Text.From([Edad]))
in
    ColumnaNueva
```

### Metadatos y Organización

**Renombrar columnas**
```
Pasos: Doble clic en encabezado > Cambiar nombre
Ejemplo: Renombrar la columna "Ventas" a "MontoVentas"
```

**Mover/reorganizar columnas**
```
Pasos: Arrastrar encabezados
Ejemplo: Mover la columna "MontoVentas" al inicio de la tabla
```

### Cargar Datos al Modelo

**Crear tablas en modelo**
```
Pasos: Inicio > Cerrar y Aplicar
Ejemplo: Inicio > Cerrar y Aplicar > Crear tabla "Ventas2022"
```

**Guardar archivo .pbix**
```
Pasos: Archivo > Guardar como
Ejemplo: Archivo > Guardar como > "ModeloVentas2022.pbix"
```

### Buenas Prácticas

**Documentar cada paso y criterios aplicados**
**Aplicar lógica consistente al limpiar datos**
**Validar calidad y consistencia final**
**Exportar datos a Excel si se requiere**
```
Pasos: Inicio > Exportar > Exportar a Excel
Ejemplo: Inicio > Exportar > Exportar datos a Excel > "VentasLimpias.xlsx"
```

**Optimización de Consultas**
```
Revisar pasos aplicados y simplificar consulta
Aplicar transformaciones con código M más eficiente
Evitar pasos redundantes o innecesarios
Aprovechar funciones de llenado, reemplazo, etc.
```

## Relaciones y Modelado

### Verificar tipos de datos adecuados
```
Pasos: Pestaña Datos > Tabla > Ver tipos de datos de columnas
Ejemplo: Verificar que la columna "IdCliente" en la tabla "Clientes" sea del tipo Entero
```

### Crear relaciones entre tablas
```
Pasos: Vista Modelo > Administrar Relaciones > Nueva
Ejemplo: Crear relación entre "Pedidos[IdCliente]" y "Clientes[Id]"
```

### Verificar cardinalidad de relaciones
```
Pasos: Vista Modelo > Administrar Relaciones > Seleccionar relación
Ejemplo: Verificar que la relación entre "Pedidos" y "Clientes" sea de "Muchos a uno"
```

### Modificar filtros cruzados
```
Pasos: Vista Modelo > Administrar Relaciones > Editar > Filtros cruzados
Ejemplo: Cambiar la dirección de filtros cruzados a "Ambas" en la relación entre "Pedidos" y "Clientes"
```

### Crear jerarquías
```
Pasos: Tabla > Columna > Crear jerarquía
Ejemplo: Crear jerarquía "Ubicación" en la tabla "Clientes" con las columnas "País", "Provincia" y "Ciudad"
```

## DAX (Data Analysis Expressions)

### Crear columnas calculadas
```
Pasos: Tabla > Nueva Columna > Fórmula personalizada
Ejemplo: Crear columna "NombreCompleto" en la tabla "Clientes":
NombreCompleto = Clientes[Nombre] & " " & Clientes[Apellido]
```

### Crear medidas
```
Pasos: Tabla > Nueva Medida > Fórmula DAX
Ejemplo: Crear medida "TotalGastosEnvio" en la tabla "Pedidos":
TotalGastosEnvio = SUM(Pedidos[GastosEnvio])
```

### Usar medidas rápidas
```
Pasos: Inicio > Medidas rápidas > Seleccionar categoría
Ejemplo: Crear una medida rápida de "Valor filtrado" para "Gastos de Envío" en "Miami"
```

### Funciones DAX Esenciales

**SUM**
```
Ejemplo: SUM(Pedidos[GastosEnvio])
```

**CALCULATE**
```
Ejemplo: CALCULATE(SUM(Pedidos[GastosEnvio]), Pedidos[Ciudad] = "Miami")
```

**DIVIDE**
```
Ejemplo: DIVIDE(SUM(Pedidos[GastosEnvio]), SUM(Pedidos[Cantidad]), 0)
```

**VAR**
```
Ejemplo:
TotalVentas = SUM(Pedidos[MontoVentas])
TotalGastos = SUM(Pedidos[GastosEnvio])
Margen = VAR TotalVentas = SUM(Pedidos[MontoVentas])
        VAR TotalGastos = SUM(Pedidos[GastosEnvio])
        RETURN TotalVentas - TotalGastos
```

## Visualizaciones

### Gráficos

#### Gráfico de Columnas

**Crear un gráfico de columnas agrupadas**
```
Pasos: Seleccionar Gráfico de Columnas Agrupadas > Arrastrar "Categoría de Producto" al eje X > Arrastrar "Precio" al eje Y
Ejemplo: Mostrar la relación entre categorías de productos y precios listados
```

#### Gráfico Circular

**Crear un gráfico circular**
```
Pasos: Seleccionar Gráfico Circular > Arrastrar "Cantidad" al valor > Arrastrar "Ciudad" a la leyenda
Ejemplo: Mostrar la distribución de cantidades por ciudad
```

#### Gráfico de Embudo

**Crear un gráfico de embudo**
```
Pasos: Seleccionar Embudo > Arrastrar "Cantidad" al valor > Arrastrar "Nombre" de la tabla "Empleados" a la categoría
Ejemplo: Mostrar la cantidad de unidades comercializadas por cada empleado
```

#### Gráfico de Barras

**Crear un gráfico de barras apiladas**
```
Pasos: Seleccionar Gráfico de Barras Apiladas > Arrastrar "Cantidad" al valor > Arrastrar "Mes" al eje X > Arrastrar "Ciudad" a la leyenda
Ejemplo: Mostrar la cantidad de productos vendidos en diferentes ciudades por mes
```

#### Gráfico de Líneas

**Crear un gráfico de líneas**
```
Pasos: Seleccionar Gráfico de Líneas > Arrastrar "Fecha" al eje X > Arrastrar "Ventas" al valor
Ejemplo: Mostrar la tendencia de ventas a lo largo del tiempo
```

### Tablas y Matrices

**Crear una tabla**
```
Pasos: Seleccionar Tabla > Arrastrar "NombreCliente" a la tabla > Arrastrar "MontoVentas" a la tabla
Ejemplo: Listar nombres de clientes y montos de ventas asociados
```

**Crear una matriz**
```
Pasos: Seleccionar Matriz > Arrastrar "Categoría de Producto" a las filas > Arrastrar "Mes" a las columnas > Arrastrar "Ventas" al valor
Ejemplo: Mostrar una matriz de ventas por categoría de producto y mes
```

### Slicers

**Agregar un slicer**
```
Pasos: Seleccionar Slicer > Arrastrar "Ciudad" al slicer
Ejemplo: Filtrar los datos del reporte por diferentes ciudades
```

### Mapas

**Crear un mapa**
```
Pasos: Seleccionar Mapa > Arrastrar "Ciudad" al valor > Arrastrar "Ventas" al tamaño
Ejemplo: Mostrar ventas por ciudad en un mapa
```

### Tarjetas y KPI

**Crear una tarjeta**
```
Pasos: Seleccionar Tarjeta > Arrastrar "MontoTotalVentas" a la tarjeta
Ejemplo: Mostrar el monto total de ventas en una tarjeta
```

**Crear un KPI**
```
Pasos: Seleccionar KPI > Arrastrar "Fecha" al eje > Arrastrar "Ventas" al valor > Definir valor objetivo
Ejemplo: Mostrar el KPI de ventas con el valor objetivo definido
```

## Conclusión

Este cuaderno de apuntes y atajos de Power BI cubre los aspectos esenciales del proceso ETL, modelado de datos, fórmulas DAX y visualización de datos. Siguiendo estos pasos y ejemplos, podrás manejar y analizar datos de manera eficiente utilizando Power BI.
