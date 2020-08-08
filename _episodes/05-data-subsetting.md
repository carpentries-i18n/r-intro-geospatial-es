---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 05-data-subsetting.md in _episodes_rmd/
title: Subconjunto de Datos
enseñanza: 25
ejercicios: 10
preguntas:
- "¿Cómo puedo trabajar con subconjuntos de datos en R?"
objetivos:
- "Para poder obtener subconjunos de vectores y data frames"
- "Para poder extraer un elemento individual o multiples elementos: por índice, por nombre, usando operadores de comparación"
- "Para poder saltear y eliminar elementos de varias estructuras de datos."
Puntos clave:
- "El indexado en R empieza en 1, no en 0."
- "Accedes a valores individuales por ubicación utilizando `[]`."
- "Accedes a porciones de datos utilizando `[bajo:alto]`."
- "Accedes  a conjuntos de datos arbitrarios utilizando `[c(...)]`."
- "Usas operaciones lógicas y vectores lógicos para acceder a subconjuntos de datos."
source: Rmd
---



R tiene muchos operadores poderosos para crear subconjuntos. Dominarlos te permitirá realizar operaciones complejas de manera sencilla en cualquier tipo de dataset.

Hay 6 formas diferentes que podemos obtener subconjuntos de cualquier tipo de objeto, y tres diferentes operadores de subconjunto para las diferentes estructuras de datos.

Empezaremos con el caballito de batalla de R: un vector numérico simple.


~~~
x <- c(5.4, 6.2, 7.1, 4.8, 7.5)
names(x) <- c('a', 'b', 'c', 'd', 'e')
x
~~~
{: .language-r}



~~~
  a   b   c   d   e 
5.4 6.2 7.1 4.8 7.5 
~~~
{: .output}

> ## Vectores atómicos
>
> En R, los vectores simples que contienen cadenas de caracteres, números, o valores lógicos
> se llaman vectores *atómicos*  porque no pueden simplificarse más.
{: .callout}

Entonces ahora que  hemos creado un  vector ficticio para jugar, ¿cómo accedemos a su
contenido?

## Acceder a elementos usando sus índices

Para extraer elementos de un vector podemos dar su correspondiente índice, empezando
desde uno:


~~~
x[1]
~~~
{: .language-r}



~~~
  a 
5.4 
~~~
{: .output}


~~~
x[4]
~~~
{: .language-r}



~~~
  d 
4.8 
~~~
{: .output}

Puede parecer distinto, pero el operador corchete es una función. Para vectores
(y matrices), significa "dame el n-ésimo elemento".

Podemos pedir múltiples elementos de una vez:


~~~
x[c(1, 3)]
~~~
{: .language-r}



~~~
  a   c 
5.4 7.1 
~~~
{: .output}

O porciones del vector:


~~~
x[1:4]
~~~
{: .language-r}



~~~
  a   b   c   d 
5.4 6.2 7.1 4.8 
~~~
{: .output}

el operador `:`  crea una secuencia de números desde el elemento de la izquierda hasta el de la derecha.

~~~
1:4
~~~
{: .language-r}



~~~
[1] 1 2 3 4
~~~
{: .output}



~~~
c(1, 2, 3, 4)
~~~
{: .language-r}



~~~
[1] 1 2 3 4
~~~
{: .output}


Podemos pedir el mismo elemento muchas veces:


~~~
x[c(1, 1, 3)]
~~~
{: .language-r}



~~~
  a   a   c 
5.4 5.4 7.1 
~~~
{: .output}

Si pedimos un índice mayor a la longitud del vector, R devolverá un valor faltante:

~~~
x[6]
~~~
{: .language-r}



~~~
<NA> 
  NA 
~~~
{: .output}

Este es un vector de longitud uno que contiene un `NA`, cuyo nombre es también `NA`.

Si pedimos el 0-ésimo elemento, obtendremos un vector vacío:


~~~
x[0]
~~~
{: .language-r}



~~~
named numeric(0)
~~~
{: .output}

> ## La numeración de vectores en R empieza en 1
>
> En muchos lenguajes de  programación (C y Python, por ejemplo), el primer
> elemento de un vector tiene índice 0. En R, el primer elemento es 1.
{: .callout}

Salteando y eliminando elementos

Si en un vector usamos un número negativo como índice, R devolverá
todos los elementos *excepto* el número de elemento especificado:


~~~
x[-2]
~~~
{: .language-r}



~~~
  a   c   d   e 
5.4 7.1 4.8 7.5 
~~~
{: .output}

Podemos saltear múltiples elementos:


~~~
x[c(-1, -5)]  # or x[-c(1,5)]
~~~
{: .language-r}



~~~
  b   c   d 
6.2 7.1 4.8 
~~~
{: .output}

> ## Consejo: Orden de operaciones
>
>  Un error común en las personas novatass occurre cuando quieren saltear
> porciones de un vector. Es natural tratar negando una
> secuencia como esto:
>
> 
> ~~~
> x[-1:3]
> ~~~
> {: .language-r}
>
> Eso devuelve un error incomprensible:
>
> 
> ~~~
> Error in x[-1:3]: only 0's may be mixed with negative subscripts
> ~~~
> {: .error}
>
> Pero recuerda el orden de operaciones. `:` es en realidad una función.
> Toma como primer argumento un -1, y como segundo el 3,
> por lo cual genera la secuencia de números: `c(-1, 0, 1, 2, 3)`.
>
> La solución correcta sería envolver la función y sus argumentos con un paréntesis, para
> que el operador `-`  se aplique al resultado:
>
> 
> ~~~
> x[-(1:3)]
> ~~~
> {: .language-r}
> 
> 
> 
> ~~~
>   d   e 
> 4.8 7.5 
> ~~~
> {: .output}
{: .callout}


Para eliminar elementos de un vector, necesitamos asignar el resultado a 
la misma variable:


~~~
x <- x[-4]
x
~~~
{: .language-r}



~~~
  a   b   c   e 
5.4 6.2 7.1 7.5 
~~~
{: .output}

> ## Challenge 1
>
> Dado el siguiente código :
>
> 
> ~~~
> x <- c(5.4, 6.2, 7.1, 4.8, 7.5)
> names(x) <- c('a', 'b', 'c', 'd', 'e')
> print(x)
> ~~~
> {: .language-r}
> 
> 
> 
> ~~~
>   a   b   c   d   e 
> 5.4 6.2 7.1 4.8 7.5 
> ~~~
> {: .output}
>
> Escribe por lo menos 3 comandos distintos que produzcan la siguiente salida:
>
> 
> ~~~
>   b   c   d 
> 6.2 7.1 4.8 
> ~~~
> {: .output}
>
> Después que hayas encontrado 3 comandos distintos, compara tus notas con tu vecino. Tuvieron diferentes estrategias?
>
> > ## Solución al desafío 1
> >
> > 
> > ~~~
> > x[2:4]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> > 
> > ~~~
> > x[-c(1,5)]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> > 
> > ~~~
> > x[c("b", "c", "d")]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> > 
> > ~~~
> > x[c(2,3,4)]
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   b   c   d 
> > 6.2 7.1 4.8 
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## subconjunto por nombre

Podemos extraer elementos usando su nombre, en vez de extraerlos usando su índice.


~~~
x <- c(a = 5.4, b = 6.2, c = 7.1, d = 4.8, e = 7.5) # podemos nombrar un vector sobre la marcha
x[c("a", "c")]
~~~
{: .language-r}



~~~
  a   c 
5.4 7.1 
~~~
{: .output}

Normalmente esta es una manera mucho más fiable de crear subconjuntos:
la posición de varios elementos a menudo puede cambiar cuando se encadenan
operadores para crear subconjuntos, pero los nombres siempre permanecen igual!

## Haciendo subconjuntos usando otros operadores lógicos

También podemos usar cualquier otro vector de tipo logical para crear subconjuntos:


~~~
x[c(FALSE, FALSE, TRUE, FALSE, TRUE)]
~~~
{: .language-r}



~~~
  c   e 
7.1 7.5 
~~~
{: .output}

Dado que los operadores de comparación (e.g. `>`,`<`,`==`) evalúan vectores lógicos,
también podemos usarlos para crear subconjuntos de vectores: la siguiente
declaración da el mismo resultado que la anterior.


~~~
x[x > 7]
~~~
{: .language-r}



~~~
  c   e 
7.1 7.5 
~~~
{: .output}

Analizándolo, esta declaración primero evalúa `x>7`, generando
un vector de tipo logical `c(FALSE, FALSE, TRUE, FALSE, TRUE)`, y después
selecciona los elementos de `x` que corresponden a los valores `TRUE`.

Podemos usar `==` para imitar el método previo de indexar por nombre
(recuerda que tiene que usar `==` en vez de `=` para comparaciones):


~~~
x[names(x) == "a"]
~~~
{: .language-r}



~~~
  a 
5.4 
~~~
{: .output}

> ## Sugerencia: Combinando condiciones lógicas
>
> A menudo queremos combinar múltiples criterios lógicos.
> Por ejemplo, podríamos querer encontrar todos los países que
> están en Asia **or** Europa **and** tienen expectativa de vida dentro de un cierto
> rango. Existen varias operaciones para combinar vectores lógicos en R:
>
>  * `&`, el operador "logical AND": retorna `TRUE` si ambos la izquierda y la derecha
>    son `TRUE`.
>  * `|`, el operador "logical OR": retorna `TRUE`, si cualquiera la izquierda o la derecha
>    (o ambos) son `TRUE`.
>
> A veces puedes ver `&&` y `||` en vez de `&` y `|`. Estos operadores de dos caracteres
> sólo miran al primer elemento de cada vector e ignoran el resto de
> elementos restantes. En general deberías no usar los operadores
> de dos caracteres en análisis de datos; resérvalos
> para programar, i.e. decidir si ejecutar una declaración o no.
>
>  * Operadores `!`, y "logical NOT": convierten `TRUE` en `FALSE` y `FALSE` en
>    `TRUE`. Puede negar una condición lógica (e.g. `!TRUE` ser convierte en
>    `FALSE`), o un vector entero de condiciones(e.g. `!c(TRUE, FALSE)` se convierte en
>    `c(FALSE, TRUE)`).
>
> Además, puedes comparar los elementos dentro de un único vector usando la
> función `all` (retorna `TRUE` si cada elemento del vector es `TRUE`)
> y la función `any` (retorna `TRUE` si uno o más elementos del
> vector son `TRUE`).
{: .callout}

> ## Challenge 2
>
> Dado el siguiente código :
>
> 
> ~~~
> x <- c(5.4, 6.2, 7.1, 4.8, 7.5)
> names(x) <- c('a', 'b', 'c', 'd', 'e')
> print(x)
> ~~~
> {: .language-r}
> 
> 
> 
> ~~~
>   a   b   c   d   e 
> 5.4 6.2 7.1 4.8 7.5 
> ~~~
> {: .output}
>
> Escribe un comando de hacer subconjuntos que retorne los valores de x que son mayores que 4 y menores que 7.
>
> > ## Solución al desafío 2
> >
> > 
> > ~~~
> > x_subset <- x[x<7 & x>4]
> > print(x_subset)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> >   a   b   d 
> > 5.4 6.2 4.8 
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Sugerencia: Obteniendo ayuda para los operadores
>
> Recuerda que puedes obtener ayuda para los operadores empaquetándolos entre comillas:
> `help("%in%")` or `?"%in%"`.
{: .callout}


> ## Manejando valores especiales
> En algún momento encontraremos funciones en R que no pueden manejar valores faltantes, infinito
> o datos indefinidos.
>
> Existen algunas funciones especiales que puedes usar para filtrar estos datos:
>
> * `is.na` regresa todas las posiciones de un vector, matriz. o data frame
> que contengan `NA` (o `NaN`)
> * de la misma manera, `is.nan`, y `is.infinite` hacen los mismo para `NaN` y `Inf`.
> * `is.finite` regresa todas las posiciones de un vector, matriz, o data frame
>   que no contengan `NA`, `NaN` o `Inf`.
> * `na.omit` filtra todos los valores faltantes de un vector
{: .callout}

## Data frames

Recordemos que las data frames son listas, por lo que aplican reglas similares.
Sin embargo estos también son objetos de dos dimensiones:

`[` con un argumento funcionará de la misma manera que para las listas, donde cada elemento
de la lista corresponde a una columna. El objecto devuelto será un data frame:


~~~
head(gapminder[3])
~~~
{: .language-r}



~~~
       pop
1  8425333
2  9240934
3 10267083
4 11537966
5 13079460
6 14880372
~~~
{: .output}

Similarmente, `[[` extraerá *una sola columna*:


~~~
head(gapminder[["lifeExp"]])
~~~
{: .language-r}



~~~
[1] 28.801 30.332 31.997 34.020 36.088 38.438
~~~
{: .output}

Y `$` proporciona atajo para extraer columnas por nombre:


~~~
head(gapminder$year)
~~~
{: .language-r}



~~~
[1] 1952 1957 1962 1967 1972 1977
~~~
{: .output}

Para seleccionar filas y/o columnas específicas, puedes proporcionar dos argumentos a `[` 


~~~
gapminder[1:3, ]
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap
1 Afghanistan 1952  8425333      Asia  28.801  779.4453
2 Afghanistan 1957  9240934      Asia  30.332  820.8530
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
~~~
{: .output}

Si nuestro subconjunto es una sola fila, el resultado será una data frame (porque los elementos son de distintos tipos):


~~~
gapminder[3, ]
~~~
{: .language-r}



~~~
      country year      pop continent lifeExp gdpPercap
3 Afghanistan 1962 10267083      Asia  31.997  853.1007
~~~
{: .output}

Pero para una sola columna el resultado será un vector (esto puede cambiarse con 
el tercer argumento, `drop = FALSE`).

> ## Challenge 3
>
> Corrige cada uno de los siguientes errores para hacer subconjuntos de data frames:
>
> 1. Extraer observaciones colectadas en el año 1957
>
>    
>    ~~~
>    gapminder[gapminder$year = 1957, ]
>    ~~~
>    {: .language-r}
>
> 2. Extraer todas las columnas excepto de la 1 a la 4
>
>    
>    ~~~
>    gapminder[, -1:4]
>    ~~~
>    {: .language-r}
>
> 3. Extraer las filas donde la esperanza de vida es mayor de 80 años
>
>    
>    ~~~
>    gapminder[gapminder$lifeExp > 80]
>    ~~~
>    {: .language-r}
>
> 4. Extraer la primera fila, y la cuarta y quinta columna
>   (`lifeExp` and `gdpPercap`).
>
>    
>    ~~~
>    gapminder[1, 4, 5]
>    ~~~
>    {: .language-r}
>
> 5. Avanzado: extraer las filas que contienen información para los años 2002
>    y 2007
>
>    
>    ~~~
>    gapminder[gapminder$year == 2002 | 2007,]
>    ~~~
>    {: .language-r}
>
> > ## Solución al desafío 3
> >
> > Corrige cada uno de los siguientes errores para hacer subconjuntos de data frames:
> >
> > 1. Extraer observaciones colectadas en el año 1957
> >
> >    
> >    ~~~
> >    # gapminder[gapminder$year = 1957, ]
> >    gapminder[gapminder$year == 1957, ]
> >    ~~~
> >    {: .language-r}
> >
> > 2. Extraer todas las columnas excepto de la 1 a la 4
> >
> >    
> >    ~~~
> >    # gapminder[, -1:4]
> >    gapminder[,-c(1:4)]
> >    ~~~
> >    {: .language-r}
> >
> > 3. Extraer las filas donde la esperanza de vida es mayor de 80 años
> >
> >    
> >    ~~~
> >    # gapminder[gapminder$lifeExp > 80]
> >    gapminder[gapminder$lifeExp > 80,]
> >    ~~~
> >    {: .language-r}
> >
> > 4. Extraer la primera fila, y la cuarta y quinta columna
> >   (`lifeExp` and `gdpPercap`).
> >
> >    
> >    ~~~
> >    # gapminder[1, 4, 5]
> >    gapminder[1, c(4, 5)]
> >    ~~~
> >    {: .language-r}
> >
> > 5. Avanzado: extraer las filas que contienen información para los años 2002
> >    and 2007
> >
> >     
> >     ~~~
> >     # gapminder[gapminder$year == 2002 | 2007,]
> >     gapminder[gapminder$year == 2002 | gapminder$year == 2007,]
> >     gapminder[gapminder$year %in% c(2002, 2007),]
> >     ~~~
> >     {: .language-r}
> {: .solution}
{: .challenge}

> ## Desafío 4
>
> 1. ¿Por qué `gapminder[1:20]` regresa un error? ¿En qué difiere de
>    `gapminder[1:20, ]`?
>
> 2. Crea un `data.frame` nuevo llamado `gapminder_small` que sólo contenga las filas
> de la 1 a la 9 y de la 19 a la 23. Puedes hacerlo en uno o dos pasos.
>
> > ## Solución al desafío 4
> >
> > 1.  `gapminder` es un data frame por lo que para hacer un subconjunto necesita dos dimensiones. `gapminder[1:20, ]` genera un subconjunto de los datos de las primeras 20 filas y todas las columnas.
> >
> > 2.
> >
> > 
> > ~~~
> > gapminder_small <- gapminder[c(1:9, 19:23),]
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}
