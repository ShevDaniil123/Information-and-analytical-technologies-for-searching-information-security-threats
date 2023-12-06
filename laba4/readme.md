# Лабораторная работа №4
Шевченко Д.Д.

## Цель Работы

1.  Закрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Закрепить навыки исследования метаданных DNS трафика

## Ход работы

### Подготовка

``` r
library('dplyr')
```


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

``` r
library('tidyverse')
```

    Warning: пакет 'tidyverse' был собран под R версии 4.3.2

    Warning: пакет 'ggplot2' был собран под R версии 4.3.2

    Warning: пакет 'tidyr' был собран под R версии 4.3.2

    Warning: пакет 'readr' был собран под R версии 4.3.2

    Warning: пакет 'purrr' был собран под R версии 4.3.2

    Warning: пакет 'forcats' был собран под R версии 4.3.2

    Warning: пакет 'lubridate' был собран под R версии 4.3.2

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ forcats   1.0.0     ✔ readr     2.1.4
    ✔ ggplot2   3.4.4     ✔ stringr   1.5.0
    ✔ lubridate 1.9.3     ✔ tibble    3.2.1
    ✔ purrr     1.0.2     ✔ tidyr     1.3.0

    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
dns <- read_tsv("dns.log")
```

    New names:
    Rows: 427934 Columns: 23
    ── Column specification
    ──────────────────────────────────────────────────────── Delimiter: "\t" chr
    (13): CWGtK431H9XuaTN4fi, 192.168.202.100, 192.168.27.203, udp, *\x00\x0... dbl
    (5): 1331901005.510000, 45658, 137, 33008, 1...20 lgl (5): F...16, F...17,
    F...18, F...19, F...23
    ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    Specify the column types or set `show_col_types = FALSE` to quiet this message.
    • `1` -> `1...10`
    • `F` -> `F...16`
    • `F` -> `F...17`
    • `F` -> `F...18`
    • `F` -> `F...19`
    • `1` -> `1...20`
    • `-` -> `-...21`
    • `-` -> `-...22`
    • `F` -> `F...23`

``` r
dns
```

    # A tibble: 427,934 × 23
       `1331901005.510000` CWGtK431H9XuaTN4fi `192.168.202.100` `45658`
                     <dbl> <chr>              <chr>               <dbl>
     1         1331901015. C36a282Jljz7BsbGH  192.168.202.76        137
     2         1331901016. C36a282Jljz7BsbGH  192.168.202.76        137
     3         1331901017. C36a282Jljz7BsbGH  192.168.202.76        137
     4         1331901006. C36a282Jljz7BsbGH  192.168.202.76        137
     5         1331901007. C36a282Jljz7BsbGH  192.168.202.76        137
     6         1331901007. C36a282Jljz7BsbGH  192.168.202.76        137
     7         1331901006. ClEZCt3GLkJdtGGmAa 192.168.202.89        137
     8         1331901007. ClEZCt3GLkJdtGGmAa 192.168.202.89        137
     9         1331901008. ClEZCt3GLkJdtGGmAa 192.168.202.89        137
    10         1331901007. CpD4i41jyaYqmTBMH3 192.168.202.89        137
    # ℹ 427,924 more rows
    # ℹ 19 more variables: `192.168.27.203` <chr>, `137` <dbl>, udp <chr>,
    #   `33008` <dbl>,
    #   `*\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00` <chr>,
    #   `1...10` <chr>, C_INTERNET <chr>, `33` <chr>, SRV <chr>, `0` <chr>,
    #   NOERROR <chr>, F...16 <lgl>, F...17 <lgl>, F...18 <lgl>, F...19 <lgl>,
    #   `1...20` <dbl>, `-...21` <chr>, `-...22` <chr>, F...23 <lgl>

## Задание 1

### Добавьте пропущенные данные о структуре данных (назначении столбцов)

``` r
names(dns) <- c("ts", "uid", "id_or_h", "or_p", "id_re_h", "re_p","proto", "trans_id","query","qclass", "qclass_name", "qtype", "qtype_name", "rcode","rcode_name", "AA", "TC","RD","RA","Z","answer","TTLs","rejected")
```

## Задание 2

### Просмотрите общую структуру данных с помощью функции glimpse()

``` r
glimpse(dns)
```

    Rows: 427,934
    Columns: 23
    $ ts          <dbl> 1331901015, 1331901016, 1331901017, 1331901006, 1331901007…
    $ uid         <chr> "C36a282Jljz7BsbGH", "C36a282Jljz7BsbGH", "C36a282Jljz7Bsb…
    $ id_or_h     <chr> "192.168.202.76", "192.168.202.76", "192.168.202.76", "192…
    $ or_p        <dbl> 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137…
    $ id_re_h     <chr> "192.168.202.255", "192.168.202.255", "192.168.202.255", "…
    $ re_p        <dbl> 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137…
    $ proto       <chr> "udp", "udp", "udp", "udp", "udp", "udp", "udp", "udp", "u…
    $ trans_id    <dbl> 57402, 57402, 57402, 57398, 57398, 57398, 62187, 62187, 62…
    $ query       <chr> "HPE8AA67", "HPE8AA67", "HPE8AA67", "WPAD", "WPAD", "WPAD"…
    $ qclass      <chr> "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", "1"…
    $ qclass_name <chr> "C_INTERNET", "C_INTERNET", "C_INTERNET", "C_INTERNET", "C…
    $ qtype       <chr> "32", "32", "32", "32", "32", "32", "32", "32", "32", "33"…
    $ qtype_name  <chr> "NB", "NB", "NB", "NB", "NB", "NB", "NB", "NB", "NB", "SRV…
    $ rcode       <chr> "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-"…
    $ rcode_name  <chr> "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-"…
    $ AA          <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FA…
    $ TC          <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FA…
    $ RD          <lgl> TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, FALS…
    $ RA          <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FA…
    $ Z           <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0…
    $ answer      <chr> "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-"…
    $ TTLs        <chr> "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-"…
    $ rejected    <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FA…

## Задание 3

### Сколько участников информационного обмена в сети Доброй Организации?

``` r
select(dns,uid) %>% group_by(uid) %>% count() %>% nrow()
```

    [1] 162495

Ответ: 162495

## Задание 4

### Какое соотношение участников обмена внутри сети и участников обращений к внешним ресурсам?

``` r
#a <- filter(dns, query != '-',query == '(empty)') %>% group_by(uid) %>% count() %>% nrow()
a <- filter(dns, qtype_name == 'A'| qtype_name == 'AA' | qtype_name =='AAA' | qtype_name == 'AAAA') %>% group_by(uid) %>% count() %>% nrow() 
b <- filter(dns, qtype_name != 'A', qtype_name !='AA', qtype_name !='AAA', qtype_name !='AAAA') %>% group_by(uid) %>% count() %>% nrow()
#b <- filter(dns, query !='-',query != '(empty)') %>% group_by(uid) %>% count() %>% nrow()
b/a
```

    [1] 0.5084645

Ответ: 0.5084645

## Задание 5

### Найдите топ-10 участников сети, проявляющих наибольшую сетевую активность.

``` r
select(dns,uid) %>% group_by(uid) %>% count() %>% arrange(desc(n)) %>% head(10)
```

    # A tibble: 10 × 2
    # Groups:   uid [10]
       uid                    n
       <chr>              <int>
     1 CHwsqo48JzsgOOx5u5 18622
     2 C69INN8eedNqxIAs2   9082
     3 CQX0cW23Ci1D08eA78  8914
     4 CM87gu1xIgp1q0nWej  8101
     5 CzNRck2zqMl2K4BvIh  7724
     6 CFHJkD5qSIAnIDAnb   6140
     7 CrASxG4WWqN5lFYZpd  5403
     8 Cvfa4A2CK3vpoyJO9   4621
     9 CZ6P023bXFwrV0Waxj  2829
    10 Cq7OOsGzpAIeJK3x7   2318

## Задание 6

### Найдите топ-10 доменов, к которым обращаются пользователи сети и соответственное количество обращений

``` r
top_dom <- dns %>% filter(query !='-', qtype_name == 'A'| qtype_name == 'AA' | qtype_name =='AAA' | qtype_name == 'AAAA') %>% select(query) %>% group_by(query) %>% count() %>% arrange(desc(n)) %>% head(10)
top_dom
```

    # A tibble: 10 × 2
    # Groups:   query [10]
       query                               n
       <chr>                           <int>
     1 teredo.ipv6.microsoft.com       39273
     2 tools.google.com                14057
     3 www.apple.com                   13390
     4 safebrowsing.clients.google.com 11658
     5 imap.gmail.com                   5543
     6 stats.norton.com                 5537
     7 www.google.com                   5171
     8 ratings-wrs.symantec.com         4464
     9 api.twitter.com                  4348
    10 api.facebook.com                 4137

## Задание 7

### Опеределите базовые статистические характеристики (функция summary()) интервала времени между последовательным обращениями к топ-10 доменам.

``` r
summary(diff((dns %>% filter(tolower(query) %in% top_dom$query) %>% arrange(ts))$ts))
```

        Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
        0.00     0.00     0.00     1.08     0.31 49924.53 

``` r
#dns %>% filter(query !='-',ts !='NA') %>% select(query,mean(ts)) %>% group_by(query) %>% count() %>% arrange(desc(n)) %>% head(10)
```

## Задание 8

### Часто вредоносное программное обеспечение использует DNS канал в качестве канала управления, периодически отправляя запросы на подконтрольный злоумышленникам DNS сервер. По периодическим запросам на один и тот же домен можно выявить скрытый DNS канал. Есть ли такие IP адреса в исследуемом датасете?

``` r
t <- dns %>% group_by(id_or_h, query) %>% summarise(total = n()) %>% filter(total > 1)
```

    `summarise()` has grouped output by 'id_or_h'. You can override using the
    `.groups` argument.

``` r
unique(t$id_or_h)%>% head()
```

    [1] "10.10.10.10"     "10.10.117.209"   "10.10.117.210"   "128.244.37.196" 
    [5] "169.254.109.123" "169.254.228.26" 

## Задание 9

### Определите местоположение (страну, город) и организацию-провайдера для топ-10 доменов.

## Вывод

### Удалось закрепить знания основных функций обработки данных экосистемы tidyverse языка R, а так же навыки исследования метаданных DNS файла
