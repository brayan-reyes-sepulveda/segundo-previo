Segundo examen, Brayan Reyes 1950182
================

## Planta de oxidacion

en este informe del segundo examen de diseño experimental procesaremos la informacion de la base de datos stackloss y daremos el respectivo analisis a dichos datos. la base de datos stackloss (con la cual trabajaremos) nos proporciona informacion sobre una planta de oxidacion de amoniaco a acido nitrico. con 4 variables las cuales son 1. tasa de funcionamiento de la planta (Air.Flow) 2. temperatura del agua (Water.Temp) 3. concentracion del acido circulante (Acid.Conc.) 4. eficiencia de la planta (stackloss)

``` r
data(stackloss)
```

## Procesamiento de Datos

tomando en cuenta la informacion procedemos con el procesado de datos. 1. creacion de 2 nuevas columnas en las cuales proporcionaremos los datos del % de la concentracion del acido y una donde este la relacion entre la temperatura del agua y la tasa del funcionamiento de la planta (respectivamente).

``` r
##llamado a la libreria
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
##llamado a la base de datos
data(stackloss)

##creacion de la columna concentracion, la cual tambien es asignada a la base de datos principal para tener un mejor control 
stackloss<- mutate(stackloss, concentracion= (Acid.Conc./10)+50)

##creacion de la columna relacion_temp_func la cual nos dara las relaciones respectivas entre la temperatura y el funcionamiento de la planta 
stackloss<- mutate(stackloss, relacion_Temp_Func=Water.Temp/Air.Flow)

##mediante el comando summarise y el comando mean calculamos el promedio de la columna relacion
summarise(stackloss, promedio=mean(relacion_Temp_Func))
```

    ##    promedio
    ## 1 0.3507887

``` r
##filtramos los datos en base a la temperatura y calculamos la desviacion estandar
##NOTA: los valores filtrados los asigno a una nueva base de datos con el fin de facilitar la lectura de dischos datos manteniendo la base de datos stackloss intacta
c<- filter(stackloss, Water.Temp>18 & Water.Temp<24)
c %>% summarise(desviacion=sd(Water.Temp))
```

    ##   desviacion
    ## 1   1.666667

promedio: 0.3507887 desviacion: 1.666667 por lo cual indica que los datos de temperatura se encuentran un poco dispersos lo aconsejable seria reducir esta dispersion para un mejor control de calidad(desviacion&gt;1)

## Graficas de densidad

para realizar un mejor control de calidad en la planta es mbueno conocer valores por medio de graficas y emplearemos dos en este caso una para la variable temperatura y la segunda para la variable concentracion, con el fin de posteriormente comparar el resultado.

![](segundoprevio_files/figure-markdown_github/pressure-1.png)![](segundoprevio_files/figure-markdown_github/pressure-2.png)

de estas dos graficas podemos observarlos valores donde tienden a estar mayormente agrupadas las observaciones. para la temperatura: la densiad muestra dos zonas de agrupacion lo cual en un proceso de control de calida debe de reducirse pues tener 2 valores de temperaturas diferentes y no proximos para una misma reaccion quimica en un proceso industrial puede generar un producto no deseado, descomposicion del producto o que simplemente la reaccion no ocurra en cualquier caso el resultado seria negativo para la planta.

para la concentracion: dado que esta concentracion es la concentracion del acido nitrico y la densidad es una forma de conocer las zonas de agrupacion lo primero que se aprecia es la alta densidad cerca del 59% de la concentracion por lo tanto el proceso esta siendo efectivo pero podria mejorar manteniendo un mejor control en la temperatura del agua.
