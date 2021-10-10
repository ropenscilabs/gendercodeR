
<!-- README.md is generated from README.Rmd. Please edit that file -->

# gendercoder

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/gendercoder)](https://CRAN.R-project.org/package=gendercoder)
[![Lifecycle:
stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)
[![Project Status: Active – The project has reached a stable, usable
state and is being actively
developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![R-CMD-check](https://github.com/ropenscilabs/gendercoder/workflows/R-CMD-check/badge.svg)](https://github.com/ropenscilabs/gendercoder/actions)
[![Codecov test
coverage](https://codecov.io/gh/ropenscilabs/gendercoder/branch/master/graph/badge.svg)](https://codecov.io/gh/ropenscilabs/gendercoder?branch=master)
<!-- badges: end -->

The goal of gendercoder is to allow simple re-coding of free-text gender
responses. This is intended to permit representation of gender
diversity, while managing troll-responses and the workload implications
of manual coding.

## Installation

This package is not on CRAN. To use this package please run the
following code:

``` r
devtools::install_github("ropenscilabs/gendercoder")
library(gendercoder)
```

## Basic use

The gendercoder package permits the efficient re-coding of free-text
gender responses within a tidyverse pipeline. It contains two built-in
English output dictionaries, a default `broad_en` dictionary which
corrects spelling and standardises terms while maintaining the diversity
of responses and a `narrow_en` dictionary which contains fewer gender
categories, “man”, “woman”, “boy”, “girl”, and “sex and gender diverse”.

The core function, `gender_recode()`, takes 3 arguments,

-   `gender` the vector of free-text gender,

-   `dictionary` the preferred dictionary, and

-   `retain_unmatched` a logical indicating whether original values
    should be carried over if there is no match.

Basic usage is demonstrated below.

``` r
library(gendercoder)

tibble(gender = c("male", "MALE", "mle", "I am male", "femail", "female", "enby")) %>% 
  mutate(broad_gender  = recode_gender(gender, dictionary = broad_en, retain_unmatched = TRUE),
         narrow_gender = recode_gender(gender, dictionary = narrow_en, retain_unmatched = FALSE)
  )
#> Results not matched from the dictionary have been filled with the user inputted values
#> # A tibble: 7 x 3
#>   gender    broad_gender narrow_gender         
#>   <chr>     <chr>        <chr>                 
#> 1 male      man          man                   
#> 2 MALE      man          man                   
#> 3 mle       man          man                   
#> 4 I am male I am male    <NA>                  
#> 5 femail    woman        woman                 
#> 6 female    woman        woman                 
#> 7 enby      non-binary   sex and gender diverse
```

## Contributing to this package

This package is a reflection of cultural context of the package
contributors; we welcome issues and pull requests to make the package
more inclusive and/or suitable for a broader range of cultural contexts.
We particularly welcome addition of non-English dictionaries or of other
gender-diverse responses to the broad and narrow dictionaries.

## Citation Information

Please cite this package as:

Jennifer Beaudry, Emily Kothe, Felix Singleton Thorn, Rhydwyn McGuire,
Nicholas Tierney and Mathew Ling (2020). gendercoder: Recodes Sex/Gender
Descriptions into a Standard Set. R package version 0.0.0.9000.
<https://github.com/ropenscilabs/gendercoder>

## Acknowledgement of Country

We acknowledge the Wurundjeri people of the Kulin Nation as the
custodians of the land on which this package was developed and pay
respects to elders past, present and future.
