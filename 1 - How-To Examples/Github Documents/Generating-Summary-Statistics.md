Generating Summary Statistics
================
Mr. Adams

# Using R to Generate Statistics

R is an incredibly powerful tool to help you quickly and efficiently
make sense of a dataset. This document will show you how to generate
summary statistics and build tables.

## Load Tidyverse and Skimr

As always, we need to go to our tool shed to get out the toolboxes we’ll
need to start building\!

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

``` r
library(skimr)
library(ggridges)
```

## Summarizing Quantitative Data

When analyzing quantitative data, it’s important to examine the shape,
center, and spread of that distribution. Here are two ways you can do
that.

### Using the summarize function to generate summary statistics.

### Summarizing one variable

The summarize function is a great tool to use when you want to look at
summary statistics for one variable or when grouping variables by a
category. We will do both.

For this example, we will use the Diamonds dataset that contains “the
prices and other attributes of almost 54,000 diamonds.” This dataset is
part of the ggplot2 package which is one of the many included in the
tidyverse package you loaded above.

Let’s say you just made the following histogram showing the distribution
of price.

![](Generating-Summary-Statistics_files/figure-gfm/price%20density%20curve,%20-1.png)<!-- -->

To properly explain what this shows, you need to include summary
statistics. With nearly 54,000 rows, you won’t be doing this by hand\!
The code below will generate the summary statistics - mean, median,
standard deviation, and IQR for the price variable.

``` r
price_summary_stats <- diamonds %>%
                    summarize(avg = mean(price), 
                              med = median(price), 
                              standard_dev = sd(price), 
                              iqr = IQR(price))
price_summary_stats
```

    ## # A tibble: 1 x 4
    ##     avg   med standard_dev   iqr
    ##   <dbl> <dbl>        <dbl> <dbl>
    ## 1 3933.  2401        3989. 4374.

#### Questions to Answer

##### 1\. Describe the price of diamonds. In doing so, be sure to reference the statistics you just generated to help you specifically describe the center and spread.

##### 2\. Another quantitative variable in the dataset is carat. This refers to the size of the diamond. Write code in the space below to generate the summary statistics for the variable carat. \*\*hint: copy and paste is your friend.

### Using Group\_by and Summarize Functions to Expolore the Distributions Quantitative Data Across Different Groups

#### Question to Answer

##### 1\. After producing the summary statistics and visualization above, what is a follow-up question you could ask that would force us to take a deeper look at this dataset. Tip: If you type ?diamonds into a grey space, it will give you more information about each variable in the dataset.

Example answer for the question above: Does the color of a diamond
impact the price?

To answer this question, maybe you start by making a ridge plot.

``` r
diamonds %>%
  ggplot(aes(x = price, y = color, fill = color, color = color)) +
  geom_density_ridges(alpha = 0.5) +
  labs(x = "Price of the Diamond", y = "Color", title = "The Distribution of Diamond Prices by Color") +
  theme_minimal()
```

    ## Picking joint bandwidth of 535

![](Generating-Summary-Statistics_files/figure-gfm/price%20color%20ridge%20plot-1.png)<!-- -->

Now we need to get the summary statistics for each of these. We won’t
necessarily use all of them, but we need to get them so we can decide
what we will reference. To generate these statsitics, we will group the
diamonds by color and then take the summary statistics for price.

``` r
price_color_ss <- diamonds %>%
    group_by(color) %>%
    summarize(avg = mean(price), med = median(price), standard_dev = sd(price), 
                    iqr = IQR(price))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
price_color_ss
```

    ## # A tibble: 7 x 5
    ##   color   avg   med standard_dev   iqr
    ##   <ord> <dbl> <dbl>        <dbl> <dbl>
    ## 1 D     3170. 1838         3357. 3302.
    ## 2 E     3077. 1739         3344. 3121 
    ## 3 F     3725. 2344.        3785. 3886.
    ## 4 G     3999. 2242         4051. 5117 
    ## 5 H     4487. 3460         4216. 4996.
    ## 6 I     5092. 3730         4722. 6081.
    ## 7 J     5324. 4234         4438. 5834.

#### Questions to Answer

##### 1\. Using both the visualizationa and the summary statistics, write down two key insights shown by the imagines.

##### 2\. Now, let’s see if there is a relationship between color and carat. In the gray space below, create a ridge plot and generate the summary statisitcs for carat grouped by color. \*\*Hint: Again, copy and paste is your friend.

### Select and Skimr to explore multiple variables all at once.

Let’s say, when you look at a dataset, you are not quite sure exactly
where to start. A good strategy is to look at the summary statistics for
a few variables. By examing a few variables and making some initial
conclusions, you can ask further questions and dive deeper into your
analysis.

For this example, let’s use the diamonds dataset again, but let’s look
at the depth, carat, and price variables.

``` r
diamonds %>%
  select(carat, depth, price) %>%
  skim()
```

|                                                  |            |
| :----------------------------------------------- | :--------- |
| Name                                             | Piped data |
| Number of rows                                   | 53940      |
| Number of columns                                | 3          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| numeric                                          | 3          |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: numeric**

| skim\_variable | n\_missing | complete\_rate |    mean |      sd |    p0 |   p25 |    p50 |     p75 |     p100 | hist  |
| :------------- | ---------: | -------------: | ------: | ------: | ----: | ----: | -----: | ------: | -------: | :---- |
| carat          |          0 |              1 |    0.80 |    0.47 |   0.2 |   0.4 |    0.7 |    1.04 |     5.01 | ▇▂▁▁▁ |
| depth          |          0 |              1 |   61.75 |    1.43 |  43.0 |  61.0 |   61.8 |   62.50 |    79.00 | ▁▁▇▁▁ |
| price          |          0 |              1 | 3932.80 | 3989.44 | 326.0 | 950.0 | 2401.0 | 5324.25 | 18823.00 | ▇▂▁▁▁ |

#### Questions to Answer

##### 1\. What additional information did this code give you compared to the summarize function?

##### 2\. 25% of diamonds are larger than what size?

##### 3\. The middle 50% of diamonds have a price betwen what two dollar values?
