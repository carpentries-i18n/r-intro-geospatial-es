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
a sú directorio `data/`

#### [Data Structures]({{ relative_root_path }}/{% link _episodes/03-data-structures-part1.md %})

* Learners will work with factors in the following lesson. Be sure to 
cover this concept.
* If needed for time reasons, you can skip the section on lists. The learners
don't use lists in the rest of the workshop.

#### [Exploring Data Frames]({{ relative_root_path }}/{% link _episodes/04-data-structures-part2.md %})

* Pay attention to and explain the errors and warnings generated from the examples in this episode.

#### [Subsetting Data]({{ relative_root_path }}/{% link _episodes/05-data-subsetting.md %})

* The episode after this one covers the `dplyr` package, which has an 
alternate subsetting mechanism. Learners do still need to learn the 
base R subsetting covered here, as `dplyr` won't work in all situations. However,
the examples in the rest of the workshop focus on `dplyr` syntax.

#### [Dataframe Manipulation with dplyr]({{ relative_root_path }}/{% link _episodes/06-dplyr.md %})

* Introduce the `dplyr` package as a simpler, more intuitive way of doing
subsetting. 
* Unlike other SWC and DC R lessons, this lesson does **not** include data 
reshaping with `tidyr` as it isn't used in the rest of the workshop.

#### [Introduction to Visualization]({{ relative_root_path }}/{% link _episodes/07-plot-ggplot2.md %})

* This episode introduces `geom_col` and `geom_histogram`. These geoms are used
in the rest of the workshop, along with geoms specifically for geospatial data.
* Emphasize that we will go much deeper into visualization and creating
publication-quality graphics later in the workshop.

#### [Writing Data]({{ relative_root_path }}/{% link _episodes/08-writing-data.md %})

* Learners will need to have created the directory structure described in 
[Project Management With RStudio]({{ relative_root_path }}{% link _episodes/02-project-intro.md %}) in order for the code
in this episode to work. 

#### Concluding remarks

* Now that learners know the fundamentals of R, the rest of the workshop
will apply these concepts to working with geospatial data in R. 
* Packages and functions specific for working with geospatial data will be
the focus of the rest of the workshop. 
* They will have lots of changes to practice applying and expanding these
skills in the next lesson. 

## Technical tips and tricks

* Leave about 30 minutes at the start of each workshop and another 15 mins
at the start of each session for technical difficulties like WiFi and
installing things (even if you asked students to install in advance, longer if
not).

* Be sure to actually go through examples of an R help page: help files
can be intimidating at first, but knowing how to read them is tremendously
useful.

* Don't worry about being correct or knowing the material back-to-front. Use
mistakes as teaching moments: the most vital skill you can impart is how to
debug and recover from unexpected errors.

## Common problems

TBA - Instructors please add situations you encounter here.


{% include links.md %}

