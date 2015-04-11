

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

3. Asigne el valor 5 a una variable x. Asigne el valor 5L a una variable y. Observe ahora el valor de cada variable. Son diferentes? Verifique la clase de cada objeto. Son diferentes?


Práctica 1: Temas 1-3
=======================================================

4. Cree un objeto de las siguientes clases y llámelo como prefiera: `"character"`, `"integer"`, `"numeric"`, `"logical"`, `"complex"` (lo mismo que imaginario). TODOS deben ser de longitud `1`; Verifique la clase de cada objeto con las funciones que ya conoce. Alternativamente puede probar con `is.'clase_particular'('objeto')` (e.g., `is.integer(x)`)

5. Cree un objeto con los números enteros del 1 al 5. Puede hacerlo por medio de la función `c()`, que `c`oncatena elementos en un vector. (Sugerencias: Escriba 1, 2, ..., 5 en dicha función, o asigne el valor de 1:5 a este. Los resultados difieren?)


Práctica 1: Temas 1-3
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
+ "Dos" + "Tres" == "Cinco"
+ 5**2 != 100/4
+ is.character(TRUE)
+ is.character("TRUE")
+ is.complex(3 + i)


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




=======================================================

=======================================================
# FUNCIONES, ESTRUCTURAS DE CONTROL, E INTRODUCCIÓN A LA SIMULACIÓN

Funciones (programación)
=======================================================
* Si hay una tarea de debemos repetir, tal vez sea buena idea crear una función que automatice dicha tarea
* Presentan cuatro componentes: nombre, argumentos, cuerpo y ambiente
