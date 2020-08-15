---
# Por favor no edites este archivo directamente; este se genera automáticamente.
# en su lugar, por favor edita 03-data-structures-part1.md in _episodes_rmd/
title: "Estructura de datos"
teaching: 40
exercises: 15
questions:
- "¿Cómo puedo leer datos en R?"
- "¿Cuáles son los tipos de datos básicos en R?"
- "¿Cómo puedo representar información categórica en R?"
objectives:
- "Conocer los distintos tipos de datos."
- "Iniciar a explorar data frames, y entender como están relacionados con los vectores, factores y listas."
- "Ser capaz de hacerle preguntas a R sobre el tipo, la clase y la estructura de un objeto."
keypoints:
- "Usar `read.csv` para leer datos tabulados desde R."
- "Los tipos de datos fundamentales en R son dobles, enteros, complejos, lógicos y caracteres."
- "Usar factores para representar categorías en R."
source: Rmd
---



Uno de las características más poderosas de R es su capacidad de manejar datos tabulados - 
como los que tal vez ya tengas en una hoja de cálculo o un archivo CSV.
Empecemos por
descargar y leer un archivo `nordic-data.csv`. 
Guardaremos estos datos como un objeto llamado `nordic`:


~~~
nordic <- read.csv("data/nordic-data.csv")
~~~
{: .language-r}

La función `read.table` se usa para leer datos tabulados guardados en un archivo de
texto donde las columnas de los datos están separadas por
caracteres de puntuación como sucede en
los archivos CSV (csv = valores separados por comas). Tabuladores y comas son los caracteres más usados para separar o delimitar datos en archivos csv.
Por comodidad R provee dos otras versiones de `read.table`. Esas son: `read.csv`
para archivos donde los datos están separados por comas y `read.delim` para archivos
donde los datos están separados por tabuladores. De esas tres funciones `read.csv` es
 la más usada. Si es necesario, es posible cambiar las el carácter por defecto
 delimitando las marcas de puntuación  para ambos `read.csv` y `read.delim`.

Podemos empezar explorando nuestro conjunto de datos de inmediato, extrayendo columnas especificándolas
usando el operador `$`:


~~~
nordic$country
~~~
{: .language-r}



~~~
[1] "Denmark" "Sweden"  "Norway" 
~~~
{: .output}



~~~
nordic$lifeExp
~~~
{: .language-r}



~~~
[1] 77.2 80.0 79.0
~~~
{: .output}

Podemos hacer otras operaciones en las columnas. Por ejemplo, si descubrimos que la esperanza de vida es dos años más alta:


~~~
nordic$lifeExp + 2
~~~
{: .language-r}



~~~
[1] 79.2 82.0 81.0
~~~
{: .output}

Pero qué pasa:


~~~
nordic$lifeExp + nordic$country
~~~
{: .language-r}



~~~
Error in nordic$lifeExp + nordic$country: non-numeric argument to binary operator
~~~
{: .error}

Entender lo que sucedió aquí es clave para analizar con éxito los datos en R.

## Tipo de datos

Si pensaste que el último comando resultaría en un error porque  `77.2` más `"Denmark"` no tiene sentido, entonces acertaste - y ya tienes una intuición para un
concepto importante en programación llamado *clases de datos*. Podemos preguntar qué clase de
 datos es algo:


~~~
class(nordic$lifeExp)
~~~
{: .language-r}



~~~
[1] "numeric"
~~~
{: .output}

Hay 6 tipos de datos fundamentales: `numeric`, `integer`, `complex`, `logical`, `character`, y `factor`.


~~~
class(3.14)
~~~
{: .language-r}



~~~
[1] "numeric"
~~~
{: .output}



~~~
class(1L) # El sufijo L fuerza que el número sea un entero ya que R los guarda como punto flotante por defecto
~~~
{: .language-r}



~~~
[1] "integer"
~~~
{: .output}



~~~
class(1+1i)
~~~
{: .language-r}



~~~
[1] "complex"
~~~
{: .output}



~~~
class(TRUE)
~~~
{: .language-r}



~~~
[1] "logical"
~~~
{: .output}



~~~
class('banana')
~~~
{: .language-r}



~~~
[1] "character"
~~~
{: .output}



~~~
class(factor('banana'))
~~~
{: .language-r}



~~~
[1] "factor"
~~~
{: .output}

No importa cuan
 complicado sea nuestro análisis, todos los datos en R se convierten a una 
clase 
de datos específica. Este rigor tiene algunas consecuencias realmente importantes.

Un usuario ha añadido nuevos detalles a la esperanza de vida. Dicha información está en el archivo
`data/nordic-data-2.csv`.

Carga los datos nórdicos nuevos como `nordic_2`, y comprueba que clase de datos encontramos en la columna
`lifeExp`:


~~~
nordic_2 <- read.csv("data/nordic-data-2.csv")
class(nordic_2$lifeExp)
~~~
{: .language-r}



~~~
[1] "character"
~~~
{: .output}

¡Oh no, nuestra esperanza de vida lifeExp ya no es de tipo numérico! Si intentamos hacer los mismos cálculos matemáticos que hicimos con ellos antes, nos metemos en problemas:


~~~
nordic_2$lifeExp + 2
~~~
{: .language-r}



~~~
Error in nordic_2$lifeExp + 2: non-numeric argument to binary operator
~~~
{: .error}

¿Qué ha sucedido? Cuando R lee un archivo csv en una de esas tablas, R insiste que
todo en una columna sea de la misma clase. Si R no puede entender
*todo* en una columna como numérico, entonces a *nada* en la columna se le asigna el tipo numérico. La tabla en la que R cargó nuestros datos nórdicos es algo conocido como marco de datos (dataframe), y es nuestro primer ejemplo de lo que se conoce como una *estructura
 de datos* - es decir, una estructura que R sabe como construir partiendo de tipo de datos básicos.

Podemos ver que us un marco de datos (**dataframe**) llamándo la función `class()` en ella:


~~~
class(nordic)
~~~
{: .language-r}



~~~
[1] "data.frame"
~~~
{: .output}

Para usar con éxito nuestros datos en R, necesitamos entender cuales son las estructuras de datos fundamentales
y como se comportan.

## Vectores y Tipo de Coerción

Para mejor entender este comportamiento, conozcamos otra de las estructuras de datos:
el vector.


~~~
my_vector <- vector(length = 3)
my_vector
~~~
{: .language-r}



~~~
[1] FALSE FALSE FALSE
~~~
{: .output}

Un vector en R es esencialmente un lista de cosas ordenadas, con la condición 
especial de que todo en el vector tiene que ser del mismo tipo de dato. Si
no eliges el tipo de dato, por defecto será `lógico`; o, puedes declarar
un vector vacío del tipo que quieras.


~~~
another_vector <- vector(mode = 'character', length = 3)
another_vector
~~~
{: .language-r}



~~~
[1] "" "" ""
~~~
{: .output}

Puedes revisar si algo es un vector:


~~~
str(another_vector)
~~~
{: .language-r}



~~~
 chr [1:3] "" "" ""
~~~
{: .output}

El resultado un poco críptico de este comando indica el tipo básico de dato
encontrado en este vector - en este caso `chr`, carácter; una indicación del
numero de cosas en el vector - en realidad, los índices del vector, en este
caso `[1:3]`; y unos ejemplos de lo que está realmente en el vector - en este caso
cadenas de caracteres vacíos. Si lo hacemos de manera similar


~~~
str(nordic$lifeExp)
~~~
{: .language-r}



~~~
 num [1:3] 77.2 80 79
~~~
{: .output}

vemos que `nordic$lifeExp` también es un vector - las columnas de datos que cargamos en los 
data frames en R, son todas vectores, y es por eso que R obliga que todo en
una columna para ser del mismo tipo de dato básico.

> ## Discusión 1
>
> ¿Por qué R es tan dogmático con los datos que ponemos en nuestras columnas?
> ¿Cómo esto nos ayuda?
>
> > ## Discusión 1
> >
> > Manteniendo todo en una columna igual , nos permitimos hacer simples supuestos
> >  sobre nuestros datos; si puedes interpretar una entrada en una columna como un 
> > número, entonces puedes interpretar *todas* ellas como números, así no tenemos que
> > verificar todo el tiempo. Esta consistencia es a lo que se refieren las personas cuando hablan
> > de *datos limpios*; a la larga, la estricta consistencia contribuye considerablemente a hacer
> > nuestras vidas más fáciles en R.
> {: .solution}
{: .discussion}

También puedes crear vectores con contenido explícito usando la función combine:


~~~
combine_vector <- c(2, 6, 3)
combine_vector
~~~
{: .language-r}



~~~
[1] 2 6 3
~~~
{: .output}

Dado lo que aprendimos hasta ahora, ¿qué crees que va a resultar de lo siguente?


~~~
quiz_vector <- c(2, 6, '3')
~~~
{: .language-r}

Esto es algo llamado *tipo coerción*, y es la fuente de muchas sorpresas
y la razón por la que debemos conocer los tipos de dato básicos y cómo R
los interpreta. Cuando R consigue una mezcla de tipos (aquí numéricos y de caracteres) para
combinarlos en un sólo vector, los obligará a todos ser del mismo tipo. Considera:


~~~
coercion_vector <- c('a', TRUE)
coercion_vector
~~~
{: .language-r}



~~~
[1] "a"    "TRUE"
~~~
{: .output}



~~~
another_coercion_vector <- c(0, TRUE)
another_coercion_vector
~~~
{: .language-r}



~~~
[1] 0 1
~~~
{: .output}

Las reglas de coerción son: `logical` -> `integer` -> `numeric` -> `complex` ->
`character`, donde -> puede ser leído como *se transfoman en*. Puedes intentar
forzar la coerción contra este flujo usando las funciones `as.`:


~~~
character_vector_example <- c('0', '2', '4')
character_vector_example
~~~
{: .language-r}



~~~
[1] "0" "2" "4"
~~~
{: .output}



~~~
character_coerced_to_numeric <- as.numeric(character_vector_example)
character_coerced_to_numeric
~~~
{: .language-r}



~~~
[1] 0 2 4
~~~
{: .output}



~~~
numeric_coerced_to_logical <- as.logical(character_coerced_to_numeric)
numeric_coerced_to_logical
~~~
{: .language-r}



~~~
[1] FALSE  TRUE  TRUE
~~~
{: .output}

Como puedes ver, ¡algunas cosas sorprendentes pueden ocurrir cuando R fuerza un tipo de datos básico
en otro! Dejando de lado la cuestión de la coerción de tipo, el punto es: si tus
datos no se parecen a lo que pensabas que iban a ser , la coerción de tipo
bien puede ser la culpable; asegúrate que todo sea del mismo tipo en tus vectores y
en tus columnas del data frame , o ¡tendrás sorpresas desagradables!

> ## Desafío 1
> 
> Dado lo que sabe ahora sobre la conversión de tipos, observe la clase de
> datos en `nordic_2$lifeExp` y compáralo con `nordic$lifeExp`. ¿Por qué
> estas columnas son de diferentes clases?
> 
> > ## Solución
> > 
> > ~~~
> > str(nordic_2$lifeExp)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >  chr [1:3] "77.2" "80" "79.0 or 83"
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > str(nordic$lifeExp)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >  num [1:3] 77.2 80 79
> > ~~~
> > {: .output}
> > Los datos en `nordic_2$lifeExp` son almacenados como factor en lugar de
> > numérico. Esto es por el caracter tipo texto  (*string*) "or" en la tercer
> > punto de datos. "Factor" es el término especial de R para los datos categóricos.
> > Trabajaremos más con datos de factores más adelante en este taller.
> {: .solution}
{: .challenge}

La función de combinación, `c()`, también agregará cosas a un vector existente:


~~~
ab_vector <- c('a', 'b')
ab_vector
~~~
{: .language-r}



~~~
[1] "a" "b"
~~~
{: .output}



~~~
combine_example <- c(ab_vector, 'DC')
combine_example
~~~
{: .language-r}



~~~
[1] "a"  "b"  "DC"
~~~
{: .output}

También puedes hacer series de números:


~~~
my_series <- 1:10
my_series
~~~
{: .language-r}



~~~
 [1]  1  2  3  4  5  6  7  8  9 10
~~~
{: .output}



~~~
seq(10)
~~~
{: .language-r}



~~~
 [1]  1  2  3  4  5  6  7  8  9 10
~~~
{: .output}



~~~
seq(1,10, by = 0.1)
~~~
{: .language-r}



~~~
 [1]  1.0  1.1  1.2  1.3  1.4  1.5  1.6  1.7  1.8  1.9  2.0  2.1  2.2  2.3  2.4
[16]  2.5  2.6  2.7  2.8  2.9  3.0  3.1  3.2  3.3  3.4  3.5  3.6  3.7  3.8  3.9
[31]  4.0  4.1  4.2  4.3  4.4  4.5  4.6  4.7  4.8  4.9  5.0  5.1  5.2  5.3  5.4
[46]  5.5  5.6  5.7  5.8  5.9  6.0  6.1  6.2  6.3  6.4  6.5  6.6  6.7  6.8  6.9
[61]  7.0  7.1  7.2  7.3  7.4  7.5  7.6  7.7  7.8  7.9  8.0  8.1  8.2  8.3  8.4
[76]  8.5  8.6  8.7  8.8  8.9  9.0  9.1  9.2  9.3  9.4  9.5  9.6  9.7  9.8  9.9
[91] 10.0
~~~
{: .output}

Puedes hacer algunas preguntas sobre vectores:


~~~
sequence_example <- seq(10)
head(sequence_example,n = 2)
~~~
{: .language-r}



~~~
[1] 1 2
~~~
{: .output}



~~~
tail(sequence_example, n = 4)
~~~
{: .language-r}



~~~
[1]  7  8  9 10
~~~
{: .output}



~~~
length(sequence_example)
~~~
{: .language-r}



~~~
[1] 10
~~~
{: .output}



~~~
class(sequence_example)
~~~
{: .language-r}



~~~
[1] "integer"
~~~
{: .output}

Finalmente, puedes poner nombres a los elementos en tu vector: 


~~~
my_example <- 5:8
names(my_example) <- c("a", "b", "c", "d")
my_example
~~~
{: .language-r}



~~~
a b c d 
5 6 7 8 
~~~
{: .output}



~~~
names(my_example)
~~~
{: .language-r}



~~~
[1] "a" "b" "c" "d"
~~~
{: .output}

> ## Desafío 2
>
>Empieza por hacer un vector con los números 1 a 26. 
>Multiplica el vector por 2, y da al vector resultante los 
>nombres A a Z (sugerencia: hay un vector incorporado llamado `LETTERS`)
>
>>##Solución al Desafío 2 
>>
>>
>>~~~
>><- 1:26
> > x <- x * 2
> > names(x) <- LETTERS
>> ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}


## Factores

Dijimos que las columnas en los **dataframes** eran vectores: 


~~~
str(nordic$lifeExp)
~~~
{: .language-r}



~~~
 num [1:3] 77.2 80 79
~~~
{: .output}



~~~
str(nordic$year)
~~~
{: .language-r}



~~~
int [1:3] 2002 2002 2002
~~~
{: .output}

Esto tiene sentido. Pero qué pasa con


~~~
str(nordic$country)
~~~
{: .language-r}



~~~
chr [1:3] "Denmark" "Sweden" "Norway"
~~~
{: .output}

Otra estructura de datos importante se llama factor. 
Los factores se parecen a los datos de tipo carácter, 
pero son usados para representar información categórica. 
Por ejemplo, hagamos 
un vector de tipo **string** (cadena de caracteres) etiquetando los países nórdicos para todos los países de nuestro
 estudio. 


~~~
nordic_countries <- c('Norway', 'Finland', 'Denmark', 'Iceland', 'Sweden')
nordic_countries
~~~
{: .language-r}



~~~
[1] "Norway"  "Finland" "Denmark" "Iceland" "Sweden" 
~~~
{: .output}



~~~
str(nordic_countries)
~~~
{: .language-r}



~~~
 chr [1:5] "Norway" "Finland" "Denmark" "Iceland" "Sweden"
~~~
{: .output}

Podemos convertir un vector en un factor así: 


~~~
categories <- factor(nordic_countries)
class(categories)
~~~
{: .language-r}



~~~
[1] "factor"
~~~
{: .output}



~~~
str(categories)
~~~
{: .language-r}



~~~
 Factor w/ 5 levels "Denmark","Finland",..: 4 2 1 3 5
~~~
{: .output}

Ahora R identificó que hay 5 categorías posibles en nuestros datos - pero también realizó algo sorprendente; 
en vez de imprimir la secuencia de caracteres que le dimos, tenemos un montón de números en su lugar. 
R remplazó nuestras categorías legibles para humanos con índices numerados por detrás, 
esto es necesario ya que muchos cálculos estadísticos utilizan esta representación numérica para datos categóricos. 


~~~
class(nordic_countries)
~~~
{: .language-r}



~~~
[1] "character"
~~~
{: .output}



~~~
class(categories)
~~~
{: .language-r}



~~~
[1] "factor"
~~~
{: .output}

> ## Desafío
>
> ¿Puedes adivinar por qué estos números son utilizados para representar a estos países?
>
>> ## Solución
>> 
>> Están ordenados alfabéticamente. 
> {: .solution}
{: .challenge}

> ## Desafío 3
>
> ¿Hay un factor en nuestro **dataframe** `nordic`? ¿Cual es su nombre? Trata de usar
> `?read.csv` para deducir como mantener las columnas de texto como vectores de caracteres
> en vez de factores; luego escribe un comando o dos para mostrar que el factor en
> `nordic` es en realidad un vector de caracteres cuando está cargado de esta manera .
>
> > ## Solución al Desafío 3
> >
> > Una solución es usar el argumento `stringAsFactors`:
> >
> > 
> > ~~~
> > nordic <- read.csv(file = "data/nordic-data.csv", stringsAsFactors = FALSE)
> > str(nordic$country)
> > ~~~
> > {: .language-r}
> >
> > Otra solución es usar el argumento `colClasses`
> > que permite un control más fino.
> >
> > 
> > ~~~
> > nordic <- read.csv(file="data/nordic-data.csv", colClasses=c(NA, NA, "character"))
> > str(nordic$country)
> > ~~~
> > {: .language-r}
> >
> > Nota: nuevos estudiantes encuentran difícil de entender los archivos de ayuda ; asegúrate de hacerles saber
> > que es común, y de alentarlos a hacer su mejor conjetura sobre el significado semántico,
> > incluso si no están seguros.
> {: .solution}
{: .challenge}

Al hacer modelos estadísticos, es importante conocer cuales son los **levels** (categorías) de base. 
Se supone que este es el primer factor, pero por defecto los factores
se etiquetan alfabéticamente. Puedes cambiar esto al especificar los **levels** (categorías):


~~~
mydata <- c("case", "control", "control", "case")
factor_ordering_example <- factor(mydata, levels = c("control", "case"))
str(factor_ordering_example)
~~~
{: .language-r}



~~~
 Factor w/ 2 levels "control","case": 2 1 1 2
~~~
{: .output}

En este caso, le dijimos a R que "control" debería ser representado con 1, 
y "case" con 2. ¡Esta designación puede ser muy importante para interpretar los 
resultados de modelos estadísticos!

## Listas

Otra estructura de datos que querrás tener en tu bolsa de trucos es la `list`. 
Una lista es en de algún modo más simple que otros tipos, porque
puedes poner lo quieras dentro: 


~~~
list_example <- list(1, "a", TRUE, c(2, 6, 7))
list_example
~~~
{: .language-r}



~~~
[[1]]
[1] 1

[[2]]
[1] "a"

[[3]]
[1] TRUE

[[4]]
[1] 2 6 7
~~~
{: .output}



~~~
another_list <- list(title = "Numbers", numbers = 1:10, data = TRUE )
another_list
~~~
{: .language-r}



~~~
$title
[1] "Numbers"

$numbers
 [1]  1  2  3  4  5  6  7  8  9 10

$data
[1] TRUE
~~~
{: .output}

Ahora podemos entender algo un poco sorprendente en nuestro **dataframe**; que ocurre si comparamos `str(nordic)` y `str(another_list)`:


~~~
str(nordic)
~~~
{: .language-r}



~~~
'data.frame':\t3 obs. of  3 variables:
 $ country: chr  "Denmark" "Sweden" "Norway"
 $ year   : int  2002 2002 2002
 $ lifeExp: num  77.2 80 79
~~~
{: .output}



~~~
str(another_list)
~~~
{: .language-r}



~~~
List of 3
 $ title  : chr "Numbers"
 $ numbers: int [1:10] 1 2 3 4 5 6 7 8 9 10
 $ data   : logi TRUE
~~~
{: .output}

Vemos que los resultados para estos dos objetos se ven parecidos. Esto es porque
los dataframes son listas 'tras bambalinas'. Los **dataframes** son un caso especial de lista donde cada elemento (las columnas del **dataframe**) tiene el mismo largo. 

En nuestro ejemplo `nordic`, tenemos una variable **integer**, una variable **double** y una variable **logical**. 
Como ya vimos, cada columna del **dataframe** es un vector. 


~~~
nordic$country
~~~
{: .language-r}



~~~
[1] "Denmark" "Sweden"  "Norway" 
~~~
{: .output}



~~~
nordic[, 1]
~~~
{: .language-r}



~~~
[1] "Denmark" "Sweden"  "Norway" 
~~~
{: .output}



~~~
class(nordic[, 1])
~~~
{: .language-r}



~~~
[1] "character"
~~~
{: .output}



~~~
str(nordic[, 1])
~~~
{: .language-r}



~~~
chr [1:3] "Denmark" "Sweden" "Norway"
~~~
{: .output}

Cada fila es una *observación* de diferentes variables, en sí misma un **dataframe**, y 
entonces puede estar compuesto de elementos de diferentes tipos. 


~~~
nordic[1, ]
~~~
{: .language-r}



~~~
  country year lifeExp
1 Denmark 2002    77.2
~~~
{: .output}



~~~
class(nordic[1, ])
~~~
{: .language-r}



~~~
[1] "data.frame"
~~~
{: .output}



~~~
str(nordic[1, ])
~~~
{: .language-r}



~~~
'data.frame':\t1 obs. of  3 variables:
 $ country: chr "Denmark"
 $ year   : int 2002
 $ lifeExp: num 77.2
~~~
{: .output}

> ## Desafío 4
>
> Hay varias maneras sutilmente diferentes de llamar variables, observaciones y
> elementos de los **dataframes**:
>
> - `nordic[1]`
> - `nordic[[1]]`
> - `nordic$country`
> - `nordic["country"]`
> - `nordic[1, 1]`
> - `nordic[, 1]`
> - `nordic[1, ]`
>
> Prueba estos ejemplos y explica que se regresa en cada uno.
>
> *Sugerencia:* Usa la función `class()` para examinar que se devuelve en cada caso.
>
> > ## Solución al Desafío 4
> >
> > 
> > ~~~
> > nordic[1]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   country
> > 1 Denmark
> > 2  Sweden
> > 3  Norway
> > ~~~
> > {: .output}
> >
> > Podemos pensar en un **dataframe** como una lista de vectores. El corchete simple `[1]`
> > devuelve la primer parte de la lista, como otra lista. En este caso es la
> > primer columna del **dataframe**.
> >
> > 
> > ~~~
> > nordic[[1]]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] "Denmark" "Sweden"  "Norway" 
> > ~~~
> > {: .output}
> >
> > El corchete doble `[[1]]`  regresa el contenido del elemento de la lista. En este caso
> >  es el contenido de la primer columna, un_vector_del tipo _factor_.
> >
> > 
> > ~~~
> > nordic$country
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] "Denmark" "Sweden"  "Norway" 
> > ~~~
> > {: .output}
> >
> > Este ejemplo use el carácter `$` para dirigirse a elementos por su nombre. _coat_ es la
> > primer columna del **dataframe**, de nuevo un  _vector_ de tipo _factor_.
> X
> > 
> > ~~~
> > nordic["country"]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   country
> > 1 Denmark
> > 2  Sweden
> > 3  Norway
> > ~~~
> > {: .output}
> > Aquí usamos un corchete sencillo `["country"]` remplazando el índice numérico
> > con el nombre de la columna. Como en el ejemplo 1, el objeto devuelto es una _lista_.
> >
> > 
> > ~~~
> > nordic[1, 1]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] "Denmark"
> > ~~~
> > {: .output}
> >
> > Este ejemplo usa un corchete sencillo, pero esta vez brindamos las coordenadas
> de fila y columna. El objeto devuelto es el valor en la fila 1, columna 1. El objeto
> un _integer_ pero debido a que es parte de un _vector_ de tipo _factor_, R
> muestra la etiqueta "Denmark" asociada con el valor entero (**integer**).
> >
> > 
> > ~~~
> > nordic[, 1]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] "Denmark" "Sweden"  "Norway" 
> > ~~~
> > {: .output}
> >
> > Como los ejemplos previos, usamos el corchete sencillos y brindamos las coordenadas de
> > fila y columna. La coordenada de fila no está especificada, R interpreta este valor
> > faltante como todos los elementos en esta _columna_ _vector_
> >
> > 
> > ~~~
> > nordic[1, ]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   country year lifeExp
> > 1 Denmark 2002    77.2
> > ~~~
> > {: .output}
> >
> > Otra vez usamos el corchete sencillo con las coordenadas de fila y columna. La coordenada de
> > columna no está especificada. El valor devuelto es una *lista* que contiene todos los
> > valores en la primer fila.
> {: .solution}
{: .challenge}

