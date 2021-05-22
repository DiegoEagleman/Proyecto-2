Proyecto 2 Data Mining
================
Diego Aguilar Dañobeitía
21/5/2021

## Cargar los datos

Lo primero que se tiene que hacer para iniciar el análisis de los datos
es cargar el archivo que los contiene, lo que se guardará en la variable
“data”:

``` r
setwd("D:/Documentos/Files & Stuff/U/Data Mining/Proyecto 2")

load("beats.RData")

head(beats)
```

    ##   artist_name              artist_id               album_id album_type
    ## 1        2Pac 1ZwdS5xdxEREPySFridCfh 1nGbXgS6toEOcFCDwEl5R3      album
    ## 2        2Pac 1ZwdS5xdxEREPySFridCfh 1nGbXgS6toEOcFCDwEl5R3      album
    ## 3        2Pac 1ZwdS5xdxEREPySFridCfh 1nGbXgS6toEOcFCDwEl5R3      album
    ## 4        2Pac 1ZwdS5xdxEREPySFridCfh 1nGbXgS6toEOcFCDwEl5R3      album
    ## 5        2Pac 1ZwdS5xdxEREPySFridCfh 1nGbXgS6toEOcFCDwEl5R3      album
    ## 6        2Pac 1ZwdS5xdxEREPySFridCfh 1nGbXgS6toEOcFCDwEl5R3      album
    ##   album_release_date album_release_year album_release_date_precision
    ## 1         2019-08-01               2019                          day
    ## 2         2019-08-01               2019                          day
    ## 3         2019-08-01               2019                          day
    ## 4         2019-08-01               2019                          day
    ## 5         2019-08-01               2019                          day
    ## 6         2019-08-01               2019                          day
    ##   danceability energy key loudness mode speechiness acousticness
    ## 1        0.656  0.882   0   -3.011    1      0.0941      0.03300
    ## 2        0.810  0.642   8   -8.647    1      0.2440      0.04800
    ## 3        0.548  0.590   4   -9.301    0      0.4750      0.11300
    ## 4        0.839  0.657   5   -4.959    0      0.2220      0.05260
    ## 5        0.854  0.694   0   -4.258    0      0.1230      0.00944
    ## 6        0.697  0.598   2   -9.604    1      0.1360      0.00522
    ##   instrumentalness liveness valence   tempo               track_id
    ## 1         0.000000   0.6700   0.782  91.661 6ayeqYtOtwVhqVB6k6MKoh
    ## 2         0.000000   0.2640   0.694  90.956 1UDsnzBp8gUCFsrzUDlZI9
    ## 3         0.000722   0.2290   0.267  87.841 3bKs15o7F9VP6GBExCbb6H
    ## 4         0.000106   0.3910   0.615  85.111 4L0iAst3yLonw8aGxTRCvb
    ## 5         0.071900   0.0767   0.776 104.379 66men3J5qFERvIY06M5hQ9
    ## 6         0.000000   0.1720   0.387  85.862 7GVCAVH7SZnjrzHI1FmfeA
    ##                                                       analysis_url
    ## 1 https://api.spotify.com/v1/audio-analysis/6ayeqYtOtwVhqVB6k6MKoh
    ## 2 https://api.spotify.com/v1/audio-analysis/1UDsnzBp8gUCFsrzUDlZI9
    ## 3 https://api.spotify.com/v1/audio-analysis/3bKs15o7F9VP6GBExCbb6H
    ## 4 https://api.spotify.com/v1/audio-analysis/4L0iAst3yLonw8aGxTRCvb
    ## 5 https://api.spotify.com/v1/audio-analysis/66men3J5qFERvIY06M5hQ9
    ## 6 https://api.spotify.com/v1/audio-analysis/7GVCAVH7SZnjrzHI1FmfeA
    ##   time_signature disc_number duration_ms explicit
    ## 1              4           1      347973    FALSE
    ## 2              4           1      241026    FALSE
    ## 3              4           1      240013    FALSE
    ## 4              4           1      295026    FALSE
    ## 5              4           1      241000    FALSE
    ## 6              4           1      224026    FALSE
    ##                                                 track_href is_local
    ## 1 https://api.spotify.com/v1/tracks/6ayeqYtOtwVhqVB6k6MKoh    FALSE
    ## 2 https://api.spotify.com/v1/tracks/1UDsnzBp8gUCFsrzUDlZI9    FALSE
    ## 3 https://api.spotify.com/v1/tracks/3bKs15o7F9VP6GBExCbb6H    FALSE
    ## 4 https://api.spotify.com/v1/tracks/4L0iAst3yLonw8aGxTRCvb    FALSE
    ## 5 https://api.spotify.com/v1/tracks/66men3J5qFERvIY06M5hQ9    FALSE
    ## 6 https://api.spotify.com/v1/tracks/7GVCAVH7SZnjrzHI1FmfeA    FALSE
    ##               track_name
    ## 1        California Love
    ## 2 Slippin' Into Darkness
    ## 3            Ride or Die
    ## 4     I Ain't Mad At Cha
    ## 5              Static II
    ## 6                Runnin'
    ##                                                                                             track_preview_url
    ## 1 https://p.scdn.co/mp3-preview/93e456ef0b73f23f50eeadaeaad852d79d4f4610?cid=ac26d97eca664234ab133e5208ea5737
    ## 2 https://p.scdn.co/mp3-preview/440595604d3f49464bcf28efc867f7df31d62e53?cid=ac26d97eca664234ab133e5208ea5737
    ## 3 https://p.scdn.co/mp3-preview/cc18dc90d609d37591e5993615a0cea1fa25f428?cid=ac26d97eca664234ab133e5208ea5737
    ## 4 https://p.scdn.co/mp3-preview/d138f0170423cd9a14f31006d4add57c07f705c4?cid=ac26d97eca664234ab133e5208ea5737
    ## 5 https://p.scdn.co/mp3-preview/dddb7d0ea0205338a00c591e6045b0c21cd7c9fc?cid=ac26d97eca664234ab133e5208ea5737
    ## 6 https://p.scdn.co/mp3-preview/fc169c99acc9d8bb19b34cf1aaad9f1b0b9b68e8?cid=ac26d97eca664234ab133e5208ea5737
    ##   track_number  type                            track_uri
    ## 1            1 track spotify:track:6ayeqYtOtwVhqVB6k6MKoh
    ## 2            2 track spotify:track:1UDsnzBp8gUCFsrzUDlZI9
    ## 3            3 track spotify:track:3bKs15o7F9VP6GBExCbb6H
    ## 4            4 track spotify:track:4L0iAst3yLonw8aGxTRCvb
    ## 5            5 track spotify:track:66men3J5qFERvIY06M5hQ9
    ## 6            6 track spotify:track:7GVCAVH7SZnjrzHI1FmfeA
    ##                                   external_urls.spotify      album_name
    ## 1 https://open.spotify.com/track/6ayeqYtOtwVhqVB6k6MKoh California Love
    ## 2 https://open.spotify.com/track/1UDsnzBp8gUCFsrzUDlZI9 California Love
    ## 3 https://open.spotify.com/track/3bKs15o7F9VP6GBExCbb6H California Love
    ## 4 https://open.spotify.com/track/4L0iAst3yLonw8aGxTRCvb California Love
    ## 5 https://open.spotify.com/track/66men3J5qFERvIY06M5hQ9 California Love
    ## 6 https://open.spotify.com/track/7GVCAVH7SZnjrzHI1FmfeA California Love
    ##   key_name mode_name key_mode
    ## 1        C     major  C major
    ## 2       G#     major G# major
    ## 3        E     minor  E minor
    ## 4        F     minor  F minor
    ## 5        C     minor  C minor
    ## 6        D     major  D major

``` r
str(beats)
```

    ## 'data.frame':    447622 obs. of  36 variables:
    ##  $ artist_name                 : chr  "2Pac" "2Pac" "2Pac" "2Pac" ...
    ##  $ artist_id                   : chr  "1ZwdS5xdxEREPySFridCfh" "1ZwdS5xdxEREPySFridCfh" "1ZwdS5xdxEREPySFridCfh" "1ZwdS5xdxEREPySFridCfh" ...
    ##  $ album_id                    : chr  "1nGbXgS6toEOcFCDwEl5R3" "1nGbXgS6toEOcFCDwEl5R3" "1nGbXgS6toEOcFCDwEl5R3" "1nGbXgS6toEOcFCDwEl5R3" ...
    ##  $ album_type                  : chr  "album" "album" "album" "album" ...
    ##  $ album_release_date          : chr  "2019-08-01" "2019-08-01" "2019-08-01" "2019-08-01" ...
    ##  $ album_release_year          : num  2019 2019 2019 2019 2019 ...
    ##  $ album_release_date_precision: chr  "day" "day" "day" "day" ...
    ##  $ danceability                : num  0.656 0.81 0.548 0.839 0.854 0.697 0.77 0.805 0.818 0.912 ...
    ##  $ energy                      : num  0.882 0.642 0.59 0.657 0.694 0.598 0.613 0.864 0.627 0.465 ...
    ##  $ key                         : int  0 8 4 5 0 2 1 11 11 7 ...
    ##  $ loudness                    : num  -3.01 -8.65 -9.3 -4.96 -4.26 ...
    ##  $ mode                        : int  1 1 0 0 0 1 0 0 1 1 ...
    ##  $ speechiness                 : num  0.0941 0.244 0.475 0.222 0.123 0.136 0.0585 0.183 0.184 0.36 ...
    ##  $ acousticness                : num  0.033 0.048 0.113 0.0526 0.00944 0.00522 0.00653 0.271 0.264 0.0585 ...
    ##  $ instrumentalness            : num  0.00 0.00 7.22e-04 1.06e-04 7.19e-02 0.00 2.83e-04 0.00 0.00 1.71e-05 ...
    ##  $ liveness                    : num  0.67 0.264 0.229 0.391 0.0767 0.172 0.276 0.389 0.132 0.0534 ...
    ##  $ valence                     : num  0.782 0.694 0.267 0.615 0.776 0.387 0.897 0.663 0.637 0.478 ...
    ##  $ tempo                       : num  91.7 91 87.8 85.1 104.4 ...
    ##  $ track_id                    : chr  "6ayeqYtOtwVhqVB6k6MKoh" "1UDsnzBp8gUCFsrzUDlZI9" "3bKs15o7F9VP6GBExCbb6H" "4L0iAst3yLonw8aGxTRCvb" ...
    ##  $ analysis_url                : chr  "https://api.spotify.com/v1/audio-analysis/6ayeqYtOtwVhqVB6k6MKoh" "https://api.spotify.com/v1/audio-analysis/1UDsnzBp8gUCFsrzUDlZI9" "https://api.spotify.com/v1/audio-analysis/3bKs15o7F9VP6GBExCbb6H" "https://api.spotify.com/v1/audio-analysis/4L0iAst3yLonw8aGxTRCvb" ...
    ##  $ time_signature              : int  4 4 4 4 4 4 4 4 4 4 ...
    ##  $ disc_number                 : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ duration_ms                 : int  347973 241026 240013 295026 241000 224026 251000 276346 197013 314013 ...
    ##  $ explicit                    : logi  FALSE FALSE FALSE FALSE FALSE FALSE ...
    ##  $ track_href                  : chr  "https://api.spotify.com/v1/tracks/6ayeqYtOtwVhqVB6k6MKoh" "https://api.spotify.com/v1/tracks/1UDsnzBp8gUCFsrzUDlZI9" "https://api.spotify.com/v1/tracks/3bKs15o7F9VP6GBExCbb6H" "https://api.spotify.com/v1/tracks/4L0iAst3yLonw8aGxTRCvb" ...
    ##  $ is_local                    : logi  FALSE FALSE FALSE FALSE FALSE FALSE ...
    ##  $ track_name                  : chr  "California Love" "Slippin' Into Darkness" "Ride or Die" "I Ain't Mad At Cha" ...
    ##  $ track_preview_url           : chr  "https://p.scdn.co/mp3-preview/93e456ef0b73f23f50eeadaeaad852d79d4f4610?cid=ac26d97eca664234ab133e5208ea5737" "https://p.scdn.co/mp3-preview/440595604d3f49464bcf28efc867f7df31d62e53?cid=ac26d97eca664234ab133e5208ea5737" "https://p.scdn.co/mp3-preview/cc18dc90d609d37591e5993615a0cea1fa25f428?cid=ac26d97eca664234ab133e5208ea5737" "https://p.scdn.co/mp3-preview/d138f0170423cd9a14f31006d4add57c07f705c4?cid=ac26d97eca664234ab133e5208ea5737" ...
    ##  $ track_number                : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ type                        : chr  "track" "track" "track" "track" ...
    ##  $ track_uri                   : chr  "spotify:track:6ayeqYtOtwVhqVB6k6MKoh" "spotify:track:1UDsnzBp8gUCFsrzUDlZI9" "spotify:track:3bKs15o7F9VP6GBExCbb6H" "spotify:track:4L0iAst3yLonw8aGxTRCvb" ...
    ##  $ external_urls.spotify       : chr  "https://open.spotify.com/track/6ayeqYtOtwVhqVB6k6MKoh" "https://open.spotify.com/track/1UDsnzBp8gUCFsrzUDlZI9" "https://open.spotify.com/track/3bKs15o7F9VP6GBExCbb6H" "https://open.spotify.com/track/4L0iAst3yLonw8aGxTRCvb" ...
    ##  $ album_name                  : chr  "California Love" "California Love" "California Love" "California Love" ...
    ##  $ key_name                    : chr  "C" "G#" "E" "F" ...
    ##  $ mode_name                   : chr  "major" "major" "minor" "minor" ...
    ##  $ key_mode                    : chr  "C major" "G# major" "E minor" "F minor" ...

``` r
dim(beats)
```

    ## [1] 447622     36

Por lo que se puede observar, existen 447622 datos con 36 atributos.

## Cargar las librerías

Luego, se procede a cargar las librerías necesarias:

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.0.5

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.3     v purrr   0.3.4
    ## v tibble  3.1.0     v dplyr   1.0.5
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   1.4.0     v forcats 0.5.1

    ## Warning: package 'ggplot2' was built under R version 4.0.5

    ## Warning: package 'tibble' was built under R version 4.0.5

    ## Warning: package 'tidyr' was built under R version 4.0.5

    ## Warning: package 'readr' was built under R version 4.0.5

    ## Warning: package 'purrr' was built under R version 4.0.5

    ## Warning: package 'dplyr' was built under R version 4.0.5

    ## Warning: package 'stringr' was built under R version 4.0.5

    ## Warning: package 'forcats' was built under R version 4.0.5

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(factoextra)
```

    ## Warning: package 'factoextra' was built under R version 4.0.5

    ## Welcome! Want to learn more? See two factoextra-related books at https://goo.gl/ve3WBa

``` r
library(flexclust)
```

    ## Warning: package 'flexclust' was built under R version 4.0.5

    ## Loading required package: grid

    ## Loading required package: lattice

    ## Loading required package: modeltools

    ## Loading required package: stats4

``` r
library(cluster)

library(R.utils)
```

    ## Warning: package 'R.utils' was built under R version 4.0.5

    ## Loading required package: R.oo

    ## Loading required package: R.methodsS3

    ## R.methodsS3 v1.8.1 (2020-08-26 16:20:06 UTC) successfully loaded. See ?R.methodsS3 for help.

    ## R.oo v1.24.0 (2020-08-26 16:11:58 UTC) successfully loaded. See ?R.oo for help.

    ## 
    ## Attaching package: 'R.oo'

    ## The following object is masked from 'package:R.methodsS3':
    ## 
    ##     throw

    ## The following objects are masked from 'package:modeltools':
    ## 
    ##     clone, dimension

    ## The following objects are masked from 'package:methods':
    ## 
    ##     getClasses, getMethods

    ## The following objects are masked from 'package:base':
    ## 
    ##     attach, detach, load, save

    ## R.utils v2.10.1 (2020-08-26 22:50:31 UTC) successfully loaded. See ?R.utils for help.

    ## 
    ## Attaching package: 'R.utils'

    ## The following object is masked from 'package:tidyr':
    ## 
    ##     extract

    ## The following object is masked from 'package:utils':
    ## 
    ##     timestamp

    ## The following objects are masked from 'package:base':
    ## 
    ##     cat, commandArgs, getOption, inherits, isOpen, nullfile, parse,
    ##     warnings

``` r
library(scales)
```

    ## Warning: package 'scales' was built under R version 4.0.5

    ## 
    ## Attaching package: 'scales'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard

    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

## Pre procesamiento de los datos

Se procede a limpiar los datos en base al objetivo: realizar una lista
de reproducción de 3 horas o más a partir de una sola canción, con las
canciones contenidas en “beats.Rdata”, tomando en cuenta las variables
que están en este archivo. Para esto, se van a tomar las variables de
“energy” y “tempo”, que son las que mayor similitud o diferencia pueden
mostrar entre canciones, musicalmente hablando, la variable
“external\_urls.spotify” para identificarlas, y la variable
“duration\_ms”, con la que vamos a determinar la duración de la lista de
reproducción.

### Eliminación de entidades duplicadas

Primero, se procede a eliminar entidades que poseen los mismos valores
para cada variable entre sí:

``` r
beatsunique <- unique(beats)

dim(beatsunique)
```

    ## [1] 446563     36

Se observa que disminuyó el número de entidades a 446563.

### Eliminación de entidades con valores faltantes

Luego se necesita limpiar las entidades que tienen valores faltantes
(NA) de los datos:

``` r
beatsclean <- na.omit(beatsunique)

dim(beatsclean)
```

    ## [1] 271748     36

Se observa que ahora existen 271748 datos, casi la mitad de los datos
anteriores

### Reducción de dimensionalidad

Después, según lo anterior, las únicas variables importantes serían las
de “energy”, “tempo”, “duration\_ms” y “external\_urls.spotify”, por lo
que se procede a eliminar las restantes:

``` r
beatsred <- beatsclean[c("energy", "tempo", "duration_ms", "external_urls.spotify")]

dim(beatsred)
```

    ## [1] 271748      4

Se observa que ahora se cuenta con los mismos 271748 datos, pero ahora
con sólo 4 variables, que son las que se necesitan.

### Sampleo

A continuación, se va a tomar una muestra de la data, debido a que por
el tamaño de esta no es posible llevar a cabo los procedimientos
analíticos siguientes. Se va a usar una muestra de tamaño 10,000.

``` r
beatsample <- sample_n(beatsred, 10000)
```

### Escalamiento

Luego, para un correcto análisis posterior, se va a escalar la variable
tempo.

``` r
beatsample$tempo = rescale(beatsample$tempo, to = c(0, 1))

beatsample %>% summary()
```

    ##      energy             tempo         duration_ms      external_urls.spotify
    ##  Min.   :0.000573   Min.   :0.0000   Min.   :  11745   Length:10000         
    ##  1st Qu.:0.087050   1st Qu.:0.3791   1st Qu.: 138945   Class :character     
    ##  Median :0.276000   Median :0.4839   Median : 202582   Mode  :character     
    ##  Mean   :0.388433   Mean   :0.4993   Mean   : 244380                        
    ##  3rd Qu.:0.685250   3rd Qu.:0.6036   3rd Qu.: 282806                        
    ##  Max.   :1.000000   Max.   :1.0000   Max.   :4044196

### Separación de la variable duration\_ms del resto

Finalmente, para que se pueda llevar a cabo el análisis, se debe separar
la variable correspondiente a la duración y a la url respecto a las que
se van a utilizar.

``` r
beatsinfo = beatsample[c("duration_ms", "external_urls.spotify")]

beatsanalize = beatsample[c("energy", "tempo")]

dim(beatsinfo)
```

    ## [1] 10000     2

``` r
dim(beatsanalize)
```

    ## [1] 10000     2

``` r
str(beatsanalize)
```

    ## 'data.frame':    10000 obs. of  2 variables:
    ##  $ energy: num  0.998 0.0373 0.221 0.124 0.377 0.797 0.00741 0.582 0.15 0.121 ...
    ##  $ tempo : num  0.799 0.386 0.557 0.527 0.385 ...

## Análisis de los datos

Ya que se han limpiado y ordenado los datos de forma correcta, se
procede al análisis de este para resolver la problemática planteada en
este caso. Para generar la lista de reproducción, se va a realizar un
análisis de clusters de K-medias con las 2 variables seleccionadas,
tomando después como muestra aleatoria canciones pertenecientes al mismo
grupo o cluster que la canción en base a la cual se va a realizar dicha
lista, hasta completar las 3 horas.

Se va a realizar un primer intento del análisis K-medias con k = 5.

### Análisis cluster K = 5

``` r
beats_kmeans <- kmeans(beatsanalize, 5)

beatsanalize$clus <- beats_kmeans$cluster %>% as.factor()

ggplot(beatsanalize, aes(energy, tempo, color=clus)) +
   geom_point(alpha=0.5, show.legend = T) +
   theme_bw()
```

![](Proyecto-2_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
info_clus <- beats_kmeans$centers

info_clus
```

    ##       energy     tempo
    ## 1 0.36805103 0.4251089
    ## 2 0.14246983 0.6404679
    ## 3 0.07948767 0.3783507
    ## 4 0.61862337 0.5710211
    ## 5 0.90921984 0.5303843

Se puede ver que existen 5 clusters no muy definidos entre sí dada la
naturaleza de los datos.

## Evaluación

Ahora vamos a evaluar nuestro análisis para mejorarlo y así lograr que
sea más preciso.

### Coeficiente de silueta

Se utilizará esta evaluación para el análisis.

``` r
beatsSil <- silhouette(beats_kmeans$cluster, dist(beatsanalize))
summary(beatsSil)
```

    ## Silhouette of 10000 units in 5 clusters from silhouette.default(x = beats_kmeans$cluster, dist = dist(beatsanalize)) :
    ##  Cluster sizes and average silhouette widths:
    ##      1509      2058      2881      1455      2097 
    ## 0.8443580 0.8402200 0.8912803 0.8125727 0.8176882 
    ## Individual silhouette widths:
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  0.5840  0.8237  0.8509  0.8468  0.8795  0.9217

``` r
fviz_silhouette(beatsSil) + coord_flip()
```

    ##   cluster size ave.sil.width
    ## 1       1 1509          0.84
    ## 2       2 2058          0.84
    ## 3       3 2881          0.89
    ## 4       4 1455          0.81
    ## 5       5 2097          0.82

![](Proyecto-2_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

Luego, se utiliza este para encontrar el mejor valor de k.

``` r
beatsSil=numeric(30)
for (k in 2:30){
  model <- kmeans(beatsanalize, centers = k)
  temp <- silhouette(model$cluster, dist(beatsanalize))
  beatsSil[k] <- mean(temp[,3])
}
tempDF=data.frame(CS=beatsSil,K=c(1:30))

ggplot(tempDF, aes(x=K, y=CS)) + 
  geom_line() +
  scale_x_continuous(breaks=c(1:30))
```

![](Proyecto-2_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

Se observa que el mejor valor de k es 4, por lo que será el que
utilizaremos.

### Análisis cluster K = 4

``` r
beats_kmeans2 <- kmeans(beatsanalize, 4)

beatsanalize$clus <- beats_kmeans2$cluster %>% as.factor()

ggplot(beatsanalize, aes(energy, tempo, color=clus)) +
   geom_point(alpha=0.5, show.legend = T) +
   theme_bw()
```

![](Proyecto-2_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## Creación de la lista de reproducción

Ahora, con los clusters definidos, se va a elegir una canción al azar y
a crear una playlist en base a esta, tomando elementos aleatorios de
esta hasta que se cumplan las 3 horas o más. Antes de esto, es necesario
fusionar la data de “beatsanalize” con la data de “beatsduration”.

### Fusión entre “beats\_kmeans” y “beatsduration”

``` r
beatsanalize$clus <- as.numeric(beatsanalize$clus)

beatsmerge <- merge(beatsanalize, beatsinfo, by = "row.names")

beatsmerge %>% summary()
```

    ##   Row.names             energy             tempo             clus     
    ##  Length:10000       Min.   :0.000573   Min.   :0.0000   Min.   :1.00  
    ##  Class :AsIs        1st Qu.:0.087050   1st Qu.:0.3791   1st Qu.:2.00  
    ##  Mode  :character   Median :0.276000   Median :0.4839   Median :2.00  
    ##                     Mean   :0.388433   Mean   :0.4993   Mean   :2.17  
    ##                     3rd Qu.:0.685250   3rd Qu.:0.6036   3rd Qu.:2.00  
    ##                     Max.   :1.000000   Max.   :1.0000   Max.   :4.00  
    ##   duration_ms      external_urls.spotify
    ##  Min.   :  11745   Length:10000         
    ##  1st Qu.: 138945   Class :character     
    ##  Median : 202582   Mode  :character     
    ##  Mean   : 244380                        
    ##  3rd Qu.: 282806                        
    ##  Max.   :4044196

### Selección de una canción al azar

Ahora se va a elegir una canción al azar para basarse en hacer la lista
de reproducción

``` r
songsample <- sample_n(beatsmerge, 1)

str(songsample)
```

    ## 'data.frame':    1 obs. of  6 variables:
    ##  $ Row.names            : 'AsIs' chr "3190"
    ##  $ energy               : num 0.2
    ##  $ tempo                : num 0.415
    ##  $ clus                 : num 2
    ##  $ duration_ms          : int 67426
    ##  $ external_urls.spotify: chr "https://open.spotify.com/track/0Uu3IFdlTddXYrMKo2FArO"

### Selección de canciones pertenencientes al mismo cluster

Luego, se van a separar las canciones que pertenecen al cluster de la
canción elegida de las demás

``` r
songcluster <- songsample[1, 4]

print(songcluster)
```

    ## [1] 2

``` r
beatscluster <- beatsmerge[beatsmerge$clus == songcluster, c("external_urls.spotify", "energy", "tempo", "duration_ms", "clus")]

beatscluster %>% summary()
```

    ##  external_urls.spotify     energy             tempo         duration_ms     
    ##  Length:6448           Min.   :0.000573   Min.   :0.0000   Min.   :  11745  
    ##  Class :character      1st Qu.:0.046675   1st Qu.:0.3607   1st Qu.: 130664  
    ##  Mode  :character      Median :0.129000   Median :0.4465   Median : 194961  
    ##                        Mean   :0.167121   Mean   :0.4730   Mean   : 256252  
    ##                        3rd Qu.:0.261000   3rd Qu.:0.5763   3rd Qu.: 308340  
    ##                        Max.   :0.621000   Max.   :0.9846   Max.   :2291647  
    ##       clus  
    ##  Min.   :2  
    ##  1st Qu.:2  
    ##  Median :2  
    ##  Mean   :2  
    ##  3rd Qu.:2  
    ##  Max.   :2

### Creación de la lista de reproducción

Ahora, podemos crear una lista de reproducción de al menos 3 horas con
estos datos. Procederemos a crearla

``` r
beatsplaylist <- sample_n(beatscluster, 200)

playlistduration <- sum(beatsplaylist$duration_ms)

playlisthours <- playlistduration/1.08e+7

print(playlisthours)
```

    ## [1] 4.527154

``` r
print(beatsplaylist$external_urls.spotify)
```

    ##   [1] "https://open.spotify.com/track/1c06Ij51DXUgENzs9DCs8P"
    ##   [2] "https://open.spotify.com/track/4oPbPWSdQoGmWaTLpLfLWa"
    ##   [3] "https://open.spotify.com/track/5BaG5g6C6zrIwHw5DCtW5c"
    ##   [4] "https://open.spotify.com/track/0xmVbJIdm78ZBDuhpfU7qN"
    ##   [5] "https://open.spotify.com/track/7FVGUX9ImYiMYhuvcHAjCP"
    ##   [6] "https://open.spotify.com/track/0a5fqFABslT7Ssa9WHYEFO"
    ##   [7] "https://open.spotify.com/track/0K1g3n2fQVDWy3isjYxkjG"
    ##   [8] "https://open.spotify.com/track/3UIiR0BsR4Coqv07Mw1wZ3"
    ##   [9] "https://open.spotify.com/track/3UDZSev2ys9dm3epCw1O5b"
    ##  [10] "https://open.spotify.com/track/2Jt2f4WqWFfVFMLBJK57Nl"
    ##  [11] "https://open.spotify.com/track/2uK8NQRxRJ0aM85Cpz1dYh"
    ##  [12] "https://open.spotify.com/track/7dvnBcYBpuhOuSmrD3yuvr"
    ##  [13] "https://open.spotify.com/track/7zwBqOW0NB2DRzsvRfTH57"
    ##  [14] "https://open.spotify.com/track/20PQdiDM0g2nSzeUQ6qVLH"
    ##  [15] "https://open.spotify.com/track/5KaiCkWFwL3nWuD9NETcsZ"
    ##  [16] "https://open.spotify.com/track/5cAMGjMULGV32aovRgpF7v"
    ##  [17] "https://open.spotify.com/track/3rIbyy5GxRp0Ky9PFthlI6"
    ##  [18] "https://open.spotify.com/track/0PKwhft2RXhJshPWippWQj"
    ##  [19] "https://open.spotify.com/track/2vow7fY4zzINwlJM9OY4EY"
    ##  [20] "https://open.spotify.com/track/3UbZGpRLjNLciWwzajG1Wx"
    ##  [21] "https://open.spotify.com/track/1Km6vNcGQ1IFRBxVsWOXfE"
    ##  [22] "https://open.spotify.com/track/1WAj6piBL6BoW4uVZEgFzk"
    ##  [23] "https://open.spotify.com/track/6pOFkEHkajoAqDzyQNDKeV"
    ##  [24] "https://open.spotify.com/track/1YkWObVUcnEyMKIErlE9n1"
    ##  [25] "https://open.spotify.com/track/1PrihbMRgUhOTsAmRjWZX1"
    ##  [26] "https://open.spotify.com/track/2avddeSlfLB1F3PItzQPVd"
    ##  [27] "https://open.spotify.com/track/2bsnkUEYTzjn0ZlwvGaJOM"
    ##  [28] "https://open.spotify.com/track/3gGMx2THJej56aOAyKmtPr"
    ##  [29] "https://open.spotify.com/track/04YJG8UvVrCLVIVC0GlHof"
    ##  [30] "https://open.spotify.com/track/6nRGpoblP3BOj888wXfpb7"
    ##  [31] "https://open.spotify.com/track/6O9Mz8unG4xPzqNzONaOyp"
    ##  [32] "https://open.spotify.com/track/43bmbicuAU6AlVNWMCmklH"
    ##  [33] "https://open.spotify.com/track/2L7VLkz5INO9BeMxHOWyUG"
    ##  [34] "https://open.spotify.com/track/0qNTrZA5QBl6n2MPB1oKjw"
    ##  [35] "https://open.spotify.com/track/27lA89tP0wG4w6mt0JG9GT"
    ##  [36] "https://open.spotify.com/track/27CydK3COpvuUlBYJg3wm0"
    ##  [37] "https://open.spotify.com/track/1wqs8CdQ2DegOD5ZEXJoUD"
    ##  [38] "https://open.spotify.com/track/1Gzw7ACddkJ9wcWLFRx7ZO"
    ##  [39] "https://open.spotify.com/track/0X1uL0kGog8C20FGwsw99z"
    ##  [40] "https://open.spotify.com/track/5Nt3QXufZPC3EUhjZjkHua"
    ##  [41] "https://open.spotify.com/track/1i5JXjxg74AKhrWbHsED4v"
    ##  [42] "https://open.spotify.com/track/0oQeGJrLhwqQXWMv2Ezds9"
    ##  [43] "https://open.spotify.com/track/6gxFRy8VgKzHivOGsSbMkF"
    ##  [44] "https://open.spotify.com/track/4lQWZGUrquRfH9se6nlmp3"
    ##  [45] "https://open.spotify.com/track/0aptVRiYvr36JaINkfjPFL"
    ##  [46] "https://open.spotify.com/track/6j4pTHv7z5FAkF9jk0Rue9"
    ##  [47] "https://open.spotify.com/track/2ZyZoQqWCglMAWFoQfNqo2"
    ##  [48] "https://open.spotify.com/track/0At92nDY3K0WQXR2xnvUOT"
    ##  [49] "https://open.spotify.com/track/2LIo5VbuXWxBTQwhwL03LZ"
    ##  [50] "https://open.spotify.com/track/3EZ7PFCxR3dJPKnNABYuuo"
    ##  [51] "https://open.spotify.com/track/2Th3JsoR5iX4XS4g9QhV7d"
    ##  [52] "https://open.spotify.com/track/2mwI0XrgpbagBCHgbLZJHa"
    ##  [53] "https://open.spotify.com/track/6QgOfnSTfCQEvoRFlgDyPo"
    ##  [54] "https://open.spotify.com/track/66UvpufsKLpP4nmc8wGsvO"
    ##  [55] "https://open.spotify.com/track/3yp3NnC9WZd0vLEHivSIjm"
    ##  [56] "https://open.spotify.com/track/0UOHxcRnuccxG4bdPTmyah"
    ##  [57] "https://open.spotify.com/track/3HFBLRKGck6zHH1sjZ9thw"
    ##  [58] "https://open.spotify.com/track/0h4YYbDn66qb1gfynIEKZU"
    ##  [59] "https://open.spotify.com/track/0bqvxTkFgRjfNP5OecZxAm"
    ##  [60] "https://open.spotify.com/track/154f7iS4ws15lEPbcLbtIH"
    ##  [61] "https://open.spotify.com/track/0oaFzEorPTCzpkSLaL1EMA"
    ##  [62] "https://open.spotify.com/track/12wFQQhZqiZxwFY8YyZLjs"
    ##  [63] "https://open.spotify.com/track/38Vfn725QWVfmUA7OGmNzf"
    ##  [64] "https://open.spotify.com/track/1hBNR5sklDpCm0WwxvyKIA"
    ##  [65] "https://open.spotify.com/track/7HHZeIrgAuztp61wD13dx2"
    ##  [66] "https://open.spotify.com/track/0imnXHHj2jLvxAtAc8PR0N"
    ##  [67] "https://open.spotify.com/track/5JY84vCRB7wuJYNSWxPLuA"
    ##  [68] "https://open.spotify.com/track/0byDXsvbL1tX6vEfCRE6Pc"
    ##  [69] "https://open.spotify.com/track/1BqsJ3LaCxXW5BNsXVGACJ"
    ##  [70] "https://open.spotify.com/track/3Ljcwgfx60gk5bR4NW6OTM"
    ##  [71] "https://open.spotify.com/track/5EmT85Wp01BNJJRMah3jGm"
    ##  [72] "https://open.spotify.com/track/4rj5GlDtvhZzNorbHGqDzI"
    ##  [73] "https://open.spotify.com/track/1gwIyVvzXFnjPF3IJvDKm5"
    ##  [74] "https://open.spotify.com/track/12KahsnCx6L1AoD284MhP4"
    ##  [75] "https://open.spotify.com/track/55YE6fe7A6fjywV2sa0Q8H"
    ##  [76] "https://open.spotify.com/track/2scDv8z1skoWi97EvGkuy0"
    ##  [77] "https://open.spotify.com/track/5fLZQWarUISdz4attMFTXl"
    ##  [78] "https://open.spotify.com/track/2m6zeT8z6JloRjiyKjtXkB"
    ##  [79] "https://open.spotify.com/track/0nrXKptP97JPzTAesWaQ3A"
    ##  [80] "https://open.spotify.com/track/4hcMB6cObt073jy7IJME51"
    ##  [81] "https://open.spotify.com/track/5bVdMo9Ekz2uF5Qo97UrVZ"
    ##  [82] "https://open.spotify.com/track/7BjS53YK6XZFWaLTbPLsFk"
    ##  [83] "https://open.spotify.com/track/0PdHHn0TAJ5WtTWbfcdxia"
    ##  [84] "https://open.spotify.com/track/5o7crnI9sNYttQzEaAMuhJ"
    ##  [85] "https://open.spotify.com/track/79F8YDitR59cOpK3SWTlBt"
    ##  [86] "https://open.spotify.com/track/0GY0i9egpD94u1LzzyOyOk"
    ##  [87] "https://open.spotify.com/track/4b2MLFJhpRk4RkcVUKz9eE"
    ##  [88] "https://open.spotify.com/track/7jdiZTIcLAsWdETwfv9cD9"
    ##  [89] "https://open.spotify.com/track/4p6zul68EusN8EPySDneu4"
    ##  [90] "https://open.spotify.com/track/04tCn7vGznLOcqOa3KIWXF"
    ##  [91] "https://open.spotify.com/track/3X5MOJGMxJ73rw7DaVWsX7"
    ##  [92] "https://open.spotify.com/track/6D0fTBHt8GkrDPYtUpZJa2"
    ##  [93] "https://open.spotify.com/track/1QkB0joXKaCi1OqtEr6gHz"
    ##  [94] "https://open.spotify.com/track/0L0zu0jou652ed77WbUvLT"
    ##  [95] "https://open.spotify.com/track/2i9iAtqEg55p4MWjZGjpUP"
    ##  [96] "https://open.spotify.com/track/602UiYYO8O9o6KKtsrVaIc"
    ##  [97] "https://open.spotify.com/track/60Qih5vSHrZnJulxKMhFfw"
    ##  [98] "https://open.spotify.com/track/0lnjeahMAbnsdc5XQffVu1"
    ##  [99] "https://open.spotify.com/track/0knEVZAPKqy8Iv4yzJMR4N"
    ## [100] "https://open.spotify.com/track/40ndfBrZh2hZ6J7olaBH1U"
    ## [101] "https://open.spotify.com/track/17ebTXlrwyhlaFzFASembd"
    ## [102] "https://open.spotify.com/track/7GySmTIoNo2HTUkdgUxewg"
    ## [103] "https://open.spotify.com/track/5siv0EDgueMe3lhKe7D2Qe"
    ## [104] "https://open.spotify.com/track/0Enu67pxXlpkxQolQlhc14"
    ## [105] "https://open.spotify.com/track/2vDW0W4PMb8sg8XYVKWDXV"
    ## [106] "https://open.spotify.com/track/6UkpSgy6JGgpk9S629uDIN"
    ## [107] "https://open.spotify.com/track/6QFx7KTUtDa015z1oAbHQ7"
    ## [108] "https://open.spotify.com/track/4YZMZQfxFtZkbsploUZzR3"
    ## [109] "https://open.spotify.com/track/5hfXgkBuguM24DALerfp0o"
    ## [110] "https://open.spotify.com/track/7iiBBxQlGZVNKgCDHlclti"
    ## [111] "https://open.spotify.com/track/3kutuwGpGkukveDl5vm6qh"
    ## [112] "https://open.spotify.com/track/43CrTFPKW6M3dg5SCMC80Y"
    ## [113] "https://open.spotify.com/track/7dPKiPg3BYsD5mcj4BYoWs"
    ## [114] "https://open.spotify.com/track/6SuwxKGmPkYj1zhTuAThDu"
    ## [115] "https://open.spotify.com/track/3zlDJ5CJpGHH3VZpjonLoz"
    ## [116] "https://open.spotify.com/track/3KiqXLiBK3nv6UuE5pM6do"
    ## [117] "https://open.spotify.com/track/7qLTqFtzopkvO9DpEtmVLp"
    ## [118] "https://open.spotify.com/track/3XCH1LO25WygbqJ2p2nys8"
    ## [119] "https://open.spotify.com/track/4Kn1CY38BkOpWr3K9NYusA"
    ## [120] "https://open.spotify.com/track/49HpPuLzPBg4ypTT7m75xt"
    ## [121] "https://open.spotify.com/track/7wpGYGBwcQqYKq6n5mRodo"
    ## [122] "https://open.spotify.com/track/31AvVYMCukDC0l91YZF3A4"
    ## [123] "https://open.spotify.com/track/3GH6N7vqhohbtz1GPK9sd5"
    ## [124] "https://open.spotify.com/track/4Xtoc1NPWScnLJYYoM7GKz"
    ## [125] "https://open.spotify.com/track/1dBhZ7w44wuxA7yknsTk7N"
    ## [126] "https://open.spotify.com/track/54UKWnwlypkSOMonre29od"
    ## [127] "https://open.spotify.com/track/0Eksuhk0vZZ4hSvHGpTP0K"
    ## [128] "https://open.spotify.com/track/4lgVT1N3PhTXyYvbhDfcgp"
    ## [129] "https://open.spotify.com/track/0iJHgqitnbZr7BTTYn2QUi"
    ## [130] "https://open.spotify.com/track/0AS2J2x4lx5wFI8vXaiTAR"
    ## [131] "https://open.spotify.com/track/1Lq8zkOcbS5SSR3tfaBKAk"
    ## [132] "https://open.spotify.com/track/12eg5Wi8FwoaLX1qZM8AlB"
    ## [133] "https://open.spotify.com/track/66dYfoYTNuYWcCBFgM5MYk"
    ## [134] "https://open.spotify.com/track/6ibfgcB88JCqXdtoQn1FH1"
    ## [135] "https://open.spotify.com/track/27Rk3efWlQCpuqtBvYPDRa"
    ## [136] "https://open.spotify.com/track/3g44ROxOt4ROPo8XJ2UR7m"
    ## [137] "https://open.spotify.com/track/7pmY0bsGJhJocJAD9McD7f"
    ## [138] "https://open.spotify.com/track/1Tv1eDlR7iT8c0XniLJ5bk"
    ## [139] "https://open.spotify.com/track/0FO3dSwoxwbtHLDUKScCNb"
    ## [140] "https://open.spotify.com/track/1kt1mKyyIwIwW3wXWmYc4I"
    ## [141] "https://open.spotify.com/track/78Dks2zLmP3h44MyJq92eZ"
    ## [142] "https://open.spotify.com/track/0DFIYO7JuVzKqb6BzT20Lx"
    ## [143] "https://open.spotify.com/track/1LyJKzqv9xIfcituvOGiBr"
    ## [144] "https://open.spotify.com/track/7riwwEmkggYDBrKZLZs5k9"
    ## [145] "https://open.spotify.com/track/6nSjbaMqIGtyoIIZCQxJ0q"
    ## [146] "https://open.spotify.com/track/0supz29PWinhdasXabROMz"
    ## [147] "https://open.spotify.com/track/0DdFgX3Vw9kUrdqPi4IRzD"
    ## [148] "https://open.spotify.com/track/7Ij1Pr6puYVCQDbJhIm886"
    ## [149] "https://open.spotify.com/track/20OzA6UXdbwXhpj5sJzC1f"
    ## [150] "https://open.spotify.com/track/5O9IcKRscrAzVvVWxDZ9Ez"
    ## [151] "https://open.spotify.com/track/3JRQdFZf7wacuevIIM5gCh"
    ## [152] "https://open.spotify.com/track/4XYcPGjNuMPIYiS5WAFN5h"
    ## [153] "https://open.spotify.com/track/53q2sTiTflfzOrfDZuIybM"
    ## [154] "https://open.spotify.com/track/6E6LEXUM0usFAv5TbWr4xb"
    ## [155] "https://open.spotify.com/track/575oJnO5iaXqb7B7xdQThP"
    ## [156] "https://open.spotify.com/track/1hi4NXqTQd1KN8nfVlYMxy"
    ## [157] "https://open.spotify.com/track/7pa40OwK2JZB3YXWlWuezI"
    ## [158] "https://open.spotify.com/track/03qxh0yQvzfkzQpbiQx9Vy"
    ## [159] "https://open.spotify.com/track/1mGqnbZxrbwowE8MBtZ9Jz"
    ## [160] "https://open.spotify.com/track/6131dCOwszHN5MjLIESBXc"
    ## [161] "https://open.spotify.com/track/1zDQB1ZAy5O7KqYjm3h6DC"
    ## [162] "https://open.spotify.com/track/1dTTzPR9x8Ectf4Ai3VUNN"
    ## [163] "https://open.spotify.com/track/5Lu9rXe3WyrObFC2joG5At"
    ## [164] "https://open.spotify.com/track/6Z9ky4UBv64c4AkMJGXcAn"
    ## [165] "https://open.spotify.com/track/3IG6hZrn8RsfBeMVpSGAwg"
    ## [166] "https://open.spotify.com/track/12q3o7tLAOrieLjdEUjg5A"
    ## [167] "https://open.spotify.com/track/0WFX7I3s1nN8G1Ls3jlWLB"
    ## [168] "https://open.spotify.com/track/6NGyA3VF6Cp05H8DaOj4ms"
    ## [169] "https://open.spotify.com/track/30PROT85L6bjn28F9Mskmj"
    ## [170] "https://open.spotify.com/track/0vEOuzuXUIl0GnFezbr8GJ"
    ## [171] "https://open.spotify.com/track/16CcsIqvnzUXhuPaCCMr7n"
    ## [172] "https://open.spotify.com/track/3ja2SrcpSxZL0bo5jwANxU"
    ## [173] "https://open.spotify.com/track/2rjdGZtXeVkoTsTfIXYm64"
    ## [174] "https://open.spotify.com/track/6dM2m1C41Sq7DiR0YoWvd4"
    ## [175] "https://open.spotify.com/track/6icBEV31HXb1aiezhYiI01"
    ## [176] "https://open.spotify.com/track/4Hw9XevNbQXB9vHFPXAEpY"
    ## [177] "https://open.spotify.com/track/3yO0QMI5MgRK8MmKjUQnaX"
    ## [178] "https://open.spotify.com/track/6clYCyrk929HSIJIWdHQB1"
    ## [179] "https://open.spotify.com/track/3kGOXjG0sgIaV5h1UnbXZW"
    ## [180] "https://open.spotify.com/track/5Tqq5jSCAJ46T5MT9mjr7C"
    ## [181] "https://open.spotify.com/track/0pOGR1GkFdtzidvtrhIiOf"
    ## [182] "https://open.spotify.com/track/51AjfUizkNRfoayZLXLhUl"
    ## [183] "https://open.spotify.com/track/0eWtO8QFxowKG6Fr7EnmLL"
    ## [184] "https://open.spotify.com/track/49jzsrLpyVXYpfxoIqltkC"
    ## [185] "https://open.spotify.com/track/4AFnOESf6n3UlaUDcyrfES"
    ## [186] "https://open.spotify.com/track/5sbR5gpnllnUiXjrQzx6vv"
    ## [187] "https://open.spotify.com/track/2VCCyMOEpuUt0kwdQ2hq25"
    ## [188] "https://open.spotify.com/track/75JxeTeQSiGz7DREh5LCeO"
    ## [189] "https://open.spotify.com/track/3sBj4S7tUG5giyUxc3j8Li"
    ## [190] "https://open.spotify.com/track/3HabJAClzTZcAU4ctUUiQw"
    ## [191] "https://open.spotify.com/track/3ec6LZbtmkGa4Kspdzmox7"
    ## [192] "https://open.spotify.com/track/7kvJv3I1eXt6CU3ueB9U3o"
    ## [193] "https://open.spotify.com/track/3vmz8KtwVYm22UimoSWyRk"
    ## [194] "https://open.spotify.com/track/5vI3kFq6qP5nlvwzkpGNrz"
    ## [195] "https://open.spotify.com/track/0UctRBApIgE5PgnNMWUPGF"
    ## [196] "https://open.spotify.com/track/5iVpzTDaw9L4cxllrsvs06"
    ## [197] "https://open.spotify.com/track/5NypAeOF85tVAhb4Ktco4i"
    ## [198] "https://open.spotify.com/track/0SCrzUb71JxqW4bYPXXFG4"
    ## [199] "https://open.spotify.com/track/1I4PlB4oPzB7RDCbVWSJpI"
    ## [200] "https://open.spotify.com/track/5bnpdRNv0ckhlZ3TJTTaed"

Aquí se tiene impresa en pantalla la lista de reproducción con todos los
links necesarios, la que dura más de 3 horas.

## Conclusión

Se obtuvo una playlist de más de 3 horas con canciones similares a una
canción tomada al azar, tomando como variables para la generación de
grupos separados y definidos el tempo y la energía de cada canción.
