Data Wrangling 101
================
Mr. Adams

Often your data frame won’t be perfectly clean, so you will have to make
slight changes to it to properly work with it to answer your research
questions. This document will detail commonly used functions for data
wrangling.

## Load Packages and Libraries

There are specific packages others have built that allow you to do
complex tasks with little effort. When you first use RStudio, be sure to
install the necessary packages. After you install the package(s), you
need to be sure to load the library for each of the packages that you
will use for your analysis.

For this class, we will use several different packages, but we will
start with the following package.

tidyverse: This contains, among other things, the packages ggplot, which
allows you to make visualizations and dplyr, which will enable you to
wrangle your data frame.

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.4     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Viewing Your Data

\#\#\#Before you begin analyzing your data, you need to familiarize
yourself with the data frame. Ask yourself: How many variables do I
have? What type of variables do I have? What are my observational units?

For this demo, we will use a data frame called “diamonds” that comes
with the Tidyverse package.

This code will allow you to see the variables and the first few
observations. The default is to show the first six observations. To
change the number of rows that appear, add a comma, and then the number
of rows you want to show up.

``` r
head(diamonds)
```

    ## # A tibble: 6 x 10
    ##   carat cut       color clarity depth table price     x     y     z
    ##   <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ## 1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
    ## 2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
    ## 3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
    ## 4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
    ## 5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
    ## 6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48

``` r
head(diamonds, 10)
```

    ## # A tibble: 10 x 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
    ##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
    ##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
    ##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
    ##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
    ##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
    ##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
    ##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
    ##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
    ## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39

``` r
diamonds
```

    ## # A tibble: 53,940 x 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
    ##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
    ##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
    ##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
    ##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
    ##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
    ##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
    ##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
    ##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
    ## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39
    ## # … with 53,930 more rows

## Using the Select Function

This function is particularly helpful when you have a lot of variables
in your dataset. If, for example, you had 50 variables, it would be hard
to focus on the few variables you want to analyze. The select function
allows you to create a new data frame that includes only the variables
you want.

The diamonds dataset has ten variables. Let’s make a new data frame that
only includes cut, clarity, carat, color, and the price.

``` r
fourcs_price <- diamonds %>%
                select(carat, cut, color, clarity, price)
head(fourcs_price)
```

    ## # A tibble: 6 x 5
    ##   carat cut       color clarity price
    ##   <dbl> <ord>     <ord> <ord>   <int>
    ## 1 0.23  Ideal     E     SI2       326
    ## 2 0.21  Premium   E     SI1       326
    ## 3 0.23  Good      E     VS1       327
    ## 4 0.290 Premium   I     VS2       334
    ## 5 0.31  Good      J     SI2       335
    ## 6 0.24  Very Good J     VVS2      336

### Questions to Answer/Action Item

#### 1\. Using the diamonds dataset, create a data frame with just 3 variables.

## Filter

Often you want to focus on a certain subset of your dataset. For
example, when analyzing the diamonds dataset, you may only want to study
a particular cut of diamond. The Filter function allows us to take out
just the subset of observations that we want. Here is an example of how
to do just that. This code can be read in plain English “Hey computer,
give me information on only the diamonds that have an Ideal cut. While
you are at it, name the new data frame, ‘Ideals.’”

``` r
ideals <- diamonds %>%
         filter(cut == "Ideal")
ideals
```

    ## # A tibble: 21,551 x 10
    ##    carat cut   color clarity depth table price     x     y     z
    ##    <dbl> <ord> <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  0.23 Ideal E     SI2      61.5    55   326  3.95  3.98  2.43
    ##  2  0.23 Ideal J     VS1      62.8    56   340  3.93  3.9   2.46
    ##  3  0.31 Ideal J     SI2      62.2    54   344  4.35  4.37  2.71
    ##  4  0.3  Ideal I     SI2      62      54   348  4.31  4.34  2.68
    ##  5  0.33 Ideal I     SI2      61.8    55   403  4.49  4.51  2.78
    ##  6  0.33 Ideal I     SI2      61.2    56   403  4.49  4.5   2.75
    ##  7  0.33 Ideal J     SI1      61.1    56   403  4.49  4.55  2.76
    ##  8  0.23 Ideal G     VS1      61.9    54   404  3.93  3.95  2.44
    ##  9  0.32 Ideal I     SI1      60.9    55   404  4.45  4.48  2.72
    ## 10  0.3  Ideal I     SI2      61      59   405  4.3   4.33  2.63
    ## # … with 21,541 more rows

You can also filter for a range of numbers. The filter below makes a
data frame, named below\_fiveK, that includes only diamonds less than
$5,000

### Question to Answer/Action Item

#### 1\. Filter the diamonds dataset in any way that you want.

#### 2\. Describe how you filtered the data.

## Mutate

You may also want to create new variables. Using the diamonds dataset,
we may wish to study the question, “What is the distribution of price
per carat?” (Carat is the units for measuring the size of a diamond.)
When looking at the diamonds data frame, you can see it does not include
price per carat. Therefore, we will use the mutate function to add it.

``` r
diamonds_with_ppc <- diamonds %>%
                      mutate(ppc = price/carat)
diamonds_with_ppc
```

    ## # A tibble: 53,940 x 11
    ##    carat cut       color clarity depth table price     x     y     z   ppc
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl> <dbl>
    ##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43 1417.
    ##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31 1552.
    ##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31 1422.
    ##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63 1152.
    ##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75 1081.
    ##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48 1400 
    ##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47 1400 
    ##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53 1296.
    ##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49 1532.
    ## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39 1470.
    ## # … with 53,930 more rows

### Question to Answer/Action Item

#### 1\. Use the mutate function to create another new variable in the the diamonds dataset.

## Group\_by

Let’s say you want to compare the prices of different color diamonds. In
doing so, you want to calculate the average price and standard deviation
of the price variable for each respective color. Therefore, you need to
put all the observations into groups of colors.

``` r
color_groups_sum_stats <- diamonds %>%
                group_by(color) %>%
                summarize(avg = mean(price), 
                          standard_deviation = sd(price))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
color_groups_sum_stats
```

    ## # A tibble: 7 x 3
    ##   color   avg standard_deviation
    ##   <ord> <dbl>              <dbl>
    ## 1 D     3170.              3357.
    ## 2 E     3077.              3344.
    ## 3 F     3725.              3785.
    ## 4 G     3999.              4051.
    ## 5 H     4487.              4216.
    ## 6 I     5092.              4722.
    ## 7 J     5324.              4438.

### Question to Answer/Action Item

#### 1\. Use the group\_by function to find the summary statistics for price across a different categorical variable.

#### 2\. Describe key insights about diamonds based on those summary stats.
