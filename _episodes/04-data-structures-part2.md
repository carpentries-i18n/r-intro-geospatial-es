---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 04-data-structures-part2.md in _episodes_rmd/
title: "Explorando Dataframes"
teaching: 20
exercises: 10
questions:
- "¿Cómo puedo manipular un dataframe?"
objectives:
- "Eliminar filas con valores `NA`."
- "Añadir dos dataframes."
- "Entender qué es un `factor`."
- "Convertir un `factor` en un vector `character` y viceversa."
- "Mostrar las propiedades básicas de los dataframes, incluido el tamaño y la clase de las columnas, los nombres y las primeras filas."
keypoints:
- "Usar `cbind()` para agregar una nueva columna a un dataframe."
- "Usar `rbind()` para agregar una nueva fila a un dataframe."
- "Eliminar filas de un dataframe."
- "Usar `na.omit()` para eliminar filas de un dataframe con valores `NA`. "
- "Usar `levels()` y `as.character()` para explorar y manipular `factores`."
- "Usar `str()`, `nrow()`, `ncol()`, `dim()`, `colnames()`, `rownames()`, `head()` y `typeof()` para comprender la estructura de un dataframe."
- "Leer en un archivo csv usando `read.csv()`."
- "Comprender quE representa`length()` en un dataframe."
source: Rmd
---



Hasta aquí, lo has visto todo: en la última lección, hemos recorrido todos 
los tipos de datos y estructuras básicas en R.  Todo lo que harás será 
utilizar esas herramientas. Pero la mayor parte del tiempo, 
la estrella del show es el data.frame—la tabla que hemos creado cargando la información desde un archivo csv. En esta lección aprenderemos algunas cosas más sobre el trabajo con `data.frames`. 

## Un ejemplo práctico

Ya hemos aprendido que las columnas de un dataframe son vectores, que permiten
que nuestros datos sean consistentes con su tipo de datos en cada columna.  
Hasta ahora, haz visto los fundamentos de la manipulación de dataframes con nuestros datos nórdicos; 
ahora usaremos esas habilidades para procesar un conjunto de datos más extenso. Leamos en R el conjunto de datos de gapminder que hemos descargado anteriormente:



> ## Consejos Varios
>
> * Otro tipo de archivos que puedes encontrar son los archivos de valores separados
 por tabulaciones (.tsv). Para especificar una pestaña como separador, usa `"\\t"` o `read.delim`.
> 
> * Los archivos también pueden ser descargados directamente de Internet a una carpeta local 
de tu elección en tu computadora usando la función `download.file`. 
La función `read.csv` se ejecuta después para leer el archivo descargado 
desde el lugar dónde se lo guardó , por ejemplo,
>
> 
> ~~~
> download.file("https://raw.githubusercontent.com/datacarpentry/r-intro-geospatial/master/_episodes_rmd/data/gapminder_data.csv",
>               destfile = "data/gapminder_data.csv")
> gapminder <- read.csv("data/gapminder_data.csv")
> ~~~
> {: .language-r}
>
> * Alternativamente, también puedes leer archivos de Internet 
directamente en R reemplazando en `read.csv` la ruta del archivo por su dirección web. 
Hay que tener en cuenta que al hacer esto no se guardará primero una copia local del archivo csv en tu computadora. Por ejemplo,
> 
> 
> ~~~
> gapminder <- read.csv("https://raw.githubusercontent.com/datacarpentry/r-intro-geospatial/master/_episodes_rmd/data/gapminder_data.csv")
> ~~~
> {: .language-r}
>
> * Puedes leer directamente las hojas de cálculo de Excel sin necesidad 
de convertirlas primero a texto plano usando el paquete [readxl](https://cran.r-project.org/package=readxl).
{: .callout}

Investiguemos un poco el dataframe `gapminder` ; lo primero que siempre debemos
hacer es comprobar cómo se ven los datos con `str`:


~~~
str(gapminder)
~~~
{: .language-r}



~~~
'data.frame':\t1704 obs. of  6 variables:
 $ country  : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
 $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop      : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent: chr  "Asia" "Asia" "Asia" "Asia" ...
 $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap: num  779 821 853 836 740 ...
~~~
{: .output}

También podemos examinar las columnas individuales del dataframe con la función `class`:


~~~
class(gapminder$year)
~~~
{: .language-r}



~~~
[1] "integer"
~~~
{: .output}



~~~
class(gapminder$country)
~~~
{: .language-r}



~~~
[1] "character"
~~~
{: .output}



~~~
str(gapminder$country)
~~~
{: .language-r}



~~~
 chr [1:1704] "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
~~~
{: .output}

También podemos interrogar el dataframe para obtener información sobre sus dimensiones;
recordando que `str(gapminder)` decía que había 1704 observaciones de 6
variables en gapminder, ¿qué crees que producirá lo siguiente, y por qué?


~~~
length(gapminder)
~~~
{: .language-r}

Una buena suposición diría que la longitud de un dataframe sería el
número de filas que tiene (1704), pero no, en éste el caso nos da el número de columnas.


~~~
class(gapminder)
~~~
{: .language-r}



~~~
[1] "data.frame"
~~~
{: .output}

Para obtener el número de filas y columnas en nuestro conjunto de datos, prueba:


~~~
nrow(gapminder)
~~~
{: .language-r}



~~~
[1] 1704
~~~
{: .output}



~~~
ncol(gapminder)
~~~
{: .language-r}



~~~
[1] 6
~~~
{: .output}

O, ambas a la vez:


~~~
dim(gapminder)
~~~
{: .language-r}



~~~
[1] 1704    6
~~~
{: .output}

También es probable que queramos saber cuáles son los nombres de todas las columnas, para que más tarde podamos consultar por nombre:


~~~
colnames(gapminder)
~~~
{: .language-r}



~~~
[1] "country"   "year"      "pop"       "continent" "lifeExp"   "gdpPercap"
~~~
{: .output}

En esta etapa, es importante preguntarnos si la estructura R que está informando 
coincide con nuestra intuición o expectativas; ¿los tipos de datos básicos informados para cada columna 
tienen sentido? Si no es así, tenemos que resolver cualquier problema ahora, antes de que se convierta 
en una mala sorpresa, usando lo que hemos aprendido sobre cómo R 
interpreta los datos, y la importancia de la *consistencia estricta* en la forma en que registramos nuestros datos.

Una vez que estamos contentas de que los tipos y estructuras de datos se ven razonables, es hora de empezar a explorar apropiadamente nuestros datos. Mira las primeras líneas:


~~~
head(gapminder)
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
4 Afghanistan 1967 11537966      Asia  34.020  836.1971
5 Afghanistan 1972 13079460      Asia  36.088  739.9811
6 Afghanistan 1977 14880372      Asia  38.438  786.1134
~~~
{: .output}

> ## Desafío 1
>
> Es una buena práctica comprobar también las últimas líneas de los datos y algunas 
> del medio. ¿Cómo lo harías?
>
> Buscar las que están específicamente en el medio no es muy difícil pero podríamos
> simplemente pedir unas pocas líneas al azar. ¿Cómo codificarías esto?
>
> > ## Solución al Desafío 1
> >
> > Comprobar las últimas líneas es relativamente simple, ya que R  tiene una
> > función para esto::
> > 
> > 
> > ~~~
> > tail(gapminder)
> > tail(gapminder, n = 15)
> > ~~~
> > {: .language-r}
> > 
> > ¿Qué tal si compruebas unas líneas al azar para más seguridad (o no, según tu punto de vista)?
> >
> > Hay varias maneras de lograr esto.
> >
> > La solución que se muestra aquí presenta una forma que utiliza funciones anidadas, es decir, una función que
> > pasa su resultado a otra función como argumento. Esto podría parecer  un concepto nuevo
> > pero de hecho ya lo estás usando.
> >
> > Recuerda que `my_dataframe[rows, cols]` va a imprimir en pantalla tu dataframe
> con el número de filas y columnas que le pediste (aunque podrías 
> > haber pedido un rango de columnas, por ejemplo). ¿Cómo obtendrías la
> > última fila si no sabes cuántas filas tiene tu dataframe? R tiene una
> > función para esto. ¿Cómo intentarías obtener una muestra (pseudo-aleatoria)? R también tiene una
> > función para esto.
> > 
> > 
> > ~~~
> > gapminder[sample(nrow(gapminder), 5), ]
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

> ## Desafío 2
>
> Lee la salida de `str(gapminder)` de nuevo; esta vez, usa lo que has aprendido
> sobre factores y vectores, así como la salida de funciones como `colnames`
> y `dim` para explicar todo lo que `str` imprime para `gapminder`
> significa. ¡Si hay alguna parte que no puedes interpretar, discútela con tus
> vecinos!
>
> > ## Solución al Desafío 2
> >
> > El objeto `gapminder` es un dataframe con columnas
> >
> > - `country` y `continent` como **factores**.
> > - `year` es un vector de enteros.
> > - `pop`, `lifeExp`, y `gdpPercap` son vectores numéricos.
> {: .solution}
{: .challenge}

## Agregando columnas y filas en dataframes

Quisiéramos crear una nueva columna que contenga información sobre si la esperanza de vida es inferior o superior a la media mundial (70,5) :


~~~
below_average <- gapminder$lifeExp < 70.5
head(gapminder)
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
4 Afghanistan 1967 11537966      Asia  34.020  836.1971
5 Afghanistan 1972 13079460      Asia  36.088  739.9811
6 Afghanistan 1977 14880372      Asia  38.438  786.1134
~~~
{: .output}

Podemos entonces añadir esto como una columna usando:


~~~
cbind(gapminder, below_average)
~~~
{: .language-r}


~~~
      country year      pop continent lifeExp gdpPercap below_average
1 Afghanistan 1952  8425333      Asia  28.801  779.4453          TRUE
2 Afghanistan 1957  9240934      Asia  30.332  820.8530          TRUE
3 Afghanistan 1962 10267083      Asia  31.997  853.1007          TRUE
4 Afghanistan 1967 11537966      Asia  34.020  836.1971          TRUE
5 Afghanistan 1972 13079460      Asia  36.088  739.9811          TRUE
6 Afghanistan 1977 14880372      Asia  38.438  786.1134          TRUE
~~~
{: .output}

Probablemente no vamos a querer imprimir el dataframe completo cada vez, así que
ponemos nuestro `cbind` dentro de una llamada de `head`  para que devuelva
sólo las primeras seis líneas del resultado.


~~~
head(cbind(gapminder, below_average))
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap below_average
1 Afghanistan 1952  8425333      Asia  28.801  779.4453          TRUE
2 Afghanistan 1957  9240934      Asia  30.332  820.8530          TRUE
3 Afghanistan 1962 10267083      Asia  31.997  853.1007          TRUE
4 Afghanistan 1967 11537966      Asia  34.020  836.1971          TRUE
5 Afghanistan 1972 13079460      Asia  36.088  739.9811          TRUE
6 Afghanistan 1977 14880372      Asia  38.438  786.1134          TRUE
~~~
{: .output}

Obsérva que si tratamos de añadir un vector de `below_average` con un número diferente de entradas que el número de filas del dataframe, va a fallar:


~~~
below_average <- c(TRUE, TRUE, TRUE, TRUE, TRUE)
head(cbind(gapminder, below_average))
~~~
{: .language-r}



~~~
Error in data.frame(..., check.names = FALSE): arguments imply differing number of rows: 1704, 5
~~~
{: .error}

¿Por qué no funcionó? R quiere ver un elemento en nuestra nueva columna
por cada fila de la tabla:


~~~
nrow(gapminder)
~~~
{: .language-r}



~~~
[1] 1704
~~~
{: .output}



~~~
length(below_average)
~~~
{: .language-r}



~~~
[1] 5
~~~
{: .output}

Entonces que para que funcione necesitamos o bien tener  `nrow(gapminder)` = `length(below_average)` o que `nrow(gapminder)` sea  multiplo de `length(below_average)`: 


~~~
below_average <- c(TRUE, TRUE, FALSE)
head(cbind(gapminder, below_average))
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap below_average
1 Afghanistan 1952  8425333      Asia  28.801  779.4453          TRUE
2 Afghanistan 1957  9240934      Asia  30.332  820.8530          TRUE
3 Afghanistan 1962 10267083      Asia  31.997  853.1007         FALSE
4 Afghanistan 1967 11537966      Asia  34.020  836.1971          TRUE
5 Afghanistan 1972 13079460      Asia  36.088  739.9811          TRUE
6 Afghanistan 1977 14880372      Asia  38.438  786.1134         FALSE
~~~
{: .output}
La secuencia `TRUE,TRUE,FALSE` se repite en todas las filas de gapminder.

Sobrescribamos el contenido de gapminder con nuestro nuevo dataframe.


~~~
below_average <-  as.logical(gapminder$lifeExp<70.5)
gapminder <- cbind(gapminder, below_average)
~~~
{: .language-r}

Ahora, ¿qué tal agregar filas? Las filas de un dataframe son listas:


~~~
new_row <- list("Norway", 2016, 5000000, "Nordic", 80.3, 49400.0, FALSE)
gapminder_norway <- rbind(gapminder, new_row)
tail(gapminder_norway)
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp  gdpPercap below_average
1700 Zimbabwe 1987  9216418    Africa  62.351   706.1573          TRUE
1701 Zimbabwe 1992 10704340    Africa  60.377   693.4208          TRUE
1702 Zimbabwe 1997 11404948    Africa  46.809   792.4500          TRUE
1703 Zimbabwe 2002 11926563    Africa  39.989   672.0386          TRUE
1704 Zimbabwe 2007 12311143    Africa  43.487   469.7093          TRUE
1705   Norway 2016  5000000    Nordic  80.300 49400.0000         FALSE
~~~
{: .output}

Para entender por qué R  da una advertencia cuando intentamos añadir esta fila, aprendamos un poco más sobre factores.

## Factores

Otra cosa que hay que tener en cuenta: en un `factor`, cada valor diferente
representa lo que se llama un "nivel" o "categoría" (`level`). En nuestro caso, el `factor` "continente" tiene 5
niveles: "Africa", "Americas", "Asia", "Europa" y "Oceania". R sólo aceptará
valores que coincidan con alguno de los niveles. Si añades un nuevo valor, se convertirá en
`NA`.

La advertencia (warning) nos dice que agregamos "nordic" sin éxito a nuestro
factor *continent*, pero 2016 (un dato de tipo numeric), 5000000 (otro numeric), 80.3 (otro numeric),
49400.0 (otro numeric) y `FALSE` (un tipo de dato logic) se agregaron con éxito a
*country*, *year*, *pop*, *lifeExp*, *gdpPercap* y *below_average*
respectivamente, ya que esas variables no son **factores**. 'Norway' también fue
agregado con éxito ya que corresponde a un nivel existente. Para agregar con
éxito una nueva fila a gapminder con un *continent* "Nordic", necesitas agregar "Nordic" como *nivel* de
factor en continent:


~~~
levels(gapminder$continent)
~~~
{: .language-r}



~~~
NULL
~~~
{: .output}



~~~
levels(gapminder$continent) <- c(levels(gapminder$continent), "Nordic")
gapminder_norway  <- rbind(gapminder,
                           list("Norway", 2016, 5000000, "Nordic", 80.3,49400.0, FALSE))
~~~
{: .language-r}



~~~
Warning in `[<-.factor`(`*tmp*`, ri, value = structure(c("Asia", "Asia", :
invalid factor level, NA generated
~~~
{: .warning}



~~~
tail(gapminder_norway)
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp  gdpPercap below_average
1700 Zimbabwe 1987  9216418      <NA>  62.351   706.1573          TRUE
1701 Zimbabwe 1992 10704340      <NA>  60.377   693.4208          TRUE
1702 Zimbabwe 1997 11404948      <NA>  46.809   792.4500          TRUE
1703 Zimbabwe 2002 11926563      <NA>  39.989   672.0386          TRUE
1704 Zimbabwe 2007 12311143      <NA>  43.487   469.7093          TRUE
1705   Norway 2016  5000000    Nordic  80.300 49400.0000         FALSE
~~~
{: .output}

Alternativamente, podemos cambiar un factor a un vector de caracteres; perderemos
categorías del factor que son tan prácticas, pero posteriormente podemos agregar cualquier palabra que queramos a la
columna sin preocuparnos por los niveles del factor:


~~~
str(gapminder)
~~~
{: .language-r}



~~~
'data.frame':\t1704 obs. of  7 variables:
 $ country      : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
 $ year         : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop          : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent    : chr  "Asia" "Asia" "Asia" "Asia" ...
  ..- attr(*, "levels")= chr "Nordic"
 $ lifeExp      : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap    : num  779 821 853 836 740 ...
 $ below_average: logi  TRUE TRUE TRUE TRUE TRUE TRUE ...
~~~
{: .output}



~~~
gapminder$continent <- as.character(gapminder$continent)
str(gapminder)
~~~
{: .language-r}



~~~
'data.frame':\t1704 obs. of  7 variables:
 $ country      : chr  "Afghanistan" "Afghanistan" "Afghanistan" "Afghanistan" ...
 $ year         : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
 $ pop          : num  8425333 9240934 10267083 11537966 13079460 ...
 $ continent    : chr  "Asia" "Asia" "Asia" "Asia" ...
 $ lifeExp      : num  28.8 30.3 32 34 36.1 ...
 $ gdpPercap    : num  779 821 853 836 740 ...
 $ below_average: logi  TRUE TRUE TRUE TRUE TRUE TRUE ...
~~~
{: .output}

## Agregando a un dataframe

Cuando se agregan datos a un dataframe, la clave es recordar que las *columnas son
vectores y filas son listas.* También podemos pegar dos dataframes con
`rbind`:


~~~
gapminder <- rbind(gapminder, gapminder)
tail(gapminder, n=3)
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap below_average
3406 Zimbabwe 1997 11404948    Africa  46.809  792.4500          TRUE
3407 Zimbabwe 2002 11926563    Africa  39.989  672.0386          TRUE
3408 Zimbabwe 2007 12311143    Africa  43.487  469.7093          TRUE
~~~
{: .output}
Pero ahora los nombres de las filas son innecesariamente complicadas (no son números consecutivos).
Podemos eliminar los nombres de las filas, y R automáticamente los renombrará secuencialmente:


~~~
rownames(gapminder) <- NULL
head(gapminder)
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap below_average
1 Afghanistan 1952  8425333      Asia  28.801  779.4453          TRUE
2 Afghanistan 1957  9240934      Asia  30.332  820.8530          TRUE
3 Afghanistan 1962 10267083      Asia  31.997  853.1007          TRUE
4 Afghanistan 1967 11537966      Asia  34.020  836.1971          TRUE
5 Afghanistan 1972 13079460      Asia  36.088  739.9811          TRUE
6 Afghanistan 1977 14880372      Asia  38.438  786.1134          TRUE
~~~
{: .output}

> ## Desafío 3
>
> Puedes crear un nuevo dataframe en R con la siguiente sintaxis:
> 
> ~~~
> df <- data.frame(id = c("a", "b", "c"),
>                  x = 1:3,
>                  y = c(TRUE, TRUE, FALSE),
>                  stringsAsFactors = FALSE)
> ~~~
> {: .language-r}
>
> Crea un dataframe que tenga ltu información:
>
> - nombre
> - apellido
> - número de la suerte
>
> Luego usa `rbind` para agregar una entrada para las personas que están cerca tuyo. Por último,
> usa `cbind` para agregar una columna con la respuesta de cada persona a la pregunta, "¿Es
> hora de ir por un café?"
>
> > ## Solución al Desafío 3
> >
> > 
> > ~~~
> > df <- data.frame(first = c("Grace"),
> >                  last = c("Rodriguez"),
> >                  lucky_number = c(0),
> >                  stringsAsFactors = FALSE)
> > df <- rbind(df, list("Marie", "Curie", 238) )
> > df <- cbind(df, coffeetime = c(TRUE, TRUE))
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

