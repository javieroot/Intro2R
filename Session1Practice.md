

INTRODUCCIÓN AL MANEJO DE DATOS Y PROGRAMACIÓN EN R: PRÁCTICA 1
========================================================
font-family: 'Serif'
author: Gustavo A. Ballen
Museu de Zoologia da Universidade de São Paulo
gaballench@gmail.com


Práctica 1: Temas 1-3
=======================================================

1. Cree una variable llamada `saludo`. Asigne a esta variable la frase `"Hola mundo de R! Llegué para quedarme"` usando el operador `<-`. Compare la presentación del valor de dicha variable con dos métodos: `print(saludo)` y `saludo`. Encuentra alguna diferencia entre ambos métodos?.

2. Indique la clase (i.e., el tipo de datos que contiene) de dicha variable. Use las funciones `class()` o `str()`; encuentra alguna diferencia entre la información obtenida por ambos métodos?.

3. Asigne el valor `5` a una variable `x`. Asigne el valor `5L` a una variable `y`. Observe ahora el valor de cada variable. Son diferentes? Verifique la clase de cada objeto. Son diferentes?


Práctica 1: Temas 1-3
=======================================================

4. Cree un objeto de las siguientes clases y llámelo como prefiera: `"character"`, `"integer"`, `"numeric"`, `"logical"`, `"complex"` (lo mismo que imaginario). TODOS deben ser de longitud `1`; Verifique la clase de cada objeto con las funciones que ya conoce. Alternativamente puede probar con `is.'clase_particular'('objeto')` (e.g., `is.integer(x)`)

5. Cree un objeto con los números enteros del 1 al 5. Puede hacerlo por medio de la función `c()`, que `c`oncatena elementos en un vector. (Sugerencias: Escriba 1, 2, ..., 5 en dicha función, o asigne el valor de 1:5 a este. Los resultados difieren?)


Práctica 1: Temas 1-3 [NO CORRER ANTES DE RESPONDER!]
=======================================================

7. Cuál es el resultado de la siguiente operación: `x + 2` dado que `x <- 1:10`. Cuál será el resultado de `y * 2` dado que `y <- 1:10`. Por qué se observan esos resultados?

8. Dados los vectores `x` y `y` arriba, cuál es el tamaño del vector `z` resultante de la siguiente línea de código: `z <- x + y`. Hay alguna diferencia con `z <- c(x, y)`? Si es así, cuál es el tamaño del vector resultante?

Práctica 1: Temas 1-3
=======================================================

1. Cree el siguiente objeto `matriz <- cbind(a = 1:10, b = 11:20, c = 21:30, d = 31:40)`. Ahora agregue una columna adicional de 10 valores de clase `integer`. Es importante que sean de la misma clase pues estamos creando una matriz y no un data frame. Cuáles son las dimensiones de ese objeto?

2. Cree ahora un data frame con el siguiente código `df <- data.frame(a = 1:10, b = c("a", "b", "c", "b", "e", "f", "g", "h", "i", "j"), d = c(T, F, F, T, F, T, T, T, F, F))`. Es igual usar la función `cbind()` o `data.frame()` para crear un objeto con columnas de diferentes clases? Por qué? Verifique corriendo esa misma línea de código pero usando la función `cbind` en vez de `data.frame`.

=======================================================

=======================================================

3. Vamos a crear nuestra primera lista con la línea `lista <- list(x, y, z, matriz, df)`. Observe el contenido de ese objeto llamado lista. En qué difiere con respecto a los objetos creados por usted hasta el momento?

=======================================================

6. Cuál va a ser el resultado de estas expresiones lógicas?

+ 2 < 3
+ 2 > 3
+ 0 <= 1
+ 1 <= 1
+ 1 >= -1
+ 3 == 3
+ 3 != 3
+ f  <- 5; 6 != !f

***

+ 6 == 5 | 8
+ 7 != 7 & 7
+ isTRUE(class("Programar en r es útil"))
+ 2 + 3 == "Cinco"
+ "Dos + Tres" == "Cinco"
+ 2 + 3 == 5
+ 5**2 != 100/4
+ is.character(TRUE)
+ is.character("TRUE")
+ is.complex(3+1i)



=======================================================




=======================================================




=======================================================




=======================================================




=======================================================




=======================================================




=======================================================




=======================================================




=======================================================




=======================================================

=======================================================
# FUNCIONES, ESTRUCTURAS DE CONTROL, E INTRODUCCIÓN A LA SIMULACIÓN

Funciones (programación)
=======================================================
* Si hay una tarea de debemos repetir, tal vez sea buena idea crear una función que automatice dicha tarea
* Presentan cuatro componentes: nombre, argumentos, cuerpo y ambiente
