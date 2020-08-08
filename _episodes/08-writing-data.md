---
#Por favor no edites este archivo directamente; Se genera automáticamente.
#En su lugar, por favor, edita 08-writing-data.md en _episodes_rmd/
title: Escribiendo datos
teaching: 10
exercises: 10
questions:
- "¿Cómo puedo guardar gráficos y datos creados en R?"
objectives:
- "Poder escribir gráficos y datos en R."
keypoints:
- "Guardar gráficos con `ggsave()` o `pdf()` combinado con `dev.off()`."
- "Usar `write.csv` para guardar datos tabulares."
source: Rmd
---




## Guardando gráficos

Puedes guardar un gráfico desde RStudio con el botón '**Export**'
en la ventana '**Plot**'. Esto te dará la opción de guardar como
.pdf o como .png, .jpg u otros formatos de imagen.

A veces querrás guardar gráficos sin crearlos en la
ventana '**Plot**' primero. Quizás quieras hacer un documento pdf con
múltiples páginas: cada una con un gráfico diferente, por ejemplo. O quizás
estás recorriendo múltiples subconjuntos de un archivo, graficando datos de
cada subconjunto y deseas guardar cada gráfico.
En este caso, puedes utilizar un enfoque más flexible. 
La función `pdf ()` crea un nuevo dispositivo pdf. Puedes controlar el tamaño y la resolución
usando los argumentos de esta función.


~~~
pdf("Distribution-of-gdpPercap.pdf", width=12, height=4)
ggplot(data = gapminder, aes(x = gdpPercap)) + 
geom_histogram()

# ¡Debes asegurarte de apagar el dispositivo pdf!

dev.off()
~~~
{: .language-r}

Abre este documento y échale un vistazo.

> ## Challenge 1
>
> Re escribe tu comando 'pdf' para imprimir una segunda
> página en el pdf, mostrando el gráfico side-by-side bar
> de gdp per capita en países de las Américas 
> en los años 1952 y 2007  que creaste en el
> episodio previo. 
> 
> > ## Solución al desafío 1
> >
> > 
> > ~~~
> > pdf("Distribution-of-gdpPercap.pdf", width = 12, height = 4)
> > ggplot(data = gapminder, aes(x = gdpPercap)) + 
> > geom_histogram()
> > 
> > ggplot(data = gapminder_small_2, aes(x = country, y = gdpPercap, fill = as.factor(year))) +
> > geom_col(position = "dodge") + coord_flip()
> > 
> > dev.off()
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}


Los comandos `jpeg`, `png`, etc. se usan de manera similar para producir
documentos en diferentes formatos.

## Escribiendo datos

En algún momento, también querrás escribir datos para usarlos fuera de R.

Podemos usar la función `write.csv` para esto, que es
muy similar a `read.csv` que vimos antes.

Vamos a crear un script de limpieza de datos, para este análisis,
sólo queremos centrarnos en los datos de gapminder para Australia:


~~~
aust_subset <- filter(gapminder, country == "Australia")

write.csv(aust_subset,
  file="cleaned-data/gapminder-aus.csv"
)
~~~
{: .language-r}

Abrimos el archivo para asegurarnos de que contiene los datos que esperamos. Navega a tu
directorio **`cleaned-data`** y haz doble clic en el nombre del archivo. Se abrirá usando el
programa que está configurado por defecto en tu computadora para abrir archivos con extensión `.csv`. Para abrir en una aplicación específica, haz clic derecho y selecciona la aplicación.Usando un programa de hoja de cálculo (como Excel) para abrir este archivo nos muestra que tenemos datos con el formato correcto incluyendo solo los datos de Australia. Sin embargo, hay números de fila asociados con los datos que no nos son útiles (se refieren a los números de fila
del conjunto de datos **gapminder**).

Veamos el archivo de ayuda para averiguar cómo cambiar este
comportamiento.


~~~
?write.csv
~~~
{: .language-r}

Por defecto, R escribirá la fila y
los nombres de las columnas al escribir datos en un archivo.
Para cambiar este comportamiento, podemos hacer lo siguiente:


~~~
write.csv(
  aust_subset,
  file="cleaned-data/gapminder-aus.csv",
  row.names=FALSE
)
~~~
{: .language-r}

> ## Challenge 2
> Filtra los datos de gapminder
> para incluir solo los datos que se recolectaron desde 1990. Escribe el nuevo subconjunto en un 
> archivo en el directorio **`clean-data/`**.
> 
> > ## Solución al desafío 2
> >
> > 
> > ~~~
> > gapminder_after_1990 <- filter(gapminder, year > 1990)
> > 
> > write.csv(gapminder_after_1990,
> >  file = "cleaned-data/gapminder-after-1990.csv",
> >  row.names = FALSE)
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

