Segundo examen, Brayan Reyes 1950182
================

## Planta de oxidacion

en este informe del segundo examen de diseño experimental procesaremos la informacion de la base de datos stackloss y daremos el respectivo analisis a dichos datos.

``` r
data(stackloss)
```

## Including Code

You can include R code in the document as follows:

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
data(stackloss)
stackloss<- mutate(stackloss, concentracion= (Acid.Conc./10)+50)

stackloss<- mutate(stackloss, relacion_Temp_Func=Water.Temp/Air.Flow)

summarise(stackloss, promedio=mean(relacion_Temp_Func))
```

    ##    promedio
    ## 1 0.3507887

``` r
c<- filter(stackloss, Water.Temp>18 & Water.Temp<24)
c %>% summarise(desviacion=sd(Water.Temp))
```

    ##   desviacion
    ## 1   1.666667

## Including Plots

You can also embed plots, for example:

![](segundoprevio_files/figure-markdown_github/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
