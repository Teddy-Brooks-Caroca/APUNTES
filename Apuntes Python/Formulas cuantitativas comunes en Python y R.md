## 1. Matemáticas Básicas

1. **Número par**
   Fórmula matemática:
   $$n\% 2 = 0$$

   ```python 
   # Python
   def es_par(n):
       return n % 2 == 0
   
   # Ejemplo
   print(es_par(4))  # True
   ```

   ```r
   # R
   es_par <- function(n) {
     return(n %% 2 == 0)
   }
   
   # Ejemplo
   print(es_par(4))  # TRUE
   ```

2. **Valor absoluto**
   Fórmula matemática:  $$|x| = { x si x ≥ 0, -x si x < 0 }$$
   
   ```python
   # Python
   abs_value = abs(-5)
   
   # Ejemplo
   print(abs_value)  # 5
   ```

   ```r
   # R
   abs_value <- abs(-5)
   
   # Ejemplo
   print(abs_value)  # 5
   ```

3. **Redondeo**
   Fórmula matemática: $$round(x) = ⌊x + 0.5⌋$$
   
   ```python
   # Python
   rounded = round(3.7)
   
   # Ejemplo
   print(rounded)  # 4
   ```

   ```r
   # R
   rounded <- round(3.7)
   
   # Ejemplo
   print(rounded)  # 4
   ```

4. **Máximo común divisor**
   Fórmula matemática: $$MCD(a,b) = MCD(b, a mod b)$$
   
   ```python
   # Python
   import math
   
   mcd = math.gcd(24, 36)
   
   # Ejemplo
   print(mcd)  # 12
   ```

   ```r
   # R
   mcd <- function(a, b) {
     while (b != 0) {
       t <- b
       b <- a %% b
       a <- t
     }
     return(a)
   }
   
   # Ejemplo
   print(mcd(24, 36))  # 12
   ```

5. **Mínimo común múltiplo**
   Fórmula matemática: $$MCM(a,b) = |a * b| / MCD(a,b)$$
   ```python
   # Python
   import math
   
   def mcm(a, b):
       return abs(a*b) // math.gcd(a, b)
   
   # Ejemplo
   print(mcm(4, 6))  # 12
   ```

   ```r
   # R
   mcm <- function(a, b) {
     return(abs(a*b) %/% mcd(a, b))
   }
   
   # Ejemplo
   print(mcm(4, 6))  # 12
   ```

6. **Factorial**
   Fórmula matemática:$$ n! = n × (n-1) × (n-2) × ... × 2 × 1$$
   ```python
   # Python
   import math
   
   fact = math.factorial(5)
   
   # Ejemplo
   print(fact)  # 120
   ```

   ```r
   # R
   fact <- factorial(5)
   
   # Ejemplo
   print(fact)  # 120
   ```

7. **Potencia**
   Fórmula matemática: $$x^n = x × x × ... × x (n veces)$$
   ```python
   # Python
   power = pow(2, 3)
   
   # Ejemplo
   print(power)  # 8
   ```

   ```r
   # R
   power <- 2^3
   
   # Ejemplo
   print(power)  # 8
   ```

8. **Raíz cuadrada**
   Fórmula matemática: $$√x = y$$ donde: $$y² = x$$
   ```python
   # Python
   import math
   
   sqrt_value = math.sqrt(16)
   
   # Ejemplo
   print(sqrt_value)  # 4.0
   ```

   ```r
   # R
   sqrt_value <- sqrt(16)
   
   # Ejemplo
   print(sqrt_value)  # 4
   ```

9. **Logaritmo natural**
   Fórmula matemática: $$y = ln(x)$$donde: $$e^y = x$$
   ```python
   # Python
   import math
   
   log_value = math.log(10)
   
   # Ejemplo
   print(log_value)  # 2.302585092994046
   ```

   ```r
   # R
   log_value <- log(10)
   
   # Ejemplo
   print(log_value)  # 2.302585
   ```

10. **Logaritmo base 10**
    Fórmula matemática: $$y = log₁₀(x)$$ donde: $$10^y = x$$
    ```python
    # Python
    import math
    
    log10_value = math.log10(100)
    
    # Ejemplo
    print(log10_value)  # 2.0
    ```

	```r
    # R
    log10_value <- log10(100)
    
    # Ejemplo
    print(log10_value)  # 2
    ```

11. **Suma de serie aritmética**
    Fórmula matemática: $$S = n(a₁ + aₙ) / 2$$ 
    `n` es el número de términos 
    `a₁` es el primer término  
    `aₙ` es el último término
    
    ```python
    # Python
    def suma_aritmetica(a1, an, n):
        return n * (a1 + an) / 2
    
    # Ejemplo
    print(suma_aritmetica(1, 100, 100))  # 5050.0
    ```

	```r
    # R
    suma_aritmetica <- function(a1, an, n) {
      return(n * (a1 + an) / 2)
    }
    
    # Ejemplo
    print(suma_aritmetica(1, 100, 100))  # 5050
    ```

12. **Suma de serie geométrica**
    Fórmula matemática: $$S = a(1 - r^n) / (1 - r)$$ 
    `a` es el primer término
    `r` es la razón  
    `n` es el número de términos
    
    ```python
    # Python
    def suma_geometrica(a, r, n):
        if r == 1:
            return a * n
        return a * (1 - r**n) / (1 - r)
    
    # Ejemplo
    print(suma_geometrica(1, 2, 5))  # 31.0
    ```

	```r
    # R
    suma_geometrica <- function(a, r, n) {
      if (r == 1) {
        return(a * n)
      }
      return(a * (1 - r^n) / (1 - r))
    }
    
    # Ejemplo
    print(suma_geometrica(1, 2, 5))  # 31
    ```

13. **Conversión de grados a radianes**
    Fórmula matemática: $$rad = (π/180) × grados$$
    ```python
    # Python
    import math
    
    def grados_a_radianes(grados):
        return grados * (math.pi / 180)
    
    # Ejemplo
    print(grados_a_radianes(180))  # 3.141592653589793
    ```

	```r
    # R
    grados_a_radianes <- function(grados) {
      return(grados * (pi / 180))
    }
    
    # Ejemplo
    print(grados_a_radianes(180))  # 3.141593
    ```

14. **Conversión de radianes a grados**
    Fórmula matemática: $$grados = (180/π) × rad$$
    ```python
    # Python
    import math
    
    def radianes_a_grados(radianes):
        return radianes * (180 / math.pi)
    
    # Ejemplo
    print(radianes_a_grados(math.pi))  # 180.0
    ```

	```r
    # R
    radianes_a_grados <- function(radianes) {
      return(radianes * (180 / pi))
    }
    
    # Ejemplo
    print(radianes_a_grados(pi))  # 180
    ```

15. **Distancia entre dos puntos**
    Fórmula matemática: $$d = √[(x₂ - x₁)² + (y₂ - y₁)²]$$
    ```python
    # Python
    import math
    
    def distancia(x1, y1, x2, y2):
        return math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
    
    # Ejemplo
    print(distancia(0, 0, 3, 4))  # 5.0
    ```

	```r
    # R
    distancia <- function(x1, y1, x2, y2) {
      return(sqrt((x2 - x1)^2 + (y2 - y1)^2))
    }
    
    # Ejemplo
    print(distancia(0, 0, 3, 4))  # 5
    ```

## 2. Geometría

1. **Perímetro de rectángulo**
   Fórmula matemática: $$P = 2(l + a)$$ 
   `l` es la longitud 
   `a` es el ancho
   
   ```python
   # Python
   def perimetro_rectangulo(l, a):
       return 2 * (l + a)
   
   # Ejemplo
   print(perimetro_rectangulo(5, 3))  # 16
   ```

   ```r
   # R
   perimetro_rectangulo <- function(l, a) {
     return(2 * (l + a))
   }
   
   # Ejemplo
   print(perimetro_rectangulo(5, 3))  # 16
   ```

2. **Perímetro de círculo**
   Fórmula matemática: $$P = 2πr$$   `r` es el radio
   
   ```python
   # Python
   import math
   
   def perimetro_circulo(r):
       return 2 * math.pi * r
   
   # Ejemplo
   print(perimetro_circulo(5))  # 31.41592653589793
   ```

   ```r
   # R
   perimetro_circulo <- function(r) {
     return(2 * pi * r)
   }
   
   # Ejemplo
   print(perimetro_circulo(5))  # 31.41593
   ```

3. **Perímetro de triángulo**
   Fórmula matemática: $$P = a + b + c$$  `a`, `b` y `c` son los lados del triángulo
   
   ```python
   # Python
   def perimetro_triangulo(a, b, c):
       return a + b + c
   
   # Ejemplo
   print(perimetro_triangulo(3, 4, 5))  # 12
   ```

   ```r
   # R
   perimetro_triangulo <- function(a, b, c) {
     return(a + b + c)
   }
   
   # Ejemplo
   print(perimetro_triangulo(3, 4, 5))  # 12
   ```

4. **Área de rectángulo**
   Fórmula matemática: $$A = l * a$$  `l` es la longitud 
    `a` es el ancho
    
   ```python
   # Python
   def area_rectangulo(l, a):
       return l * a
   
   # Ejemplo
   print(area_rectangulo(5, 3))  # 15
   ```

   ```r
   # R
   area_rectangulo <- function(l, a) {
     return(l * a)
   }
   
   # Ejemplo
   print(area_rectangulo(5, 3))  # 15
   ```

5. **Área de círculo**
   Fórmula matemática: $$A = πr²$$  `r` es el radio
   
   ```python
   # Python
   import math
   
   def area_circulo(r):
       return math.pi * r**2
   
   # Ejemplo
   print(area_circulo(5))  # 78.53981633974483
   ```

   ```r
   # R
   area_circulo <- function(r) {
     return(pi * r^2)
   }
   
   # Ejemplo
   print(area_circulo(5))  # 78.53982
   ```

6. **Área de triángulo**
   Fórmula matemática: $$A = (b * h) / 2$$  `b` es la base  
    `h` es la altura
    
   ```python
   # Python
   def area_triangulo(b, h):
       return (b * h) / 2
   
   # Ejemplo
   print(area_triangulo(6, 4))  # 12.0
   ```

   ```r
   # R
   area_triangulo <- function(b, h) {
     return((b * h) / 2)
   }
   
   # Ejemplo
   print(area_triangulo(6, 4))  # 12
   ```

7. **Área de hexágono regular**
   Fórmula matemática: $$A = (3√3 * l²) / 2$$  `l` es la longitud del lado
   
   ```python
   # Python
   import math
   
   def area_hexagono(l):
       return (3 * math.sqrt(3) * l**2) / 2
   
   # Ejemplo
   print(area_hexagono(5))  # 64.95190528383289
   ```

   ```r
   # R
   area_hexagono <- function(l) {
     return((3 * sqrt(3) * l^2) / 2)
   }
   
   # Ejemplo
   print(area_hexagono(5))  # 64.95191
   ```

8. **Área de polígono regular**
   Fórmula matemática: $$A = (n * l² * cot(π/n)) / 4$$ `n` es el número de lados 
   `l` es la longitud del lado
   
   ```python
   # Python
   import math
   
   def area_poligono(n, l):
       return (n * l**2) / (4 * math.tan(math.pi / n))
   
   # Ejemplo
   print(area_poligono(6, 5))  # 64.95190528383289
   ```

   ```r
   # R
   area_poligono <- function(n, l) {
     return((n * l^2) / (4 * tan(pi / n)))
   }
   
   # Ejemplo
   print(area_poligono(6, 5))  # 64.95191
   ```

9. **Volumen de esfera**
   Fórmula matemática: $$V = (4/3)πr³$$ `r` es el radio
   
   ```python
   # Python
   import math
   
   def volumen_esfera(r):
       return (4/3) * math.pi * r**3
   
   # Ejemplo
   print(volumen_esfera(5))  # 523.5987755982989
   ```

   ```r
   # R
   volumen_esfera <- function(r) {
     return((4/3) * pi * r^3)
   }
   
   # Ejemplo
   print(volumen_esfera(5))  # 523.5988
   ```

10. **Volumen de cono**
    Fórmula matemática: $$V = (1/3)πr²h$$ 
    `r` es el radio de la base  
    `h` es la altura
    
    ```python
    # Python
    import math
    
    def volumen_cono(r, h):
        return (1/3) * math.pi * r**2 * h
    
    # Ejemplo
    print(volumen_cono(3, 4))  # 37.69911184307752
    ```

	```r
    # R
    volumen_cono <- function(r, h) {
      return((1/3) * pi * r^2 * h)
    }
    
    # Ejemplo
    print(volumen_cono(3, 4))  # 37.69911
    ```

11. **Volumen de cilindro**
    Fórmula matemática: $$V = πr²h$$`r` es el radio de la base  
    `h` es la altura
    
    ```python
    # Python
    import math
    
    def volumen_cilindro(r, h):
        return math.pi * r**2 * h
    
    # Ejemplo
    print(volumen_cilindro(3, 4))  # 113.09733552923255
    ```
    
    ```r
    # R
    volumen_cilindro <- function(r, h) {
      return(pi * r^2 * h)
    }
    
    # Ejemplo
    print(volumen_cilindro(3, 4))  # 113.0973
    ```

12. **Teorema de Pitágoras**
    Fórmula matemática: $$c² = a² + b²$$ `c` es la hipotenusa  
    `a` y `b` son los catetos
    ```python
    # Python
    import math
    
    def hipotenusa(a, b):
        return math.sqrt(a**2 + b**2)
    
    # Ejemplo
    print(hipotenusa(3, 4))  # 5.0
    ```
    
    ```r
    # R
    hipotenusa <- function(a, b) {
      return(sqrt(a^2 + b^2))
    }
    
    # Ejemplo
    print(hipotenusa(3, 4))  # 5
    ```

13. **Área de paralelogramo**
    Fórmula matemática: $$A = b * h$$ `b` es la base 
    `h` es la altura
    
    ```python
    # Python
    def area_paralelogramo(b, h):
        return b * h
    
    # Ejemplo
    print(area_paralelogramo(5, 3))  # 15
    ```
    
    ```r
    # R
    area_paralelogramo <- function(b, h) {
      return(b * h)
    }
    
    # Ejemplo
    print(area_paralelogramo(5, 3))  # 15
    ```

14. **Área de trapecio**
    Fórmula matemática: $$A = ((a + b) / 2) * h$$`a` y `b` son las bases paralelas 
    `h` es la altura
    
    ```python
    # Python
    def area_trapecio(a, b, h):
        return ((a + b) / 2) * h
    
    # Ejemplo
    print(area_trapecio(3, 5, 4))  # 16.0
    ```
    
    ```r
    # R
    area_trapecio <- function(a, b, h) {
      return(((a + b) / 2) * h)
    }
    
    # Ejemplo
    print(area_trapecio(3, 5, 4))  # 16
    ```

15. **Volumen de prisma rectangular**
    Fórmula matemática: $$V = l * a * h$$`l` es la longitud 
    `a` es el ancho  
    `h` es la altura
    
    ```python
    # Python
    def volumen_prisma(l, a, h):
        return l * a * h
    
    # Ejemplo
    print(volumen_prisma(3, 4, 5))  # 60
    ```
    
    ```r
    # R
    volumen_prisma <- function(l, a, h) {
      return(l * a * h)
    }
    
    # Ejemplo
    print(volumen_prisma(3, 4, 5))  # 60
    ```

## 3. Estadística

1. **Media aritmética**
   Fórmula matemática: $$x̄ = (Σx) / n$$`Σx` es la suma de todos los valores  
   `n` es el número de valores
   
   ```python
   # Python
   def media(datos):
       return sum(datos) / len(datos)
   
   # Ejemplo
   print(media([1, 2, 3, 4, 5]))  # 3.0
   ```
   
   ```r
   # R
   media <- function(datos) {
     return(mean(datos))
   }
   
   # Ejemplo
   print(media(c(1, 2, 3, 4, 5)))  # 3
   ```

2. **Mediana**
   Fórmula matemática: El valor central cuando los datos están ordenados
   ```python
   # Python
   import statistics
   
   def mediana(datos):
       return statistics.median(datos)
   
   # Ejemplo
   print(mediana([1, 3, 3, 6, 7, 8, 9]))  # 6
   ```
   
   ```r
   # R
   mediana <- function(datos) {
     return(median(datos))
   }
   
   # Ejemplo
   print(mediana(c(1, 3, 3, 6, 7, 8, 9)))  # 6
   ```

3. **Varianza**
   Fórmula matemática: $$σ² = Σ(x - μ)² / n$$`x` son los valores individuales 
   `μ` es la media 
   `n` es el número de valores
   
   ```python
   # Python
   import statistics
   
   def varianza(datos):
       return statistics.variance(datos)
   
   # Ejemplo
   print(varianza([1, 2, 3, 4, 5]))  # 2.0
   ```
   
   ```r
   # R
   varianza <- function(datos) {
     return(var(datos))
   }
   
   # Ejemplo
   print(varianza(c(1, 2, 3, 4, 5)))  # 2.5
   ```

4. **Desviación estándar**
   Fórmula matemática: $$σ = √σ²$$`σ²` es la varianza
   
   ```python
   # Python
   import statistics
   
   def desviacion_estandar(datos):
       return statistics.stdev(datos)
   
   # Ejemplo
   print(desviacion_estandar([1, 2, 3, 4, 5]))  # 1.4142135623730951
   ```
   
   ```r
   # R
   desviacion_estandar <- function(datos) {
     return(sd(datos))
   }
   
   # Ejemplo
   print(desviacion_estandar(c(1, 2, 3, 4, 5)))  # 1.581139
   ```

5. **Coeficiente de variación**
   Fórmula matemática: $$CV = (σ / μ) * 100$$`σ` es la desviación estándar 
   `μ` es la media
   
   ```python
   # Python
   import statistics
   
   def coeficiente_variacion(datos):
       return (statistics.stdev(datos) / statistics.mean(datos)) * 100
   
   # Ejemplo
   print(coeficiente_variacion([1, 2, 3, 4, 5]))  # 47.14045207910317
   ```
   
   ```r
   # R
   coeficiente_variacion <- function(datos) {
     return((sd(datos) / mean(datos)) * 100)
   }
   
   # Ejemplo
   print(coeficiente_variacion(c(1, 2, 3, 4, 5)))  # 52.70462
   ```

6. **Covarianza**
   Fórmula matemática: $$cov(X,Y) = Σ((x - μx)(y - μy)) / n$$`μx` y `μy` son las medias de `X` e `Y` respectivamente
   
   ```python
   # Python
   import numpy as np
   
   def covarianza(x, y):
       return np.cov(x, y)[0][1]
   
   # Ejemplo
   print(covarianza([1, 2, 3, 4, 5], [2, 4, 5, 4, 5]))  # 1.5
   ```
   
   ```r
   # R
   covarianza <- function(x, y) {
     return(cov(x, y))
   }
   
   # Ejemplo
   print(covarianza(c(1, 2, 3, 4, 5), c(2, 4, 5, 4, 5)))  # 1.5
   ```

7. **Coeficiente de correlación de Pearson**
   Fórmula matemática: $$r = cov(X,Y) / (σx * σy)$$
   `cov(X,Y)` es la covarianza 
   `σx` y `σy` son las desviaciones estándar de `X` e `Y`
   
   ```python
   # Python
   import numpy as np
   
   def correlacion(x, y):
       return np.corrcoef(x, y)[0, 1]
   
   # Ejemplo
   print(correlacion([1, 2, 3, 4, 5], [2, 4, 5, 4, 5]))  # 0.8717797887081348
   ```
   
   ```r
   # R
   correlacion <- function(x, y) {
     return(cor(x, y))
   }
   
   # Ejemplo
   print(correlacion(c(1, 2, 3, 4, 5), c(2, 4, 5, 4, 5)))  # 0.8717798
   ```

8. **Regresión lineal simple**
   Fórmula matemática: $$y = mx + b$$`m` es la pendiente  
   `b` es la intersección con el eje `y`
   
   ```python
   # Python
   import numpy as np
   
   def regresion_lineal(x, y):
       m, b = np.polyfit(x, y, 1)
       return m, b
   
   # Ejemplo
   x = [1, 2, 3, 4, 5]
   y = [2, 4, 5, 4, 5]
   m, b = regresion_lineal(x, y)
   print(f"y = {m}x + {b}")  # y = 0.6x + 2.2
   ```
   
   ```r
   # R
   regresion_lineal <- function(x, y) {
     modelo <- lm(y ~ x)
     return(coef(modelo))
   }
   
   # Ejemplo
   x <- c(1, 2, 3, 4, 5)
   y <- c(2, 4, 5, 4, 5)
   coeficientes <- regresion_lineal(x, y)
   print(paste("y =", coeficientes[2], "x +", coeficientes[1]))  # y = 0.6 x + 2.2
   ```

9. **Error estándar de la media**
   Fórmula matemática: $$SE = σ / √n$$`σ` es la desviación estándar 
   `n` es el tamaño de la muestra
   
   ```python
   # Python
   import statistics
   import math
   
   def error_estandar(datos):
       return statistics.stdev(datos) / math.sqrt(len(datos))
   
   # Ejemplo
   print(error_estandar([1, 2, 3, 4, 5]))  # 0.6324555320336759
   ```
   
   ```r
   # R
   error_estandar <- function(datos) {
     return(sd(datos) / sqrt(length(datos)))
   }
   
   # Ejemplo
   print(error_estandar(c(1, 2, 3, 4, 5)))  # 0.7071068
   ```

10. **Intervalo de confianza para la media**
    Fórmula matemática: $$IC = x̄ ± (t * (σ / √n))$$`t` es el valor crítico de la distribución `t de Student`
     
    ```python
    # Python
    import scipy.stats as stats
    import numpy as np
    
    def intervalo_confianza(datos, nivel_confianza=0.95):
        n = len(datos)
        media = np.mean(datos)
        error_estandar = stats.sem(datos)
        t = stats.t.ppf((1 + nivel_confianza) / 2, n - 1)
        margen_error = t * error_estandar
        return (media - margen_error, media + margen_error)
    
    # Ejemplo
    print(intervalo_confianza([1, 2, 3, 4, 5]))  # (1.2414, 4.7586)
    ```
    
    ```r
    # R
    intervalo_confianza <- function(datos, nivel_confianza=0.95) {
      t.test(datos, conf.level = nivel_confianza)$conf.int
    }
    
    # Ejemplo
    print(intervalo_confianza(c(1, 2, 3, 4, 5)))  # 1.241434 4.758566
    ```

11. **Prueba t de Student**
    Fórmula matemática: $$t = (x̄ - μ) / (s / √n)$$ `x̄` es la media muestral 
    `μ` es la media poblacional 
    `s` es la desviación estándar muestral  
    `n` es el tamaño de la muestra
    
    ```python
    # Python
    import scipy.stats as stats
    
    def prueba_t(datos, media_poblacional):
        t_stat, p_value = stats.ttest_1samp(datos, media_poblacional)
        return t_stat, p_value
    
    # Ejemplo
    print(prueba_t([1, 2, 3, 4, 5], 2.5))  # (1.2649110640673518, 0.2752192360274093)
    ```
    
    ```r
    # R
    prueba_t <- function(datos, media_poblacional) {
      resultado <- t.test(datos, mu = media_poblacional)
      return(c(t_stat = resultado$statistic, p_value = resultado$p.value))
    }
    
    # Ejemplo
    print(prueba_t(c(1, 2, 3, 4, 5), 2.5))  # t 1.2649111 p_value 0.2752192
    ```

12. **Chi-cuadrado**
    Fórmula matemática: $$χ² = Σ((O - E)² / E)$$
    `O` son las frecuencias observadas  
    `E` son las frecuencias esperadas
    
    ```python
    # Python
    import scipy.stats as stats
    
    def chi_cuadrado(observado, esperado):
        chi2, p_value = stats.chisquare(observado, esperado)
        return chi2, p_value
    
    # Ejemplo
    print(chi_cuadrado([16, 18, 16, 14, 12, 12], [16, 16, 16, 16, 16, 8]))  
    # (3.5, 0.6234898018587335)
    ```
    
    ```r
    # R
    chi_cuadrado <- function(observado, esperado) {
      resultado <- chisq.test(observado, p = esperado/sum(esperado))
      return(c(chi2 = resultado$statistic, p_value = resultado$p.value))
    }
    
    # Ejemplo
    print(chi_cuadrado(c(16, 18, 16, 14, 12, 12), c(16, 16, 16, 16, 16, 8)))  # X-squared 3.5 p-value 0.6234898
    ```

13. **Coeficiente de determinación (R²)**
    Fórmula matemática: $$R² = 1 - (SSres / SStot)$$ 
    `SSres` es la suma de los cuadrados de los residuos y 
    `SStot` es la suma total de los cuadrados
    
    ```python
    # Python
    from sklearn.metrics import r2_score
    
    def r_cuadrado(y_true, y_pred):
        return r2_score(y_true, y_pred)
    
    # Ejemplo
    y_true = [3, 5, 7, 9, 11]
    y_pred = [2.5, 4.8, 7.2, 9.5, 11.2]
    print(r_cuadrado(y_true, y_pred))  # 0.9870013605442177
    ```
    
    ```r
    # R
    r_cuadrado <- function(y_true, y_pred) {
      return(1 - sum((y_true - y_pred)^2) / sum((y_true - mean(y_true))^2))
    }
    
    # Ejemplo
    y_true <- c(3, 5, 7, 9, 11)
    y_pred <- c(2.5, 4.8, 7.2, 9.5, 11.2)
    print(r_cuadrado(y_true, y_pred))  # 0.9870014
    ```

14. **Coeficiente de asimetría (Skewness)**
    Fórmula matemática: $$g1 = m3 / (m2^(3/2))$$ `m3` es el tercer momento central 
    `m2` es el segundo momento central (varianza)
    
    ```python
    # Python
    import scipy.stats as stats
    
    def asimetria(datos):
        return stats.skew(datos)
    
    # Ejemplo
    print(asimetria([2, 8, 0, 4, 1, 9, 9, 0]))  # 0.3265308888575352
    ```
    ```r
    # R
    library(e1071)
    
    asimetria <- function(datos) {
      return(skewness(datos))
    }
    
    # Ejemplo
    print(asimetria(c(2, 8, 0, 4, 1, 9, 9, 0)))  # 0.3265309
    ```

15. **Curtosis**
    Fórmula matemática: $$g2 = (m4 / m2^2) - 3$$`m4` es el cuarto momento central 
    `m2` es el segundo momento central (varianza)
    
    ```python
    # Python
    import scipy.stats as stats
    
    def curtosis(datos):
        return stats.kurtosis(datos)
    
    # Ejemplo
    print(curtosis([2, 8, 0, 4, 1, 9, 9, 0]))  # -1.0258550018600711
    ```
    
    ```r
    # R
    library(e1071)
    
    curtosis <- function(datos) {
      return(kurtosis(datos))
    }
    
    # Ejemplo
    print(curtosis(c(2, 8, 0, 4, 1, 9, 9, 0)))  # -1.025855
    ```
    
16. **Curva Cuadrática**
    Fórmula matemática: $$y = ax² + bx + c$$
```python
# Python
def cuadratica(x, a, b, c):
    return a * x**2 + b * x + c

# Ejemplo
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-5, 5, 100)
y = cuadratica(x, 1, 0, 0)  # a = 1, b = 0, c = 0

plt.plot(x, y)
plt.title('Curva Cuadrática')
plt.show()
```

```r
# R
cuadratica <- function(x, a, b, c) {
  a * x^2 + b * x + c
}

# Ejemplo
x <- seq(-5, 5, length.out = 100)
y <- cuadratica(x, 1, 0, 0)  # a = 1, b = 0, c = 0

plot(x, y, type = "l", main = "Curva Cuadrática")
```

17. **Curva Logarítmica**
    Fórmula matemática: $$y = a log(x) + b$$

```python
# Python
import numpy as np

def logaritmica(x, a, b):
    return a * np.log(x) + b

# Ejemplo
import matplotlib.pyplot as plt

x = np.linspace(0.1, 10, 100)  # Empezamos en 0.1 para evitar log(0)
y = logaritmica(x, 2, 1)  # a = 2, b = 1

plt.plot(x, y)
plt.title('Curva Logarítmica')
plt.show()
```

```r
# R
logaritmica <- function(x, a, b) {
  a * log(x) + b
}

# Ejemplo
x <- seq(0.1, 10, length.out = 100)  # Empezamos en 0.1 para evitar log(0)
y <- logaritmica(x, 2, 1)  # a = 2, b = 1

plot(x, y, type = "l", main = "Curva Logarítmica")
```

## 4. Finanzas

1. **Valor Presente (VP)**
   Fórmula matemática: $$VP = FV / (1 + r)^n$$ `FV` es el valor futuro
    `r` es la tasa de interés 
    `n` es el número de períodos
    
   ```python
   # Python
   def valor_presente(FV, r, n):
       return FV / (1 + r)**n
   
   # Ejemplo
   print(valor_presente(1000, 0.05, 5))  # 783.5262424159805
   ```
   
   ```r
   # R
   valor_presente <- function(FV, r, n) {
     return(FV / (1 + r)^n)
   }
   
   # Ejemplo
   print(valor_presente(1000, 0.05, 5))  # 783.5262
   ```

2. **Valor Futuro (VF)**
   Fórmula matemática: $$VF = PV * (1 + r)^n$$ `PV` es el valor presente
    `r` es la tasa de interés 
    `n` es el número de períodos
    
   ```python
   # Python
   def valor_futuro(PV, r, n):
       return PV * (1 + r)**n
   
   # Ejemplo
   print(valor_futuro(1000, 0.05, 5))  # 1276.2815625000003
   ```
   
   ```r
   # R
   valor_futuro <- function(PV, r, n) {
     return(PV * (1 + r)^n)
   }
   
   # Ejemplo
   print(valor_futuro(1000, 0.05, 5))  # 1276.282
   ```

3. **Tasa Interna de Retorno (TIR)**
   Fórmula matemática: $$0 = Σ(Ct / (1 + TIR)^t)$$ `Ct` es el flujo de caja en el período `t`
   
   ```python
   # Python
   import numpy as np
   
   def tir(flujos_caja):
       return np.irr(flujos_caja)
   
   # Ejemplo
   print(tir([-1000, 300, 400, 500]))  # 0.1715247261633708
   ```
   
   ```r
   # R
   tir <- function(flujos_caja) {
     return(irr(flujos_caja))
   }
   
   # Ejemplo
   print(tir(c(-1000, 300, 400, 500)))  # 0.1715247
   ```

4. **Valor Presente Neto (VPN)**
   Fórmula matemática: $$VPN = Σ(Ct / (1 + r)^t) - C0$$ `Ct` es el flujo de caja en el período `t`
    `r` es la tasa de descuento 
    `C0` es la inversión inicial
    
   ```python
   # Python
   import numpy as np
   
   def vpn(flujos_caja, tasa):
       return np.npv(tasa, flujos_caja)
   
   # Ejemplo
   print(vpn(0.1, [-1000, 300, 400, 500]))  # 78.82442051086969
   ```
   
   ```r
   # R
   vpn <- function(tasa, flujos_caja) {
     return(NPV(tasa, flujos_caja))
   }
   
   # Ejemplo
   print(vpn(0.1, c(-1000, 300, 400, 500)))  # 78.82442
   ```

5. **Retorno de la Inversión (ROI)**
   Fórmula matemática: $$ROI = \text{(Ganancia - Costo de inversión) / Costo de inversión}$$
   ```python
   # Python
   def roi(ganancia, costo):
       return (ganancia - costo) / costo
   
   # Ejemplo
   print(roi(1500, 1000))  # 0.5
   ```
   
   ```r
   # R
   roi <- function(ganancia, costo) {
     return((ganancia - costo) / costo)
   }
   
   # Ejemplo
   print(roi(1500, 1000))  # 0.5
   ```

6. **Depreciación en Línea Recta**
   Fórmula matemática: $$\text{Depreciación anual = (Valor inicial - Valor residual) / Vida útil}$$
   ```python
   # Python
   def depreciacion_lineal(valor_inicial, valor_residual, vida_util):
       return (valor_inicial - valor_residual) / vida_util
   
   # Ejemplo
   print(depreciacion_lineal(10000, 2000, 5))  # 1600.0
   ```
   
   ```r
   # R
   depreciacion_lineal <- function(valor_inicial, valor_residual, vida_util) {
     return((valor_inicial - valor_residual) / vida_util)
   }
   
   # Ejemplo
   print(depreciacion_lineal(10000, 2000, 5))  # 1600
   ```

7. **Punto de Equilibrio**
   Fórmula matemática: $$PE = CF / (P - CV)$$ `CF` son los costos fijos 
    `P` es el precio por unidad 
    `CV` es el costo variable por unidad
    
   ```python
   # Python
   def punto_equilibrio(costos_fijos, precio, costo_variable):
       return costos_fijos / (precio - costo_variable)
   
   # Ejemplo
   print(punto_equilibrio(50000, 100, 60))  # 1250.0
   ```
   
   ```r
   # R
   punto_equilibrio <- function(costos_fijos, precio, costo_variable) {
     return(costos_fijos / (precio - costo_variable))
   }
   
   # Ejemplo
   print(punto_equilibrio(50000, 100, 60))  # 1250
   ```

8. **Margen de Contribución**
   Fórmula matemática: $$MC = P - CV$$ `P` es el precio por unidad  
   `CV` es el costo variable por unidad
   
   ```python
   # Python
   def margen_contribucion(precio, costo_variable):
       return precio - costo_variable
   
   # Ejemplo
   print(margen_contribucion(100, 60))  # 40
   ```
   
   ```r
   # R
   margen_contribucion <- function(precio, costo_variable) {
     return(precio - costo_variable)
   }
   
   # Ejemplo
   print(margen_contribucion(100, 60))  # 40
   ```

9. **Razón de Deuda**
   Fórmula matemática: $$\text{Razón de Deuda = Deuda Total / Activos Totales}$$
   ```python
   # Python
   def razon_deuda(deuda_total, activos_totales):
       return deuda_total / activos_totales
   
   # Ejemplo
   print(razon_deuda(500000, 1000000))  # 0.5
   ```
   
   ```r
   # R
   razon_deuda <- function(deuda_total, activos_totales) {
     return(deuda_total / activos_totales)
   }
   
   # Ejemplo
   print(razon_deuda(500000, 1000000))  # 0.5
   ```

10. **Razón de Liquidez Corriente**
    Fórmula matemática: $$\text{Razón Corriente = Activos Corrientes / Pasivos Corrientes}$$
    ```python
    # Python
    def razon_corriente(activos_corrientes, pasivos_corrientes):
        return activos_corrientes / pasivos_corrientes
    
    # Ejemplo
    print(razon_corriente(100000, 50000))  # 2.0
    ```
    
    ```r
    # R
    razon_corriente <- function(activos_corrientes, pasivos_corrientes) {
      return(activos_corrientes / pasivos_corrientes)
    }
    
    # Ejemplo
    print(razon_corriente(100000, 50000))  # 2
    ```

11. **Rotación de Inventarios**
    Fórmula matemática: $$\text{Rotación de Inventarios = Costo de Ventas / Inventario Promedio}$$
    ```python
    # Python
    def rotacion_inventarios(costo_ventas, inventario_promedio):
        return costo_ventas / inventario_promedio
    
    # Ejemplo
    print(rotacion_inventarios(500000, 100000))  # 5.0
    ```
    ```r
    # R
    rotacion_inventarios <- function(costo_ventas, inventario_promedio) {
      return(costo_ventas / inventario_promedio)
    }
    
    # Ejemplo
    print(rotacion_inventarios(500000, 100000))  # 5
    ```

12. **Margen de Utilidad Neta**
    Fórmula matemática: $$\text{Margen de Utilidad Neta = Utilidad Neta / Ventas Netas}$$
    ```python
    # Python
    def margen_utilidad_neta(utilidad_neta, ventas_netas):
        return utilidad_neta / ventas_netas
    
    # Ejemplo
    print(margen_utilidad_neta(100000, 1000000))  # 0.1
    ```
    ```r
    # R
    margen_utilidad_neta <- function(utilidad_neta, ventas_netas) {
      return(utilidad_neta / ventas_netas)
    }
    
    # Ejemplo
    print(margen_utilidad_neta(100000, 1000000))  # 0.1
    ```

13. **Rendimiento sobre Activos (ROA)**
    Fórmula matemática: $$\text{ROA = Utilidad Neta / Activos Totales}$$
    ```python
    # Python
    def roa(utilidad_neta, activos_totales):
        return utilidad_neta / activos_totales
    
    # Ejemplo
    print(roa(100000, 1000000))  # 0.1
    ```
    ```r
    # R
    roa <- function(utilidad_neta, activos_totales) {
      return(utilidad_neta / activos_totales)
    }
    
    # Ejemplo
    print(roa(100000, 1000000))  # 0.1
    ```

14. **Rendimiento sobre Capital (ROE)**
    Fórmula matemática: $$\text{ROE = Utilidad Neta / Capital Contable}$$
    ```python
    # Python
    def roe(utilidad_neta, capital_contable):
        return utilidad_neta / capital_contable
    
    # Ejemplo
    print(roe(100000, 500000))  # 0.2
    ```
    ```r
    # R
    roe <- function(utilidad_neta, capital_contable) {
      return(utilidad_neta / capital_contable)
    }
    
    # Ejemplo
    print(roe(100000, 500000))  # 0.2
    ```

15. **Valor Económico Agregado (EVA)**
    Fórmula matemática: $$EVA = NOPAT - (\text{Capital Invertido} * WACC)$$`NOPAT` es la Utilidad Operativa Neta después de Impuestos 
    `WACC` es el Costo Promedio Ponderado de Capital
    
    ```python
    # Python
    def eva(nopat, capital_invertido, wacc):
        return nopat - (capital_invertido * wacc)
    
    # Ejemplo
    print(eva(100000, 1000000, 0.1))  # 0.0
    ```
    ```r
    # R
    eva <- function(nopat, capital_invertido, wacc) {
      return(nopat - (capital_invertido * wacc))
    }
    
    # Ejemplo
    print(eva(100000, 1000000, 0.1))  # 0
    ```

## 5. Álgebra

1. **Fórmula cuadrática**
   Fórmula matemática: $$x = (-b ± √(b² - 4ac)) / (2a)$$ para: $$ax² + bx + c = 0$$
   ```python
   # Python
   import math

   def formula_cuadratica(a, b, c):
       discriminante = b**2 - 4*a*c
       if discriminante < 0:
           return None
       x1 = (-b + math.sqrt(discriminante)) / (2*a)
       x2 = (-b - math.sqrt(discriminante)) / (2*a)
       return x1, x2

   # Ejemplo
   print(formula_cuadratica(1, 5, 6))  # (-2.0, -3.0)
   ```
   
   ```r
   # R
   formula_cuadratica <- function(a, b, c) {
     discriminante <- b^2 - 4*a*c
     if (discriminante < 0) {
       return(NULL)
     }
     x1 <- (-b + sqrt(discriminante)) / (2*a)
     x2 <- (-b - sqrt(discriminante)) / (2*a)
     return(c(x1, x2))
   }

   # Ejemplo
   print(formula_cuadratica(1, 5, 6))  # -2 -3
   ```

2. **Distancia entre dos puntos**
   Fórmula matemática: $$d = √((x₂ - x₁)² + (y₂ - y₁)²)$$
   ```python
   # Python
   import math

   def distancia_puntos(x1, y1, x2, y2):
       return math.sqrt((x2 - x1)**2 + (y2 - y1)**2)

   # Ejemplo
   print(distancia_puntos(0, 0, 3, 4))  # 5.0
   ```
   
   ```r
   # R
   distancia_puntos <- function(x1, y1, x2, y2) {
     return(sqrt((x2 - x1)^2 + (y2 - y1)^2))
   }

   # Ejemplo
   print(distancia_puntos(0, 0, 3, 4))  # 5
   ```

3. **Pendiente de una recta**
   Fórmula matemática: $$m = (y₂ - y₁) / (x₂ - x₁)$$
   ```python
   # Python
   def pendiente(x1, y1, x2, y2):
       return (y2 - y1) / (x2 - x1)

   # Ejemplo
   print(pendiente(0, 0, 3, 4))  # 1.3333333333333333
   ```
   
   ```r
   # R
   pendiente <- function(x1, y1, x2, y2) {
     return((y2 - y1) / (x2 - x1))
   }

   # Ejemplo
   print(pendiente(0, 0, 3, 4))  # 1.333333
   ```

4. **Ecuación de la recta (punto-pendiente)**
   Fórmula matemática: $$y - y₁ = m(x - x₁)$$
   ```python
   # Python
   def ecuacion_recta(x1, y1, m):
       return f"y - {y1} = {m}(x - {x1})"

   # Ejemplo
   print(ecuacion_recta(2, 3, 4))  # y - 3 = 4(x - 2)
   ```
   
   ```r
   # R
   ecuacion_recta <- function(x1, y1, m) {
     return(paste("y -", y1, "=", m, "(x -", x1, ")"))
   }

   # Ejemplo
   print(ecuacion_recta(2, 3, 4))  # "y - 3 = 4 (x - 2)"
   ```

5. **Suma de una progresión aritmética**
   Fórmula matemática: $$S = n(a₁ + aₙ) / 2$$`n` es el número de términos 
   `a₁` es el primer término  
   `aₙ` es el último término
   
   ```python
   # Python
   def suma_progresion_aritmetica(a1, an, n):
       return n * (a1 + an) / 2

   # Ejemplo
   print(suma_progresion_aritmetica(1, 100, 100))  # 5050.0
   ```
   
   ```r
   # R
   suma_progresion_aritmetica <- function(a1, an, n) {
     return(n * (a1 + an) / 2)
   }

   # Ejemplo
   print(suma_progresion_aritmetica(1, 100, 100))  # 5050
   ```

6. **Suma de una progresión geométrica**
   Fórmula matemática: $$S = a(1 - rⁿ) / (1 - r)$$`a` es el primer término
   `r` es la razón  
   `n` es el número de términos
   
   ```python
   # Python
   def suma_progresion_geometrica(a, r, n):
       if r == 1:
           return a * n
       return a * (1 - r**n) / (1 - r)

   # Ejemplo
   print(suma_progresion_geometrica(1, 2, 5))  # 31.0
   ```
   
   ```r
   # R
   suma_progresion_geometrica <- function(a, r, n) {
     if (r == 1) {
       return(a * n)
     }
     return(a * (1 - r^n) / (1 - r))
   }

   # Ejemplo
   print(suma_progresion_geometrica(1, 2, 5))  # 31
   ```

7. **Teorema del binomio**
   Fórmula matemática: $$(x + y)ⁿ = Σᵏ₌₀ⁿ (ⁿₖ)xⁿ⁻ᵏyᵏ$$
   ```python
   # Python
   from math import comb

   def expansion_binomial(x, y, n):
       return sum(comb(n, k) * (x**(n-k)) * (y**k) for k in range(n+1))

   # Ejemplo
   print(expansion_binomial(1, 1, 2))  # 4.0
   ```
   
   ```r
   # R
   expansion_binomial <- function(x, y, n) {
     return(sum(choose(n, 0:n) * (x^(n:0)) * (y^(0:n))))
   }

   # Ejemplo
   print(expansion_binomial(1, 1, 2))  # 4
   ```

8. **Factorización de diferencia de cuadrados**
   Fórmula matemática: $$a² - b² = (a+b)(a-b)$$
   ```python
   # Python
   def factorizacion_diferencia_cuadrados(a, b):
       return f"({a}+{b})({a}-{b})"

   # Ejemplo
   print(factorizacion_diferencia_cuadrados('x', 'y'))  # (x+y)(x-y)
   ```
   
   ```r
   # R
   factorizacion_diferencia_cuadrados <- function(a, b) {
     return(paste0("(", a, "+", b, ")(", a, "-", b, ")"))
   }

   # Ejemplo
   print(factorizacion_diferencia_cuadrados('x', 'y'))  # "(x+y)(x-y)"
   ```

9. **Resolución de sistemas de ecuaciones lineales (método de Cramer)**
   Fórmula matemática: $$x = Dx / D, y = Dy / D$$ `D` es el determinante de la matriz de coeficientes
   
   ```python
   # Python
   def cramer(a1, b1, c1, a2, b2, c2):
       D = a1*b2 - a2*b1
       Dx = c1*b2 - c2*b1
       Dy = a1*c2 - a2*c1
       if D != 0:
           return Dx/D, Dy/D
       return None

   # Ejemplo
   print(cramer(2, 1, 4, 1, 3, 5))  # (1.0, 2.0)
   ```
   
   ```r
   # R
   cramer <- function(a1, b1, c1, a2, b2, c2) {
     D <- a1*b2 - a2*b1
     Dx <- c1*b2 - c2*b1
     Dy <- a1*c2 - a2*c1
     if (D != 0) {
       return(c(Dx/D, Dy/D))
     }
     return(NULL)
   }

   # Ejemplo
   print(cramer(2, 1, 4, 1, 3, 5))  # 1 2
   ```

10. **Fórmula del término general de una progresión aritmética**
    Fórmula matemática: $$aₙ = a₁ + (n - 1)d$$`a₁` es el primer término 
    `n` es el número de término  
    `d` es la diferencia común
    
    ```python
    # Python
    def termino_general_aritmetica(a1, n, d):
        return a1 + (n - 1) * d

    # Ejemplo
    print(termino_general_aritmetica(2, 5, 3))  # 14
    ```
    ```r
    # R
    termino_general_aritmetica <- function(a1, n, d) {
      return(a1 + (n - 1) * d)
    }

    # Ejemplo
    print(termino_general_aritmetica(2, 5, 3))  # 14
    ```

11. **Fórmula del término general de una progresión geométrica**
    Fórmula matemática: $$aₙ = a₁rⁿ⁻¹$$`a₁` es el primer término
    `r` es la razón  
    `n` es el número de término
    
    ```python
    # Python
    def termino_general_geometrica(a1, r, n):
        return a1 * r**(n-1)

    # Ejemplo
    print(termino_general_geometrica(2, 3, 4))  # 54
    ```
    
    ```r
    # R
    termino_general_geometrica <- function(a1, r, n) {
      return(a1 * r^(n-1))
    }

    # Ejemplo
    print(termino_general_geometrica(2, 3, 4))  # 54
    ```

12. **Fórmula de la distancia de un punto a una recta**
    Fórmula matemática: $$d = |Ax₀ + By₀ + C| / √(A² + B²)$$`(x₀, y₀)` es el punto  
    `Ax + By + C = 0` es la ecuación de la recta
    
    ```python
    # Python
    import math

    def distancia_punto_recta(A, B, C, x0, y0):
        return abs(A*x0 + B*y0 + C) / math.sqrt(A**2 + B**2)

    # Ejemplo
    print(distancia_punto_recta(1, 1, -3, 2, 2))  # 0.7071067811865476
    ```
    
    ```r
    # R
    distancia_punto_recta <- function(A, B, C, x0, y0) {
      return(abs(A*x0 + B*y0 + C) / sqrt(A^2 + B^2))
    }

    # Ejemplo
    print(distancia_punto_recta(1, 1, -3, 2, 2))  # 0.7071068
    ```

13. **Fórmula de las raíces de una ecuación cúbica**
    Fórmula matemática: $$x = -b/(3a) + (S + T), x = -b/(3a) - (S + T)/2 + i√3(S - T)/2, x = -b/(3a) - (S + T)/2 - i√3(S - T)/2$$
    `S` = ∛(R + √(Q³ + R²)) 
    `T` = ∛(R - √(Q³ + R²))
    `Q` = (3ac - b²)/(9a²) 
    `R` = (9abc - 27a²d - 2b³)/(54a³)
    
    ```python
    # Python
    import cmath

    def raices_cubicas(a, b, c, d):
        p = (3*a*c - b**2) / (3*a**2)
        q = (2*b**3 - 9*a*b*c + 27*a**2*d) / (27*a**3)
        D = (q**2/4) + (p**3/27)
        
        u1 = (-q/2 + cmath.sqrt(D))**(1/3)
        u2 = (-q/2 - cmath.sqrt(D))**(1/3)
        
        y1 = u1 + u2 - b/(3*a)
        y2 = -(u1 + u2)/2 - b/(3*a) + 1j * (u1 - u2) * cmath.sqrt(3)/2
        y3 = -(u1 + u2)/2 - b/(3*a) - 1j * (u1 - u2) * cmath.sqrt(3)/2
        
        return y1, y2, y3

    # Ejemplo
    print(raices_cubicas(1, 0, -7, 6))  # ((1+0j), (-3+0j), (2+0j))
    ```
    
    ```r
    # R
    raices_cubicas <- function(a, b, c, d) {
      p <- (3*a*c - b^2) / (3*a^2)
      q <- (2*b^3 - 9*a*b*c + 27*a^2*d) / (27*a^3)
      D <- (q^2/4) + (p^3/27)
      
      u1 <- (-q/2 + sqrt(as.complex(D)))^(1/3)
      u2 <- (-q/2 - sqrt(as.complex(D)))^(1/3)
      
      y1 <- u1 + u2 - b/(3*a)
      y2 <- -(u1 + u2)/2 - b/(3*a) + 1i * (u1 - u2) * sqrt(3)/2
      y3 <- -(u1 + u2)/2 - b/(3*a) - 1i * (u1 - u2) * sqrt(3)/2
      
      return(c(y1, y2, y3))
    }

    # Ejemplo
    print(raices_cubicas(1, 0, -7, 6))  # 1+0i -3+0i 2+0i
    ```

14. **Fórmula de la suma de los ángulos internos de un polígono**
    Fórmula matemática: $$S = (n - 2) * 180°$$`n` es el número de lados del polígono
    
    ```python
    # Python
    def suma_angulos_internos(n):
        return (n - 2) * 180

    # Ejemplo
    print(suma_angulos_internos(5))  # 540
    ```
    
    ```r
    # R
    suma_angulos_internos <- function(n) {
      return((n - 2) * 180)
    }

    # Ejemplo
    print(suma_angulos_internos(5))  # 540
    ```

15. **Fórmula del interés compuesto**
    Fórmula matemática: $$A = P(1 + r)^t$$`A` es el monto final 
    `P` es el principal (monto inicial) 
    `r` es la tasa de interés  
    `t` es el tiempo
    
    ```python
    # Python
    def interes_compuesto(P, r, t):
        return P * (1 + r)**t

    # Ejemplo
    print(interes_compuesto(1000, 0.05, 5))  # 1276.2815625000003
    ```
    
    ```r
    # R
    interes_compuesto <- function(P, r, t) {
      return(P * (1 + r)^t)
    }

    # Ejemplo
    print(interes_compuesto(1000, 0.05, 5))  # 1276.282
    ```

## 7. Combinatoria

1. **Permutaciones sin repetición**
   Fórmula matemática: $$P(n,r) = n! / (n-r)!$$
   ```python
   # Python
   import math

   def permutaciones_sin_repeticion(n, r):
       return math.factorial(n) // math.factorial(n - r)

   # Ejemplo
   print(permutaciones_sin_repeticion(5, 3))  # 60
   ```
   
   ```r
   # R
   permutaciones_sin_repeticion <- function(n, r) {
     return(factorial(n) / factorial(n - r))
   }

   # Ejemplo
   print(permutaciones_sin_repeticion(5, 3))  # 60
   ```

2. **Combinaciones sin repetición**
   Fórmula matemática: $$C(n,r) = n! / (r! * (n-r)!)$$
   ```python
   # Python
   import math

   def combinaciones_sin_repeticion(n, r):
       return math.comb(n, r)

   # Ejemplo
   print(combinaciones_sin_repeticion(5, 3))  # 10
   ```
   
   ```r
   # R
   combinaciones_sin_repeticion <- function(n, r) {
     return(choose(n, r))
   }

   # Ejemplo
   print(combinaciones_sin_repeticion(5, 3))  # 10
   ```

3. **Permutaciones con repetición**
   Fórmula matemática: $$PR(n,r) = n^r$$
   ```python
   # Python
   def permutaciones_con_repeticion(n, r):
       return n**r

   # Ejemplo
   print(permutaciones_con_repeticion(3, 2))  # 9
   ```
   
   ```r
   # R
   permutaciones_con_repeticion <- function(n, r) {
     return(n^r)
   }

   # Ejemplo
   print(permutaciones_con_repeticion(3, 2))  # 9
   ```

4. **Combinaciones con repetición**
   Fórmula matemática: $$CR(n,r) = C(n+r-1, r)$$
   ```python
   # Python
   import math

   def combinaciones_con_repeticion(n, r):
       return math.comb(n + r - 1, r)

   # Ejemplo
   print(combinaciones_con_repeticion(3, 2))  # 6
   ```
   
   ```r
   # R
   combinaciones_con_repeticion <- function(n, r) {
     return(choose(n + r - 1, r))
   }

   # Ejemplo
   print(combinaciones_con_repeticion(3, 2))  # 6
   ```

5. **Principio de inclusión-exclusión (2 conjuntos)**
   Fórmula matemática: $$|A ∪ B| = |A| + |B| - |A ∩ B|$$
   ```python
   # Python
   def inclusion_exclusion_2(A, B):
       return len(A) + len(B) - len(set(A) & set(B))

   # Ejemplo
   print(inclusion_exclusion_2([1,2,3], [2,3,4]))  # 4
   ```
   
   ```r
   # R
   inclusion_exclusion_2 <- function(A, B) {
     return(length(A) + length(B) - length(intersect(A, B)))
   }

   # Ejemplo
   print(inclusion_exclusion_2(c(1,2,3), c(2,3,4)))  # 4
   ```

6. **Principio de inclusión-exclusión (3 conjuntos)**
   Fórmula matemática: $$|A ∪ B ∪ C| = |A| + |B| + |C| - |A ∩ B| - |A ∩ C| - |B ∩ C| + |A ∩ B ∩ C|$$
   ```python
   # Python
   def inclusion_exclusion_3(A, B, C):
       return (len(A) + len(B) + len(C) 
               - len(set(A) & set(B)) - len(set(A) & set(C)) - len(set(B) & set(C))
               + len(set(A) & set(B) & set(C)))

   # Ejemplo
   print(inclusion_exclusion_3([1,2,3], [2,3,4], [3,4,5]))  # 5
   ```
   
   ```r
   # R
   inclusion_exclusion_3 <- function(A, B, C) {
     return(length(A) + length(B) + length(C) 
            - length(intersect(A, B)) - length(intersect(A, C)) - length(intersect(B, C))
            + length(intersect(intersect(A, B), C)))
   }

   # Ejemplo
   print(inclusion_exclusion_3(c(1,2,3), c(2,3,4), c(3,4,5)))  # 5
   ```

7. **Número de Stirling de segunda especie**
   Fórmula matemática: $$S(n,k) = S(n-1,k-1) + k*S(n-1,k)$$
   ```python
   # Python
   def stirling_segunda_especie(n, k):
       if k == 1 or k == n:
           return 1
       return stirling_segunda_especie(n-1, k-1) + k * stirling_segunda_especie(n-1, k)

   # Ejemplo
   print(stirling_segunda_especie(4, 2))  # 7
   ```
   
   ```r
   # R
   stirling_segunda_especie <- function(n, k) {
     if (k == 1 || k == n) {
       return(1)
     }
     return(stirling_segunda_especie(n-1, k-1) + k * stirling_segunda_especie(n-1, k))
   }

   # Ejemplo
   print(stirling_segunda_especie(4, 2))  # 7
   ```

8. **Número de Bell**
   Fórmula matemática: $$B(n+1) = Σᵏ₌₀ⁿ C(n,k)B(k)$$
   ```python
   # Python
   def bell_number(n):
       if n == 0 or n == 1:
           return 1
       bell = [[0 for i in range(n+1)] for j in range(n+1)]
       bell[0][0] = 1
       for i in range(1, n+1):
           bell[i][0] = bell[i-1][i-1]
           for j in range(1, i+1):
               bell[i][j] = bell[i-1][j-1] + bell[i][j-1]
       return bell[n][0]

   # Ejemplo
   print(bell_number(4))  # 15
   ```
   
   ```r
   # R
   bell_number <- function(n) {
     if (n == 0 || n == 1) {
       return(1)
     }
     bell <- matrix(0, nrow=n+1, ncol=n+1)
     bell[1,1] <- 1
     for (i in 2:(n+1)) {
       bell[i,1] <- bell[i-1,i-1]
       for (j in 2:i) {
         bell[i,j] <- bell[i-1,j-1] + bell[i,j-1]
       }
     }
     return(bell[n+1,1])
   }

   # Ejemplo
   print(bell_number(4))  # 15
   ```

9. **Número de Catalan**
   Fórmula matemática: $$C(n) = (1 / (n+1)) * C(2n,n)$$
   ```python
   # Python
   import math

   def catalan_number(n):
       return math.comb(2*n, n) // (n + 1)

   # Ejemplo
   print(catalan_number(4))  # 14
   ```
   
   ```r
   # R
   catalan_number <- function(n) {
     return(choose(2*n, n) / (n + 1))
   }

   # Ejemplo
   print(catalan_number(4))  # 14
   ```

10. **Coeficiente multinomial**
    Fórmula matemática: $$C(n; k₁, k₂, ..., kₘ) = n! / (k₁! * k₂! * ... * kₘ!)$$
    ```python
    # Python
    import math

    def coeficiente_multinomial(*args):
        n = sum(args)
        denominador = 1
        for k in args:
            denominador *= math.factorial(k)
        return math.factorial(n) // denominador

    # Ejemplo
    print(coeficiente_multinomial(2, 1, 1))  # 12
    ```
    
    ```r
    # R
    coeficiente_multinomial <- function(...) {
      args <- c(...)
      n <- sum(args)
      denominador <- prod(factorial(args))
      return(factorial(n) / denominador)
    }

    # Ejemplo
    print(coeficiente_multinomial(2, 1, 1))  # 12
    ```

11. **Número de particiones de un conjunto**
    Fórmula matemática: $$P(n) = Σᵏ₌₁ⁿ S(n,k)$$`S(n,k)` es el número de Stirling de segunda especie
    
    ```python
    # Python
    def particiones_conjunto(n):
        return sum(stirling_segunda_especie(n, k) for k in range(1, n+1))

    # Ejemplo
    print(particiones_conjunto(4))  # 15
    ```
    
    ```r
    # R
    particiones_conjunto <- function(n) {
      return(sum(sapply(1:n, function(k) stirling_segunda_especie(n, k))))
    }

    # Ejemplo
    print(particiones_conjunto(4))  # 15
    ```

12. **Variaciones sin repetición**
    Fórmula matemática: $$V(n,r) = n! / (n-r)!$$
    ```python
    # Python
    import math

    def variaciones_sin_repeticion(n, r):
        return math.factorial(n) // math.factorial(n - r)

    # Ejemplo
    print(variaciones_sin_repeticion(5, 3))  # 60
    ```
    
    ```r
    # R
    variaciones_sin_repeticion <- function(n, r) {
      return(factorial(n) / factorial(n - r))
    }

    # Ejemplo
    print(variaciones_sin_repeticion(5, 3))  # 60
    ```

13. **Variaciones con repetición**
    Fórmula matemática: $$VR(n,r) = n^r$$
    ```python
    # Python
    def variaciones_con_repeticion(n, r):
        return n**r

    # Ejemplo
    print(variaciones_con_repeticion(3, 2))  # 9
    ```
    
    ```r
    # R
    variaciones_con_repeticion <- function(n, r) {
      return(n^r)
    }

    # Ejemplo
    print(variaciones_con_repeticion(3, 2))  # 9
    ```

14. **Número de derangements**
    Fórmula matemática: $$D(n) = n! * (1 - 1/1! + 1/2! - 1/3! + ... + (-1)ⁿ/n!)$$
    ```python
    # Python
    import math

    def derangements(n):
        return round(math.factorial(n) / math.e)

    # Ejemplo
    print(derangements(4))  # 9
    ```
    
    ```r
    # R
    derangements <- function(n) {
      return(round(factorial(n) / exp(1)))
    }

    # Ejemplo
    print(derangements(4))  # 9
    ```

15. **Coeficiente binomial generalizado**
    Fórmula matemática: $$C(x,k) = (x * (x-1) * ... * (x-k+1)) / k!$$
    ```python
    # Python
    import math

    def coeficiente_binomial_generalizado(x, k):
        numerador = 1
        for i in range(k):
            numerador *= (x - i)
        return numerador // math.factorial(k)

    # Ejemplo
    print(coeficiente_binomial_generalizado(5, 2))  # 10
    ```
    
    ```r
    # R
    coeficiente_binomial_generalizado <- function(x, k) {
      numerador <- prod(x - 0:(k-1))
      return(numerador / factorial(k))
    }

    # Ejemplo
    print(coeficiente_binomial_generalizado(5, 2))  # 10
    ```

## 8. Teoría de Números

1. **Criba de Eratóstenes**
   Algoritmo para encontrar números primos hasta n
   ```python
   # Python
   def criba_eratostenes(n):
       primos = [True] * (n + 1)
       primos[0] = primos[1] = False
       for i in range(2, int(n**0.5) + 1):
           if primos[i]:
               for j in range(i*i, n+1, i):
                   primos[j] = False
       return [i for i in range(n+1) if primos[i]]

   # Ejemplo
   print(criba_eratostenes(20))  # [2, 3, 5, 7, 11, 13, 17, 19]
   ```
   
   ```r
   # R
   criba_eratostenes <- function(n) {
     primos <- rep(TRUE, n+1)
     primos[1] <- FALSE
     for (i in 2:sqrt(n)) {
       if (primos[i]) {
         primos[seq(i*i, n+1, i)] <- FALSE
       }
     }
     return(which(primos))
   }

   # Ejemplo
   print(criba_eratostenes(20))  # 2 3 5 7 11 13 17 19
   ```

2. **Algoritmo de Euclides (MCD)**
   Fórmula recursiva: $$MCD(a,b) = MCD(b, \text{a mod b})$$
   ```python
   # Python
   def mcd(a, b):
       while b:
           a, b = b, a % b
       return a

   # Ejemplo
   print(mcd(48, 18))  # 6
   ```
   
   ```r
   # R
   mcd <- function(a, b) {
     while (b != 0) {
       t <- b
       b <- a %% b
       a <- t
     }
     return(a)
   }

   # Ejemplo
   print(mcd(48, 18))  # 6
   ```

3. **Mínimo Común Múltiplo (MCM)**
   Fórmula: $$MCM(a,b) = |a * b| / MCD(a,b)$$
   ```python
   # Python
   def mcm(a, b):
       return abs(a * b) // mcd(a, b)

   # Ejemplo
   print(mcm(12, 18))  # 36
   ```
   
   ```r
   # R
   mcm <- function(a, b) {
     return(abs(a * b) %/% mcd(a, b))
   }

   # Ejemplo
   print(mcm(12, 18))  # 36
   ```

4. **Teorema Fundamental de la Aritmética**
   Factorización en primos
   ```python
   # Python
   def factorizacion_primos(n):
       factores = []
       d = 2
       while n > 1:
           while n % d == 0:
               factores.append(d)
               n //= d
           d += 1
           if d * d > n:
               if n > 1:
                   factores.append(n)
               break
       return factores

   # Ejemplo
   print(factorizacion_primos(84))  # [2, 2, 3, 7]
   ```
   
   ```r
   # R
   factorizacion_primos <- function(n) {
     factores <- c()
     d <- 2
     while (n > 1) {
       while (n %% d == 0) {
         factores <- c(factores, d)
         n <- n %/% d
       }
       d <- d + 1
       if (d * d > n) {
         if (n > 1) {
           factores <- c(factores, n)
         }
         break
       }
     }
     return(factores)
   }

   # Ejemplo
   print(factorizacion_primos(84))  # 2 2 3 7
   ```

5. **Función Phi de Euler**
   Cuenta los números coprimos con n menores que n
   ```python
   # Python
   def phi_euler(n):
       result = n
       for i in range(2, int(n**0.5) + 1):
           if n % i == 0:
               while n % i == 0:
                   n //= i
               result *= (1 - 1/i)
       if n > 1:
           result *= (1 - 1/n)
       return int(result)

   # Ejemplo
   print(phi_euler(36))  # 12
   ```
   
   ```r
   # R
   phi_euler <- function(n) {
     result <- n
     for (i in 2:sqrt(n)) {
       if (n %% i == 0) {
         while (n %% i == 0) {
           n <- n %/% i
         }
         result <- result * (1 - 1/i)
       }
     }
     if (n > 1) {
       result <- result * (1 - 1/n)
     }
     return(as.integer(result))
   }

   # Ejemplo
   print(phi_euler(36))  # 12
   ```

6. **Teorema de Fermat (Pequeño)**
   Si p es primo y a no es divisible por p, entonces: $$a^(p-1) ≡ 1 (mod p)$$
   ```python
   # Python
   def fermat_pequeno(a, p):
       return pow(a, p-1, p) == 1

   # Ejemplo
   print(fermat_pequeno(2, 7))  # True
   ```
   
   ```r
   # R
   fermat_pequeno <- function(a, p) {
     return((a^(p-1) %% p) == 1)
   }

   # Ejemplo
   print(fermat_pequeno(2, 7))  # TRUE
   ```

7. **Test de primalidad de Miller-Rabin**
   Test probabilístico de primalidad
   ```python
   # Python
   import random

   def miller_rabin(n, k=5):
       if n < 2:
           return False
       for p in [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]:
           if n % p == 0:
               return n == p
       s, d = 0, n - 1
       while d % 2 == 0:
           s, d = s + 1, d // 2
       for _ in range(k):
           a = random.randrange(2, n - 1)
           x = pow(a, d, n)
           if x == 1 or x == n - 1:
               continue
           for _ in range(s - 1):
               x = pow(x, 2, n)
               if x == n - 1:
                   break
           else:
               return False
       return True

   # Ejemplo
   print(miller_rabin(997))  # True
   ```
   
   ```r
   # R
   miller_rabin <- function(n, k=5) {
     if (n < 2) return(FALSE)
     for (p in c(2, 3, 5, 7, 11, 13, 17, 19, 23, 29)) {
       if (n %% p == 0) return(n == p)
     }
     s <- 0
     d <- n - 1
     while (d %% 2 == 0) {
       s <- s + 1
       d <- d %/% 2
     }
     for (i in 1:k) {
       a <- sample(2:(n-2), 1)
       x <- (a^d) %% n
       if (x == 1 || x == n-1) next
       for (r in 1:(s-1)) {
         x <- (x^2) %% n
         if (x == n-1) break
       }
       if (x != n-1) return(FALSE)
     }
     return(TRUE)
   }

   # Ejemplo
   print(miller_rabin(997))  # TRUE
   ```

8. **Congruencia Lineal**
   Resuelve $$ax ≡ b (\text{mod m})$$
   ```python
   # Python
   def congruencia_lineal(a, b, m):
       g = mcd(a, m)
       if b % g:
           return None
       a, b, m = a//g, b//g, m//g
       x = (pow(a, -1, m) * b) % m
       return x

   # Ejemplo
   print(congruencia_lineal(3, 4, 7))  # 6
   ```
   
   ```r
   # R
   congruencia_lineal <- function(a, b, m) {
     g <- mcd(a, m)
     if (b %% g != 0) return(NULL)
     a <- a %/% g
     b <- b %/% g
     m <- m %/% g
     x <- (b * as.integer(solve(a, m))) %% m
     return(x)
   }

   # Ejemplo
   print(congruencia_lineal(3, 4, 7))  # 6
   ```

9. **Teorema Chino del Resto**
   Resuelve sistema de congruencias
   ```python
   # Python
   from functools import reduce

   def teorema_chino_resto(residuos, modulos):
       total = 0
       producto = reduce(lambda a, b: a*b, modulos)
       for residuo, modulo in zip(residuos, modulos):
           p = producto // modulo
           total += residuo * pow(p, -1, modulo) * p
       return total % producto

   # Ejemplo
   print(teorema_chino_resto([2, 3, 2], [3, 5, 7]))  # 23
   ```
   
   ```r
   # R
   teorema_chino_resto <- function(residuos, modulos) {
     total <- 0
     producto <- prod(modulos)
     for (i in 1:length(residuos)) {
       p <- producto %/% modulos[i]
       total <- total + residuos[i] * (p * solve(p %% modulos[i], modulos[i])) %% producto
     }
     return(total %% producto)
   }

   # Ejemplo
   print(teorema_chino_resto(c(2, 3, 2), c(3, 5, 7)))  # 23
   ```

10. **Función de Möbius**
    μ(n) = 1 si n es libre de cuadrados con un número par de factores primos
    μ(n) = -1 si n es libre de cuadrados con un número impar de factores primos
    μ(n) = 0 si n tiene un factor cuadrado
    ```python
    # Python
    def mobius(n):
        if n == 1:
            return 1
        p = 0
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0:
                if n % (i*i) == 0:
                    return 0
                n //= i
                p += 1
            while n % i == 0:
                n //= i
        if n > 1:
            p += 1
        return 1 if p % 2 == 0 else -1

    # Ejemplo
    print(mobius(30))  # -1
    ```
    
    ```r
    # R
    mobius <- function(n) {
      if (n == 1) return(1)
      p <- 0
      for (i in 2:sqrt(n)) {
        if (n %% i == 0) {
          if (n %% (i*i) == 0) return(0)
          n <- n %/% i
          p <- p + 1
        }
        while (n %% i == 0) {
          n <- n %/% i
        }
      }
      if (n > 1) p <- p + 1
      return(ifelse(p %% 2 == 0, 1, -1))
    }

    # Ejemplo
    print(mobius(30))  # -1
    ```

11. **Función Suma de Divisores**
    σ(n) = suma de todos los divisores positivos de n
    ```python
    # Python
    def suma_divisores(n):
        result = 1
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0:
                s = 1
                t = 1
                while n % i == 0:
                    n //= i
                    t *= i
                    s += t
                result *= s
        if n > 1:
            result *= (1 + n)
        return result

    # Ejemplo
    print(suma_divisores(12))  # 28
    ```
    
    ```r
    # R
    suma_divisores <- function(n) {
      result <- 1
      for (i in 2:sqrt(n)) {
        if (n %% i == 0) {
          s <- 1
          t <- 1
          while (n %% i == 0) {
            n <- n %/% i
            t <- t * i
            s <- s + t
          }
          result <- result * s
        }
      }
      if (n > 1) {
        result <- result * (1 + n)
      }
      return(result)
    }

    # Ejemplo
    print(suma_divisores(12))  # 28
    ```

12. **Orden multiplicativo**
    El menor entero positivo k tal que $$a^k ≡ 1 (\text{mod n})$$
    ```python
    # Python
    def orden_multiplicativo(a, n):
        if mcd(a, n) != 1:
            return None
        k = 1
        while pow(a, k, n) != 1:
            k += 1
        return k

    # Ejemplo
    print(orden_multiplicativo(2, 7))  # 3
    ```
    
    ```r
    # R
    orden_multiplicativo <- function(a, n) {
      if (mcd(a, n) != 1) return(NULL)
      k <- 1
      while ((a^k %% n) != 1) {
        k <- k + 1
      }
      return(k)
    }

    # Ejemplo
    print(orden_multiplicativo(2, 7))  # 3
    ```

13. **Función de Carmichael**
    λ(n) es el menor m tal que a^m ≡ 1 (mod n) para todo a coprimo con n
    ```python
    # Python
    def carmichael(n):
        if n == 1:
            return 1
        result = 1
        for prime, exp in factorizacion_primos_exp(n):
            if prime == 2 and exp > 2:
                result = mcm(result, 2**(exp-2))
            else:
                result = mcm(result, (prime-1) * prime**(exp-1))
        return result

    def factorizacion_primos_exp(n):
        factors = []
        d = 2
        while n > 1:
            exp = 0
            while n % d == 0:
                exp += 1
                n //= d
            if exp > 0:
                factors.append((d, exp))
            d += 1
            if d * d > n:
                if n > 1:
                    factors.append((n, 1))
                break
        return factors

    # Ejemplo
    print(carmichael(12))  # 2
    ```
    
    ```r
    # R
    carmichael <- function(n) {
      if (n == 1) return(1)
      result <- 1
      factors <- factorizacion_primos_exp(n)
      for (i in 1:nrow(factors)) {
        prime <- factors[i, 1]
        exp <- factors[i, 2]
        if (prime == 2 && exp > 2) {
          result <- mcm(result, 2^(exp-2))
        } else {
          result <- mcm(result, (prime-1) * prime^(exp-1))
        }
      }
      return(result)
    }

    factorizacion_primos_exp <- function(n) {
      factors <- matrix(nrow=0, ncol=2)
      d <- 2
      while (n > 1) {
        exp <- 0
        while (n %% d == 0) {
          exp <- exp + 1
          n <- n %/% d
        }
        if (exp > 0) {
          factors <- rbind(factors, c(d, exp))
        }
        d <- d + 1
        if (d * d > n) {
          if (n > 1) {
            factors <- rbind(factors, c(n, 1))
          }
          break
        }
      }
      return(factors)
    }

    # Ejemplo
    print(carmichael(12))  # 2
    ```

14. **Residuos cuadráticos (símbolo de Legendre)**
    (a|p) = 1 si a es residuo cuadrático módulo p
    (a|p) = -1 si a no es residuo cuadrático módulo p
    (a|p) = 0 si p divide a a
    ```python
    # Python
    def legendre(a, p):
        if a % p == 0:
            return 0
        result = pow(a, (p - 1) // 2, p)
        return -1 if result == p - 1 else result

    # Ejemplo
    print(legendre(2, 7))  # 1
    ```
    
    ```r
    # R
    legendre <- function(a, p) {
      if (a %% p == 0) return(0)
      result <- (a^((p - 1) %/% 2)) %% p
      return(ifelse(result == p - 1, -1, result))
    }

    # Ejemplo
    print(legendre(2, 7))  # 1
    ```

15. **Ecuación diofántica lineal**
    Resuelve $$ax + by = c$$
    ```python
    # Python
    def diofantica(a, b, c):
        g, x, y = mcd_extendido(a, b)
        if c % g != 0:
            return None
        x *= c // g
        y *= c // g
        return x, y

    def mcd_extendido(a, b):
        if b == 0:
            return a, 1, 0
        else:
            g, x, y = mcd_extendido(b, a % b)
            return g, y, x - (a // b) * y

    # Ejemplo
    print(diofantica(3, 5, 7))  # (-4, 3)
    ```
    
    ```r
    # R
    diofantica <- function(a, b, c) {
      result <- mcd_extendido(a, b)
      g <- result$g
      x <- result$x
      y <- result$y
      if (c %% g != 0) return(NULL)
      x <- x * (c %/% g)
      y <- y * (c %/% g)
      return(list(x=x, y=y))
    }

    mcd_extendido <- function(a, b) {
      if (b == 0) {
        return(list(g=a, x=1, y=0))
      } else {
        result <- mcd_extendido(b, a %% b)
        g <- result$g
        x <- result$y
        y <- result$x - (a %/% b) * result$y
        return(list(g=g, x=x, y=y))
      }
    }

    # Ejemplo
    print(diofantica(3, 5, 7))  # $x -4 $y 3
    ```

## 9. Lógica Matemática

1. **Tabla de verdad para la conjunción (AND)**
   $$p ∧ q$$
   ```python
   # Python
   def conjuncion(p, q):
       return p and q

   # Ejemplo
   print(conjuncion(True, False))  # False
   ```
   
   ```r
   # R
   conjuncion <- function(p, q) {
     return(p & q)
   }

   # Ejemplo
   print(conjuncion(TRUE, FALSE))  # FALSE
   ```

2. **Tabla de verdad para la disyunción (OR)**
   $$p ∨ q$$
   ```python
   # Python
   def disyuncion(p, q):
       return p or q

   # Ejemplo
   print(disyuncion(True, False))  # True
   ```
   
   ```r
   # R
   disyuncion <- function(p, q) {
     return(p | q)
   }

   # Ejemplo
   print(disyuncion(TRUE, FALSE))  # TRUE
   ```

3. **Tabla de verdad para la negación (NOT)**
  $$ ¬p$$
   ```python
   # Python
   def negacion(p):
       return not p

   # Ejemplo
   print(negacion(True))  # False
   ```
   
   ```r
   # R
   negacion <- function(p) {
     return(!p)
   }

   # Ejemplo
   print(negacion(TRUE))  # FALSE
   ```

4. **Tabla de verdad para la implicación**
   p → q
   ```python
   # Python
   def implicacion(p, q):
       return (not p) or q

   # Ejemplo
   print(implicacion(True, False))  # False
   ```
   ```r
   # R
   implicacion <- function(p, q) {
     return(!p | q)
   }

   # Ejemplo
   print(implicacion(TRUE, FALSE))  # FALSE
   ```

5. **Tabla de verdad para la doble implicación (equivalencia)**
   p ↔ q
   ```python
   # Python
   def doble_implicacion(p, q):
       return p == q

   # Ejemplo
   print(doble_implicacion(True, False))  # False
   ```
   ```r
   # R
   doble_implicacion <- function(p, q) {
     return(p == q)
   }

   # Ejemplo
   print(doble_implicacion(TRUE, FALSE))  # FALSE
   ```

6. **Leyes de De Morgan**
   ¬(p ∧ q) ↔ (¬p ∨ ¬q)
   ¬(p ∨ q) ↔ (¬p ∧ ¬q)
   ```python
   # Python
   def de_morgan_1(p, q):
       return (not (p and q)) == ((not p) or (not q))

   def de_morgan_2(p, q):
       return (not (p or q)) == ((not p) and (not q))

   # Ejemplo
   print(de_morgan_1(True, False))  # True
   print(de_morgan_2(True, False))  # True
   ```
   ```r
   # R
   de_morgan_1 <- function(p, q) {
     return(!(p & q) == (!p | !q))
   }

   de_morgan_2 <- function(p, q) {
     return(!(p | q) == (!p & !q))
   }

   # Ejemplo
   print(de_morgan_1(TRUE, FALSE))  # TRUE
   print(de_morgan_2(TRUE, FALSE))  # TRUE
   ```

7. **Ley de la doble negación**
   ¬(¬p) ↔ p
   ```python
   # Python
   def doble_negacion(p):
       return not (not p) == p

   # Ejemplo
   print(doble_negacion(True))  # True
   ```
   ```r
   # R
   doble_negacion <- function(p) {
     return(!!p == p)
   }

   # Ejemplo
   print(doble_negacion(TRUE))  # TRUE
   ```

8. **Leyes de idempotencia**
   p ∧ p ↔ p
   p ∨ p ↔ p
   ```python
   # Python
   def idempotencia_and(p):
       return (p and p) == p

   def idempotencia_or(p):
       return (p or p) == p

   # Ejemplo
   print(idempotencia_and(True))  # True
   print(idempotencia_or(False))  # True
   ```
   ```r
   # R
   idempotencia_and <- function(p) {
     return((p & p) == p)
   }

   idempotencia_or <- function(p) {
     return((p | p) == p)
   }

   # Ejemplo
   print(idempotencia_and(TRUE))  # TRUE
   print(idempotencia_or(FALSE))  # TRUE
   ```

9. **Leyes conmutativas**
   p ∧ q ↔ q ∧ p
   p ∨ q ↔ q ∨ p
   ```python
   # Python
   def conmutativa_and(p, q):
       return (p and q) == (q and p)

   def conmutativa_or(p, q):
       return (p or q) == (q or p)

   # Ejemplo
   print(conmutativa_and(True, False))  # True
   print(conmutativa_or(True, False))  # True
   ```
   ```r
   # R
   conmutativa_and <- function(p, q) {
     return((p & q) == (q & p))
   }

   conmutativa_or <- function(p, q) {
     return((p | q) == (q | p))
   }

   # Ejemplo
   print(conmutativa_and(TRUE, FALSE))  # TRUE
   print(conmutativa_or(TRUE, FALSE))  # TRUE
   ```

10. **Leyes asociativas**
    (p ∧ q) ∧ r ↔ p ∧ (q ∧ r)
    (p ∨ q) ∨ r ↔ p ∨ (q ∨ r)
    ```python
    # Python
    def asociativa_and(p, q, r):
        return ((p and q) and r) == (p and (q and r))

    def asociativa_or(p, q, r):
        return ((p or q) or r) == (p or (q or r))

    # Ejemplo
    print(asociativa_and(True, False, True))  # True
    print(asociativa_or(True, False, True))  # True
    ```
    ```r
    # R
    asociativa_and <- function(p, q, r) {
      return(((p & q) & r) == (p & (q & r)))
    }

    asociativa_or <- function(p, q, r) {
      return(((p | q) | r) == (p | (q | r)))
    }

    # Ejemplo
    print(asociativa_and(TRUE, FALSE, TRUE))  # TRUE
    print(asociativa_or(TRUE, FALSE, TRUE))  # TRUE
    ```

11. **Leyes distributivas**
    p ∧ (q ∨ r) ↔ (p ∧ q) ∨ (p ∧ r)
    p ∨ (q ∧ r) ↔ (p ∨ q) ∧ (p ∨ r)
    ```python
    # Python
    def distributiva_and_or(p, q, r):
        return (p and (q or r)) == ((p and q) or (p and r))

    def distributiva_or_and(p, q, r):
        return (p or (q and r)) == ((p or q) and (p or r))

    # Ejemplo
    print(distributiva_and_or(True, False, True))  # True
    print(distributiva_or_and(True, False, True))  # True
    ```
    ```r
    # R
    distributiva_and_or <- function(p, q, r) {
      return((p & (q | r)) == ((p & q) | (p & r)))
    }

    distributiva_or_and <- function(p, q, r) {
      return((p | (q & r)) == ((p | q) & (p | r)))
    }

    # Ejemplo
    print(distributiva_and_or(TRUE, FALSE, TRUE))  # TRUE
    print(distributiva_or_and(TRUE, FALSE, TRUE))  # TRUE
    ```

12. **Leyes de absorción**
    p ∧ (p ∨ q) ↔ p
    p ∨ (p ∧ q) ↔ p
    ```python
    # Python
    def absorcion_and(p, q):
        return (p and (p or q)) == p

    def absorcion_or(p, q):
        return (p or (p and q)) == p

    # Ejemplo
    print(absorcion_and(True, False))  # True
    print(absorcion_or(False, True))  # True
    ```
    ```r
    # R
    absorcion_and <- function(p, q) {
      return((p & (p | q)) == p)
    }

    absorcion_or <- function(p, q) {
      return((p | (p & q)) == p)
    }

    # Ejemplo
    print(absorcion_and(TRUE, FALSE))  # TRUE
    print(absorcion_or(FALSE, TRUE))  # TRUE
    ```

13. **Leyes de identidad**
    p ∧ True ↔ p
    p ∨ False ↔ p
    ```python
    # Python
    def identidad_and(p):
        return (p and True) == p

    def identidad_or(p):
        return (p or False) == p

    # Ejemplo
    print(identidad_and(False))  # True
    print(identidad_or(True))  # True
    ```
    ```r
    # R
    identidad_and <- function(p) {
      return((p & TRUE) == p)
    }

    identidad_or <- function(p) {
      return((p | FALSE) == p)
    }

    # Ejemplo
    print(identidad_and(FALSE))  # TRUE
    print(identidad_or(TRUE))  # TRUE
    ```

14. **Leyes de complemento**
    p ∧ ¬p ↔ False
    p ∨ ¬p ↔ True
    ```python
    # Python
    def complemento_and(p):
        return (p and not p) == False

    def complemento_or(p):
        return (p or not p) == True

    # Ejemplo
    print(complemento_and(True))  # True
    print(complemento_or(False))  # True
    ```
    ```r
    # R
    complemento_and <- function(p) {
      return((p & !p) == FALSE)
    }

    complemento_or <- function(p) {
      return((p | !p) == TRUE)
    }

    # Ejemplo
    print(complemento_and(TRUE))  # TRUE
    print(complemento_or(FALSE))  # TRUE
    ```

15. **Modus ponens**
    Si p → q es verdadero y p es verdadero, entonces q es verdadero
    ```python
    # Python
    def modus_ponens(p, q):
        return (implicacion(p, q) and p) == q

    # Ejemplo
    print(modus_ponens(True, True))  # True
    print(modus_ponens(True, False))  # False
    ```
    ```r
    # R
    modus_ponens <- function(p, q) {
      return((implicacion(p, q) & p) == q)
    }

    # Ejemplo
    print(modus_ponens(TRUE, TRUE))  # TRUE
    print(modus_ponens(TRUE, FALSE))  # FALSE
    ```

Estas son las 15 fórmulas para la sección de Lógica Matemática. ¿Deseas que continúe con la última sección de Series y Sucesiones?
Entendido. Continuaré con las 15 fórmulas para la sección de Series y Sucesiones:

## 10. Series y Sucesiones

1. **Suma de una serie aritmética**
   S_n = n(a_1 + a_n) / 2, donde a_1 es el primer término, a_n el último término y n el número de términos
   ```python
   # Python
   def suma_serie_aritmetica(a1, an, n):
       return n * (a1 + an) / 2

   # Ejemplo
   print(suma_serie_aritmetica(1, 100, 100))  # 5050.0
   ```
   ```r
   # R
   suma_serie_aritmetica <- function(a1, an, n) {
     return(n * (a1 + an) / 2)
   }

   # Ejemplo
   print(suma_serie_aritmetica(1, 100, 100))  # 5050
   ```

2. **Suma de una serie geométrica**
   S_n = a(1 - r^n) / (1 - r), donde a es el primer término, r es la razón y n es el número de términos
   ```python
   # Python
   def suma_serie_geometrica(a, r, n):
       if r == 1:
           return a * n
       return a * (1 - r**n) / (1 - r)

   # Ejemplo
   print(suma_serie_geometrica(1, 2, 5))  # 31.0
   ```
   ```r
   # R
   suma_serie_geometrica <- function(a, r, n) {
     if (r == 1) {
       return(a * n)
     }
     return(a * (1 - r^n) / (1 - r))
   }

   # Ejemplo
   print(suma_serie_geometrica(1, 2, 5))  # 31
   ```

3. **Término general de una sucesión aritmética**
   a_n = a_1 + (n - 1)d, donde a_1 es el primer término, n es la posición del término y d es la diferencia común
   ```python
   # Python
   def termino_general_aritmetica(a1, n, d):
       return a1 + (n - 1) * d

   # Ejemplo
   print(termino_general_aritmetica(2, 5, 3))  # 14
   ```
   ```r
   # R
   termino_general_aritmetica <- function(a1, n, d) {
     return(a1 + (n - 1) * d)
   }

   # Ejemplo
   print(termino_general_aritmetica(2, 5, 3))  # 14
   ```

4. **Término general de una sucesión geométrica**
   a_n = a_1 * r^(n-1), donde a_1 es el primer término, r es la razón y n es la posición del término
   ```python
   # Python
   def termino_general_geometrica(a1, r, n):
       return a1 * r**(n-1)

   # Ejemplo
   print(termino_general_geometrica(2, 3, 4))  # 54
   ```
   ```r
   # R
   termino_general_geometrica <- function(a1, r, n) {
     return(a1 * r^(n-1))
   }

   # Ejemplo
   print(termino_general_geometrica(2, 3, 4))  # 54
   ```

5. **Suma de los cuadrados de los primeros n números naturales**
   S_n = n(n+1)(2n+1) / 6
   ```python
   # Python
   def suma_cuadrados(n):
       return n * (n + 1) * (2*n + 1) // 6

   # Ejemplo
   print(suma_cuadrados(5))  # 55
   ```
   ```r
   # R
   suma_cuadrados <- function(n) {
     return(n * (n + 1) * (2*n + 1) %/% 6)
   }

   # Ejemplo
   print(suma_cuadrados(5))  # 55
   ```

6. **Suma de los cubos de los primeros n números naturales**
   S_n = (n(n+1)/2)^2
   ```python
   # Python
   def suma_cubos(n):
       return (n * (n + 1) // 2)**2

   # Ejemplo
   print(suma_cubos(4))  # 100
   ```
   ```r
   # R
   suma_cubos <- function(n) {
     return((n * (n + 1) %/% 2)^2)
   }

   # Ejemplo
   print(suma_cubos(4))  # 100
   ```

7. **Serie armónica**
   H_n = 1 + 1/2 + 1/3 + ... + 1/n
   ```python
   # Python
   def serie_armonica(n):
       return sum(1/i for i in range(1, n+1))

   # Ejemplo
   print(serie_armonica(5))  # 2.283333333333333
   ```
   ```r
   # R
   serie_armonica <- function(n) {
     return(sum(1 / 1:n))
   }

   # Ejemplo
   print(serie_armonica(5))  # 2.283333
   ```

8. **Números de Fibonacci**
   F_n = F_(n-1) + F_(n-2), con F_0 = 0 y F_1 = 1
   ```python
   # Python
   def fibonacci(n):
       if n <= 1:
           return n
       a, b = 0, 1
       for _ in range(2, n+1):
           a, b = b, a + b
       return b

   # Ejemplo
   print(fibonacci(7))  # 13
   ```
   ```r
   # R
   fibonacci <- function(n) {
     if (n <= 1) return(n)
     a <- 0
     b <- 1
     for (i in 2:n) {
       c <- a + b
       a <- b
       b <- c
     }
     return(b)
   }

   # Ejemplo
   print(fibonacci(7))  # 13
   ```

9. **Números triangulares**
   T_n = n(n+1) / 2
   ```python
   # Python
   def numero_triangular(n):
       return n * (n + 1) // 2

   # Ejemplo
   print(numero_triangular(5))  # 15
   ```
   ```r
   # R
   numero_triangular <- function(n) {
     return(n * (n + 1) %/% 2)
   }

   # Ejemplo
   print(numero_triangular(5))  # 15
   ```

10. **Números de Catalan**
    C_n = (1 / (n+1)) * C(2n,n)
    ```python
    # Python
    import math

    def catalan(n):
        return math.comb(2*n, n) // (n + 1)

    # Ejemplo
    print(catalan(4))  # 14
    ```
    ```r
    # R
    catalan <- function(n) {
      return(choose(2*n, n) %/% (n + 1))
    }

    # Ejemplo
    print(catalan(4))  # 14
    ```

11. **Serie geométrica infinita**
    S_∞ = a / (1 - r), donde |r| < 1
    ```python
    # Python
    def serie_geometrica_infinita(a, r):
        if abs(r) >= 1:
            return None
        return a / (1 - r)

    # Ejemplo
    print(serie_geometrica_infinita(1, 0.5))  # 2.0
    ```
    ```r
    # R
    serie_geometrica_infinita <- function(a, r) {
      if (abs(r) >= 1) {
        return(NULL)
      }
      return(a / (1 - r))
    }

    # Ejemplo
    print(serie_geometrica_infinita(1, 0.5))  # 2
    ```

12. **Suma de los primeros n términos de una progresión aritmética-geométrica**
    S_n = a(1-r^n)/(1-r) + d(r-r^n)/((1-r)^2), donde a es el primer término, r es la razón geométrica y d es la diferencia aritmética
    ```python
    # Python
    def suma_aritmetica_geometrica(a, r, d, n):
        if r == 1:
            return a*n + d*n*(n-1)/2
        return a*(1-r**n)/(1-r) + d*(r-r**n)/((1-r)**2)

    # Ejemplo
    print(suma_aritmetica_geometrica(1, 2, 1, 5))  # 57.0
    ```
    ```r
    # R
    suma_aritmetica_geometrica <- function(a, r, d, n) {
      if (r == 1) {
        return(a*n + d*n*(n-1)/2)
      }
      return(a*(1-r^n)/(1-r) + d*(r-r^n)/((1-r)^2))
    }

    # Ejemplo
    print(suma_aritmetica_geometrica(1, 2, 1, 5))  # 57
    ```

13. **Números de Stirling de primera especie**
    s(n,k) = s(n-1,k-1) - (n-1)s(n-1,k)
    ```python
    # Python
    def stirling_primera_especie(n, k):
        if n == k == 0:
            return 1
        if n > 0 and k == 0:
            return 0
        if k > n:
            return 0
        return stirling_primera_especie(n-1, k-1) - (n-1) * stirling_primera_especie(n-1, k)

    # Ejemplo
    print(stirling_primera_especie(5, 2))  # 50
    ```
    ```r
    # R
    stirling_primera_especie <- function(n, k) {
      if (n == 0 && k == 0) return(1)
      if (n > 0 && k == 0) return(0)
      if (k > n) return(0)
      return(stirling_primera_especie(n-1, k-1) - (n-1) * stirling_primera_especie(n-1, k))
    }

    # Ejemplo
    print(stirling_primera_especie(5, 2))  # 50
    ```

14. **Números de Bell**
    B_n = Σᵏ₌₀ⁿ S(n,k), donde S(n,k) son los números de Stirling de segunda especie
    ```python
    # Python
    def bell_number(n):
        if n == 0 or n == 1:
            return 1
        bell = [[0 for i in range(n+1)] for j in range(n+1)]
        bell[0][0] = 1
        for i in range(1, n+1):
            bell[i][0] = bell[i-1][i-1]
            for j in range(1, i+1):
                bell[i][j] = bell[i-1][j-1] + bell[i][j-1]
        return bell[n][0]

    # Ejemplo
    print(bell_number(5))  # 52
    ```
    ```r
    # R
    bell_number <- function(n) {
      if (n == 0 || n == 1) return(1)
      bell <- matrix(0, nrow=n+1, ncol=n+1)
      bell[1,1] <- 1
      for (i in 2:(n+1)) {
        bell[i,1] <- bell[i-1,i-1]
        for (j in 2:i) {
          bell[i,j] <- bell[i-1,j-1] + bell[i,j-1]
        }
      }
      return(bell[n+1,1])
    }

    # Ejemplo
    print(bell_number(5))  # 52
    ```

15. **Serie de Taylor**
    f(x) ≈ Σᵏ₌₀ⁿ (f^(k)(a)/k!) * (x-a)^k
    ```python
    # Python
    import math

    def taylor_series(f, a, x, n):
        result = 0
        for k in range(n+1):
            result += (f(k, a) / math.factorial(k)) * (x - a)**k
        return result

    # Ejemplo: e^x alrededor de x=0
    def exp_deriv(k, a):
        return math.exp(a)

    print(taylor_series(exp_deriv, 0, 1, 5))  # 2.7166666666666663
    ```
    ```r
    # R
    taylor_series <- function(f, a, x, n) {
      result <- 0
      for (k in 0:n) {
        result <- result + (f(k, a) / factorial(k)) * (x - a)^k
      }
      return(result)
    }

    # Ejemplo: e^x alrededor de x=0
    exp_deriv <- function(k, a) {
      return(exp(a))
    }

    print(taylor_series(exp_deriv, 0, 1, 5))  # 2.708333
    ```
