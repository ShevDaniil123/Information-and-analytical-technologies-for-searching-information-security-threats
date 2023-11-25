# Лабораторная работа №3
Шевченко Д. Д.

# Цель работы:

### 1) Зекрепить практические навыки использования языка программирования R для обработки данных

### 2) Закрепить знания основных функций обработки данных экосистемы tidyverse языка R

### 3) Развить пркатические навыки использования функций обработки данных пакета dplyr – функции select(), filter(), mutate(), arrange(), group_by()

# Ход работы:

## Задание №1

### Сколько встроенных в пакет nycflights13 датафреймов?

### nycflights13::

### В пакете nycflights13 встроено 5 датафреймов.

## Задание №2

### Сколько строк в каждом датафрейме?

``` r
library('nycflights13')
```

    Warning: пакет 'nycflights13' был собран под R версии 4.3.2

``` r
library('dplyr')
```


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

``` r
nycflights13::airlines %>% nrow()
```

    [1] 16

``` r
nycflights13::airports %>% nrow()
```

    [1] 1458

``` r
nycflights13::flights %>% nrow()
```

    [1] 336776

``` r
nycflights13::planes %>% nrow()
```

    [1] 3322

``` r
nycflights13::weather %>% nrow()
```

    [1] 26115

### Ответ:

### airlines - 16 строк

### airports - 1458 строк

### flights - 336776 строк

### planes - 3322 строк

### weather - 26115 строк

## Задание №3

### Сколько столбцов в каждом датафрейме?

``` r
library('nycflights13')
library('dplyr')
nycflights13::airlines %>% ncol()
```

    [1] 2

``` r
nycflights13::airports %>% ncol()
```

    [1] 8

``` r
nycflights13::flights %>% ncol()
```

    [1] 19

``` r
nycflights13::planes %>% ncol()
```

    [1] 9

``` r
nycflights13::weather %>% ncol()
```

    [1] 15

### Ответ:

### airlines - 2

### airports - 8

### flights - 19

### planes - 9

### weather - 15

## Задание №4

### Как просмотреть примерный вид датафрейма?

``` r
library('nycflights13')
library('dplyr')
nycflights13::airlines %>% str()
```

    tibble [16 × 2] (S3: tbl_df/tbl/data.frame)
     $ carrier: chr [1:16] "9E" "AA" "AS" "B6" ...
     $ name   : chr [1:16] "Endeavor Air Inc." "American Airlines Inc." "Alaska Airlines Inc." "JetBlue Airways" ...

``` r
nycflights13::airports %>% str()
```

    tibble [1,458 × 8] (S3: tbl_df/tbl/data.frame)
     $ faa  : chr [1:1458] "04G" "06A" "06C" "06N" ...
     $ name : chr [1:1458] "Lansdowne Airport" "Moton Field Municipal Airport" "Schaumburg Regional" "Randall Airport" ...
     $ lat  : num [1:1458] 41.1 32.5 42 41.4 31.1 ...
     $ lon  : num [1:1458] -80.6 -85.7 -88.1 -74.4 -81.4 ...
     $ alt  : num [1:1458] 1044 264 801 523 11 ...
     $ tz   : num [1:1458] -5 -6 -6 -5 -5 -5 -5 -5 -5 -8 ...
     $ dst  : chr [1:1458] "A" "A" "A" "A" ...
     $ tzone: chr [1:1458] "America/New_York" "America/Chicago" "America/Chicago" "America/New_York" ...
     - attr(*, "spec")=List of 3
      ..$ cols   :List of 12
      .. ..$ id     : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
      .. ..$ name   : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      .. ..$ city   : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      .. ..$ country: list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      .. ..$ faa    : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      .. ..$ icao   : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      .. ..$ lat    : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
      .. ..$ lon    : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
      .. ..$ alt    : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
      .. ..$ tz     : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_double" "collector"
      .. ..$ dst    : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      .. ..$ tzone  : list()
      .. .. ..- attr(*, "class")= chr [1:2] "collector_character" "collector"
      ..$ default: list()
      .. ..- attr(*, "class")= chr [1:2] "collector_guess" "collector"
      ..$ skip   : num 0
      ..- attr(*, "class")= chr "col_spec"

``` r
nycflights13::flights %>% str()
```

    tibble [336,776 × 19] (S3: tbl_df/tbl/data.frame)
     $ year          : int [1:336776] 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 ...
     $ month         : int [1:336776] 1 1 1 1 1 1 1 1 1 1 ...
     $ day           : int [1:336776] 1 1 1 1 1 1 1 1 1 1 ...
     $ dep_time      : int [1:336776] 517 533 542 544 554 554 555 557 557 558 ...
     $ sched_dep_time: int [1:336776] 515 529 540 545 600 558 600 600 600 600 ...
     $ dep_delay     : num [1:336776] 2 4 2 -1 -6 -4 -5 -3 -3 -2 ...
     $ arr_time      : int [1:336776] 830 850 923 1004 812 740 913 709 838 753 ...
     $ sched_arr_time: int [1:336776] 819 830 850 1022 837 728 854 723 846 745 ...
     $ arr_delay     : num [1:336776] 11 20 33 -18 -25 12 19 -14 -8 8 ...
     $ carrier       : chr [1:336776] "UA" "UA" "AA" "B6" ...
     $ flight        : int [1:336776] 1545 1714 1141 725 461 1696 507 5708 79 301 ...
     $ tailnum       : chr [1:336776] "N14228" "N24211" "N619AA" "N804JB" ...
     $ origin        : chr [1:336776] "EWR" "LGA" "JFK" "JFK" ...
     $ dest          : chr [1:336776] "IAH" "IAH" "MIA" "BQN" ...
     $ air_time      : num [1:336776] 227 227 160 183 116 150 158 53 140 138 ...
     $ distance      : num [1:336776] 1400 1416 1089 1576 762 ...
     $ hour          : num [1:336776] 5 5 5 5 6 5 6 6 6 6 ...
     $ minute        : num [1:336776] 15 29 40 45 0 58 0 0 0 0 ...
     $ time_hour     : POSIXct[1:336776], format: "2013-01-01 05:00:00" "2013-01-01 05:00:00" ...

``` r
nycflights13::planes %>% str()
```

    tibble [3,322 × 9] (S3: tbl_df/tbl/data.frame)
     $ tailnum     : chr [1:3322] "N10156" "N102UW" "N103US" "N104UW" ...
     $ year        : int [1:3322] 2004 1998 1999 1999 2002 1999 1999 1999 1999 1999 ...
     $ type        : chr [1:3322] "Fixed wing multi engine" "Fixed wing multi engine" "Fixed wing multi engine" "Fixed wing multi engine" ...
     $ manufacturer: chr [1:3322] "EMBRAER" "AIRBUS INDUSTRIE" "AIRBUS INDUSTRIE" "AIRBUS INDUSTRIE" ...
     $ model       : chr [1:3322] "EMB-145XR" "A320-214" "A320-214" "A320-214" ...
     $ engines     : int [1:3322] 2 2 2 2 2 2 2 2 2 2 ...
     $ seats       : int [1:3322] 55 182 182 182 55 182 182 182 182 182 ...
     $ speed       : int [1:3322] NA NA NA NA NA NA NA NA NA NA ...
     $ engine      : chr [1:3322] "Turbo-fan" "Turbo-fan" "Turbo-fan" "Turbo-fan" ...

``` r
nycflights13::weather %>% str()
```

    tibble [26,115 × 15] (S3: tbl_df/tbl/data.frame)
     $ origin    : chr [1:26115] "EWR" "EWR" "EWR" "EWR" ...
     $ year      : int [1:26115] 2013 2013 2013 2013 2013 2013 2013 2013 2013 2013 ...
     $ month     : int [1:26115] 1 1 1 1 1 1 1 1 1 1 ...
     $ day       : int [1:26115] 1 1 1 1 1 1 1 1 1 1 ...
     $ hour      : int [1:26115] 1 2 3 4 5 6 7 8 9 10 ...
     $ temp      : num [1:26115] 39 39 39 39.9 39 ...
     $ dewp      : num [1:26115] 26.1 27 28 28 28 ...
     $ humid     : num [1:26115] 59.4 61.6 64.4 62.2 64.4 ...
     $ wind_dir  : num [1:26115] 270 250 240 250 260 240 240 250 260 260 ...
     $ wind_speed: num [1:26115] 10.36 8.06 11.51 12.66 12.66 ...
     $ wind_gust : num [1:26115] NA NA NA NA NA NA NA NA NA NA ...
     $ precip    : num [1:26115] 0 0 0 0 0 0 0 0 0 0 ...
     $ pressure  : num [1:26115] 1012 1012 1012 1012 1012 ...
     $ visib     : num [1:26115] 10 10 10 10 10 10 10 10 10 10 ...
     $ time_hour : POSIXct[1:26115], format: "2013-01-01 01:00:00" "2013-01-01 02:00:00" ...

## Задание №5

### Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?

``` r
library('nycflights13')
library('dplyr')
nycflights13::airlines %>% nrow()
```

    [1] 16

### Ответ:

### \[1\] 16

## Задание №6

### Сколько рейсов принял аэропорт John F Kennedy Intl в мае?

``` r
library('nycflights13')
a <- filter(flights, origin == 'JFK' & month == 5)
count(a)
```

    # A tibble: 1 × 1
          n
      <int>
    1  9397

### Ответ: 9397

## Задание №7

### Какой самый северный аэропорт?

``` r
library('nycflights13')
a <- max(nycflights13::airports$lat, na.rm = TRUE)
nycflights13::airports %>% select(name,lat) %>% filter(lat==a)
```

    # A tibble: 1 × 2
      name                      lat
      <chr>                   <dbl>
    1 Dillant Hopkins Airport  72.3

### Ответ: Dillant Hopkins Airport 72.3

## Задание №8

### Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?

``` r
library('nycflights13')
a <- filter(weather, pressure != 'NA')
b <- max(a$pressure)
c <- filter(weather, pressure == b)
d <- select(c,origin)
d
```

    # A tibble: 2 × 1
      origin
      <chr> 
    1 JFK   
    2 JFK   

### Ответ: JFK

## Задание №9

### Какие бортовые номера у самых старых самолетов?

``` r
library('nycflights13')
a <- filter(planes, year != 'NA')
b <- min(a$year)
c <- filter(planes, year == b)
select (c, tailnum)
```

    # A tibble: 1 × 1
      tailnum
      <chr>  
    1 N381AA 

### Ответ: N381AA

## Задание №10

### Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).

``` r
library('nycflights13')
a <- filter(weather, origin == 'JFK', month == 9, temp != 'NA')
b <- summarize(a, delay = mean(temp, na.rm = TRUE ))
c <- 5/9*(b-32)
c
```

         delay
    1 19.38764

### Ответ: 19.38764

## Задание №11

### Самолеты какой авиакомпании совершили больше всего вылетов в июне?

``` r
library('nycflights13')
a <- filter(flights, month == 6, carrier != 'NA', month != 'NA')
b <- group_by(a, carrier)
c <- count(b, carrier)
d <- filter(c, n == max(c$n))
f <- filter(airlines, carrier == d$carrier)
f
```

    # A tibble: 1 × 2
      carrier name                 
      <chr>   <chr>                
    1 UA      United Air Lines Inc.

### Ответ: United Air Lines Inc

## Задание №12

### Самолеты какой авиакомпании задерживались чаще других в 2013 году?

``` r
library('nycflights13')
library('dplyr')
a <- filter(flights, year == 2013, dep_delay != 'NA', arr_delay != 'NA', arr_delay > 0, dep_delay > 0)
b <- group_by(a,carrier)
c <- count(b,carrier)
d <- filter(c, n == max(c$n))
f <- filter(airlines, carrier == d$carrier)
f
```

    # A tibble: 1 × 2
      carrier name                    
      <chr>   <chr>                   
    1 EV      ExpressJet Airlines Inc.

### Ответ: ExpressJet Airlines Inc

## Вывод

### Получилось развить пркатические навыки использования функций обработки данных пакета dplyr – функции select(), filter(), mutate(), arrange(), group_by()
