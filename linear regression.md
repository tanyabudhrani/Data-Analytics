# linear regression

type: lecture

### where linear regression would be helpful

- large differences in price and quality between years, although wine is produced in a similar way since its meant to be aged, so it is hard to tell if wine will be good when it is on the market
- can analytics be used to come up with a different system for judging wine?

## linear regression vs. wine

- two types of variables are designed

- **dependent variable y**:
    - typical price in 1990-1991 wine auctions (approximates quality)

- **independent variable x**:
    - age (older wines are more expensive)
    - weather
    - average growing season temperature
    - harvest rain
    - winter rain

# linear regression

- suppose we have collected bivariate data ($x_i$, $y_1$), $i = 1,…,n$
- **goal**: to model the relationship between x and y by finding a function y = f(x) that is a close fit to the data
- **assumptions**: $x_i$ is NOT random and that $y_i$ is a function of $x_i$ plus some random noise

## example one

- cost of a first-class stamp in cents over time
- using the R function lm() we found the least squares fit for a line, which is $y = -0.06558 + 0.87574x$  where x is the number of years since 1960 and y is in cents
- to predict the price for 2016 stamp, we let x = 56, then y = 48.98
    
## example two

- suppose we have n pairs of fathers and adult sons
    - let $x_i$ and $y_i$ be the heights of the i-th father and son, respectively— the least squares line for this data could be used to predict the adult height of a young boy from that of his father

## example three

- we are not limited to best fit lines
    - for all positive d, the method of least squares may be used to find a polynomial of degree d with the best fit to the data
    

## fitting a line with least squares

- suppose we have several data points
- **goal**: find a line $y = ß_1x + ß_0$ best fitting the data
    - $ß_1$: regression coefficient for the independent variable
    - $ß_0$: intercept coefficient
- **assumption**: each $y_i$ is predicted by $x_i$ up to some error
    - $y_i = ß_1x + ß_0 + e_i$ [error]
- **errors**: the sum of the square errors
    - $S(ß_0, ß_1) = ∑_ie^2= ∑_i(y_i-ß_ix_i-ß_0)^2$
    - the method of least squares finds the values $ˆβ_0$ and 
    $ˆβ_1$ of $ß_0$ and $ß_1$ that minimizes $S(ß_0,ß_1)$, the sum of the squared errors
    
- use least squares to fit a line to the following three data points: (0,1), (2,1), (3,4)
    - mean of x = 5/3 | mean of y = 2 | $s_x$$_x$ = 7/3 | $s$$_x$$_y$ = 2
        - $sxx = 1/n-1∑(x_i-x̄)^2$ | $sxy = 1/n-1∑(x_i-x̄)(y_i-ȳ)$
    - so, the least squares line as an equation is $y = 6/7x + 4/7$
    

> **note**:
the word “linear” in linear regression does not refer to fitting a line, though it is the most common curve to fit— when we fit a line to **bivariate data**, it is called **simple linear regression**
> 

## residuals in fitting a line

- suppose the model is $y_i = ß_1x + ß_0 + e_i$
    - $ß_1x + ß_0$ as the predicting or explaining $y_i$
    - the left-over term $e_i$ is called the residual
- when plotting the residuals out, the data points should hover near the regression line— the residuals should look about the same across the range of x

## homoscendasticity in fitting a line

- when the residuals have the same variance for all $i$
    - the opposite case is called heteroscendasticity

## linear regression for multivariate

- for multivatiate data, you need to fit the data with a line (in high dimensional space): $y = ß_1x_1 + ß_2x_2 +…+ß_mx_m$ where x is the **explanatory** variable
- the total square error is: $∑_i(ß_1x_1 + ß_2x_2 +…+ß_mx_m - y_1)^2$

## fitting polynomials

- “linear” refers to the linear algebraic equations for unknown parameters $ß_1$ (e.g. each $ß_i$ has exponent 1)
- use least squares to fit a line to the following three data points: (0,1), (2,1), and (3,4)
    - the parabola has the formula $y = ß_0 + ß_1x + ß_2x^2$
    - the error — $S(ß_0, ß_1, ß_2) = ∑_i(ß_0 + ß_1x_i + ß_2x_1$$^2-y_i)^2$
- the minimum solutions $ˆβ_0, ˆβ_1, ˆβ_2$ should be used to fit the polynomials

## measuring the fit

- data and predicted values of the response variable:
    - $y = (y_1, y_2,…, y_n)$
    - **$ŷ = (ŷ_1,ŷ_2,…ŷ_n)$**

- **total sum of squares** (TSS): $∑_i(y_i-Ȳ)^2$

- **residual sum of squares** (RSS): $∑_i(y_i-Ȳ_i)^2$
- **the goodness of fit**: $R^2 = 1 - RSS/TSS$
    - more complex model, better fitness and smaller $R^2$
    - tradeoff between goodness of fit and complexity

# time series analysis

## why we analyze time-series?

| compact description of data | • level: the average value in the series <br> • trend: the increasing or decreasing value in the series <br> • seasonality: the repeating short-term cycle in the series <br> • noise: the random variation in the series |
| --- | --- |
| interpretation | (e.g. seasonal adjustment) |
| forecasting | (e.g. predict unemployment) |
| control | (e.g. analyze impact of monetary policy on unemployment) |
| hypothesis testing | (e.g. global warming) |
| simulation | (e.g. estimate probability of catastrophic events) |


### example

- monthly number of unemployed people over years in australia
