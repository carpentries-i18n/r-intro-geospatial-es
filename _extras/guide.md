---
layout: page
title: "Notas del Instructor"
---
{% include base_path.html %}

relative path root: {{ relative_root_path }}

## Notas del instructor

## Motivación de la lección y objetivos de aprendizaje

Esta lección esta diseñada para introducir a los estudiantes conceptos básicos de R que necesitarán para completar las otras lecciones de este taller. Esta planeado para estudiantes que no tienen experiencia previa con R. Si todos los alumnos del taller han completado otro taller de Software o Data Carpentry R, o ha realizado otros cursos de R, puede saltarse esta lección y ir directamente a la lección [Introduction to Geospatial Raster and Vector Data with R](https://datacarpentry.org/r-raster-vector-geospatial/)

Esta lección es una versión reducida de la lección SWC [R for Reproducible Scientific Analysis](http://swcarpentry.github.io/r-novice-gapminder). No cubre la visualización en detalle, ya que la última lección de este taller cubre la visualización en el contexto de los datos geospaciales. 

## Diseño de la lección

#### [Introducción a R y RStudio]({{ relative_root_path }}/{% link _episodes/01-rstudio-intro.md %})

* Si el taller incluye lecciones de [Introduction to Geospatial Concepts](https://datacarpentry.org/organization-geospatial/), los estudiantes tendrán
la introducción a RStudio en el contexto general del software geoespacial
* Haga que sus alumnos abran RStudio y le sigan mientras que explica cada panel. Asegúrese de que el entorno de Rstudio sea el predeterminado para que los alumnos puedan seguirlo
* Asegúrese de explicar cómo ejecutar el código desde la ventana de script, tanto si usted esta utilizando el botón Run o desde el atajo desde el teclado
* Los estudiantes usarán varias biblioteca en la próxima lección, así que debe de asegurarse de introducir como introducir una biblioteca y cómo se instala.

#### [Project Management With RStudio]({{ relative_root_path }}/{% link _episodes/02-project-intro.md %})

*  Asegúrese de que los alumnos descarguen los archivo de datos en el Desafío 1 y muevan esos datos 
a su directorio `data/`

#### [Data Structures]({{ relative_root_path }}/{% link _episodes/03-data-structures-part1.md %})

* Los alumnos trabajarán con factores en la siguiente lección.
Asegúrate de
cubrir este concepto.
* Si por razones de tiempo es necesario, puede saltearse la sección de listas. Las estudiantes no usan listas en el resto del taller.

#### [Exploring Data Frames]({{ relative_root_path }}/{% link _episodes/04-data-structures-part2.md %})

* Presta atención y explica los errores y advertencias generados a partir de los ejemplos de este episodio.

#### [Subsetting Data]({{ relative_root_path }}/{% link _episodes/05-data-subsetting.md %})

* El episodio siguiente cubre el paquete  `dplyr` , que tiene un
mecanismo alternativo de extraer subconjuntos. Las estudiantes todavía tienen que aprender
la extracción de subconjuntos de R base vista aquí, ya que `dplyr` no va a funcionar en todas las situaciones. Sin embargo,
los ejemplos del resto del taller se centran en la sintaxis `dplyr`.

#### [Dataframe Manipulation with dplyr]({{ relative_root_path }}/{% link _episodes/06-dplyr.md %})

* Introduce el paquete `dplyr` como una forma más simple, más intuitiva de 
extraer subconjuntos. 
* A diferencia de otras lecciones de R de SWC y DC, esta lección no incluye 
modificación de datos con `tidyr` ya que no se usa en el resto del taller.

#### [Introduction to Visualization]({{ relative_root_path }}/{% link _episodes/07-plot-ggplot2.md %})

* Este episodio introduce `geom_col` y  `geom_histogram`. Estas geoms se usan
en el resto del taller, junto con geoms específicas para datos geoespaciales.
* Enfatiza que iremos mucho más profundo en la visualización y la creación
de gráficos con calidad de publicación más tarde en el taller.

#### [Writing Data]({{ relative_root_path }}/{% link _episodes/08-writing-data.md %})

* Las alumnas necesitan haber creado la estructura de directorio descrita en 
[Project Management With RStudio]({{ relative_root_path }}{% link _episodes/02-project-intro.md %}) para que el código
de este episodio funcione. 

#### Observaciones finales

* Ahora que las alumnas conocen los fundamentos de R, en el resto del taller
aplicarán estos conceptos para trabajar con datos geoespaciales en R. 
* Los paquetes y funciones específicos para trabajar con datos geoespaciales serán el centro del resto del taller. 
* Tendrán muchos cambios para practicar aplicando y expandiendo esas habilidades en la siguiente lección.

## Trucos y consejos técnicos

* Deje unos 30 minutos al comienzo de cada taller y otros 15 minutos.
al inicio de cada sesión por dificultades técnicas como WiFi o
instalar cosas (incluso si les pediste a los estudiantes que lo instalaran con anticipación, más tiempo si
no).

* Asegúrate de revisar ejemplos de una página de ayuda de R: archivos de ayuda
Puede resultar intimidante al principio, pero saber leerlos es tremendamente
útil.

* No te preocupe por ser correcto o conocer el material al derecho y al revé. Úsalo
Errores como momentos de enseñanza: la habilidad más vital que puede impartir es cómo 
depurar y  recuperarse de errores inesperados.

## Problemas comunes

TBA - Instructores, aquí agreguen situaciones que encuentren.

