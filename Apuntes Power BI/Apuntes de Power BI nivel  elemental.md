
## 1. Introducción al análisis de datos

• Descripción de la herramienta:
Power BI es una suite de herramientas de análisis empresarial de Microsoft que permite conectar diversas fuentes de datos, transformarlos y visualizarlos de forma interactiva.

• Entorno Power BI Desktop:
Power BI Desktop es la aplicación principal para crear informes y dashboards. Consta de tres vistas principales:
1. Vista de Datos: para ver y editar tablas de datos.
2. Vista de Modelo: para establecer relaciones entre tablas.
3. Vista de Informe: para crear visualizaciones.

• Ejemplos de uso:
- Análisis de ventas por región y producto.
- Seguimiento de KPIs financieros.
- Monitoreo de rendimiento de campañas de marketing.

• Trabajo con datos:
Power BI puede conectarse a diversas fuentes de datos como Excel, bases de datos SQL, servicios web, etc. 

Pasos para importar datos:
1. En Power BI Desktop, haz clic en "Obtener datos".
2. Selecciona la fuente de datos deseada.
3. Sigue el asistente para conectarte y seleccionar las tablas o datos necesarios.
4. Haz clic en "Cargar" o "Transformar datos" según sea necesario.

• Normalizaciones:
La normalización en Power BI implica estructurar los datos de manera eficiente para reducir la redundancia y mejorar la integridad de los datos.

Procedimiento de normalización en Power BI:
1. Identifica las columnas que contienen datos repetidos en múltiples filas.
2. Crea una nueva tabla para estos datos repetidos.
3. En el Editor de Power Query, selecciona la columna a normalizar.
4. Haz clic derecho y selecciona "Quitar duplicados" para crear una lista única.
5. Asigna un identificador único a cada valor en esta nueva tabla.
6. En la tabla original, reemplaza los valores repetidos con los identificadores correspondientes.
7. Establece una relación entre las dos tablas utilizando el identificador.

• Limpieza y transformación de datos:
Power BI ofrece diversas herramientas para limpiar y transformar datos en el Editor de Power Query.

Ejemplos de transformaciones comunes:
- Eliminar filas o columnas innecesarias.
- Cambiar tipos de datos.
- Combinar o dividir columnas.
- Reemplazar valores.
- Pivotar o despivotar tablas.

Pasos para realizar transformaciones:
1. En Power BI Desktop, haz clic en "Transformar datos" al cargar los datos.
2. En el Editor de Power Query, selecciona la columna o tabla a transformar.
3. Utiliza las opciones en la cinta de opciones o haz clic derecho para acceder a más transformaciones.
4. Aplica las transformaciones necesarias.
5. Haz clic en "Cerrar y aplicar" cuando hayas terminado.

• Breve introducción al lenguaje M:
M es el lenguaje de fórmulas utilizado en Power Query para realizar transformaciones de datos más avanzadas.

Ejemplo básico de código M:
```
let
    Origen = Excel.Workbook(File.Contents("C:\Datos\Ventas.xlsx"), null, true),
    Hoja1_Table = Origen{[Item="Hoja1",Kind="Table"]}[Data],
    TiposCambiados = Table.TransformColumnTypes(Hoja1_Table,{{"Fecha", type date}, {"Ventas", type number}})
in
    TiposCambiados
```

Este código carga una hoja de Excel, selecciona una tabla específica y cambia los tipos de datos de algunas columnas.

Por supuesto, continuemos con el cuaderno de apuntes sobre Power BI, enfocándonos ahora en el modelado de datos:

## 2. Modelado de datos

• Modelo de datos:
El modelo de datos en Power BI es una representación de cómo se organizan y se relacionan las diferentes tablas de datos. Un buen modelo de datos es fundamental para crear informes eficientes y precisos.

Principios clave del modelado de datos:
1. Simplicidad: Mantén el modelo lo más simple posible.
2. Integridad: Asegúrate de que las relaciones entre tablas sean correctas.
3. Rendimiento: Optimiza el modelo para consultas rápidas.

• Tipos de datos:
Power BI soporta varios tipos de datos para asegurar que la información se almacene y procese correctamente.

Tipos de datos comunes:
- Texto
- Número entero
- Número decimal
- Fecha
- Fecha/Hora
- Booleano (Verdadero/Falso)
- Moneda

Pasos para cambiar el tipo de datos:
1. En la vista de Datos, selecciona la columna deseada.
2. En la pestaña "Herramientas de tabla", haz clic en "Tipo de datos".
3. Selecciona el tipo de datos apropiado de la lista desplegable.

• Relaciones y campos clave:
Las relaciones conectan tablas en el modelo de datos, generalmente a través de campos clave.

Tipos de relaciones:
1. Uno a muchos (1:*): La más común. Un registro en la tabla A se relaciona con varios en la tabla B.
2. Uno a uno (1:1): Un registro en la tabla A se relaciona con uno en la tabla B.
3. Muchos a muchos (*:*): Varios registros en la tabla A se relacionan con varios en la tabla B (requiere una tabla intermedia).

Pasos para crear una relación:
1. Ve a la vista de Modelo.
2. Arrastra el campo clave de una tabla al campo correspondiente en otra tabla.
3. Ajusta las propiedades de la relación en el panel que aparece.

Ejemplo:
Relacionar una tabla de Ventas con una tabla de Productos usando el campo "ID_Producto" como clave.

• Jerarquías:
Las jerarquías permiten organizar datos en niveles, facilitando la navegación y el análisis.

Tipos comunes de jerarquías:
- Tiempo: Año > Trimestre > Mes > Día
- Geografía: País > Estado > Ciudad
- Productos: Categoría > Subcategoría > Producto

Pasos para crear una jerarquía:
1. En la vista de Datos o Informe, haz clic derecho en el campo que será el nivel superior.
2. Selecciona "Crear jerarquía".
3. Arrastra los campos adicionales a la jerarquía en el orden deseado.

Ejemplo de jerarquía geográfica:
1. Clic derecho en "País" > Crear jerarquía
2. Nombrar la jerarquía como "Geografía"
3. Arrastrar "Estado" debajo de "País"
4. Arrastrar "Ciudad" debajo de "Estado"

Beneficios de usar jerarquías:
- Facilita la navegación en visualizaciones como gráficos de árbol o mapas.
- Permite hacer drill-down/up rápidamente en los informes.
- Mejora la organización del panel de campos.

Consejos adicionales para el modelado de datos:
1. Usa nombres descriptivos para tablas y columnas.
2. Crea medidas para cálculos complejos en lugar de columnas calculadas cuando sea posible.
3. Considera el uso de tablas de dimensiones y hechos para modelos más complejos (modelado en estrella).
4. Revisa y optimiza regularmente tu modelo de datos para mantener el rendimiento.

Perfecto, continuemos con el tema de cálculos y expresiones DAX en Power BI:

## 3. Cálculos y expresiones DAX

• Introducción a DAX:
DAX (Data Analysis Expressions) es un lenguaje de fórmulas utilizado en Power BI para crear cálculos personalizados y análisis avanzados.

Características clave de DAX:
- Sintaxis similar a Excel, pero más potente
- Trabaja con tablas y relaciones
- Permite crear medidas y columnas calculadas

• Funciones comunes:

1. Funciones de agregación:
   - SUM(), AVERAGE(), COUNT(), MIN(), MAX()

   Ejemplo: 
   ```
   Total Ventas = SUM(Ventas[Monto])
   ```

2. Funciones de texto:
   - CONCATENATE(), LEFT(), RIGHT(), LEN()

   Ejemplo:
   ```
   Nombre Completo = CONCATENATE(Empleados[Nombre], " ", Empleados[Apellido])
   ```

3. Funciones de fecha y hora:
   - YEAR(), MONTH(), DAY(), DATEADD(), DATEDIFF()

   Ejemplo:
   ```
   Edad = DATEDIFF(Empleados[Fecha Nacimiento], TODAY(), YEAR)
   ```

4. Funciones lógicas:
   - IF(), AND(), OR(), SWITCH()

   Ejemplo:
   ```
   Categoría de Ventas = 
   IF(Ventas[Monto] > 1000, "Alto", 
      IF(Ventas[Monto] > 500, "Medio", "Bajo"))
   ```

• Columnas calculadas:
Las columnas calculadas se calculan para cada fila de una tabla y se almacenan en el modelo.

Pasos para crear una columna calculada:
1. En la vista de Datos, selecciona la tabla deseada.
2. Haz clic en "Nueva columna" en la pestaña de Modelado.
3. Escribe la fórmula DAX en la barra de fórmulas.

Ejemplo:
```
Margen = Ventas[Precio de Venta] - Ventas[Costo]
```

• Medidas implícitas y explícitas:

Medidas implícitas:
- Creadas automáticamente al arrastrar campos numéricos a visualizaciones.
- Utilizan agregaciones predeterminadas (suma, conteo, etc.).

Medidas explícitas:
- Creadas manualmente por el usuario.
- Ofrecen mayor control y flexibilidad.

Pasos para crear una medida explícita:
1. En la vista de Datos o Informe, haz clic derecho en la tabla deseada.
2. Selecciona "Nueva medida".
3. Escribe la fórmula DAX en la barra de fórmulas.

Ejemplo:
```
Promedio de Ventas = AVERAGE(Ventas[Monto])
```

• Funciones de filtrado:
Permiten realizar cálculos en contextos específicos.

Funciones comunes:
- FILTER(), ALL(), ALLEXCEPT(), RELATED()

Ejemplo:
```
Ventas de Productos Caros = 
CALCULATE(SUM(Ventas[Monto]), FILTER(Productos, Productos[Precio] > 1000))
```

• Funciones de inteligencia de tiempos:
Facilitan los cálculos basados en períodos de tiempo.

Funciones comunes:
- DATEADD(), SAMEPERIODLASTYEAR(), TOTALYTD(), PARALLELPERIOD()

Ejemplo:
```
Ventas Año Anterior = 
CALCULATE(SUM(Ventas[Monto]), SAMEPERIODLASTYEAR(Calendario[Fecha]))
```

• DAX con inteligencia artificial:
Power BI incorpora funcionalidades de IA para ayudar en la creación de fórmulas DAX.

Características:
1. Sugerencias de fórmulas: Power BI sugiere fórmulas basadas en el contexto y los datos.
2. Autocompletado inteligente: Ofrece sugerencias relevantes mientras escribes.
3. Explicaciones en lenguaje natural: Proporciona descripciones de las funciones y su uso.

Cómo usar DAX con IA:
1. Comienza a escribir una fórmula en la barra de fórmulas.
2. Observa las sugerencias que aparecen.
3. Utiliza las flechas del teclado para navegar por las sugerencias.
4. Presiona Tab o Enter para aceptar una sugerencia.

Ejemplo de uso:
Al escribir "CALC", Power BI podría sugerir "CALCULATE" y explicar su función.

Consejos para trabajar con DAX:
1. Comprende el contexto de fila y contexto de filtro.
2. Usa variables para simplificar fórmulas complejas.
3. Practica con diferentes escenarios para mejorar tus habilidades.
4. Utiliza el analizador de rendimiento para optimizar fórmulas.

## 4. Visualizaciones

• Visuales predeterminados:
Power BI ofrece una variedad de visualizaciones incorporadas:

1. Gráficos de barras y columnas
2. Gráficos de líneas y áreas
3. Gráficos circulares y de anillos
4. Tablas y matrices
5. Tarjetas y KPIs
6. Mapas

Pasos para crear una visualización:
1. En la vista de Informe, selecciona el tipo de visual deseado del panel de Visualizaciones.
2. Arrastra los campos relevantes a los contenedores de campos del visual.

• Galería de visuales:
Power BI permite importar visuales personalizados desde la Galería de Power BI.

Cómo importar un visual personalizado:
1. En Power BI Desktop, ve a "Obtener más visuales" en el panel de Visualizaciones.
2. Busca y selecciona el visual deseado.
3. Haz clic en "Agregar" para importarlo a tu informe.

• Formatos y analítica:
Cada visual tiene opciones de formato para personalizar su apariencia y comportamiento.

Aspectos comunes de formato:
- Colores y estilos
- Etiquetas y leyendas
- Ejes y escalas
- Interactividad (como drill-through)

Características analíticas:
- Líneas de tendencia
- Pronósticos
- Líneas constantes

• Mapas:
Power BI ofrece varios tipos de mapas:
- Mapa de relleno
- Mapa de burbujas
- Mapa de formas

Pasos para crear un mapa:
1. Selecciona el tipo de mapa deseado.
2. Arrastra un campo geográfico (como país o ciudad) al contenedor "Ubicación".
3. Agrega un campo numérico al contenedor "Tamaño" o "Color saturation".

• Filtros:
Los filtros permiten refinar los datos mostrados en las visualizaciones.

Tipos de filtros:
1. Filtros de visual
2. Filtros de página
3. Filtros de informe
4. Segmentaciones de datos

Cómo aplicar filtros:
1. Selecciona el nivel de filtro deseado en el panel de Filtros.
2. Arrastra el campo por el que quieres filtrar.
3. Selecciona los valores específicos o define un rango.

• Informes de alto impacto visual:
Para crear informes visualmente atractivos:
1. Usa una paleta de colores coherente.
2. Mantén un diseño limpio y organizado.
3. Utiliza jerarquías visuales para guiar la atención.
4. Incluye interactividad para fomentar la exploración.

• Inteligencia artificial en gráficos:
Power BI incorpora capacidades de IA en sus visualizaciones:

1. Análisis de clave: Identifica automáticamente factores influyentes en un KPI.
2. Detección de anomalías: Resalta valores atípicos en los datos.
3. Agrupación: Agrupa automáticamente datos similares.

Cómo usar la IA en gráficos:
1. Crea una visualización.
2. En el panel de Análisis, selecciona la opción de IA deseada.
3. Configura los parámetros según sea necesario.

## 5. Servicio Power BI

• Descripción:
El servicio Power BI es una plataforma basada en la nube para compartir y colaborar en informes y dashboards.

• Diferencias con Power BI Desktop:
1. Power BI Desktop: Herramienta de creación y modelado.
2. Servicio Power BI: Plataforma de publicación y colaboración.

Principales diferencias:
- El servicio no permite modelado de datos complejo.
- El servicio ofrece características de colaboración y compartición.
- El servicio permite crear dashboards (no disponible en Desktop).

• Paneles o dashboards:
Los dashboards son colecciones de visualizaciones de uno o más informes.

Características de los dashboards:
- Vista de una página
- Actualizaciones en tiempo real
- Pueden combinar visualizaciones de múltiples conjuntos de datos

Cómo crear un dashboard:
1. En el servicio Power BI, ve a "Mi espacio de trabajo".
2. Haz clic en "Nuevo dashboard".
3. Ancla visualizaciones de tus informes al dashboard.

• Publicar y compartir dashboards e informes:

Publicar desde Power BI Desktop:
1. En Power BI Desktop, haz clic en "Publicar" en la pestaña Inicio.
2. Selecciona el espacio de trabajo de destino.
3. Haz clic en "Publicar".

Compartir en el servicio Power BI:
1. Abre el informe o dashboard que quieres compartir.
2. Haz clic en "Compartir" en la esquina superior derecha.
3. Ingresa las direcciones de correo electrónico de los destinatarios.
4. Configura los permisos (ver, editar).
5. Haz clic en "Compartir".

Consejos para compartir:
- Usa grupos de seguridad para gestionar permisos a gran escala.
- Considera el uso de la opción "Publicar en la web" para contenido público.
- Utiliza aplicaciones de Power BI para distribuir conjuntos de informes y dashboards.


