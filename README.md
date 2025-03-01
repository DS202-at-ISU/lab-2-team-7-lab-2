
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

=======

``` r
library(classdata)
View(ames)

head(ames)
```

    ##    Parcel ID                       Address             Style
    ## 1 0903202160      1024 RIDGEWOOD AVE, AMES 1 1/2 Story Frame
    ## 2 0907428215 4503 TWAIN CIR UNIT 105, AMES     1 Story Frame
    ## 3 0909428070        2030 MCCARTHY RD, AMES     1 Story Frame
    ## 4 0923203160         3404 EMERALD DR, AMES     1 Story Frame
    ## 5 0520440010       4507 EVEREST  AVE, AMES              <NA>
    ## 6 0907275030       4512 HEMINGWAY DR, AMES     2 Story Frame
    ##                        Occupancy  Sale Date Sale Price Multi Sale YearBuilt
    ## 1 Single-Family / Owner Occupied 2022-08-12     181900       <NA>      1940
    ## 2                    Condominium 2022-08-04     127100       <NA>      2006
    ## 3 Single-Family / Owner Occupied 2022-08-15          0       <NA>      1951
    ## 4                      Townhouse 2022-08-09     245000       <NA>      1997
    ## 5                           <NA> 2022-08-03     449664       <NA>        NA
    ## 6 Single-Family / Owner Occupied 2022-08-16     368000       <NA>      1996
    ##   Acres TotalLivingArea (sf) Bedrooms FinishedBsmtArea (sf) LotArea(sf)  AC
    ## 1 0.109                 1030        2                    NA        4740 Yes
    ## 2 0.027                  771        1                    NA        1181 Yes
    ## 3 0.321                 1456        3                  1261       14000 Yes
    ## 4 0.103                 1289        4                   890        4500 Yes
    ## 5 0.287                   NA       NA                    NA       12493  No
    ## 6 0.494                 2223        4                    NA       21533 Yes
    ##   FirePlace              Neighborhood
    ## 1       Yes       (28) Res: Brookside
    ## 2        No    (55) Res: Dakota Ridge
    ## 3        No        (32) Res: Crawford
    ## 4        No        (31) Res: Mitchell
    ## 5        No (19) Res: North Ridge Hei
    ## 6       Yes   (37) Res: College Creek

``` r
str(ames)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    6935 obs. of  16 variables:
    ##  $ Parcel ID            : chr  "0903202160" "0907428215" "0909428070" "0923203160" ...
    ##  $ Address              : chr  "1024 RIDGEWOOD AVE, AMES" "4503 TWAIN CIR UNIT 105, AMES" "2030 MCCARTHY RD, AMES" "3404 EMERALD DR, AMES" ...
    ##  $ Style                : Factor w/ 12 levels "1 1/2 Story Brick",..: 2 5 5 5 NA 9 5 5 5 5 ...
    ##  $ Occupancy            : Factor w/ 5 levels "Condominium",..: 2 1 2 3 NA 2 2 1 2 2 ...
    ##  $ Sale Date            : Date, format: "2022-08-12" "2022-08-04" ...
    ##  $ Sale Price           : num  181900 127100 0 245000 449664 ...
    ##  $ Multi Sale           : chr  NA NA NA NA ...
    ##  $ YearBuilt            : num  1940 2006 1951 1997 NA ...
    ##  $ Acres                : num  0.109 0.027 0.321 0.103 0.287 0.494 0.172 0.023 0.285 0.172 ...
    ##  $ TotalLivingArea (sf) : num  1030 771 1456 1289 NA ...
    ##  $ Bedrooms             : num  2 1 3 4 NA 4 5 1 3 4 ...
    ##  $ FinishedBsmtArea (sf): num  NA NA 1261 890 NA ...
    ##  $ LotArea(sf)          : num  4740 1181 14000 4500 12493 ...
    ##  $ AC                   : chr  "Yes" "Yes" "Yes" "Yes" ...
    ##  $ FirePlace            : chr  "Yes" "No" "No" "No" ...
    ##  $ Neighborhood         : Factor w/ 42 levels "(0) None","(13) Apts: Campus",..: 15 40 19 18 6 24 14 40 13 23 ...

``` r
summary(ames)
```

    ##   Parcel ID           Address                        Style     
    ##  Length:6935        Length:6935        1 Story Frame    :3732  
    ##  Class :character   Class :character   2 Story Frame    :1456  
    ##  Mode  :character   Mode  :character   1 1/2 Story Frame: 711  
    ##                                        Split Level Frame: 215  
    ##                                        Split Foyer Frame: 156  
    ##                                        (Other)          : 218  
    ##                                        NA's             : 447  
    ##                           Occupancy      Sale Date            Sale Price      
    ##  Condominium                   : 711   Min.   :2017-07-03   Min.   :       0  
    ##  Single-Family / Owner Occupied:4711   1st Qu.:2019-03-27   1st Qu.:       0  
    ##  Townhouse                     : 745   Median :2020-09-22   Median :  170900  
    ##  Two-Family Conversion         : 139   Mean   :2020-06-14   Mean   : 1017479  
    ##  Two-Family Duplex             : 182   3rd Qu.:2021-10-14   3rd Qu.:  280000  
    ##  NA's                          : 447   Max.   :2022-08-31   Max.   :20500000  
    ##                                                                               
    ##   Multi Sale          YearBuilt        Acres         TotalLivingArea (sf)
    ##  Length:6935        Min.   :   0   Min.   : 0.0000   Min.   :   0        
    ##  Class :character   1st Qu.:1956   1st Qu.: 0.1502   1st Qu.:1095        
    ##  Mode  :character   Median :1978   Median : 0.2200   Median :1460        
    ##                     Mean   :1976   Mean   : 0.2631   Mean   :1507        
    ##                     3rd Qu.:2002   3rd Qu.: 0.2770   3rd Qu.:1792        
    ##                     Max.   :2022   Max.   :12.0120   Max.   :6007        
    ##                     NA's   :447    NA's   :89        NA's   :447         
    ##     Bedrooms      FinishedBsmtArea (sf)  LotArea(sf)          AC           
    ##  Min.   : 0.000   Min.   :  10.0        Min.   :     0   Length:6935       
    ##  1st Qu.: 3.000   1st Qu.: 474.0        1st Qu.:  6553   Class :character  
    ##  Median : 3.000   Median : 727.0        Median :  9575   Mode  :character  
    ##  Mean   : 3.299   Mean   : 776.7        Mean   : 11466                     
    ##  3rd Qu.: 4.000   3rd Qu.:1011.0        3rd Qu.: 12088                     
    ##  Max.   :10.000   Max.   :6496.0        Max.   :523228                     
    ##  NA's   :447      NA's   :2682          NA's   :89                         
    ##   FirePlace                            Neighborhood 
    ##  Length:6935        (27) Res: N Ames         : 854  
    ##  Class :character   (37) Res: College Creek  : 652  
    ##  Mode  :character   (57) Res: Investor Owned : 474  
    ##                     (29) Res: Old Town       : 469  
    ##                     (34) Res: Edwards        : 444  
    ##                     (19) Res: North Ridge Hei: 420  
    ##                     (Other)                  :3622

## Step 1 Results

Inspected the first few lines of the data set. The variables are Parcel
ID, Address, Style, Occupancy, Sale Date, Sale Price, Multi Sale,
YearBuilt, Acres, Total Living Area, Bedrooms, Finished Basement, Lot
Area, AC, Fireplace, and Neighborhood. The types of variables are
numerical, character, date, and factor/categorical.

**Parcel ID**

- Character variable that describes ID of sale

**Address**

- Character variable that states home address

**Style**

- Factor/Categorical variable that describes the style of the home

- Has 12 different categories

**Occupancy**

- Factor/Categorical variable that describes the home occupancy

- Has 5 different categories

**Sale Date**

- Date variable of the format “2022-08-12” that records the date of the
  sale

- Minimum of 2017-07-03 and maximum of 2022-08-31

**Sale Price**

- Numerical variable that records the price of the sale

- Ranges from 0 to 20500000

**Multi Sale**

- Character variable that indicates whether it was a multi sale or not

**YearBuilt**

- Numerical variable that records the year the home was built

- Ranges from 0 (but in reality, 1880) to 2022

**Acres**

- Numerical variable that records the number of acres the home is

- Ranges from 0 to 12.012

**TotalLivingArea (sf)**

- Numerical variable that records the square feet of the living area

- Ranges from 0 to 6007

**Bedrooms**

- Numerical variable indicating the number of bedrooms in the home

- Ranges from 0 to 10

**FinishedBsmtArea (sf)**

- Numerical variable that states the area of finished basement in square
  feet

- Ranges from 10 to 6496

**LotArea (sf)**

- Numerical variable that states the lot area

- Ranges from 0 to 523228

**AC**

- Character variable that indicates if the home has air conditioning or
  not

**Fireplace**

- Character variable that indicates if the home has a fireplace or not

**Neighborhood**

- Factor/categorical variable that state the neighboorhood of the home

- 42 categories

## Step 2 Results

**Sale Price** is the variable that we decided was the variable of
interest. There are quite a few *\$0* values meaning that they were
“sold” for *\$0*. We are assuming that meant that there was no sale
price for them in the data and instead of *NA* the values assigned was
*\$0*.

## Step 3 Results

The following code creates the histogram for Sale Price. I have log
transformed it to show the distribution more accurately.

``` r
data <- classdata::ames
library(ggplot2)
ggplot(data, aes(x = log(`Sale Price`))) +
  geom_histogram(binwidth = 0.1, fill = "steelblue", color = "black") +
  labs(title = "Histogram of Log(Sale Price)",
       x = "Log(Sale Price)",
       y = "Count") +
  theme_minimal()
```

    ## Warning: Removed 2206 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

The following code creates the histogram for Sale Price.

``` r
ggplot(data, aes(x = `Sale Price`)) +
  geom_histogram(binwidth = 10000, fill = "steelblue", color = "black") +
  labs(title = "Histogram of Sale Price",
       x = "Sale Price",
       y = "Count") +
  theme_minimal()
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

The followoing code returns the range of the Sale Price Variable.

``` r
range_sale_price <- range(data$`Sale Price`, na.rm = TRUE)
range_sale_price
```

    ## [1]        0 20500000

Points of interest: There seem to be sale prices of \$0 which does not
make sense. It is likely that these 0’s represent data that that does
not have any value for sale price but is not listed as NA. I believe it
is best to remove such observations.

## Step 4 Results

**Grace’s Work:** Variable used: TotalLivingArea (sf)

``` r
summary(ames)
```

    ##   Parcel ID           Address                        Style     
    ##  Length:6935        Length:6935        1 Story Frame    :3732  
    ##  Class :character   Class :character   2 Story Frame    :1456  
    ##  Mode  :character   Mode  :character   1 1/2 Story Frame: 711  
    ##                                        Split Level Frame: 215  
    ##                                        Split Foyer Frame: 156  
    ##                                        (Other)          : 218  
    ##                                        NA's             : 447  
    ##                           Occupancy      Sale Date            Sale Price      
    ##  Condominium                   : 711   Min.   :2017-07-03   Min.   :       0  
    ##  Single-Family / Owner Occupied:4711   1st Qu.:2019-03-27   1st Qu.:       0  
    ##  Townhouse                     : 745   Median :2020-09-22   Median :  170900  
    ##  Two-Family Conversion         : 139   Mean   :2020-06-14   Mean   : 1017479  
    ##  Two-Family Duplex             : 182   3rd Qu.:2021-10-14   3rd Qu.:  280000  
    ##  NA's                          : 447   Max.   :2022-08-31   Max.   :20500000  
    ##                                                                               
    ##   Multi Sale          YearBuilt        Acres         TotalLivingArea (sf)
    ##  Length:6935        Min.   :   0   Min.   : 0.0000   Min.   :   0        
    ##  Class :character   1st Qu.:1956   1st Qu.: 0.1502   1st Qu.:1095        
    ##  Mode  :character   Median :1978   Median : 0.2200   Median :1460        
    ##                     Mean   :1976   Mean   : 0.2631   Mean   :1507        
    ##                     3rd Qu.:2002   3rd Qu.: 0.2770   3rd Qu.:1792        
    ##                     Max.   :2022   Max.   :12.0120   Max.   :6007        
    ##                     NA's   :447    NA's   :89        NA's   :447         
    ##     Bedrooms      FinishedBsmtArea (sf)  LotArea(sf)          AC           
    ##  Min.   : 0.000   Min.   :  10.0        Min.   :     0   Length:6935       
    ##  1st Qu.: 3.000   1st Qu.: 474.0        1st Qu.:  6553   Class :character  
    ##  Median : 3.000   Median : 727.0        Median :  9575   Mode  :character  
    ##  Mean   : 3.299   Mean   : 776.7        Mean   : 11466                     
    ##  3rd Qu.: 4.000   3rd Qu.:1011.0        3rd Qu.: 12088                     
    ##  Max.   :10.000   Max.   :6496.0        Max.   :523228                     
    ##  NA's   :447      NA's   :2682          NA's   :89                         
    ##   FirePlace                            Neighborhood 
    ##  Length:6935        (27) Res: N Ames         : 854  
    ##  Class :character   (37) Res: College Creek  : 652  
    ##  Mode  :character   (57) Res: Investor Owned : 474  
    ##                     (29) Res: Old Town       : 469  
    ##                     (34) Res: Edwards        : 444  
    ##                     (19) Res: North Ridge Hei: 420  
    ##                     (Other)                  :3622

The range of TotalLivingArea is 6007 (ranges from 0 to 6007).

``` r
library(ggplot2)
ggplot(data = ames, mapping = aes(x = `TotalLivingArea (sf)`)) + geom_histogram(binwidth = 10)
```

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggplot(data = ames, mapping = aes(x = `TotalLivingArea (sf)`, y = `Sale Price`)) + geom_point()
```

    ## Warning: Removed 447 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
ggplot(data = ames, mapping = aes(x = log(`TotalLivingArea (sf)`), y = log(`Sale Price`))) + geom_point()
```

    ## Warning: Removed 447 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-6-3.png)<!-- -->

As TotalLivingArea increases, Sale Price also increases, indicating that
sale price and total living area have a positive correlation. The two
variables do not have a very strong correlation however, as the data
points are scattered. There are some outliers; homes with a
significantly higher sale price than the others. However, those homes
with much higher sale prices don’t have a notably high total living
area. There are also some homes that have a sale price of \$0, which are
likely homes that don’t have a listed sale price. There are also a
couple homes that have a significantly higher total living area than
others.

**Akshat’s Work**: Variable Used: Bedrooms

The following Code is the code that returns the range of the feature
bedroom:

``` r
range_bedrooms <- range(data$Bedrooms, na.rm = TRUE)
range_bedrooms
```

    ## [1]  0 10

The following code creates a bar chart of the bedroom variable.

``` r
ggplot(data, aes(x = Bedrooms)) +
  geom_bar(fill = "steelblue", color = "black") +
  labs(title = "Distribution of Bedrooms",
       x = "Number of Bedrooms",
       y = "Count") +
  theme_minimal()
```

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_count()`).

![](README_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

The following code creates a scatterplot of the variables Sale Price and
Bedroom. I also went ahead and added a regression line.

``` r
ggplot(data = data,
       aes(x = `Bedrooms`, y = `Sale Price`)) +
       geom_point() +
       stat_smooth() +
       labs(title = 'Bedrooms vs. Sale Price',
            x = "Number of Bedrooms",
            y = "Sale Price in USD")
```

    ## `geom_smooth()` using method = 'gam' and formula = 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 447 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

The discrete variable of bedrooms shows that it is not correlated with
Sale Price as there is no obvious pattern that shows that my hypothesis
that more bedrooms would be correlated with a higher sale price.

Oddities: There are some houses with a sale price of \$0 as mentioned
earlier. We would need to filter the data and remove such observations
to have a better understanding of how bedrooms and sale price are
correlated.

**Harsh’s work** Variable used: LotArea(sf)

``` r
library(ggplot2)
ggplot(data = ames, mapping = aes(x = `LotArea(sf)`)) + 
  geom_histogram(binwidth = 5000, fill = "steelblue", color = "black") + 
  labs(title = "Distribution of Lot Area",
       x = "Lot Area",
       y = "Count") + 
  theme_minimal()
```

    ## Warning: Removed 89 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](README_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
ggplot(data = ames, mapping = aes(x = `LotArea(sf)`, y = `Sale Price`)) + 
  geom_point() + 
  labs(title = "Lot Area vs Price",
       x = "Lot Area",
       y = "Price") + 
  theme_minimal()
```

    ## Warning: Removed 89 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-10-2.png)<!-- -->

``` r
ggplot(data = ames, mapping = aes(x = log(`LotArea(sf)`), y = log(`Sale Price`))) + 
  geom_point() + 
  labs(title = "log(Lot Area) vs lot(Price)",
       x = "log(Lot Area)",
       y = "lof(price)") + 
  theme_minimal()
```

    ## Warning: Removed 89 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-10-3.png)<!-- -->

As Lot Area increases, Sale Price also increases, indicating that sale
price and Lot Area have a positive correlation. The two variables do not
have a very strong correlation as there are some clusters and a decent
spread of the points.

There are some outliers; homes with a significantly higher sale price
than the others. Some homes have a much higher sale price and don’t have
a high Lot Area. There are some homes that have a sale price of \$0,
which are most probably homes that don’t have a listed sale price. There
are also a few homes that have a significantly higher Lot Area than
others, but dont have a much change in sale price.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.
