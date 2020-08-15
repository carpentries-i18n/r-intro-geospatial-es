---
# Por favor, no edites este archivo directamente; se genera de forma automática.
# En cambio, edita 01-rstudio-intro.md en _episodes_rmd/
title: "Introducción a R y RStudio"
teaching: 20
exercises: 5
questions:
- "¿Cómo encontrar lo que buscas en RStudio?"
- "¿Cómo interactuar con R?"
- "¿Cómo instalar paquetes?"
objectives:
- "Describe el propósito y el uso de cada panel en el IDE RStudio"
- "Localiza botones y opciones en el IDE RStudio"
- "Define una variable"
- "Asigna datos a una variable"
- "Usa operadores matemáticos y de comparación"
- "Llama funciones"
- "Administra paquetes"
keypoints:
- "Usa RStudio para escribir y ejecutar programas R."
- "R tiene los operadores aritméticos habituales."
- "Usa `<-` para asignar valores a las variables."
- "Usa `install.packages()` para instalar paquetes (bibliotecas)."
source: Rmd
---




## Motivación

La ciencia es un proceso de múltiples etapas: una vez que haz diseñado un experimento y
recolectado datos, ¡empieza la diversión real! Esta lección te enseñará cómo empezar
 este proceso usando R y RStudio. Empezaremos con datos crudos, realizaremos 
análisis exploratorios y aprenderemos cómo graficar los resultados. Este ejemplo
empieza con un conjunto de datos de [gapminder.org](https://www.gapminder.org) que contiene
información poblacional para muchos países a través del tiempo.
¿Puedes leer los datos en R? ¿Puedes graficar la población para Senegal? ¿Puedes calcular el ingreso promedio para países del continente asiático? Al final de estas lecciones, 
¡serás capaz de hacer cosas tales como graficar la población de todos estos países
en menos de un minuto!

## Antes de comenzar el taller

Por favor asegúrate de tener la última versión de R y de RStudio instalada en tu computadora. Esto es importante, porque algunos paquetes utilizados en el taller pueden no instalarse correctamente (o directamente no instalarse) si R no está al día.

- [Descarga e instala la última versión de R aquí](https://www.r-project.org/)
- [Descarga e instala RStudio aquí](https://www.rstudio.com/)

## Introducción a RStudio

A lo largo de esta lección, te enseñaremos algunos de los fundamentos
del lenguaje R así como algunas de las mejores prácticas para organizar el código para
proyectos científicos, lo que te hará la vida más fácil.

Usaremos RStudio: un entorno de desarrollo integrado (IDE por su nombre en inglés) gratuito y de código abierto.
RStudio provee un editor incorporado, funciona en todas las plataformas (incluyendo servidores)
y provee muchas ventajas como el hecho de integrarse con control de versiones y manejo de proyectos.



**Diseño básico**

Cuando abres RStudio por primera vez, serás bienvenida por tres paneles:

* La consola interactiva de R (panel completo a la izquierda)
* Entorno/Historia (pestañas arriba a la derecha)
* Archivos/Gráficos/Paquetes/Ayuda/Visualización (pestañas abajo a la derecha)

![Diseño de RStudio]({{ site.baseurl }}/fig/01-rstudio.png)

Una vez que abres archivos, como scripts de R, un panel de edición se abrirá también
arriba a la izquierda.

![Diseño de RStudio con un archivo .R abierto]({{ site.baseurl }}/fig/01-rstudio-script.png)


## Flujo de trabajo dentro de RStudio

Hay dos maneras principales en las que se puede trabajar dentro de RStudio.

1. Evaluar y ejecutar dentro de la consola interactiva de R y luego copiar el código dentro
de un archivo .R para correrlo más tarde
   *  Esto funciona bien cuando se hacen pequeñas pruebas y al inicio del trabajo.
   *  Rápidamente se transforma en un método laborioso
2. Comenzar escribiendo en un archivo .R y usar los atajos de teclado de RStudio para el comando Ejecutar
para llevar la línea actual, las líneas seleccionadas o líneas modificadas a la consola interactiva de R.
   * Esta es una manera genial de comenzar; todo tu código es guardado para más tarde
   * Podrás correr el archivo que has creado dentro de RStudio
o usando la función R's `source()`.

> ## Consejo: correr segmentos de tu código
>
> RStudio te ofrece una gran flexibilidad para correr código dentro de la ventana del editor.
> Hay botones, menúes de elección y atajos de teclado. Para correr la
> línea actual, puedes 
>
> 1. hacer clic en el botón `Run` arriba del panel de edición, o
> 2. seleccionar "Run Lines" del menú "Code", o 
> 3. presionar <kbd>Ctrl</kbd>+<kbd>Enter</kbd> en Windows,
> <kbd>Ctrl</kbd>+<kbd>Enter</kbd> en Linux, 
> o <kbd>&#8984;</kbd>+<kbd>Enter</kbd> en OS X.
> (Este atajo también puede ser visualizado al posicionar
> el ratón sobre el botón). Para correr un bloque de código, selecciónalo y luego `Run`.
> Si haz modificado una línea de código dentro de un bloque de código que acabas de ejecutar,
> no hay necesidad de re-seleccionar la sección y `Run`, puedes usar el siguiente
> botón
> por su cuenta, `Re-run the previous region`. Esto ejecutará el bloque de código anterior
> incluyendo las modificaciones que hayas realizado.
{: .callout}

## Introducción a R

Pasarás mucho de tu tiempo en R en la consola interactiva
Allí es donde ejecutarás todo tu código y puede ser un
entorno útil para probar ideas antes de agregarlas a un archivo de script de R.
Esta consola en RStudio es la misma que tendrías si
escribieras en el entorno de línea de comandos de `R`.

Lo primero que verás en la sesión interactiva de R es un conjunto de
información, seguida de un ">" y un cursor titilante. De muchas maneras
esto es similr al entorno de consola que has aprendido en las lecciones de consola:
opera sobre la misma idea de un ciclo de "Lectura, evaluación y visualización":
escribes comandos, R intenta ejecutarlos y luego devuelve un resultado.

## Usando R como una calculadora

Lo más simple que puedes hacer en R es aritmética:


~~~
1 + 100
~~~
{: .language-r}



~~~
[1] 101
~~~
{: .output}

Y R va a mostrar la respuesta, con un "`[1]`" precedente. No te preocupes por
esto por ahora, lo explicaremos más tarde. Por ahora piensa que eso es un indicador
de un resultado.

Como bash, si escribes un comando incompleto, R esperará que tú lo completes:

~~~
> 1 +
~~~
{: .language-r}

~~~
+
~~~
{: .output}

En cualquier momento que presiones Enter y la sesión de R muestre "`+`" en vez de un "`>`",
significa que R está esperando que completes el comando. Si quieres cancelar un
comando puedes simplemente "<kbd>Esc</kbd>" y RStudio te devolverá el indicador "`>`".

> ## Sugerencia: Cancelando comandos
> Si estás utilizando R desde la línea de comando en lugar de RStudio,
> necesitas usar  <kbd>Ctrl</kbd>+<kbd>C</kbd>en lugar de <kbd>Esc</kbd>
> para cancelar el comando. ¡Esto también se aplica a los usuarios de Mac!
>
> Cancelar un comando no solo es útil para interrumpir comandos incompletos:
> también puedes usarlo para decirle a R que deje de ejecutar código (por ejemplo, si está
> tardando mucho más de lo que esperas), o para deshacerte del código que estás
> escribiendo en ese momento.
{: .callout}

Cuando usas R como calculadora, el orden de las operaciones es el mismo que
habrías aprendido en la escuela. 

De mayor a menor precedencia:

* Paréntesis: `(`, `)`
 * Exponente: `^` o `**`
* Divide: `/`
 * Multiplica: `*`
 * Suma: `+`
 * Resta: `-`


~~~
3 + 5 * 2
~~~
{: .language-r}



~~~
[1] 13
~~~
{: .output}

Usa paréntesis para agrupar operaciones y forzar el orden de
evaluación si difiere de la predeterminada, o para aclarar tu
objetivo.


~~~
(3 + 5) * 2
~~~
{: .language-r}



~~~
[1] 16
~~~
{: .output}

Esto puede volverse incómodo cuando no es necesario, pero clarifica tus intenciones.
Recuerde que otros pueden leer tu código más adelante.


~~~
(3 + (5 * (2 ^ 2))) # difícil de leer
3 + 5 * 2 ^ 2       # claro, si recuerdas las reglas
3 + 5 * (2 ^ 2)     # si no recuerdas algunas reglas, esto puede ayudar
~~~
{: .language-r}


El texto luego de cada línea de código se llama
"comentario". Cualquier cosa que siga a un signo numeral
`#` es ignorado por R cuando ejecuta código. 

Números muy pequeños o muy grandes obtienen una notación científica:


~~~
2/10000
~~~
{: .language-r}



~~~
[1] 2e-04
~~~
{: .output}

Que es la versión abreviada de "multiplicado por `10^XX`". Entonces, `2e-4`
es la abreviación de `2 * 10^(-4)`.

También puedes escribir número en notación científica:


~~~
5e3  # Note la falta de menos aquí
~~~
{: .language-r}



~~~
[1] 5000
~~~
{: .output}

No te preocupes por tratar de recordar cada función en R. Puedes buscarlas
en Google, o si puedes recordar el comienzo del nombre de la función, usa completar con 
Tab en RStudio.

Esta es una ventaja que RStudio tiene sobre R por sí mismo, tiene capacidades de 
autocompletado que te permiten buscar más fácilmente las funciones, sus argumentos y
los valores que estos toman.

Escribir un `?` antes del nombre de un comando abrirá la página de ayuda 
del mismo. Además de proporcionar una descripción detallada del comando y cómo
funciona, desplazarse hasta la parte inferior de la página de ayuda generalmente mostrará una colección
de ejemplos de código que ilustran el uso del comando. Veremos un ejemplo
más tarde.

## Comparando cosas

También podemos realizar comparaciones en R:


~~~
1 == 1  # igualdad (dos signos de igual se leen como "es igual a")
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 != 2  # distinto de
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 < 2  # menor que
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 <= 1  # menor o igual a
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 > 0  # mayor que
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 >= -9 # mayor o igual a
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}

> ## Sugerencia: Comparando números
>
> Una advertencia sobre la comparación de los números: nunca
> deberías usar `==` para comparar dos números a menos que sean
> **integers** (un tipo de datos que representa específicamente
> solo números enteros).
>
> Las computadoras sólo pueden representar números decimales con un
> cierto grado de precisión, por lo que dos números que parecen
>iguales al imprimirlos en R, pueden en realidad tener
> diferentes representaciones subyacentes y, por lo tanto, pueden
> diferir por un pequeño margen de error (llamado 
> Machine numeric tolerance).
>
> En lugar de eso, deberías usar la función  `all.equal`.
>
> Leer más en: [http://floating-point-gui.de/](http://floating-point-gui.de/)
{: .callout}

## Variables y asignación

Podemos almacenar valores en variables usando el operador de asignación `<-`, así:


~~~
x <- 1/40
~~~
{: .language-r}

Observa que la asignación no imprime un valor. En cambio, lo almacenamos para más
tarde en algo llamado **variable**. `x` ahora contiene el **valor**` 0.025`:


~~~
x
~~~
{: .language-r}



~~~
[1] 0.025
~~~
{: .output}

Más precisamente, el valor almacenado es una *aproximación decimal* de esta fracción llamada [número de coma flotante](http://en.wikipedia.org/wiki/Floating_point).

Busca la pestaña `Environment` en uno de los paneles de RStudio, y verás que ` x` y su valor
han aparecido. Nuestra variable `x` puede usarse en lugar de un número en cualquier cálculo que espere un número:


~~~
log(x)
~~~
{: .language-r}



~~~
[1] -3.688879
~~~
{: .output}

Observa también que las variables pueden ser reasignadas:


~~~
x <- 100
~~~
{: .language-r}

`x` contenía el valor 0.025 y ahora tiene el valor 100.

Los valores de asignación pueden contener la variable a la que se asignan:


~~~
x <- x + 1 #Observa como RStudio actualiza su descripción de x en la pestaña superior derecha
y <- x * 2
~~~
{: .language-r}

El lado derecho de la asignación puede ser cualquier expresión válida de R.
El lado derecho se *evalúa por completo* antes de que ocurra la asignación.

> ## Desafío 1
>
> ¿Cuál será el valor de cada variable después de cada
> declaración en el siguiente programa?
>
> 
> ~~~
> mass (masa) <- 47.5
> age (edad) <- 122
> mass (masa) <- mass * 2.3
> age (edad) <- age - 20
> ~~~
> {: .language-r}
>
> > ## Solución  al desafío 1
> >
> > 
> > ~~~
> > mass (masa) <- 47.5
> > ~~~
> > {: .language-r}
> > Esto dará un valor de 47.5 para la variable mass (masa)
> >
> > 
> > ~~~
> > age (edad) <- 122
> > ~~~
> > {: .language-r}
> > Esto dará un valor de 122 para la variable age (edad)
> >
> > 
> > ~~~
> > mass (masa) <- mass * 2.3
> > ~~~
> > {: .language-r}
> > Esto multiplicará el valor existente de 47.5 by 2.3 para dar un nuevo valor de
> > 109.25 para la variable mass (masa).
> >
> > 
> > ~~~
> > age (edad) <- age - 20
> > ~~~
> > {: .language-r}
> > Esto restará 20 del valor existente de 122 para dar un nuevo valor
> > de 102 a la variable age (edad).
> {: .solution}
{: .challenge}


> ## Desafío 2
>
> Ejecuta el código del desafío anterior y escribe un comando para
> comparar la masa con la edad. ¿La masa es mayor que la edad?
>
> > ## Solución al desafío 2
> >
> > Una forma de responder a esta pregunta en R es usar el `>` para configurar lo siguiente:
> > 
> > ~~~
> > mass > age
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] TRUE
> > ~~~
> > {: .output}
> > Esto debería producir un valor booleano de VERDADERO (TRUE) ya que  109.25 es más grande que 102.
> {: .solution}
{: .challenge}


Los nombres de las variables pueden contener letras, números, guiones bajos y puntos. Ellos
no puede comenzar con un número ni contener espacios en absoluto. Diferentes personas usan
diferentes convenciones para nombres de variables largos, estas incluyen

  * puntos.entre.palabras
  * guiones_ bajos\ _entre_palabras
  * CamelCaseParaSepararPalabras

Lo que uses depende de ti, pero **debes ser consistente**.

También es posible utilizar el operador `=` para la asignación:


~~~
x = 1/40
~~~
{: .language-r}

Pero esto es mucho menos común entre los usuarios de R. Lo mas importante es
**Ser consistennte** con el operador que uses. Ocasionalmente hay lugares
donde es menos confuso usar `<-` que` = `, y este es el símbolo más común
en la comunidad. Entonces la recomendación es usar `<-`. 

> ## Desafío 3
>
> ¿Cuáles de los siguientes son nombres de variables válidos en R?
> 
> ~~~
> min_height
> max.height
> _age
> .mass
> MaxLength
> min-length
> 2widths
> celsius2kelvin
> ~~~
> {: .language-r}
>
> > ## Solución al desafío 3
> >
> > Los siguientes nombres pueden estar usados para variables en R:
> > 
> > ~~~
> > min_height
> > max.height
> > MaxLength
> > celsius2kelvin
> > ~~~
> > {: .language-r}
> >
> > Lo siguiente crea una variable oculta:
> > 
> > ~~~
> > .mass
> > ~~~
> > {: .language-r}
> >
> > No discutiremos las variables ocultas en esta lección. Recomendamos no utilizar un punto en el
> > comienzo de los nombres de las variables a menos que desee ocultar sus variables.
> >
> > Los siguientes nombres no se podrán utilizar para crear una variable
> > 
> > ~~~
> > _age
> > min-length
> > 2widths
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

