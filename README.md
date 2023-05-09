Tidy Data - Pivot Wider
================

## Tidy data - pivot wider to organize data for ease of analysis

This code reshapes the `Titanic` data into a wider data frame. It uses the `Titanic` dataset built-into R which provides information about the survival of passengers on the Titanic voyage. Using the [`pivot_wider()`](https://tidyr.tidyverse.org/reference/pivot_wider.html) function, it increases the number of columns while decreasing the number of rows.

The `Pivot_wider()` function from `tidyr`uses arguments `names_from` to
specify which variables should be used as column names and `values_from`
for variables that contain the values. Because `pivot_wider` creates
unique combinations of all columns not included in the arguments, it
generates an output with NAs for each combination. This code identifies
unique observations by using the `distinct()` function. It renders a restructured tidy data that simplifies column comparisons.

``` r
  class = Titanic %>%
    distinct() %>%
    pivot_wider(
              names_from = Class,    # name of col containing the names
              values_from = Freq) %>%  # name of col containing the values
   select(3, First = 4, Second = 5, Third = 6, 7) %>%   # rename & filter cols
   unnest(cols = everything()) # removes duplicate rows if needed
   
   knitr::kable(class)
```

| Survived | First | Second | Third | Crew |
|:---------|------:|-------:|------:|-----:|
| No       |     0 |      0 |    35 |    0 |
| No       |     0 |      0 |    17 |    0 |
| No       |   118 |    154 |   387 |  670 |
| No       |     4 |     13 |    89 |    3 |
| Yes      |     5 |     11 |    13 |    0 |
| Yes      |     1 |     13 |    14 |    0 |
| Yes      |    57 |     14 |    75 |  192 |
| Yes      |   140 |     80 |    76 |   20 |
