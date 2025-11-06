# Programming assignment 3

2025-11-06

\##Load libraries and data

``` r
library(dplyr)
```


    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
library(ggplot2)
```

\##Descriptive statistics

``` r
vowel_data <- read.csv("data/vowel_data.csv",
                fileEncoding = "UTF-16",
                encoding = "UTF-8",
                sep = ",",
                stringsAsFactors = TRUE)
```

``` r
vowel_data |> 
  summarise(
    mean_F1 = mean(f1_cent, na.rm = TRUE),
    sd_F1 = sd(f1_cent, na.rm = TRUE),
    mean_F2 = mean(f2_cent, na.rm = TRUE),
    sd_F2 = sd(f2_cent, na.rm = TRUE),
    mean_tl = mean(tl, na.rm = TRUE),
    sd_tl = sd(tl, na.rm = TRUE),
    n=n()
  ) 
```

       mean_F1    sd_F1  mean_F2    sd_F2  mean_tl    sd_tl  n
    1 535.1117 188.5376 1699.766 381.7847 1774.383 928.2713 36

\##Plots

``` r
ggplot(vowel_data) +
  geom_boxplot(aes(x = vowel, y = tl))
```

![](pa_3_files/figure-commonmark/unnamed-chunk-4-1.png)

``` r
ggplot(vowel_data) +
  geom_boxplot(aes(x = language, y = tl))
```

![](pa_3_files/figure-commonmark/unnamed-chunk-5-1.png)

``` r
ggplot(vowel_data) +
  geom_boxplot(aes(x = language, y = tl, fill = vowel))
```

![](pa_3_files/figure-commonmark/unnamed-chunk-6-1.png)

``` r
ggplot(vowel_data) +
  geom_boxplot(aes(x = language, y = f1_cent, fill = vowel)) +
  labs(y = "F1 centroid (Hz)",
       x = "Language",
       fill = "Vowel",
       title = "F1 centroid by language and vowel")
```

![](pa_3_files/figure-commonmark/unnamed-chunk-7-1.png)

``` r
ggplot(vowel_data) +
  geom_boxplot(aes(x = language, y = f2_cent, fill = vowel)) +
  labs(y = "F2 centroid (Hz)",
       x = "Language",
       fill = "Vowel",
       title = "F2 centroid by language and vowel")
```

![](pa_3_files/figure-commonmark/unnamed-chunk-8-1.png)

``` r
ggplot(vowel_data) +
  geom_point(aes(x = f1_cent, y = f2_cent, color = tl)) +
  labs(x = "F1 centroid (Hz)",
       y = "F2 centroid (Hz)",
       color = "Trajectory length (Hz)")
```

![](pa_3_files/figure-commonmark/unnamed-chunk-9-1.png)

\##Questions 1-This part of the script calculates several key points
between a starting point (vonset) and an ending point (voffset). It
first measures the total distance or duration between the two points
(durationV = voffset - vonset), then uses that value to find positions
at 20%, 35%, 50%, 65%, and 80% of the way between the start and end.

2-First, the goal is to get vonset at the initial of vowel, and then get
the end point of the vowel, duration of the vowel , and finally
calculate the midpoint at different percentage.

3-It’s different form the previous pa because for this we had to
calculate the f1, f2, and on top of that the vowel centroids.
