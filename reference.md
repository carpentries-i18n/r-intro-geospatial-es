---
layout: reference
---
{% include base_path.html %}

## Referencia

## [Introducción a R y RStudio]({{ relative_root_path }}/{% link _episodes/01-rstudio-intro.md %})

 - Use la tecla **escape** para cancelar comandos incompletos o el código en ejecución
   (Ctrl+C) si está usando R desde la terminal.
 - Las operaciones aritméticas básicas siguen un orden estándar de precedencia:
   - Paréntesis: `(`, `)`
   - Exponentes: `^` o `**`
   - División: `/`
   - Multiplicación: `*`
   - Suma: `+`
   - Resta: `-`
 - La notación científica está disponible, por ejemplo: `2e-3`
 - Todo lo que se encuentre a la derecha de un símbolo `#` es un comentario, y R lo ignorará!
 - Las funciones se denotan por `function_name()`. Las expresiones dentro de
   los paréntesis se evalúan antes de ser pasadas a la función, y las
   funciones pueden estar anidadas.
 - Operadores de comparación: `<`, `<=`, `>`, `>=`, `==`, `!=`
 - Utilice `all.equal` para comparar valores numéricos!
 - `<-` es el operador de asignación. Todo a su derecha se evalúa, y luego
   es almacenado en una variable nombrada a la izquierda.
 - `ls` genera una lista de todas las variables y funciones creadas
 - `rm` se puede utilizar para eliminarlas
 - Al asignar valores a los argumentos de una función,  debe usar `=`.

## [Gestión de proyectos con RStudio]({{ relative_root_path }}/{% link _episodes/02-project-intro.md %})

 - Para crear un nuevo proyecto, diríjase a Archivo -> Nuevo Proyecto
 - Algunas buenas practicas:
   * Trate a los datos como sólo lectura
   * Mantenga los datos ordenados separados de los datos crudos desordenados
   * Trate la salida generada como desechable
   * Mantenga los datos relacionados juntos
   * Utilice un esquema consistente de nomenclatura

## [Estructura de datos]({{ relative_root_path }}/{% link _episodes/03-data-structures-part1.md %})

- Utilice `read.csv()` para importar los datos a la memoria
- ` class()` devuelve la clase de datos de su objeto
- R convierte automáticamente los tipos de datos
- Las funciones: `length()`, `nrow()`, `head()`, `tail()`, y `str()` pueden ser
  útiles para explorar los datos.
- Los **factors** (factores) son una clase especial para trabajar con datos categóricos.
- Las **lists** (listas) proveen un tipo flexible de datos.
- Los **data frames** son un caso especial de listas.

## [Explorando **Data Frames**]({{ relative_root_path }}/{% link _episodes/04-data-structures-part2.md %})

* R facilita la importación de datos almacenados en forma remota
* **[**Data Frames**]({{ relative_root_path }}/05-data-structures-part2/)**
 - `?data.frame` es una estructura de datos clave. Es una `lista` de `vectores`.
 - `cbind()` adicionará una columna (vector) a un **data.frame**.
 - `rbind()` adicionará una fila (lista) a un **data.frame**.

 **Funciones útiles para consultar la estructura de los datos:**
 - `?str` estructura, imprime un resumen de la estructura de datos
 - `?class` indica cual es la clase de los datos
 - `?head` imprime los primeros `n` elementos (filas para objetos bidimensionales)
 - `?tail` imprime los últimos `n` elementos (filas para los objetos bidimensionales)
 - `?rownames`, `?colnames`, `?dimnames` recupera o modifica los nombres de filas
   y de columnas de un objeto.
 - `?length` devuelve el número de elementos en un vector atómico
 - `?nrow`, `?ncol`, `?dim` da las dimensiones de un objeto n-dimensional (No funciona en vectores atómicos o listas).
* Si tu **data frame** contiene factores, debes seguir algunos pasos adicionales para agregar filas
  que contengan nuevos valores de categorías (level).

- `read.csv` para leer datos en una estructura regular
   - `sep` argumento para especificar el separador
     - "," para el separador coma
     - "\t" para  el separador tabulador
   - Otros argumentos:
     - `header=TRUE` si hay una fila de encabezado


## [Subconjunto de datos]({{ relative_root_path }}/{% link _episodes/05-data-subsetting.md %})

 - Se puede acceder a los elementos con:
   - Índice
   - Nombre
   - Vectores lógicos

- `[` corchetes simples:
   - *extract* (extraer) elementos individuales o *subset* (subdividir) vectores
    - por ejemplo, `x[1]` extrae el primer elemento de un vector x.
   - *extract* elementos simples de una lista. El valor devuelto será otra `list()`.
   - *extract* columnas de un **data.frame**
 - `[` con dos argumentos para:
   - *extract* renglones y/o columnas de 
     - matrices
     - data.frames
     - ejemplo `x[1,2]` extraerá el valor en el renglón 1, columna 2.
     - ejemplo `x[2,:]` extraerá la segunda columna de valores completa.

 - `[[` dobles corchetes para extraer elementos de una  lista.
 - `$` para acceder a las columnas o elementos lista por nombre
 - indices negativos saltan elementos


## [Manipulación de Data frame con dplyr]({{ relative_root_path }}/{% link _episodes/06-dplyr.md %})


 - `?select` para extraer variables por nombre.
 - `?filter` regresa filas con condiciones que se cumplen.
 - `?group_by` agrupa los datos por una o mas variables.
 - `?summarize` resume múltiples valores en un solo valor.
 - `?mutate` agrega nuevas variables a un **data.frame**.
 - `?count` y `?n` para contar los valores en el data frame.
 - Combina operadores usando el operador pipe `?"%>%"`.


## [Control del flujo]({{ relative_root_path }}/{% link _episodes/07-plot-ggplot2.md %})


 -Las figuras se pueden crear con la gramática de los gráficos:
   - `library(ggplot2)`
   - `ggplot` para crear la base de la figura
   - `aes` especifica la estética de los ejes, la forma, color, y tamaño de los datos
   - `geom` funciones que especifican el tipo de gráfico, por ejemplo  `point`, `line`, `density`, `box`
   - `geom` estas funciones también agregan transformaciones estadisticas, por ejemplo. `geom_smooth`
   - `scale` función que cambia el mapeo de datos a estética
   - `facet` función que estratifica la figura dentro de paneles
   - `aes` se aplica a capas individuales, o puede ser definido para la grafica completa
     dentro de `ggplot`.
   - `theme` función que cambia la apariencia completa de la gráfica
   - ¡El orden de las capas(layers) importa!
   - `ggsave` para salvar una figura.


## [Escribiendo datos]({{ relative_root_path }}/{% link _episodes/08-writing-data.md %})

 - `write.table` para escribir objetos en formato regular


## Glosario

{:auto_ids}
argumentos
:   Un valor dado a una función o programa mientras corre.
    El termino es frecuentemente intercambiando  (inconsistentemente) con  [parámetro](#parameter).

asignar
: Darle un nombre a un valor al asociarlo a una variable.

cuerpo
: (de una función): las instrucciones y comandos que se ejecutan cuando se corre una función.

comentario
: Una observación en un programa destinado a ayudar a los lectores humanos a comprender lo que está sucediendo, pero que es ignorado por la computadora.
Los comentarios en Python, R y la consola de Unix comienzan con un carácter `#` y se ejecutan hasta el final de la línea;
     los comentarios en SQL comienzan con `--`,
     y otros lenguajes tienen otras convenciones.

valores separados por coma
: (CSV) Una representación textual común para tablas
en el que los valores en cada fila están separados por comas.

delimitador
: Un caracter o caracteres utilizados para separar valores individuales,
como las comas entre columnas en un archivo [CSV](#comma-separated-values).

documentación
: Texto en lenguaje humano escrito para explicar qué hace un software,
cómo funciona o cómo usarlo.

número de coma flotante
: Un número que contiene una parte fraccionaria y un exponente.
Ver también: [entero](#integer).

bucle for
: Un bucle que se ejecuta una vez para cada valor que hay en un conjunto, lista o rango.
Ver también: [bucle while](# while-loop).

indice
: Un subíndice que especifica la ubicación de un solo valor en una colección,
como un solo píxel en una imagen.

entero
: Un número entero, como -12343. Ver también: [número de coma flotante](#floating-point-number).

biblioteca
: En R, los directorios donde los [paquetes]](#package) son almacenados.

paquete
: Una colección de funciones de R, datos y código compilado en un formato bien definido. Los paquetes se almacenan en una [biblioteca](#library) y se cargan usando la función **library()**.

parametro
: Una variable nombrada en la declaración de la función que se utiliza para contener un valor pasado durante la llamada.
El término a menudo se usa indistintamente (e inconsistentemente) con [argumento](#argument).

sentencia de retorno
:  Una declaración que hace que una función deje de ejecutarse y devuelva un valor a quien la invocó de inmediato.

secuencia
:  Una colección de información que se presenta en un orden específico.

forma
: Dimensiones de una matriz, representadas como un vector.
Por ejemplo, la forma de una matriz de 5 × 3 es `(5,3)`.

cadena
: Abreviatura de "cadena de caracteres",
una [secuencia](#sequence) de cero o más caracteres.

error de sintaxis
:   Un error de programación que ocurre cuando las declaraciones están en un orden o contienen 
   caracteres no esperados por el lenguaje de programación.

tipo
:   La clasificación de algo en un programa (por ejemplo, el contenido de una variable)
    como un tipo de número (por ejemplo [floating-point](#float), [integer](#integer)), [string](#string),
    o algo más. En R el comando typeof() se usa para consultar el tipo de una variable.

while loop
:   Un bucle que se ejecuta siempre que una condición dada sea verdadera.
    Ver también: [for loop](#for-loop).

