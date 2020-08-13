# Data Wrangling with dplyr




In this chapter, you will be learn about how to use functionality from the **dplyr** package to wrangle your data. Data wrangling is the catchall phrase that includes the processes of cleaning, structuring, and summarizing your data. It is a skill that every educational scientist needs to have in their computational toolkit! 

We will use the [riverview.csv](https://raw.githubusercontent.com/zief0002/modeling/master/data/riverview.csv) data to illustrate several data wrangling ideas. The data contain five attributes collected from a random sample of $n=32$ employees working for the city of Riverview, a hypothetical midwestern city (see the [data codebook](http://zief0002.github.io/epsy-8251/codebooks/riverview.html)). To begin, we will load several libraries and import the data into an object called `city`.


```r
# Load libraries
library(dplyr)
library(readr)

# Read in data
city = read_csv(file = "https://raw.githubusercontent.com/zief0002/modeling/master/data/riverview.csv")
head(city)
```

```
# A tibble: 6 x 6
  education income seniority gender  male party      
      <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
1         8   37.4         7 male       1 Democrat   
2         8   26.4         9 female     0 Independent
3        10   47.0        14 male       1 Democrat   
4        10   34.2        16 female     0 Independent
5        10   25.5         1 female     0 Republican 
6        12   46.5        11 female     0 Democrat   
```

<br /><br />


## Piping: The Key to Using dplyr

Recall that functions work by taking arguments as inputs and then producing an output. For example, the `summary()` function takes the `city` data frame as its input.


```r
summary(city)
```

```
   education      income        seniority        gender         
 Min.   : 8   Min.   :25.48   Min.   : 1.00   Length:32         
 1st Qu.:12   1st Qu.:44.51   1st Qu.: 9.75   Class :character  
 Median :16   Median :55.83   Median :15.00   Mode  :character  
 Mean   :16   Mean   :53.74   Mean   :14.81                     
 3rd Qu.:20   3rd Qu.:62.72   3rd Qu.:20.25                     
 Max.   :24   Max.   :82.73   Max.   :27.00                     
      male           party          
 Min.   :0.0000   Length:32         
 1st Qu.:0.0000   Class :character  
 Median :0.0000   Mode  :character  
 Mean   :0.4375                     
 3rd Qu.:1.0000                     
 Max.   :1.0000                     
```

We could get the same result by using the piping operator (`%>%`). This operator takes a DATA FRAME (given immediately before the operator) and uses it as the FIRST argument in the function that comes immediately after the operator.



```r
# The pipe operator makes city the first argument of the summary function
city %>% summary()
```

```
   education      income        seniority        gender         
 Min.   : 8   Min.   :25.48   Min.   : 1.00   Length:32         
 1st Qu.:12   1st Qu.:44.51   1st Qu.: 9.75   Class :character  
 Median :16   Median :55.83   Median :15.00   Mode  :character  
 Mean   :16   Mean   :53.74   Mean   :14.81                     
 3rd Qu.:20   3rd Qu.:62.72   3rd Qu.:20.25                     
 Max.   :24   Max.   :82.73   Max.   :27.00                     
      male           party          
 Min.   :0.0000   Length:32         
 1st Qu.:0.0000   Class :character  
 Median :0.0000   Mode  :character  
 Mean   :0.4375                     
 3rd Qu.:1.0000                     
 Max.   :1.0000                     
```

Note since the `summary()` function did NOT include any additional arguments, we do not include anything between the parentheses after we pipe. Here is another example that illustrate the use of the pipe operator.


```r
# Count number of rows in city data frame
nrow(city)
```

```
[1] 32
```

```r
# Can be written using the pipe operator as...
city %>% nrow()
```

```
[1] 32
```

The `filter()` function from the **dplyr** package is used to select certain rows from a data frame. For example, the syntax below selects all rows from the `city` data frame that have a `gender` value of `female`. To do this we provide a logical statement as the second argument to the `filter()` function.


```r
# Select the rows from city that have a gender value of "female" 
filter(city, gender == "female")
```

```
# A tibble: 18 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1         8   26.4         9 female     0 Independent
 2        10   34.2        16 female     0 Independent
 3        10   25.5         1 female     0 Republican 
 4        12   46.5        11 female     0 Democrat   
 5        12   52.5        16 female     0 Independent
 6        14   32.6         5 female     0 Independent
 7        15   37.3         8 female     0 Democrat   
 8        16   38.6        11 female     0 Independent
 9        16   55.9        22 female     0 Independent
10        16   59.5        20 female     0 Independent
11        17   60.1        10 female     0 Independent
12        18   54.8        20 female     0 Republican 
13        18   62.5        16 female     0 Republican 
14        19   56.0        21 female     0 Independent
15        20   56.3        22 female     0 Independent
16        20   54.7        12 female     0 Independent
17        21   71.2        26 female     0 Democrat   
18        22   56.3         8 female     0 Independent
```

```r
# Can be written using the pipe operator as...
city %>% filter(gender == "female")
```

```
# A tibble: 18 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1         8   26.4         9 female     0 Independent
 2        10   34.2        16 female     0 Independent
 3        10   25.5         1 female     0 Republican 
 4        12   46.5        11 female     0 Democrat   
 5        12   52.5        16 female     0 Independent
 6        14   32.6         5 female     0 Independent
 7        15   37.3         8 female     0 Democrat   
 8        16   38.6        11 female     0 Independent
 9        16   55.9        22 female     0 Independent
10        16   59.5        20 female     0 Independent
11        17   60.1        10 female     0 Independent
12        18   54.8        20 female     0 Republican 
13        18   62.5        16 female     0 Republican 
14        19   56.0        21 female     0 Independent
15        20   56.3        22 female     0 Independent
16        20   54.7        12 female     0 Independent
17        21   71.2        26 female     0 Democrat   
18        22   56.3         8 female     0 Independent
```

Here, since the `filter()` function included a second argument, we include that argument in the function that the data frame is piped into. What is piped into the function, in this case `city`, will be automatically inputted into the FIRST argument.


<br /><br />


## Common dplyr Functions for Data Wrangling

Here are some common operations that researchers use to prepare data for analysis (i.e., data preparation, data wrangling, data cleaning) and the corresponding **dplyr** functions.

<table style="width:60%; margin-left: auto; margin-right: auto;" class="table">
<caption>(\#tab:unnamed-chunk-7)Common data wrangling activities and the corresponding **dplyr** function.</caption>
 <thead>
  <tr>
   <th style="text-align:left;text-align: center;"> Data wrangling activity </th>
   <th style="text-align:left;text-align: center;"> dplyr function </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Select a subset of rows from a data frame. </td>
   <td style="text-align:left;"> `filter()` </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Select a subset of columns from a data frame. </td>
   <td style="text-align:left;"> `select()` </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Add new columns to a data frame. </td>
   <td style="text-align:left;"> `mutate()` </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Sort and re-order data in a data frame. </td>
   <td style="text-align:left;"> `arrange()` </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Compute summaries of columns in a data frame. </td>
   <td style="text-align:left;"> `summarize()` </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Group the data to carry out computations for each group. </td>
   <td style="text-align:left;"> `group_by()` </td>
  </tr>
</tbody>
</table>

<br /><br />


## Select a Subset of Rows: Filtering

To select a subset of rows, we will pipe the data frame we want to select rows from into the `filter()` function. The argument(s) for this function are logical expressions that will be used to select the rows. 


```r
# Select the female employees
city %>% 
  filter(gender == "female")
```

```
# A tibble: 18 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1         8   26.4         9 female     0 Independent
 2        10   34.2        16 female     0 Independent
 3        10   25.5         1 female     0 Republican 
 4        12   46.5        11 female     0 Democrat   
 5        12   52.5        16 female     0 Independent
 6        14   32.6         5 female     0 Independent
 7        15   37.3         8 female     0 Democrat   
 8        16   38.6        11 female     0 Independent
 9        16   55.9        22 female     0 Independent
10        16   59.5        20 female     0 Independent
11        17   60.1        10 female     0 Independent
12        18   54.8        20 female     0 Republican 
13        18   62.5        16 female     0 Republican 
14        19   56.0        21 female     0 Independent
15        20   56.3        22 female     0 Independent
16        20   54.7        12 female     0 Independent
17        21   71.2        26 female     0 Democrat   
18        22   56.3         8 female     0 Independent
```

Here we are selecting only the rows where the gender variable is equal to (`==`) the character string "female". Recall that a single equals sign (`=`) is the assignment operator and that to say "is equal to", we need to use two equals signs (`==`).

:::protip
It is a good coding practice to use multiple lines when you are piping rather than putting all the syntax on a single line. When you do this, the pipe operator (`%>%`) needs to come at the end of the line. For example, in the code above, the pip operator is at the end of the first line of syntax rather than at the beginning of the second line of syntax. Include a line break after every pipe operator you use. 
:::

Note that the output from this computation (the rows of female employees) is only printed to the screen. If you want to keep the filtered data or operate on it further, you need to assign the output into an object.


```r
# Filter the female employees
female_employees = city %>% 
  filter(gender == "female")

# Count the number of rows (females)
nrow(female_employees)
```

```
[1] 18
```

We could have found the same result exclusively using piping; without the interim assignment.


```r
city %>% 
  filter(gender == "female") %>%
  nrow()
```

```
[1] 18
```

The first pipe operator uses the `city` data frame in the `filter()` function to select the female employees. This output (only the female employees) is then used in the `nrow()` function to count the number of rows. At is akin to a constant pipeline of chaining functions together; the output of a computation is used as the input into the next computation in the pipeline.

Here we use `filter()` to select the employees that have less than a high school level of education and then summarize all of the columns using the `summary()` function.


```r
city %>% 
  filter(education < 12) %>%
  summary()
```

```
   education        income        seniority       gender               male    
 Min.   : 8.0   Min.   :25.48   Min.   : 1.0   Length:5           Min.   :0.0  
 1st Qu.: 8.0   1st Qu.:26.43   1st Qu.: 7.0   Class :character   1st Qu.:0.0  
 Median :10.0   Median :34.18   Median : 9.0   Mode  :character   Median :0.0  
 Mean   : 9.2   Mean   :34.11   Mean   : 9.4                      Mean   :0.4  
 3rd Qu.:10.0   3rd Qu.:37.45   3rd Qu.:14.0                      3rd Qu.:1.0  
 Max.   :10.0   Max.   :47.03   Max.   :16.0                      Max.   :1.0  
    party          
 Length:5          
 Class :character  
 Mode  :character  
                   
                   
                   
```

<br /><br />


### Filtering on Multiple Attributes

You can filter on multiple attributes by including more than one logical statement in the `filter()` function. For example, the syntax below counts the number of female employees with less than a high school level of education.


```r
city %>% 
  filter(gender == "female", education < 12) %>%
  nrow()
```

```
[1] 3
```

Here, when we included multiple logical expressions in the `filter()` function, separated by a comma, they were linked using the AND (`&`) operator. This means that both expressions have to evaluate as `TRUE` to be included. We could also have explicitly used the `&` operator to link the two statements.


```r
city %>% 
  filter(gender == "female", education < 12)

# Is equivalent to...
city %>% 
  filter(gender == "female" & education < 12)
```

We can also `filter()` using the OR (`|`) operator. This means that if EITHER expression evaluates as TRUE it is included.


```r
city %>% 
  filter(gender == "female" | education < 12)
```

```
# A tibble: 20 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1         8   37.4         7 male       1 Democrat   
 2         8   26.4         9 female     0 Independent
 3        10   47.0        14 male       1 Democrat   
 4        10   34.2        16 female     0 Independent
 5        10   25.5         1 female     0 Republican 
 6        12   46.5        11 female     0 Democrat   
 7        12   52.5        16 female     0 Independent
 8        14   32.6         5 female     0 Independent
 9        15   37.3         8 female     0 Democrat   
10        16   38.6        11 female     0 Independent
11        16   55.9        22 female     0 Independent
12        16   59.5        20 female     0 Independent
13        17   60.1        10 female     0 Independent
14        18   54.8        20 female     0 Republican 
15        18   62.5        16 female     0 Republican 
16        19   56.0        21 female     0 Independent
17        20   56.3        22 female     0 Independent
18        20   54.7        12 female     0 Independent
19        21   71.2        26 female     0 Democrat   
20        22   56.3         8 female     0 Independent
```

This syntax would select any employee that is either female OR has an education less than 12 years.

<br /><br />


## Selecting a Subset and Renaming Columns

To select a subset of columns, we will use the `select()` function. The argument(s) for this function are the column names of the data frame that you want to select. For example, to select the `education`, `income`, and `gender` columns from the `city` data frame we would use the following syntax:


```r
city %>% 
  select(education, income, gender)
```

```
# A tibble: 32 x 3
   education income gender
       <dbl>  <dbl> <chr> 
 1         8   37.4 male  
 2         8   26.4 female
 3        10   47.0 male  
 4        10   34.2 female
 5        10   25.5 female
 6        12   46.5 female
 7        12   37.7 male  
 8        12   50.3 male  
 9        12   52.5 female
10        14   32.6 female
# … with 22 more rows
```

There are a number of helper functions you can use within the `select()` function. For example, `starts_with()`, `ends_with()`, and `contains()`. These let you quickly match larger blocks of columns that meet some criterion. The syntax below selects all the columns that have a column name that ends in 'e'.



```r
city %>% 
  select(ends_with("e"))
```

```
# A tibble: 32 x 2
   income  male
    <dbl> <dbl>
 1   37.4     1
 2   26.4     0
 3   47.0     1
 4   34.2     0
 5   25.5     0
 6   46.5     0
 7   37.7     1
 8   50.3     1
 9   52.5     0
10   32.6     0
# … with 22 more rows
```


<br /><br />


### Renaming Columns

You can rename a column by using the `rename()` function. Here we select the `education`, `income`, and `gender` columns from the `city` data frame and then rename the `education` column to `educ`. Note that this works similar to assignment in that the new column name is to the left of the equal sign.


```r
city %>% 
  select(education, income, gender) %>%
  rename(educ = education)
```

```
# A tibble: 32 x 3
    educ income gender
   <dbl>  <dbl> <chr> 
 1     8   37.4 male  
 2     8   26.4 female
 3    10   47.0 male  
 4    10   34.2 female
 5    10   25.5 female
 6    12   46.5 female
 7    12   37.7 male  
 8    12   50.3 male  
 9    12   52.5 female
10    14   32.6 female
# … with 22 more rows
```

<br /><br />


## Create New Columns: Mutating

To create new columns, we will use the `mutate()` function. Here we create a new column called `income2` based on multiplying the original `income` column by 1000.


```r
city %>% 
  mutate(
    income2 = income * 1000
    )
```

```
# A tibble: 32 x 7
   education income seniority gender  male party       income2
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>         <dbl>
 1         8   37.4         7 male       1 Democrat      37449
 2         8   26.4         9 female     0 Independent   26430
 3        10   47.0        14 male       1 Democrat      47034
 4        10   34.2        16 female     0 Independent   34182
 5        10   25.5         1 female     0 Republican    25479
 6        12   46.5        11 female     0 Democrat      46488
 7        12   37.7        14 male       1 Democrat      37656
 8        12   50.3        24 male       1 Democrat      50265
 9        12   52.5        16 female     0 Independent   52480
10        14   32.6         5 female     0 Independent   32631
# … with 22 more rows
```

Depending on your print options, the results in `income2` may be in scientific notation. For example `3.74e+04` is equivalent to $3.74 \times 10^4=37400$.

:::protip
You can "turn off" scientific notation by running the following syntax in your R session:


```r
options(scipen = 99)
```

You will need to run this syntax every R session.
:::


You can create multiple new columns within the same `mutate()` function. Simply include each new column as an argument. Below we again create `income2`, but we also additionally create `cent_educ` which computes the difference between each employee's education level and the mean education level.


```r
city %>% 
  mutate(
    income2 = income * 1000,
    cent_educ = education - mean(education)
    )
```

```
# A tibble: 32 x 8
   education income seniority gender  male party       income2 cent_educ
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>         <dbl>     <dbl>
 1         8   37.4         7 male       1 Democrat      37449        -8
 2         8   26.4         9 female     0 Independent   26430        -8
 3        10   47.0        14 male       1 Democrat      47034        -6
 4        10   34.2        16 female     0 Independent   34182        -6
 5        10   25.5         1 female     0 Republican    25479        -6
 6        12   46.5        11 female     0 Democrat      46488        -4
 7        12   37.7        14 male       1 Democrat      37656        -4
 8        12   50.3        24 male       1 Democrat      50265        -4
 9        12   52.5        16 female     0 Independent   52480        -4
10        14   32.6         5 female     0 Independent   32631        -2
# … with 22 more rows
```

<br /><br />


## Sorting the Data: Arranging

The `arrange()` function sorts the data based on the values within one or more specified columns. The data is ordered based on the column name provided in the argument(s). The syntax below sorts the rows in the `city` data frame from smallest to largest income.


```r
city %>% 
  arrange(income)
```

```
# A tibble: 32 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1        10   25.5         1 female     0 Republican 
 2         8   26.4         9 female     0 Independent
 3        14   32.6         5 female     0 Independent
 4        10   34.2        16 female     0 Independent
 5        15   37.3         8 female     0 Democrat   
 6         8   37.4         7 male       1 Democrat   
 7        12   37.7        14 male       1 Democrat   
 8        16   38.6        11 female     0 Independent
 9        12   46.5        11 female     0 Democrat   
10        10   47.0        14 male       1 Democrat   
# … with 22 more rows
```

Providing the `arrange()` function multiple arguments sort initially by the column name given in first argument, and then by the columns given in subsequent arguments. Here the data are sorted first by gender (alphabetically since `gender` is a character string) and then by income (lowest to highest).


```r
city %>% 
  arrange(gender, income)
```

```
# A tibble: 32 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1        10   25.5         1 female     0 Republican 
 2         8   26.4         9 female     0 Independent
 3        14   32.6         5 female     0 Independent
 4        10   34.2        16 female     0 Independent
 5        15   37.3         8 female     0 Democrat   
 6        16   38.6        11 female     0 Independent
 7        12   46.5        11 female     0 Democrat   
 8        12   52.5        16 female     0 Independent
 9        20   54.7        12 female     0 Independent
10        18   54.8        20 female     0 Republican 
# … with 22 more rows
```

Use the `desc()` function on a column name to sort the data in descending order. Here the data are sorted first by gender (alphabetically since `gender` is a character string) and then by income. Here the data are sorted first by gender (alphabetically) and then by income (highest to lowest).


```r
city %>% 
  arrange(gender, desc(income))
```

```
# A tibble: 32 x 6
   education income seniority gender  male party      
       <dbl>  <dbl>     <dbl> <chr>  <dbl> <chr>      
 1        21   71.2        26 female     0 Democrat   
 2        18   62.5        16 female     0 Republican 
 3        17   60.1        10 female     0 Independent
 4        16   59.5        20 female     0 Independent
 5        20   56.3        22 female     0 Independent
 6        22   56.3         8 female     0 Independent
 7        19   56.0        21 female     0 Independent
 8        16   55.9        22 female     0 Independent
 9        18   54.8        20 female     0 Republican 
10        20   54.7        12 female     0 Independent
# … with 22 more rows
```

<br /><br />


## Computing Summaries of Data in a Column

The `summarize()` function is used to compute summaries of data in a given column. Here we compute the mean income for all the employees.


```r
city %>% 
  summarize(
    M = mean(income)
    )
```

```
# A tibble: 1 x 1
      M
  <dbl>
1  53.7
```

The output from `summarize()` is a data frame with a single row and one or more columns, depending on how many summaries you computed. Here we computed a single summary so there is only one column. We also named the column `M` within the `summarize()` function.

Multiple summaries can be computed by providing more than one argument to the `summarize()` function. The output is still a single row data frame, but now there will be multiple columns, one for each summary computation. Here we compute the mean income for all the employees and the standard deviation of the incomes.


```r
city %>% 
  summarize(
    M  = mean(income),
    SD = sd(income)
    )
```

```
# A tibble: 1 x 2
      M    SD
  <dbl> <dbl>
1  53.7  14.6
```

<br /><br />


## Computations on Groups

The `group_by()` function groups the data by a specified variable. By itself, this function essentially does nothing. But it is powerful when the grouped output is piped to other functions, such as `summarize()`. Here we use `group_by(gender)` to compute the mean income and the standard deviation of the incomes for both males and females.


```r
city %>% 
  group_by(gender) %>%
  summarize(
    M  = mean(income),
    SD = sd(income)
    )
```

```
# A tibble: 2 x 3
  gender     M    SD
  <chr>  <dbl> <dbl>
1 female  48.9  13.3
2 male    59.9  14.2
```

You can also use `group_by()` with multiple attributes. Simply add additional column names in the `group_by()` function to create more conditional groups. For example to compute the mean income and standard deviation for males and females conditioned on political party, we can use the following syntax.


```r
city %>% 
  group_by(gender, party) %>%
  summarize(
    M  = mean(income),
    SD = sd(income)
    )
```

```
# A tibble: 6 x 4
# Groups:   gender [2]
  gender party           M    SD
  <chr>  <chr>       <dbl> <dbl>
1 female Democrat     51.7 17.5 
2 female Independent  48.6 12.0 
3 female Republican   47.6 19.5 
4 male   Democrat     53.0 14.9 
5 male   Independent  61.6 10.4 
6 male   Republican   70.8  9.41
```

This produces the summary measures for each of the combinations of the levels of gender and political affiliation in the data.

<br /><br />





<!-- ```{r echo=FALSE, out.width="60%", fig.cap="LEFT: A visual mnemonic for a vector is a single-column bookcase. RIGHT: A visual mnemonic for a data frame is a multi-column bookcase."} -->
<!-- knitr::include_graphics("figs/15-vector-df.png") -->
<!-- ``` -->

