Homework 02: Explore Gapminder and use dplyr
================
Stephen Chignell
September 24, 2018

Overview
--------

The following exercise explores the **gapminder** dataset using a number of tools in R. Below is a list of some helpful resources to refer to throughout this exercise (and in the future!):

-   [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
-   [R Markdown Cheat Sheet](https://www.rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf)
-   [Dplyr Cheat Sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)
-   [Useful Dplyr Functions](https://www.r-bloggers.com/useful-dplyr-functions-wexamples/)
-   [ggplot2 Cheat Sheet](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)
-   [R Language Definition](https://stat.ethz.ch/R-manual/R-devel/doc/manual/R-lang.html#Objects)
-   [Tibbles](https://blog.rstudio.com/2016/03/24/tibble-1-0-0)

Preparation
-----------

### Load "tidyverse"

Note: The tidyverse package includes the dplyr package!

``` r
#install.packages("tidyverse")
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts ------------------------------------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

### Load the data

``` r
library(gapminder)
```

### Get familiar

It's always a good idea to check the data, to make sure it's loading correctly and is what you think it is.

The `head` function is a great way to do this. It returns the first 6 rows by default, or you can specify a number. Let's look at the first 10 rows:

``` r
head(gapminder, 10)
```

    ## # A tibble: 10 x 6
    ##    country     continent  year lifeExp      pop gdpPercap
    ##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Afghanistan Asia       1952    28.8  8425333      779.
    ##  2 Afghanistan Asia       1957    30.3  9240934      821.
    ##  3 Afghanistan Asia       1962    32.0 10267083      853.
    ##  4 Afghanistan Asia       1967    34.0 11537966      836.
    ##  5 Afghanistan Asia       1972    36.1 13079460      740.
    ##  6 Afghanistan Asia       1977    38.4 14880372      786.
    ##  7 Afghanistan Asia       1982    39.9 12881816      978.
    ##  8 Afghanistan Asia       1987    40.8 13867957      852.
    ##  9 Afghanistan Asia       1992    41.7 16317921      649.
    ## 10 Afghanistan Asia       1997    41.8 22227415      635.

The `tail` function is the same, but starts from the bottom of the dataset:

``` r
tail(gapminder, 10)
```

    ## # A tibble: 10 x 6
    ##    country  continent  year lifeExp      pop gdpPercap
    ##    <fct>    <fct>     <int>   <dbl>    <int>     <dbl>
    ##  1 Zimbabwe Africa     1962    52.4  4277736      527.
    ##  2 Zimbabwe Africa     1967    54.0  4995432      570.
    ##  3 Zimbabwe Africa     1972    55.6  5861135      799.
    ##  4 Zimbabwe Africa     1977    57.7  6642107      686.
    ##  5 Zimbabwe Africa     1982    60.4  7636524      789.
    ##  6 Zimbabwe Africa     1987    62.4  9216418      706.
    ##  7 Zimbabwe Africa     1992    60.4 10704340      693.
    ##  8 Zimbabwe Africa     1997    46.8 11404948      792.
    ##  9 Zimbabwe Africa     2002    40.0 11926563      672.
    ## 10 Zimbabwe Africa     2007    43.5 12311143      470.

Take a closer look
------------------

Let's dig deeper into `gapminder`.

#### 1. What type of object is it?

``` r
typeof(gapminder) 
```

    ## [1] "list"

#### 2. What is its class?

``` r
class(gapminder)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

#### 3. How many columns/variables?

``` r
ncol(gapminder)
```

    ## [1] 6

#### 4. How many rows/observations?

``` r
nrow(gapminder)
```

    ## [1] 1704

### An easier way?

We could also use `str` function to answer many of the previous questions:

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

`str` also includes variable names, types, and examples of the data contents. This approach might be good as an initial check, but could also be overwhelming if you were only interested in knowing one aspect of the data.

R Markdown
----------

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

``` r
#Summarize the cars dataset
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

Including Plots
---------------

You can also embed plots, for example:

![](hw02-schignel_files/figure-markdown_github/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
