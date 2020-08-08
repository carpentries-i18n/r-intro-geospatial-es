---
# Por favor no edites este archivo directamente; es autogenerado.
# en su lugar, porfavor edita el epidosio 02-project-intro.md en _episodes_rmd/
title: "Gestión de proyectos con RStudio"
teaching: 10
exercises: 5
questions:
- "¿Cómo puedo manejar mis proyectos en RStudio?"
objectives:
- Crear proyectos en RStudio
keypoints:
- "Usa RStudio para crear y manejar proyectos de una manera consistente."
- "Trata los datos originales sólo para lectura."
- "Trata los resultados generados como salida desechable."
source: Rmd
---



## Introducción

El proceso científico es naturalmente incremental, y muchos proyectos comienzan la vida como
notas al azar, algo de código, luego un manuscrito, y eventualmente todo estará un poco
mezclado. Organizar un proyecto que involucra datos espaciales no es diferente de
cualquier otro proyecto de análisis de datos, aunque puede requerir más espacio en disco que
lo usual.

<div class="text-center">
<blockquote class="twitter-tweet"><p> Gestionar los proyectos de manera reproducible no sólo hace que la ciencia sea reproducible, sino que te facilita la vida.</p>— Vince Buffalo (@vsbuffalo) <a href="https://twitter.com/vsbuffalo/status/323638476153167872">April 15, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

Algunas personas organizan sus proyectos así:

![]({{ site.baseurl }}/fig/bad_layout.png)

Hay muchas razones por las que *SIEMPRE* debemos evitar esto:

1. Es difícil saber qué versión de tus datos es
la original y cuál es la modificada;
2. Está desorganizado porque mezcla archivos con varias extensiones juntas;
3. Se necesita más tiempo para encontrar cosas y para encontrar el código que se utilizó para generar las figuras.

Un buen diseño de proyecto hará tu vida más fácil:

*  Ayudará a garantizar la integridad de tus datos;
*  Facilita compartir tu código con otra persona
(un compañero de laboratorio, colaborador o supervisor);
* Te permite subir fácilmente tu código cuando envías tu manuscrito;
* Facilita la volver al proyecto después de un descanso.

## Una solución posible

 Afortunadamente, existen herramientas y paquetes que pueden ayudarte a administrar su trabajo de manera efectiva.

 Uno de los aspectos más potentes y útiles de RStudio es su funcionalidad para gestión de proyectos.
Usaremos esto hoy para crear un proyecto autocontenido, reproducible.


> ## Desafío: Crear un proyecto autocontenido
>
> Vamos a crear un nuevo proyecto en RStudio:
>
>  1. Dale clic en el botón de menú "Archivo", luego en "Nuevo proyecto".
> 2. Dale clic en "Nuevo directorio".
> 3. Dale clic en "Proyecto vacío".
> 4. Escribe "r-geoespacial" como el nombre del directorio.
> 5. Dale clic en el botón "Crear proyecto".
{: .challenge}

Una ventaja clave de un proyecto en RStudio es que cada vez que abrimos este proyecto en
sesiones posteriores de RStudio nuestro directorio de trabajo *siempre* se establecerá en la misma
carpeta, por ejemplo la que creamos `r-geoespacial`.
Verifiquemos nuestro directorio de trabajo ingresando lo siguiente en la consola de R:

```r
getwd()
```

R retornará `your/path/r-geospatial` como el directorio de trabajo.

## Buenas prácticas para la organización del proyecto

Aunque no hay una "mejor" manera de diseñar un proyecto, hay algunos
principios a seguir que harán que la gestión del proyecto sea más fácil:

### Tratar los datos como sólo lectura

Este es probablemente el objetivo más importante de establecer un proyecto. Collectar datos
normalmente requiere mucho tiempo y / o es costoso. Trabajajando con datos
interactivamente (por ejemplo, en Excel) te permite modificar los datos todo el tiempo y significa que nunca estás
segura de dónde provienen los datos o cómo se han modificado desde la recopilación.
Por lo tanto, es una buena idea tratar tus datos como "sólo lectura".

### Limpiando datos

En muchos casos, tus datos estarán "desordenados": y necesitarán un preprocesamiento
para obtener un formato para R (o cualquier otro lenguaje de programación). Esta
tarea a veces se denomina "limpiar datos". Resulta útil guardar estos pasos en una carpeta
separada llamada `scripts` y crear una segunda carpeta de `datos_limpios` "de solo lectura" para guardar el
conjuntos de datos "limpios".

### Trata los resultados generados como salida desechable

Cualquier cosa generada por tus scripts debe tratarse como desechable: los resultados deberán
poderse regenerarse a partir de tus scripts.

Hay muchas formas diferentes de administrar las salida. Me parece útil
tener una carpeta de salida con diferentes subdirectorios para cada análisis por separado.
Esto lo hace más fácil luego, ya que muchos de mis análisis son exploratorios.
y talvés no terminan siendo utilizados en el proyecto final, y algunos de los análisis se pueden
compartir entre otros proyectos.

### Mantiene los datos relacionados juntos

Los formatos de los archivos GIS son realmente 3-6 archivos que necesitan ser mantenidos juntos y tener el mismo nombre, 
por ejemplo, los **shapefiles**. Sería tentador almacenar estos componentes de forma separada, 
pero tus datos espaciales se volverán inútiles si haces eso.

### Manten un esquema de nombres consistente
Es generalmente mejor evitar renombrar los datos espaciales descargados
para que se mantenga una clara conexión con el punto de origen.
De otra forma te encontrarás preguntándote si `file_A` realmente es sólo una copia del  `archivo_oficial de_la_pagina_web` o no.

Para los conjuntos de datos que tu generes, vale la pena tomarse el tiempo para crear una convención de nombres que funcione para tu proyecto,
y apegarse a eso. Los nombres de los archivos no tienen que ser largos, solo tienen que ser lo suficientemente largos para que puedas saber cuál es el archivo. 
La fecha de generación, el tema y si un producto es intermedio o final son buenos datos para mantener
en un nombre de archivo. Para obtener más consejos sobre cómo nombrar archivos, consulta [las diapositivas de la charla de Jenny Bryan "Naming things" del 2015 Reproducible Science Workshop](https://speakerdeck.com/jennybc/how-to-name-files) en inglés.

> ## Sugerencia: Buenas prácticas para la computación científica
>
> [Buenas prácticas para computación científica](https://github.com/swcarpentry/good-enough-practices-in-scientific-computing/blob/gh-pages/good-enough-practices-for-scientific-computing. pdf) da las siguientes recomendaciones para la organización del proyecto:
>
> 1. Coloca cada proyecto en su propio directorio, que lleva el nombre del proyecto.
> 2. Coloca los documentos de texto asociados con el proyecto en el directorio `doc`.
> 3. Coloca los datos sin procesar y los metadatos en el directorio `datos`, y los archivos generados durante la limpieza y el análisis en un directorio `resultados`.
> 4. Pon la fuente de los scripts y programas del proyecto en el directorio `src`, y los programas traídos de otro lugar o compilados localmente en el directorio `bin`.
> 5. Nombra todos los archivos para reflejar su contenido o función.
{: .callout}

### Guarde los datos en el directorio de datos

Ahora que tenemos una buena estructura para el proyecto, guardaremos nuestros archivos de datos en el directorio `datos/`.

> ## Challenge 1
> 1 \. Descarga cada uno de los archivos de datos enumerados a continuación (<kbd>Ctrl</kbd>+<kbd>S</kbd>, haz clic con el botón derecho del ratón -> "Guardar como" o Archivo -> "Guardar página como")
> 
> - [datos de los países nórdicos](https://raw.githubusercontent.com/datacarpentry/r-intro-geospatial/master/_episodes_rmd/data/nordic-data.csv)
> - [datos de países nórdicos (versión 2)](https://raw.githubusercontent.com/datacarpentry/r-intro-geospatial/master/_episodes_rmd/data/nordic-data-2.csv)
> - [datos de gapminder](https://raw.githubusercontent.com/datacarpentry/r-intro-geospatial/master/_episodes_rmd/data/gapminder_data.csv)
> 
> 2\. Asegúrate de que los archivos tengan los siguientes nombres:
> - `nordic-data.csv`
> - `nordic-data-2.csv`
> - `gapminder_data.csv`
>
> 3\. Guarda los archivos en la carpeta `data/` dentro de tu proyecto.
>
> Cargaremos e inspeccionaremos estos datos más tarde.
{: .challenge}

> ## Challenge 2
> También queremos mover los datos que descargamos de la [página de datos](http://datacarpentry.org/geospatial-workshop/data/) a un subdirectorio
> dentro de `r-geospatial`. Si aún no has descargado los datos, puedes hacerlo haciendo clic en
> [este enlace de descargar](https://ndownloader.figshare.com/articles/2009586/versions/10). 
> 1. Mueve el archivo zip descargado al directorio `data`.
> 2. Una vez que los datos se hayan movido, descomprima todos los archivos.
{: .challenge}

Una vez que hayas terminado de mover los datos a la nueva carpeta,
su directorio de datos debe tener el siguiente aspecto:

 ```
 data/
    gapminder_data.csv
    NEON-DS-Airborne-Remote-Sensing/
    NEON-DS-Landsat-NDVI/
    NEON-DS-Met-Time-Series/
    NEON-DS-Site-Layout-Files/
    NEON-DS-Airborne-Remote-Sensing.zip
    NEON-DS-Landsat-NDVI.zip
    NEON-DS-Met-Time-Series.zip
    NEON-DS-Site-Layout-Files.zip
    nordic-data.csv
    nordic-data-2.csv
 ```


### Organiza tus scripts por etapas
Crear scripts de R o documentos Rmarkdown separados para diferentes etapas de un proyecto maximizará la eficiencia.
Por ejemplo, separar los comandos de descarga de datos en su propio archivo significa que no se volverán a descargar datos innecesariamente.

