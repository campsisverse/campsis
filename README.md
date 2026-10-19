
# campsis <img src='man/figures/logo.png' align="right" alt="" width="120" />

<!-- badges: start -->

[![R-CMD-check](https://github.com/campsisverse/campsis/workflows/R-CMD-check/badge.svg)](https://github.com/campsisverse/campsis/actions)
[![Codecov test
coverage](https://codecov.io/gh/campsisverse/campsis/graph/badge.svg)](https://app.codecov.io/gh/campsisverse/campsis)
[![CRAN
version](http://www.r-pkg.org/badges/version/campsis)](https://cran.r-project.org/package=campsis)
[![CRAN total
downloads](https://cranlogs.r-pkg.org/badges/grand-total/campsis)](https://cran.r-project.org/package=campsis)
[![CRAN total
downloads](https://cranlogs.r-pkg.org/badges/campsis)](https://cran.r-project.org/package=campsis)
<!-- badges: end -->

## Requirements

- R package `campsismod` must be installed beforehand
- Simulation engine must be installed too (`rxode2` or `mrgsolve`)

## Installation

### From CRAN

Install the latest official release from CRAN:

``` r
install.packages("campsis")
```

### From GitHub

Install the latest development version from GitHub:

``` r
remotes::install_github("campsisverse/campsis")
```

## Basic example

Import the `campsis` package:

``` r
library(campsis)
```

Create your dataset:

``` r
ds <- Dataset(50) %>%
  add(Bolus(time = 0, amount = 1000, ii = 12, addl = 2)) %>%
  add(Observations(times = seq(0, 36, by = 0.5)))
```

Load your own model or use a built-in model from the library:

``` r
model <- model_suite$pk$`2cpt_fo`
```

Simulate your results with your preferred simulation engine (`rxode2` or
`mrgsolve`):

``` r
results <- simulate(model = model, dataset = ds, dest = "mrgsolve", seed = 1)
```

Plot your results:

``` r
shaded_plot(results, "CONC")
```

![](vignettes/resources/readme_plot.png)
