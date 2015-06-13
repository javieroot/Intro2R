

INTRODUCCIÓN AL MANEJO DE DATOS Y PROGRAMACIÓN EN R
========================================================
width: 1366
height: 768
font-family: 'Serif'
author: Gustavo A. Ballen

Museu de Zoologia da Universidade de São Paulo

gaballench@gmail.com

========================================================
# SCRIPTS INFORMÁTICOS Y CÓMO OBTENER AYUDA SOBRE R

========================================================
# SCRIPTS INFORMÁTICOS

========================================================
# AYUDA!!!

Por qué es importante obtener ayuda?
========================================================

* Cualquier herramienta informática requiere de un trabajo extensivo de documentación para los usuarios, y R tiene una documentación INMENSA!
* La mayoría de la documentación proviene de la comunidad de usuarios misma, lo cual es común en proyectos de software libre (+1 para el software libre)
* Como toda herramienta de programación o análisis basado en comandos, la probabilidad de obtener errores por algún caracter faltante (e.g., una coma) es alta
* Durante la primera etapa de aprendizaje del lenguaje es muy común cometer errores de toda índole, desde errores tipográficos hasta errores de comprensión de estructura de objetos

Qué opciones tenemos cuando necesitamos ayuda?
========================================================

* Entre los materiales disponibles encontramos manuales, libros, tutoriales en video y texto, cursos gratis, cursos pagos, foros, faqs, y un inmenso etcétera
* Un aspecto importante es saber qué tan compĺicado es el problema que estamos teniendo para así elegir la fuente de ayuda más apropiada
* Es muy importante no solo saber dónde encontrar ayuda, sino cómo pedirla

Documentación básica: CRAN
========================================================

* Como ya vimos, disponible en http://cran.r-project.org/
* Aparte de ser el repositorio oficial del proyecto R, contiene una extensa lista de recursos de aprendizaje y la documentación oficial de R

<center><img src="HelpAndScripts-figure/cran.png"
        height="450px"/></center>

Documentación básica: CRAN (Manuales)
========================================================

<center><img src="HelpAndScripts-figure/cranmanuals.png"
        height="500px"/></center>

Documentación básica: CRAN (FAQS [frequently-asked questions])
========================================================

<center><img src="HelpAndScripts-figure/cranfaqs.png"
        height="500px"/></center>


Documentación básica: CRAN (Materiales contribuidos)
========================================================

<center><img src="HelpAndScripts-figure/crancontrib.png"
        height="500px"/></center>

R-project: Listas de correo
========================================================

* http://www.r-project.org/mail.html
* A estas listas de correo se pueden enviar preguntas y/o respuestas sobre R. Hay diferentes listas temáticas donde las preguntas se concentran en R aplicado a campos especiales de análisis (e.g., R-SIG-ecology sobre R aplicado a ecología)

<center><img src="HelpAndScripts-figure/mailing.png"
        height="350px"/></center>

StackOverflow.com
========================================================

* Portal social online para preguntas y respuestas relacionadas principalmente con tecnología, pero expandiéndose a otros temas tales como cultura y artes
* Podría pensarse en este como el "Yahoo respuestas" de la tecnología (incluyendo programación, lenguajes y muchos otros temas) pero sin la inmensa cantidad de preguntas cómicas que se encuentran en aquella página de yahoo.
* Presenta un cuidado serio de la comunidad, de modo que preguntas fuera de contexto o duplicadas son rápidamente marcadas y modificadas para mantener la limpieza del portal
* Disponible en http://stackoverflow.com

StackOverflow.com
========================================================

<center><img src="HelpAndScripts-figure/stackpage.png"
        height="500px"/></center>

StackOverlow.com: Cómo funciona?
========================================================

* Como algunos recursos online, tenemos que abrir una cuenta para realizar preguntas o enviar respuestas
* Si queremos solamente leer preguntas y respuestas hechas por otras personas, podemos tener acceso a estas sin necesidad de tener una cuenta
* Realizamos una pregunta _de manera adecuada_ y asociando etiquetas a la misma, de tal forma que el portal sea capaz de organizar las preguntas en categorías y así permitir a la comunidad enfocarse en asuntos relacionados con una situación particular, ya sea un sistema operativo, leguaje de programación, tipo de análisis, etc.
* En la barra superior de la página encontramos un cuadro de texto para realizar búsquedas; antes de preguntar ___siempre___ buscar por palabras clave allí para estar seguros de que lo que vamos a preguntar no ha sido preguntado antes

StackOverlow.com: Estructura de preguntas
========================================================

<center><img src="HelpAndScripts-figure/qso.png"
        height="500px"/></center>

StackOverlow.com: Estructura de respuestas
========================================================

<center><img src="HelpAndScripts-figure/aso.png"
        height="500px"/></center>

StackOverlow.com: Estructura de respuestas
========================================================

<center><img src="HelpAndScripts-figure/aso2.png"
        height="500px"/></center>


R project en español (Facebook)
========================================================

<center><img src="HelpAndScripts-figure/rfb.png"
        height="500px"/></center>

R project en español
========================================================

<center><img src="HelpAndScripts-figure/goodqrfb.png"
        height="600px"/></center>

Por último y la más importante... Google
========================================================

* La maravilla más grande de las tecnologías de la información en el S. XXI
* Ni la patineta voladora de Marty McFly es tan sensacional como google
* No existe libro, profesor, o tutorial que se le compare
* Disponible en https://www.google.com

Google.com
========================================================

<center><img src="HelpAndScripts-figure/google.png"
        height="500px"/></center>

Google.com
========================================================

<center><img src="HelpAndScripts-figure/googleanova.png"
        height="600px"/></center>

Cómo hacer buenas preguntas?
========================================================

* El arte de preguntar es algo que parece obvio pero la experiencia indica que no lo es
* Consiste en un conjunto de reglas sencillas que mezclan un poco de asertividad, creatividad, y modales
* Hay diferentes listas de normas para enviar mensajes en foros y listas de correo, las cuales deberían por sentido común aplicar a otras situaciones como grupos de facebook, sin embargo, esto no sucede... ni siquiera en las listas de correo oficiales de R

Manuales para usar listas/foros
========================================================

* http://www.r-project.org/posting-guide.html
* http://stackoverflow.com/help/how-to-ask (y referencias en esa página)


"How to ask questions the smart way"
========================================================

* http://www.catb.org/~esr/faqs/smart-questions.html
* Un sumario del contenido es

        + Before You Ask
        + When You Ask
        + How To Interpret Answers
        + On Not Reacting Like A Loser
        + Questions Not To Ask
        + Good and Bad Questions
        + If You Can't Get An Answer
        + How To Answer Questions in a Helpful Way

Y dentro de R... Cómo obtener ayuda?
========================================================

* Las funciones `help()` y `example()` permiten abrir dos componentes importantes de la documentación de una función o paquete: El archivo de documentación como tal, y ejemplos de código haciendo uso de dichas funciones
* Los operadores `?` y `??` son abreviaturas de las funciones `help()` y `help.search()`, que permiten buscar tópicos tales como funciones o palabras clave sobre procedimientos de interés. La primera de estas funciones requiere que el objeto sobre el cual queremos buscar información tenga el nombre exacto de un objeto (e.g., una función o paquete). La segunda de estas funciones es útil para extender la búsqueda a páginas de ayuda sobre temas no tan específicos (por ejemplo temas o procedimientos, digamos, varianza, especies, etc.)

Ayuda en R
========================================================


```r
# Todos estos son métodos equivalentes
help(aov) # Debe ser un nombre de objeto o estar en el nombre del archivo de ayuda 
help("aov") # Puede usarse entre comillas
?aov # Versión simplificada de la misma función
?"aov" # También permite usar comillas para realizar búsqueda
```


```r
# Estos dos son métodos equivalentes. Note que no existe ningún objeto de R llamado "variance"
help.search("variance") # Puede ser un término no incluido en el título del archivo de ayuda. Debe encontrarse entre comillas
??"variance" # Versión simplificada de la misma función. Debe estar entre comillas
```

Cómo NO hacer preguntas
========================================================

<center><img src="HelpAndScripts-figure/badq1.png"
        height="150px"/></center>

<center><img src="HelpAndScripts-figure/badq4.png"
        height="100px"/></center>

========================================================

<center><img src="HelpAndScripts-figure/badq2.png"
        height="600px"/></center>

========================================================

<center><img src="HelpAndScripts-figure/badq3.png"
        height="700px"/></center>


========================================================



========================================================



========================================================


