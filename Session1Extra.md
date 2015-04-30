

INTRODUCCIÓN AL MANEJO DE DATOS Y PROGRAMACIÓN EN R
========================================================
width: 1366
height: 768
font-family: 'Serif'
author: Gustavo A. Ballen

Museu de Zoologia da Universidade de São Paulo

gaballench@gmail.com



========================================================
# ESTRUCTURA DE OBJETOS EN R

Recordando cosas básicas
========================================================

* `R` es un dialecto que hace un uso fuerte de objetos, los cuales tienen propiedades caracteristicas
* Los tres componentes más importantes de cualquier objeto son clase, nombre y dimensiones. Otros componentes tales como los atributos no son comunes a todos los tipos de objetos posibles en `R`.
* Todos los objetos en R comparten estas caracteristicas

Recordando cosas básicas
========================================================

Objeto | Homogeneo? | dim() | length()
-------|------------|-------|---------
vector | Si | NULL* | n
matrix | Si | nrow ncol | nrow + ncol
array | Si | x y x | x + y + z 
data.frame | No | nrow ncol | nrow + ncol
list | No | NULL* | n


```r
m <- matrix(1:4, nrow = 2, ncol = 2)
m # print(m)
length(m) # nrow + ncol
dim(m) # nrow ncol
```

***

* El asterisco (\*) asociado a las dimensiones de vectores atómicos y listas indica que este resultado sale de llamar la función dim() sobre ellos. Sin embargo, son elementos de dimensión 1. 


```
     [,1] [,2]
[1,]    1    3
[2,]    2    4
```

```
[1] 4
```

```
[1] 2 2
```

Accesando y modificando la estructura interna de cuaquier objeto
========================================================

* Pensemos en los objetos como "cajas" que guardan los componentes de estos
* Las dimensiones dependerán de la forma de la caja, así como los elementos que pueda guardar y en qué forma
* En `R` podemos tener acceso a cualquier parte de la caja, a una porción de esta, o a la todalidad de sus elementos
* Si pensamos en los objetos de la siguiente forma es más fácil entender la forma de obtener acceso a sus elementos...

Objetos análogos a aquellos de R
========================================================

* Vector

<center><img src="Session1Extra-figure/vectorPlatos.jpg"
        height="500px"/></center>

Objetos análogos a aquellos de R
========================================================

* Matrix

<center><img src="Session1Extra-figure/matrixTazas.jpg"
        height="500px"/></center>

Objetos análogos a aquellos de R
========================================================

* Data Frame

<center><img src="Session1Extra-figure/dfCDs.jpg"
        height="500px"/></center>

Objetos análogos a aquellos de R
========================================================

* Lista

<center><img src="Session1Extra-figure/listArmario.jpg"
        height="500px"/></center>

Operadores de subconjuntos, concepto de índice
========================================================

* Estos operadores nos permiten tener acceso a partes de un objeto
* Su uso depende de la estructura del objeto, por lo que algunos funcionan en algunas clases y otros no
* Son supremamente poderosos en conjunto con operadores lógicos y funciones como which()
Son una de las bases de la programación en `R`, por lo que su aprendizaje es obligatorio antes de iniciar temáticas más complejas
* Sirven también para cortar y crear otros objetos
* Los índices son el puesto que ocupa un elemento particular dentro de un objeto
* Son una de las fuentes de error más comunes entre principiantes!

Índices en vectores
========================================================

* En objetos unidimensionales (vectores, listas) el índice es un solo número, corresponde con el lugar dentro del objeto de cada elemento
* Todo índice debe ser puede ser uno de cinco tipos: entero positivo, entero negativo, elemento lógico (TRUE o FALSE), ningún valor, y cero (0)
* Los positivos indican "aquel elemento", los negativos "sin aquel elemento", y los lógicos aquel o sin aquel dependiendo de si son TRUE o FALSE respectivamente, mientras que ningún valor selecciona todo el objeto y 0 ninguno

Índices en vectores
========================================================

* Supongamos que tenemos un vector con cinco letras:


```r
letras <- c("a", "c", "z", "a", "r") # "a" es 1, "c" es 2, ... "r" es 5
```

* Por medio de los índices enteros positivos o los valores lógicos TRUE podemos tener acceso y, por ejemplo, modificar o imprimir cualquiera de ellos diciéndole a `R` qué índice tiene el elemento que queremos ver o modificar
* Con enteros negativos o FALSE le decimos a R que NO queremos ver o modificar dicho elemento
* Con índice vacío obtenemos el elemento original
* Con índice 0 obtenemos un elemento vacío

Índices en objetos multidimensionales
========================================================

* Los objetos multidimensionales como matrices, data frames y arrays también tienen índices, pero en estos casos también pueden corresponder con nombres si es que las dimensiones del objeto tienen nombres


```r
df <- data.frame(a = 1:5, 
                 b = c("a", "b", "c", "b", "e"), 
                 d = c(T, F, F, T, F))
```

***


```r
df
```

```
  a b     d
1 1 a  TRUE
2 2 b FALSE
3 3 c FALSE
4 4 b  TRUE
5 5 e FALSE
```

```r
names(df)
```

```
[1] "a" "b" "d"
```

Índices en objetos multidimensionales
========================================================

* Podemos tener acceso a cada elemento dentro de un objeto multidimensional por medio de los índices de cada dimensión que corresponden a dicho elemento, algo análogo a sus coordenadas dentro del objeto


```r
m # Las coordenadas del número 4 son [2, 2], las del elemento correspondiente al número 3 son [1, 2]
```

```
     [,1] [,2]
[1,]    1    3
[2,]    2    4
```

Operadores de subconjuntos: [] en vectores
========================================================

* Da como resultado un objeto de la misma clase que el original. Por ejemplo, un subconjunto de un vector character da un vector character también
* Soporta la selección de más de un elemento. En objetos unidimensionales 
* Su sintaxis en objetos unidimensionales es `objeto[indice(s)]`. Es decir, en `objeto` seleccionar el(los) elemento(s) `índice(s)`.


```r
vector[3] # Seleccionar el elemento 3
vector[c(1, 2, 3, 5)] # Los elementos 1, 2, 3, y 5
vector[4:8] # Los elementos 4 a 8 (4, 5, 6, 7, 8)
vector[c(1, 4:9)] # los elementos 1 y 4 a 9 (1, 4, 5, 6, 7, 8, 9)
```

* Para seleccionar más de un elemento no consecutivo debe usarse la función c() para que R sepa que debe concatenar los índices y así obtener dichos valores

Operadores de subconjuntos: [] en arreglos
========================================================

* Funciona como un sistema de coordenadas. Su sintaxis es de la forma `arreglo[hileras, columnas]` para objetos bidimencionales; arreglo[a, b, c] para arreglos tridimensionales, y en general [a, b, c, ..., n] para arreglos n-dimensionales


```r
matrix[2, 3] # Seleccione el elemento en la hilera 2 y la columna 3
matrix[1:5, 4] # En las hileras 1 a 5 y columna 4
matrix[, 4] # Todas las hileras en la columna 4
matrix[c(1, 3, 4), c(5, 7)] # En las hileras 1, 3 y 4, y las columnas 5 y 7
array[3, 6, 5] # El elemento en la posición 3 de dim1, 6 de dim2 y 5 de dim3
```

Operadores de subconjuntos: [] sin índ. ent. pos.
========================================================



* Ejemplos con índice negativo


```r
vector
```

```
[1] "a" "b" "c" "d" "e"
```

```r
a <- vector[-c(3:5)]
a
```

```
[1] "a" "b"
```

```r
class(a)
```

```
[1] "character"
```

***

* Ejemplos con índice lógico


```r
vector
```

```
[1] "a" "b" "c" "d" "e"
```

```r
a <- vector[c(TRUE, FALSE, FALSE, TRUE, TRUE)]
a
```

```
[1] "a" "d" "e"
```

```r
class(a)
```

```
[1] "character"
```

Operadores de subconjuntos: [] en arreglos
========================================================

* Ejemplos con índice vacío


```r
vector
```

```
[1] "a" "b" "c" "d" "e"
```

```r
a <- vector[]
a
```

```
[1] "a" "b" "c" "d" "e"
```

```r
class(a)
```

```
[1] "character"
```

***

* Ejempĺos con índice cero


```r
vector
```

```
[1] "a" "b" "c" "d" "e"
```

```r
a <- vector[0]
a
```

```
character(0)
```

```r
class(a)
```

```
[1] "character"
```

Operadores de subconjuntos: [[]]
========================================================

* Similar al operador [ pero más restrictivo en cuanto a la cantidad de índices, pues solo acepta UNO por dimensión. No soporta
* Devuelve un elemento de clase diferente al objeto original cuando es necesario (e.g., en clases y data frames)
* Tiene la misma sintaxis que [ en vectores unidimensionales y bidimensionales

***

<small style="font-size:.7em">

```r
d <- vector[[1]] # El elemento 1 en el objeto vector
d
```

```
[1] "a"
```

```r
class(d) # Clase igual pues es un vector atómico
```

```
[1] "character"
```

```r
dd <- m[[1, 2]] # El elemento en hilera 1 y columna 2 en la matrix m 
dd
```

```
[1] 3
```

```r
class(dd) # Clase diferente, original fue matrix, esta es integer
```

```
[1] "integer"
```
</small>

Operadores de subconjuntos: [[]]
========================================================

* El operador [[ soporta una propiedad interesante y es la de simplificar el resultado, esto es, devolver la estructura más simple del objeto resultante
* Por ejemplo, vector[3] no simplifica, pues revuelve un elemento con todas las propiedades del objeto inicial, incluyendo clase y atributos. En contraste, vector[[3]] simplifica devolviendo solamente el elemento con la mínima estructura posible, es decir, clase.

***



<small style="font-size:.7em">

```r
dd <- lst[1] # lst es una lista
dd
```

```
$m
[1] 1 2 3
```

```r
class(dd) # Preserva clase y atributos como nombres
```

```
[1] "list"
```

```r
dd <- lst[[1]] # lst es una lista
dd
```

```
[1] 1 2 3
```

```r
class(dd) # No preserva clase ni atributos
```

```
[1] "numeric"
```
</small>

Operadores de subconjuntos: $
========================================================

* Es una versión simplificada para [[ para índices con nombre.
* Sin embargo presenta dos propiedades muy diferentes: Primero, permite concordancia parcial (e.g., "d" como versión simplificada de "distancia"), y segundo, permite seleccionar elementos de longitud mayor a 1 en data frames
* Es muy utilizada en objetos como data frames y listas, que con frecuencia tienen elementos o columnas nombradas

Operadores de subconjuntos: $
========================================================


```r
df # data frame con columnas a, b y d
```

```
  a b     d
1 1 a  TRUE
2 2 b FALSE
3 3 c FALSE
4 4 b  TRUE
5 5 e FALSE
```

```r
df$a # columna con nombre a
```

```
[1] 1 2 3 4 5
```

```r
df$d # columna con nombre d
```

```
[1]  TRUE FALSE FALSE  TRUE FALSE
```

***


```r
class(lst)
```

```
[1] "list"
```

```r
lst$m
```

```
[1] 1 2 3
```

```r
class(lst$m) # mismo comportamiento que [[ con respecto a clases
```

```
[1] "numeric"
```

Operadores de subconjuntos: Modificación
========================================================

* Uno de los usos más poderosos de los operadores de subconjuntos es la modificación de elementos dentro de un objeto. Usando el operador de asignación apuntando a un subconjunto podemos agregar o eliminar valores de interés


```r
vector
```

```
[1] "a" "b" "c" "d" "e"
```

```r
vector[2] <- "b de bebe" # Cambio de el segundo elemento en vector
vector <- vector[-1] # Convertir el objeto en el mismo pero sin el primer elemento
vector
```

```
[1] "b de bebe" "c"         "d"         "e"        
```