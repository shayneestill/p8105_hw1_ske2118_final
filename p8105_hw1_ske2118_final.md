p8105_hw1_ske2118_final
================
Shayne Estill
2024-09-21

# Homework 1 Set up

Here’s a **code chunk** that loads tidyverse:

# Problem 1

Here we load our penguin data:

The penguin dataset has observations about three different penguin
species (adelie, chinstrap, and gentoo) on three different islands
(biscoe, dream, and torgersen).

Data collected about these penguins included bill_length_mm,
bill_depth_mm, and flipper_length_mm (all measured in millimeters) as
well as body_mass_g (measured in grams), sex, and year.

The penguins dataset has 344 rows and 8 columns.

The mean flipper length is 200.9152047.

``` r
ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()
```

![](p8105_hw1_ske2118_final_files/figure-gfm/scatterplot-1.png)<!-- -->

``` r
ggsave("scatterplot.pdf")
```

    ## Saving 7 x 5 in image

I produced a scatterplot of bill_length_mm to flipper_length_mm in which
each species is a different color point. I suppressed the warning
regarding two observations without a number value.

# Problem 2

``` r
problem2_df = tibble(   
  vec_numeric = rnorm(10),
  vec_logical = vec_numeric>0,
  vec_char = c("A", "B", "C", "D", "E", "F", "G", "H","I", "J"),
  vec_factor = factor(c("small", "medium", "large", "small", "medium",                    "large", "small", "medium", "large", "small"))
  )
```

Now, let’s look at what happens when we try to take the means.

``` r
  mean(pull(problem2_df, vec_numeric))
```

    ## [1] 0.005967757

``` r
  mean(pull(problem2_df, vec_logical))
```

    ## [1] 0.5

``` r
  mean(pull(problem2_df, vec_char))
```

    ## Warning in mean.default(pull(problem2_df, vec_char)): argument is not numeric
    ## or logical: returning NA

    ## [1] NA

``` r
  mean(pull(problem2_df, vec_factor))
```

    ## Warning in mean.default(pull(problem2_df, vec_factor)): argument is not numeric
    ## or logical: returning NA

    ## [1] NA

The vec_numeric and vec_logical are both able to produce mean values.
The vec_char and vec_factor are NOT able to produce mean values.

Now, let’s try to explicitly convert variables from one type to another.

``` r
  problem2_df|>
  mutate(
    vec_logical = as.numeric(vec_logical),
    vec_char = as.numeric(vec_char),
    vec_factor = as.numeric(vec_factor)
  )
```

    ## Warning: There was 1 warning in `mutate()`.
    ## ℹ In argument: `vec_char = as.numeric(vec_char)`.
    ## Caused by warning:
    ## ! NAs introduced by coercion

    ## # A tibble: 10 × 4
    ##    vec_numeric vec_logical vec_char vec_factor
    ##          <dbl>       <dbl>    <dbl>      <dbl>
    ##  1     -1.27             0       NA          3
    ##  2     -0.473            0       NA          2
    ##  3     -0.0848           0       NA          1
    ##  4      0.689            1       NA          3
    ##  5      0.140            1       NA          2
    ##  6      0.671            1       NA          1
    ##  7     -0.340            0       NA          3
    ##  8      0.813            1       NA          2
    ##  9      0.180            1       NA          1
    ## 10     -0.268            0       NA          3

When we applied the as.numeric function to our dataframe, we see that
all vectors except for the character vector are able to be converted to
numeric. This is because the factor variable was able to be successfully
converted as for factor variables they can recognize the characters by
their alphabetical order and rank them in that way. However the
character vector do not have any kind of factor they can be ranked by
and thus we see the NA output for vec_char.

``` r
   mean(pull(problem2_df, vec_logical))
```

    ## [1] 0.5

``` r
  mean(pull(problem2_df, vec_char))
```

    ## Warning in mean.default(pull(problem2_df, vec_char)): argument is not numeric
    ## or logical: returning NA

    ## [1] NA

``` r
  mean(pull(problem2_df, vec_factor))
```

    ## Warning in mean.default(pull(problem2_df, vec_factor)): argument is not numeric
    ## or logical: returning NA

    ## [1] NA

This somewhat helps explain what happens when we try to take the mean in
that we still are not able to calculate means for character and factor
variables and we receive NA errors.
