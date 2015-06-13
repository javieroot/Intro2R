

INTRODUCCIÓN AL MANEJO DE DATOS Y PROGRAMACIÓN EN R: PRÁCTICA 2
========================================================
font-family: 'Serif'
width: 1366
height: 768
author: Gustavo A. Ballen

Museu de Zoologia da Universidade de São Paulo

gaballench@gmail.com

========================================================
# LLEGÓ LA HORA DE SEPARAR LOS NIÑOS DE LOS HOMBRES!

Aplicación de funciones, estr. de control y simulación
========================================================

_Problema_: Queremos estudiar la relación entre el tamaño de muestra y la dispersión, debido a que usualmente se nos dice que tamaños de muestra pequeños pueden sobrestimar o subestimar la variabilidad de los datos de una población. Básicamente queremos respondar la pregunta: Cuál es el comportamiento que presenta la desviación estandar conforme aumentamos el tamaño de muestra?

Aplicación de funciones, estr. de control y simulación
========================================================

* Este problema requiere las tres herramientas esudiadas en esta sesión: Funciones, estructuras de control, y simulación.
* En primer lugar, debemos programar las funciones de interés: Una que calcule la media de un vector de datos numéricos, y otra que calcule la desviación estándar _muestral_. Las formulas se describen a continuación. Por favor note que el siguiente es pseudocódigo que se presenta solamente como una ayuda para programar sus propias funciones, no es código válido en R:


```r
media = (suma_de_los_valores_del_vector)/cantidad_de_valores
varianza = (1/(n-1))*sumatoria(valor - media)^2 # En esta función debe usar su función para calcular la media, no aquella ofrecida internamente en R
desvest = raiz_cuadrada(varianza)
```

Paso 0: Población de datos
========================================================

* Necesitamos una población de datos para poder realizar nuestras simulaciones
*Para ello usaremos un vector de un millón de datos aleatorios provenientes de una distribución normal y asumiremos que estos son todos los datos de una población de interés
* Este paso hace parte de la simulación, pues estamos realizando un experimento hipotético con datos aleatorios



```r
pob <- rnorm(1000000)
```

Paso 1: Funciones de media y sd
========================================================

* Acá encontramos una plantilla para crear nuestras funciones, una para la media y otra para la desviación estándar
* Use las sugerencias de pseudocódigo presentadas anteriormente para ayudarse en el proceso de generar sus propias funciones



```r
media <- function() {
        # Acá va el cuerpo de la función
}

desvest <- function() {
        # Acá va el cuerpo de la función
}
```

Paso 2: Estructuras de control
========================================================

* Dentro de las estructuras de control vistas (i.e., if-else, for, while, repeat) identifique aquella adecuada para operar sobre un _número determinado_ de vectores y en cada _iteración_ calcular la desviación estándar de cada vector de valores numéricos


Paso 3: Simulación
========================================================

* Usando sus funciones y el prototipo de estructuras de control adecuado, obtenga a partir de la población de datos `pob` muestras aleatorias de 5, 10, 50, 100, 1000 y 10000 datos (sugerencia: fabrique un vector con el número de elementos a sacar de la muestra)
* Una vez obtenidas estas muestras, calcule la desviación estándar muestral de las mismas usando la función `desvest` que acabó de programar
* Una sugerencia es crear un objeto donde usted guardará valores importantes en cada iteración. Estos objetos deben ser creados _antes_ de la estructura de control y deben ser modificados _dentro_ de la estructura de control
* Grafique un scatterplot de dichos valores para explorar visualmente alguna tendencia en el comportamiento de la desviación estándar muestral

========================================================
# SOLUCIÓN PROPUESTA

Pasos 0 y 1
========================================================


```r
pob <- rnorm(1000000)
tam <- c(5, 10, 50, 100, 1000, 10000)

media <- function(vector) {
        sum(vector)/length(vector)
}

varianza <- function(vector) {
        (1/(length(vector) - 1))*sum((vector - media(vector))^2)
}

desvest <- function(vector) {
        sqrt(varianza(vector))
}
```

Pasos 2 y 3
========================================================


```r
valores <- vector()

for(i in seq_along(tam)) {
        muestra <- sample(x = pob, size = tam[i])
        valor <- desvest(muestra)
        valores <- c(valores, valor)
}
valores
```

```
[1] 1.0695163 0.7144429 0.9434248 0.9735456 0.9931959 0.9881171
```

Paso 3
========================================================


```r
plot(valores)
```

***

![plot of chunk unnamed-chunk-7](Session2Practice-figure/unnamed-chunk-7-1.png) 
