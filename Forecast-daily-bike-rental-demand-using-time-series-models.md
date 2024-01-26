Forecast daily bike rental demand using time series models
================
Natalia Miller
2024-01-24

# About Data Analysis Report

This RMarkdown file contains the report of the data analysis done for
the project on forecasting daily bike rental demand using time series
models in R. It contains analysis such as data exploration, summary
statistics and building the time series models. The final report was
completed on Wed Jan 24 22:06:03 2024.

**Data Description:**

This dataset contains the daily count of rental bike transactions
between years 2011 and 2012 in Capital bikeshare system with the
corresponding weather and seasonal information.

**Data Source:**
<https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset>

**Relevant Paper:**

Fanaee-T, Hadi, and Gama, Joao. Event labeling combining ensemble
detectors and background knowledge, Progress in Artificial Intelligence
(2013): pp. 1-15, Springer Berlin Heidelberg

# Task One: Load and explore the data

## Load data and install packages

``` r
install.packages("timetk")
```

    ## Installing package into '/usr/local/lib/R/site-library'
    ## (as 'lib' is unspecified)

``` r
install.packages("tidyverse")
```

    ## Installing package into '/usr/local/lib/R/site-library'
    ## (as 'lib' is unspecified)

``` r
install.packages("skimr")
```

    ## Installing package into '/usr/local/lib/R/site-library'
    ## (as 'lib' is unspecified)

``` r
library(timetk)
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.2     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.2     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(skimr)
data("bike_sharing_daily")
```

## Describe and explore the data

Is there a correlation between the normalized temperature and normalized
feeling temperature and the total count of bike rentals?

``` r
# Create a data frame with the temperatures and total count of rentals
correlation_df <- bike_sharing_daily %>% 
    select(temp, atemp, cnt)

cor(correlation_df)
```

    ##            temp     atemp       cnt
    ## temp  1.0000000 0.9917016 0.6274940
    ## atemp 0.9917016 1.0000000 0.6310657
    ## cnt   0.6274940 0.6310657 1.0000000

What are the mean and median temperatures for different seasons (Winter,
Fall, Summer, and Spring)?

``` r
# Create a data frame with the mean and median temperatures for each season
temperature_df <- bike_sharing_daily %>%
    summarize(avg_winter_temp = mean(temp [season == "1"], na.rm = T),
        avg_fall_temp = mean(temp[season == "4"], na.rm = T),
        avg_summer_temp = mean(temp[season == "3"], na.rm = T),
        avg_spring_temp = mean(temp[season == "2"], na.rm = T),
        median_winter_temp = median(temp[season == "1"], na.rm = T),
        median_fall_temp = median(temp[season == "4"], na.rm = T),
        median_summer_temp = median(temp[season == "3"], na.rm = T),
        median_spring_temp = median(temp[season == "2"], na.rm = T))
```

What are the mean temperature, humidity, wind speed, and total rentals
per month?

``` r
# Create a data frame with mean temperature, humidity, wind speed, 
# and total rentals per month 
monthly_averages <- bike_sharing_daily %>% 
    group_by(month = mnth) %>%
    summarize(avg_temp = mean(temp), avg_humidity = mean(hum),
        avg_wind_speed = mean(windspeed), total_rentals = sum(cnt))
```

# Task Two: Create interactive time series plots

``` r
## Read about the timetk package
# ?timetk
```

# Task Three: Smooth time series data

# Task Four: Decompose and assess the stationarity of time series data

# Task Five: Fit and forecast time series data using ARIMA models

# Task Six: Findings and Conclusions

● What did you learn throughout the process? ● Are the results what you
expected? ● What are the key findings and takeaways?
