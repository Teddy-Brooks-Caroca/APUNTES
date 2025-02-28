
## MODELOS ESTADISTICOS

### REGRESION LINEAL:

```R
# Regresión lineal simple
modelo <- lm(variable_dependiente ~ variable_independiente, data = nombre_del_dataset)

# Regresión lineal multiple
modelo <- lm(variable_dependiente ~ variable_independiente1 + variable_independiente2 + variable_independiente3, data = nombre_del_dataset)
```

- `modelo` es el nombre que le das al modelo de regresión (puedes usar cualquier nombre).
- `lm` es la función para "linear model" (modelo lineal).
- `variable_dependiente` es la variable que estás tratando de predecir.
- `variable_independiente` es la variable que usas para hacer la predicción.
- `nombre_del_dataset` es el nombre del conjunto de datos que estás utilizando.

#### EJEMPLO PRACTICO DE REGRESION LINEAL:

 Imagina que tenemos un conjunto de datos sobre el precio de casas y queremos ver cómo el tamaño de la casa (en metros cuadrados) afecta al precio.

Primero, creamos el modelo:

```R
modelo <- lm(precio ~ tamaño, data = datos_casas)
```

Luego, usamos la función `summary()` para obtener los resultados:

```R
summary(modelo)
```

Esto nos dará una salida similar a esta:

```R
Call:
lm(formula = precio ~ tamaño, data = datos_casas)

Residuals:
     Min       1Q   Median       3Q      Max 
-100000  -25000    2000   20000  150000 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) 50000     15000      3.333   0.00185 ** 
tamaño         1000      100     10.000   < 2e-16 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 40000 on 98 degrees of freedom
Multiple R-squared:  0.7, Adjusted R-squared:  0.695 
F-statistic: 100 on 1 and 98 DF,  p-value: < 2.2e-16
```

Interpretación de los resultados:

1. Coeficientes:
   - Intercept (50000): Es el precio base estimado cuando el tamaño es 0 m². En este caso, no tiene mucho sentido práctico.
   - tamaño (1000): Por cada metro cuadrado adicional, el precio de la casa aumenta en promedio 1000 unidades monetarias.

2. Significancia estadística:
   - Los asteriscos (***) indican que la variable 'tamaño' es altamente significativa (p < 0.001).
   - El valor p (Pr(>|t|)) para 'tamaño' es muy pequeño (< 2e-16), lo que sugiere una fuerte evidencia contra la hipótesis nula de que no hay relación entre tamaño y precio.

3. R-cuadrado:
   - R-squared: 0.7 significa que aproximadamente el 70% de la variabilidad en el precio puede explicarse por el tamaño de la casa.

4. F-statistic:
   - El valor p muy bajo (< 2.2e-16) indica que el modelo en general es estadísticamente significativo.

5. Residuales:
   - Los residuales nos dan una idea de qué tan bien se ajusta el modelo. En este caso, varían desde -100000 hasta 150000, lo que podría indicar que hay algunos outliers o que podría haber otros factores influyendo en el precio.

Interpretación general:
Este modelo sugiere que existe una relación positiva y significativa entre el tamaño de una casa y su precio. En promedio, cada metro cuadrado adicional aumenta el precio en 1000 unidades monetarias. El modelo explica el 70% de la variación en los precios, lo que es bastante bueno, pero indica que hay otros factores que también influyen en el precio de una casa.

### PRUEBA Y ENTRENAMIENTO:

Propósito: Evaluar el rendimiento del modelo en datos no vistos y evitar el sobreajuste.
Explicación: La muestra de entrenamiento se usa para construir el modelo, mientras que la de prueba se utiliza para evaluar su rendimiento en datos nuevos.

```R
muestra <- floor(porcentaje * nrow(data))
seleccion <- sample(1:nrow(data), size = muestra)

entrenamiento <- data[seleccion,]
prueba <- data[-seleccion,]
```

- `data` es el nombre de tu conjunto de datos.
- `porcentaje` es la proporción que quieres para tu conjunto de entrenamiento (por ejemplo, 0.8 para 80%).

Esta estructura te permite:

 Ajustar fácilmente el tamaño de tu conjunto de entrenamiento cambiando el `porcentaje`.
 Aplicar este método a cualquier conjunto de datos cambiando `data` por el nombre de tu dataframe.

Su procedimiento:

1. Primero, determinamos el tamaño de la muestra que queremos usar para entrenamiento:
   ```R
   muestra <- floor(porcentaje * nrow(data))
   ```
   Esto no saca una muestra en sí, sino que calcula cuántas filas deberían estar en la muestra de entrenamiento.

2. Luego, seleccionamos aleatoriamente las filas que formarán parte de esta muestra:
   ```R
   seleccion <- sample(1:nrow(data), size = muestra)
   ```
   Esto genera una lista de índices aleatorios que representan las filas que usaremos para entrenamiento.

3. Finalmente, utilizamos estos índices para dividir nuestros datos:
   ```R
   entrenamiento <- data[seleccion,]
   prueba <- data[-seleccion,]
   ```

Es importante notar que:

- No estamos sacando una muestra separada de nuestra base de datos original. En su lugar, estamos dividiendo toda la base de datos en dos partes: entrenamiento y prueba.
- La "selección" que hacemos es simplemente decidir qué filas irán a cada conjunto.
- Todas las filas de la base de datos original terminan en uno de los dos conjuntos (entrenamiento o prueba), sin repeticiones.

Esta técnica asegura que:
Usamos todos nuestros datos.
No hay superposición entre los conjuntos de entrenamiento y prueba.
La división es aleatoria, lo que ayuda a evitar sesgos.

Es una forma eficiente y efectiva de preparar nuestros datos para el modelado, permitiéndonos entrenar en una parte de los datos y probar en otra parte independiente.

### ARBOL DE DECISION:

Propósito: Crear un modelo de clasificación o regresión basado en reglas de decisión.
Uso: Predecir una variable objetivo basándose en múltiples variables de entrada.

```R
modelo_arbol <- ctree(variable_de_respuesta ~ ., data = entrenamiento)
```

```R
modelo_arbol <- ctree(variable_de_respuesta ~ var1 + var2 + var3, data = entrenamiento)
```
- `variable_de_respuesta`: Esta es la variable que estás tratando de predecir o explicar. Es tu variable dependiente.
- `~`: Este símbolo se lee como "en función de" o "explicado por".
- `.`: El punto después del `~` es una forma abreviada de decir "todas las otras variables en el conjunto de datos". Esto significa que estás usando todas las demás variables como predictores.
- `data = entrenamiento`: Esto especifica que estás usando el conjunto de datos de entrenamiento que creaste anteriormente.
- La función `ctree()` creará un árbol de decisión condicional, que es una variante particular de los árboles de decisión que realiza pruebas de significancia para seleccionar las variables y los puntos de división.

#### EJEMPLO PRACTICO DE ARBOL DE DECISION

 Vamos a usar el conjunto de datos "iris", que viene preinstalado en R y es comúnmente usado para ejemplos de clasificación.

Primero, carguemos las librerías necesarias y preparemos los datos:

```R
library(party)
library(datasets)

# Cargar el conjunto de datos iris
data(iris)

# Dividir los datos en conjuntos de entrenamiento y prueba
set.seed(123)  # Para reproducibilidad
muestra <- floor(0.7 * nrow(iris))
seleccion <- sample(1:nrow(iris), size = muestra)
entrenamiento <- iris[seleccion,]
prueba <- iris[-seleccion,]
```

Ahora, creemos el árbol de decisión:

```R
# Crear el modelo de árbol de decisión
modelo_arbol <- ctree(Species ~ ., data = entrenamiento)

# Visualizar el árbol
plot(modelo_arbol)
```

Este árbol de decisión intentará predecir la especie de iris basándose en las medidas de los sépalos y pétalos.

Evaluemos el modelo:

```R
# Hacer predicciones en el conjunto de prueba
predicciones <- predict(modelo_arbol, newdata = prueba)

# Crear una tabla de confusión
tabla_confusion <- table(predicciones, prueba$Species)
print(tabla_confusion)

# Calcular la precisión
precision <- sum(diag(tabla_confusion)) / sum(tabla_confusion)
print(paste("Precisión:", round(precision, 3)))
```

Finalmente, podemos usar el modelo para hacer predicciones sobre nuevas flores:

```R
# Crear un nuevo dato
nueva_flor <- data.frame(
  Sepal.Length = 5.1,
  Sepal.Width = 3.5,
  Petal.Length = 1.4,
  Petal.Width = 0.2
)

# Hacer una predicción
prediccion <- predict(modelo_arbol, newdata = nueva_flor)
print(paste("La flor probablemente es de la especie:", prediccion))
```

Este ejemplo muestra cómo:
1. Preparar los datos dividiendo en conjuntos de entrenamiento y prueba.
2. Crear un árbol de decisión para clasificar especies de iris.
3. Visualizar el árbol.
4. Evaluar el rendimiento del modelo en datos de prueba.
5. Usar el modelo para hacer predicciones sobre nuevos datos.

El conjunto de datos iris es ideal para este tipo de ejemplo porque tiene una variable categórica para predecir (Species) y varias variables numéricas como predictores (longitud y ancho de sépalos y pétalos).

### RANDOM FOREST:

Propósito: Mejorar la precisión y reducir el sobreajuste mediante la creación de múltiples árboles de decisión.
Uso: Para problemas de clasificación y regresión complejos con muchas variables.

```R
modelo_forest <- randomForest(variable_de_respuesta ~ ., data = entrenamiento)
```

Se diferencia del árbol de decisión por:

- Complejidad: Los árboles de decisión son más simples y fáciles de interpretar, mientras que Random Forest es más complejo pero generalmente más preciso.
- Robustez: Random Forest es más robusto al ruido y menos propenso al sobreajuste.
- Interpretabilidad: Los árboles de decisión individuales son más fáciles de interpretar visualmente.

#### EJEMPLO PRACTICO DE RANDOM FOREST:

Por supuesto. Vamos a crear un ejemplo práctico de Random Forest utilizando el conjunto de datos "Boston" de la librería MASS, que contiene información sobre los precios de las viviendas en Boston. Usaremos Random Forest para predecir el precio medio de las casas.

Primero, configuremos nuestro entorno y preparemos los datos:

```R
# Cargar las librerías necesarias
library(randomForest)
library(MASS)
library(caTools)  # Para dividir los datos

# Cargar el conjunto de datos
data(Boston)

# Dividir los datos en conjuntos de entrenamiento y prueba
set.seed(123)  # Para reproducibilidad
split <- sample.split(Boston$medv, SplitRatio = 0.7)
entrenamiento <- subset(Boston, split == TRUE)
prueba <- subset(Boston, split == FALSE)
```

Ahora, creemos nuestro modelo de Random Forest:

```R
# Crear el modelo de Random Forest
modelo_rf <- randomForest(medv ~ ., data = entrenamiento, ntree = 500, importance = TRUE)

# Imprimir un resumen del modelo
print(modelo_rf)
```

Evaluemos el rendimiento del modelo:

```R
# Hacer predicciones en el conjunto de prueba
predicciones <- predict(modelo_rf, newdata = prueba)

# Calcular el Error Cuadrático Medio (MSE)
mse <- mean((predicciones - prueba$medv)^2)
print(paste("Error Cuadrático Medio:", round(mse, 2)))

# Calcular el R-cuadrado
r_squared <- 1 - sum((prueba$medv - predicciones)^2) / sum((prueba$medv - mean(prueba$medv))^2)
print(paste("R-cuadrado:", round(r_squared, 3)))
```

Veamos la importancia de las variables:

```R
# Mostrar la importancia de las variables
importance(modelo_rf)

# Graficar la importancia de las variables
varImpPlot(modelo_rf)
```

Finalmente, hagamos una predicción para una nueva casa:

```R
# Crear datos para una nueva casa
nueva_casa <- data.frame(
  crim = 0.05, zn = 0, indus = 10, chas = 0, nox = 0.5,
  rm = 6, age = 50, dis = 5, rad = 5, tax = 300,
  ptratio = 15, black = 390, lstat = 10
)

# Hacer una predicción
prediccion_nueva <- predict(modelo_rf, newdata = nueva_casa)
print(paste("El precio estimado de la nueva casa es:", round(prediccion_nueva, 2)))
```

Este ejemplo muestra cómo:

1. Preparar los datos dividiéndolos en conjuntos de entrenamiento y prueba.
2. Crear un modelo de Random Forest para predecir los precios de las casas.
3. Evaluar el rendimiento del modelo usando MSE y R-cuadrado.
4. Examinar la importancia de las variables en el modelo.
5. Usar el modelo para hacer predicciones sobre nuevos datos.

El Random Forest es especialmente útil en este caso porque puede manejar relaciones no lineales y capturar interacciones complejas entre las variables, lo que es común en datos de precios de viviendas. Además, proporciona una medida de la importancia de las variables, lo que puede ser valioso para entender qué factores influyen más en los precios de las casas.
### CONTRASTE ENTRE AMBOS ARBOLES:

Para contrastar el Random Forest con el árbol de decisión, podrías seguir estos pasos:

1. Crear ambos modelos:

```R
library(party)
library(randomForest)

# Árbol de decisión
modelo_arbol <- ctree(variable_de_respuesta ~ ., data = entrenamiento)

# Random Forest
modelo_forest <- randomForest(variable_de_respuesta ~ ., data = entrenamiento)
```

2. Hacer predicciones con ambos modelos en el conjunto de prueba:

```R
# Predicciones del árbol de decisión
predicciones_arbol <- predict(modelo_arbol, newdata = prueba)

# Predicciones del Random Forest
predicciones_forest <- predict(modelo_forest, newdata = prueba)
```

3. Evaluar y comparar el rendimiento:

```R
# Para clasificación:
tabla_confusion_arbol <- table(predicciones_arbol, prueba$variable_de_respuesta)
precision_arbol <- sum(diag(tabla_confusion_arbol)) / sum(tabla_confusion_arbol)

tabla_confusion_forest <- table(predicciones_forest, prueba$variable_de_respuesta)
precision_forest <- sum(diag(tabla_confusion_forest)) / sum(tabla_confusion_forest)

print(paste("Precisión del árbol de decisión:", round(precision_arbol, 3)))
print(paste("Precisión del Random Forest:", round(precision_forest, 3)))

# Para regresión:
mse_arbol <- mean((predicciones_arbol - prueba$variable_de_respuesta)^2)
mse_forest <- mean((predicciones_forest - prueba$variable_de_respuesta)^2)

print(paste("MSE del árbol de decisión:", round(mse_arbol, 3)))
print(paste("MSE del Random Forest:", round(mse_forest, 3)))
```

4. Comparar la importancia de las variables:

```R
# Para el árbol de decisión
plot(modelo_arbol)

# Para el Random Forest
varImpPlot(modelo_forest)
```

5. Comparar el tiempo de ejecución y la complejidad:

```R
tiempo_arbol <- system.time(ctree(variable_de_respuesta ~ ., data = entrenamiento))
tiempo_forest <- system.time(randomForest(variable_de_respuesta ~ ., data = entrenamiento))

print(paste("Tiempo de ejecución del árbol de decisión:", tiempo_arbol[3], "segundos"))
print(paste("Tiempo de ejecución del Random Forest:", tiempo_forest[3], "segundos"))
```

Estos pasos te permitirán contrastar de manera efectiva el rendimiento, la interpretabilidad y la eficiencia computacional de ambos modelos. 

Recuerda que el Random Forest generalmente ofrece mejor rendimiento y es menos propenso al sobreajuste, pero a costa de una menor interpretabilidad en comparación con un único árbol de decisión.

### VARIABLES DEPENDIENTE E INDEPENDIENTE:

1. Variable Dependiente:
   - También conocida como variable de respuesta o variable objetivo.
   - Es la variable que estamos tratando de predecir o explicar.
   - Por convención, en un grafico va en el eje Y.
   - En la fórmula de R, aparece a la izquierda del símbolo '~'.
   - Ejemplo: En 'mpg ~ .', 'mpg' es la variable dependiente.

2. Variables Independientes:
   - También conocidas como variables predictoras o características.
   - Son las variables que usamos para predecir o explicar la variable dependiente.
   - Por convención, en un grafico va en el eje X.
   - En la fórmula de R, aparecen a la derecha del símbolo '~'.
   - Ejemplo: En 'mpg ~ cyl + disp + hp', 'cyl', 'disp' y 'hp' son variables independientes.

En el contexto de árboles de decisión y Random Forest:

```R
modelo_arbol <- ctree(variable_dependiente ~ variables_independientes, data = entrenamiento)
modelo_forest <- randomForest(variable_dependiente ~ variables_independientes, data = entrenamiento)
```

- La variable dependiente es lo que el modelo intenta predecir.
- Las variables independientes son las características que el modelo usa para hacer la predicción.

Ejemplos prácticos:

1. Predicción de precios de casas:
   - Variable dependiente: precio
   - Variables independientes: tamaño, ubicación, número de habitaciones, etc.

2. Clasificación de especies de flores (como en el conjunto de datos iris):
   - Variable dependiente: especie
   - Variables independientes: longitud y ancho de sépalos y pétalos

3. Predicción de ingreso anual:
   - Variable dependiente: ingreso
   - Variables independientes: edad, educación, experiencia laboral, etc.

Es importante entender esta distinción porque:
- Ayuda a formular correctamente el problema de predicción o clasificación.
- Influye en cómo interpretamos los resultados del modelo.
- Guía la selección de variables y la ingeniería de características.

En R, el uso de '.' en la fórmula (como en 'variable_dependiente ~ .') es una forma conveniente de incluir todas las demás variables del conjunto de datos como variables independientes.

### CURVAS ROC y AUC:

**ROC (Receiver Operating Characteristic)**: Es una curva que muestra el rendimiento de un modelo de clasificación binaria. Representa la tasa de verdaderos positivos (True Positive Rate, TPR) frente a la tasa de falsos positivos (False Positive Rate, FPR) a diferentes umbrales de clasificación.

**AUC (Area Under the Curve)**: Es el área bajo la curva ROC. Mide la capacidad del modelo para distinguir entre clases. Un AUC de 1 indica un modelo perfecto, mientras que un AUC de 0.5 indica un modelo que no es mejor que el azar.

```R
# Crear la curva ROC 
roc_curve <- roc(true_labels, predicted_probabilities)

# Plotear la curva ROC 
plot(roc_curve)

# Calcular el 
AUC auc(roc_curve)
```

Paso a paso:

1. Tener un vector de respuestas reales (0 y 1).
2. Tener un vector de predicciones (probabilidades).
3. Crear el objeto ROC.
4. Graficar la curva ROC.
5. Calcular el AUC.
#### CREACION DE LOS VECTORES:

1. ¿Por qué necesitamos estos vectores?

Los vectores de respuestas reales y predicciones son esenciales para evaluar el rendimiento de un modelo de clasificación:

- El vector de respuestas reales contiene los valores verdaderos o etiquetas conocidas de tus datos.
- El vector de predicciones contiene las probabilidades o puntuaciones que tu modelo asigna a cada observación.

Estos vectores son necesarios para comparar lo que el modelo predice con lo que realmente ocurre, permitiéndonos evaluar qué tan bien funciona el modelo.

2. Sintaxis para crear estos vectores

La sintaxis para crear estos vectores depende de tu situación específica:

a) Si ya tienes un conjunto de datos etiquetado:

```R
# Asumiendo que tienes un dataframe 'datos' con una columna 'etiqueta'
respuestas_reales <- datos$etiqueta
```

b) Si estás usando mtcars como en nuestro ejemplo:

```R
respuestas_reales <- mtcars$am
```

c) Para crear el vector de predicciones, normalmente usas tu modelo para generar probabilidades:

```R
# Asumiendo que ya has creado tu modelo
predicciones <- predict(modelo, type = "response")
```

d) Si quieres crear vectores de ejemplo para practicar:

```R
# Crear un vector de respuestas reales de ejemplo
set.seed(123)  # Para reproducibilidad
respuestas_reales <- sample(c(0, 1), 100, replace = TRUE)

# Crear un vector de predicciones de ejemplo (probabilidades)
predicciones <- runif(100)  # Genera 100 números aleatorios entre 0 y 1
```

En el contexto de nuestro ejemplo con mtcars:

```R
# Respuestas reales
respuestas_reales <- mtcars$am

# Crear el modelo
modelo <- glm(am ~ hp + wt, data = mtcars, family = binomial)

# Generar predicciones
predicciones <- predict(modelo, type = "response")

# Ahora puedes usar estos vectores para la curva ROC
roc_obj <- roc(respuestas_reales, predicciones)
```

En este caso, `mtcars$am` es nuestro vector de respuestas reales, y `predict(modelo, type = "response")` genera nuestro vector de predicciones (probabilidades).

Estos vectores son la base para calcular la curva ROC y el AUC, ya que permiten comparar las predicciones del modelo con los valores reales, evaluando así el rendimiento del modelo en diferentes umbrales de clasificación.

#### GENERALIZED MODEL LINEAL (GLM)

 GLM significa "Generalized Linear Model" (Modelo Lineal Generalizado). Es una extensión flexible de la regresión lineal ordinaria que permite variables de respuesta que tienen distribuciones de error diferentes a la distribución normal.

Aspectos clave de GLM:

1. Función:
   En R, `glm()` es la función para ajustar modelos lineales generalizados.

2. Sintaxis básica:
   ```R
   glm(formula, family = familia_distribución, data = datos)
   ```

3. Parámetros principales:
   - `formula`: Especifica la relación entre la variable respuesta y las variables predictoras.
   - `family`: Especifica la distribución de la variable respuesta y la función de enlace.
   - `data`: El conjunto de datos a utilizar.

4. Uso común:
   GLM se usa frecuentemente para:
   - Regresión logística (para variables de respuesta binarias)
   - Regresión de Poisson (para datos de conteo)
   - Otros tipos de regresión con diferentes distribuciones de error

5. En nuestro ejemplo con mtcars:
   ```R
   modelo <- glm(am ~ hp + wt, family = binomial, data = mtcars)
   ```
   - `am` es la variable respuesta (transmisión: automática o manual)
   - `hp` y `wt` son las variables predictoras (caballos de fuerza y peso)
   - `family = binomial` especifica que estamos haciendo una regresión logística (para respuesta binaria)

6. Ventajas:
   - Flexibilidad para manejar diferentes tipos de variables de respuesta
   - Puede modelar relaciones no lineales entre la variable respuesta y las predictoras
   - Proporciona un marco unificado para muchos tipos comunes de modelos estadísticos

GLM es crucial en nuestro ejemplo porque nos permite crear un modelo predictivo que genera probabilidades. Estas probabilidades son las que usamos luego para la curva ROC y la matriz de confusión.

### MATRIZ DE CONFUSIÓN 

Una matriz de confusión es una tabla que se utiliza para describir el rendimiento de un modelo de clasificación en un conjunto de datos de prueba para los que se conocen los valores verdaderos.

```R
tabla <- table(Predicción = predicciones_clase, Real = respuesta_real)
print(tabla)
```

#### CREACION DE VECTORES DE RESPUESTAS REALES Y DE PREDICCION

1. Uso de los vectores en la matriz de confusión:

La matriz de confusión compara las predicciones de tu modelo con los valores reales. Por eso necesitamos dos vectores:

a) Vector de respuestas reales: Contiene los valores verdaderos o etiquetas conocidas de tus datos.
b) Vector de predicciones: Contiene las clasificaciones que tu modelo ha hecho.

Estos vectores nos permiten ver cuántas veces el modelo acertó y cuántas se equivocó en sus predicciones.

2. Sintaxis para crear y usar estos vectores:

a) Vector de respuestas reales:
```R
respuestas_reales <- mtcars$am
```
Este vector ya existe en tus datos originales.

b) Vector de predicciones:
Primero, obtenemos probabilidades del modelo:
```R
probabilidades <- predict(modelo, type = "response")
```
Luego, convertimos estas probabilidades en clases (0 o 1):
```R
predicciones <- ifelse(probabilidades > 0.5, 1, 0)
```

3. Creación de la matriz de confusión:
```R
matriz_confusion <- table(Predicción = predicciones, Real = respuestas_reales)
```

4. Visualización de la matriz:
```R
print(matriz_confusion)
```

#### EJEMPLO DE MATRIZ DE CONFUSION:

```R
# Cargar datos
data(mtcars)

# Crear modelo
modelo <- glm(am ~ hp + wt, data = mtcars, family = binomial)

# Vector de respuestas reales
respuestas_reales <- mtcars$am

# Vector de predicciones
probabilidades <- predict(modelo, type = "response")
predicciones <- ifelse(probabilidades > 0.5, 1, 0)

# Crear matriz de confusión
matriz_confusion <- table(Predicción = predicciones, Real = respuestas_reales)

# Mostrar matriz
print(matriz_confusion)
```

La matriz resultante te mostrará:
- Verdaderos Negativos (VN): Predicción 0, Real 0
- Falsos Positivos (FP): Predicción 1, Real 0
- Falsos Negativos (FN): Predicción 0, Real 1
- Verdaderos Positivos (VP): Predicción 1, Real 1

Esta comparación te permite evaluar el rendimiento de tu modelo de clasificación, mostrando cuántas veces acertó y cuántas se equivocó en cada categoría.

#### MÉTRICAS EN LA MATRIZ DE CONFUSIÓN:

 Vamos a desglosar cada una de estas métricas, su significado, sintaxis y su relación con la matriz de confusión.

1. Precisión (Precision):
   - Qué hace: Mide la proporción de predicciones positivas correctas entre todas las predicciones positivas.
   - Fórmula: $VP / (VP + FP)$
   
```R
precision <- matriz_confusion[2,2] / sum(matriz_confusion[2,])
```

2. Recall (también llamado Sensibilidad o Tasa de Verdaderos Positivos):
   - Qué hace: Mide la proporción de positivos reales que fueron identificados correctamente.
   - Fórmula: $VP / (VP + FN)$

```R
recall <- matriz_confusion[2,2] / sum(matriz_confusion[,2])
```

3. F1-Score:
   - Qué hace: Es la media armónica de precisión y recall, proporcionando un único valor que balancea ambas métricas.
   - Fórmula: $2 * (Precisión * Recall) / (Precisión + Recall)$

```R
f1_score <- 2 * (precision * recall) / (precision + recall)
```

Estas métricas no son parte de la matriz de confusión en sí, pero se calculan a partir de ella. Son métricas derivadas que nos ayudan a interpretar los resultados de la matriz de confusión.

Otras métricas que pueden calcularse a partir de la matriz de confusión incluyen:

4. Exactitud (Accuracy):
   - Qué hace: Mide la proporción total de predicciones correctas.
   - Fórmula: $(VP + VN) / (VP + VN + FP + FN)$
   
```R
accuracy <- sum(diag(matriz_confusion)) / sum(matriz_confusion)
```

5. Especificidad:
   - Qué hace: Mide la proporción de negativos reales que fueron identificados correctamente.
   - Fórmula: $VN / (VN + FP)$
   
```R
especificidad <- matriz_confusion[1,1] / sum(matriz_confusion[,1])
```

6. Tasa de Falsos Positivos:
   - Qué hace: Mide la proporción de negativos reales que fueron incorrectamente clasificados como positivos.
   - Fórmula: $FP / (FP + VN)$
   
```R
tasa_falsos_positivos <- matriz_confusion[2,1] / sum(matriz_confusion[,1])
```

Ejemplo completo incluyendo todas estas métricas:

```R
# Asumiendo que ya tienes tu matriz_confusion

# Calcular métricas
precision <- matriz_confusion[2,2] / sum(matriz_confusion[2,])
recall <- matriz_confusion[2,2] / sum(matriz_confusion[,2])
f1_score <- 2 * (precision * recall) / (precision + recall)
accuracy <- sum(diag(matriz_confusion)) / sum(matriz_confusion)
especificidad <- matriz_confusion[1,1] / sum(matriz_confusion[,1])
tasa_falsos_positivos <- matriz_confusion[2,1] / sum(matriz_confusion[,1])

# Imprimir resultados
cat("Precisión:", round(precision, 3), "\n")
cat("Recall:", round(recall, 3), "\n")
cat("F1-Score:", round(f1_score, 3), "\n")
cat("Exactitud:", round(accuracy, 3), "\n")
cat("Especificidad:", round(especificidad, 3), "\n")
cat("Tasa de Falsos Positivos:", round(tasa_falsos_positivos, 3), "\n")
```

Estas métricas te dan una visión completa del rendimiento de tu modelo de clasificación, cada una enfocándose en diferentes aspectos de su desempeño.

### EJEMPLO PRACTICO DE ROC CON MATRIZ DE CONFUSION 

 Este ejemplo cubrirá la creación del modelo, la curva ROC, la matriz de confusión y las métricas derivadas.

```R
# Cargar las librerías necesarias
library(pROC)

# Cargar los datos
data(mtcars)

# 1. Crear un modelo logístico
# Predeciremos si un coche tiene transmisión automática (am = 1) o manual (am = 0)
# basándonos en los caballos de fuerza (hp) y el peso (wt)
modelo <- glm(am ~ hp + wt, data = mtcars, family = binomial)

# 2. Generar predicciones (probabilidades)
predicciones_prob <- predict(modelo, type = "response")

# 3. Curva ROC y AUC
roc_obj <- roc(mtcars$am, predicciones_prob)
plot(roc_obj, main = "Curva ROC para predicción de transmisión")
auc_valor <- auc(roc_obj)
print(paste("AUC:", round(auc_valor, 3)))

# 4. Matriz de Confusión
# Convertir probabilidades a clases usando un umbral de 0.5
predicciones_clase <- ifelse(predicciones_prob > 0.5, 1, 0)

# Crear la matriz de confusión
matriz_confusion <- table(Predicción = predicciones_clase, Real = mtcars$am)

# Mostrar la matriz de confusión
print("Matriz de Confusión:")
print(matriz_confusion)

# 5. Calcular métricas
precision <- matriz_confusion[2,2] / sum(matriz_confusion[2,])
recall <- matriz_confusion[2,2] / sum(matriz_confusion[,2])
f1_score <- 2 * (precision * recall) / (precision + recall)
accuracy <- sum(diag(matriz_confusion)) / sum(matriz_confusion)
especificidad <- matriz_confusion[1,1] / sum(matriz_confusion[,1])
tasa_falsos_positivos <- matriz_confusion[2,1] / sum(matriz_confusion[,1])

# 6. Imprimir resultados
cat("\nMétricas de rendimiento del modelo:\n")
cat("Precisión:", round(precision, 3), "\n")
cat("Recall:", round(recall, 3), "\n")
cat("F1-Score:", round(f1_score, 3), "\n")
cat("Exactitud:", round(accuracy, 3), "\n")
cat("Especificidad:", round(especificidad, 3), "\n")
cat("Tasa de Falsos Positivos:", round(tasa_falsos_positivos, 3), "\n")

# 7. Bonus: Visualización de las predicciones
plot(mtcars$hp, mtcars$wt, col = mtcars$am + 1, pch = 19,
     main = "Predicciones del modelo",
     xlab = "Caballos de fuerza (hp)", ylab = "Peso (wt)")
legend("topright", legend = c("Manual", "Automático"), col = 1:2, pch = 19)
points(mtcars$hp, mtcars$wt, col = predicciones_clase + 3, pch = 1, cex = 2)
```

Explicación paso a paso:

1. Creamos un modelo logístico para predecir la transmisión (am) basándonos en los caballos de fuerza (hp) y el peso (wt).

2. Generamos predicciones de probabilidad para cada coche en el dataset.

3. Creamos la curva ROC y calculamos el AUC. Esto nos da una medida de qué tan bien el modelo distingue entre las dos clases.

4. Creamos la matriz de confusión convirtiendo primero las probabilidades en clases (0 o 1) y luego comparándolas con los valores reales.

5. Calculamos varias métricas de rendimiento a partir de la matriz de confusión.

6. Imprimimos estas métricas para una fácil interpretación.

7. Como bonus, añadimos una visualización que muestra cómo el modelo está clasificando los coches. Los puntos sólidos muestran la clasificación real, mientras que los círculos muestran la predicción del modelo.

#### FAMILY Y TYPE:

**family = **

Sí, `family = binomial` se refiere a que la variable de respuesta es binaria (generalmente 0 y 1), pero no se limita solo a esos valores. Puede ser cualquier par de valores que representen dos categorías distintas.

Otros tipos de 'family' comunes incluyen:

- `gaussian`: Para respuestas continuas (regresión lineal normal)
- `poisson`: Para datos de conteo
- `gamma`: Para datos continuos positivos con varianza creciente

Ejemplos:

```R
# Binomial (logística)
glm(am ~ hp + wt, data = mtcars, family = binomial)

# Poisson (para datos de conteo)
glm(cyl ~ hp + wt, data = mtcars, family = poisson)

# Gaussiana (regresión lineal normal)
glm(mpg ~ hp + wt, data = mtcars, family = gaussian)
```

**type = **

En `predict(modelo, type = "response")`, el argumento `type = "response"` indica qué tipo de predicción quieres obtener. 

Los tipos más comunes son:

- `"response"`: Devuelve predicciones en la escala de la variable respuesta.
  - Para regresión logística: probabilidades (entre 0 y 1)
  - Para regresión lineal: valores predichos directamente
  - Para Poisson: conteos predichos

- `"link"`: Devuelve predicciones en la escala del predictor lineal.
  - Para regresión logística: log-odds
  - Para regresión lineal: igual que "response"
  - Para Poisson: logaritmo de los conteos predichos

Ejemplo comparativo:

```R
modelo <- glm(am ~ hp + wt, data = mtcars, family = binomial)

# Predicciones como probabilidades
pred_prob <- predict(modelo, type = "response")
print(head(pred_prob))

# Predicciones como log-odds
pred_logodds <- predict(modelo, type = "link")
print(head(pred_logodds))
```

En resumen:
- `family = binomial` se usa para respuestas binarias/categóricas.
- `type = "response"` te da las predicciones en la escala de tu variable respuesta (probabilidades para regresión logística).

Estos parámetros te permiten adaptar tu modelo y sus predicciones al tipo específico de datos con los que estás trabajando.
