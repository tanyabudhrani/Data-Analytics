# data analytics

type: lecture

# simulation

- an approximate imitation of the operation of a process or system, that is used:
    - to estimate the parameters for statistical models
    - performance tuning or optimizing
    - testing out a hypothesis or statistical method

## generating random numbers

- r comes with a set of pseudo-random number generators that allow you to simulate from well-known probability distributions
    - **rnorm**: generate random normal variates with a given mean and standard deviation
    - **dnorm**: evaluate the normal probability density (with a given mean/sd) at a point (or vector of points)
    - **pnorm**: evaluate the cumulative distribution function for a normal distribution
    
    ```r
    pnorm(2) 
    [1] 0.9772499 
    
    #the probability of a random standard normal variable of being less than 2 
    ```
    

### example

- generate standard normal random numbers
    
    ```r
    x <- rnorm(10) 
    ```
    

- generate random numbers from N(20, 2$^2$)
    
    ```r
    x <- rnorm(10, 20, 2)
    ```
    

```r
summary(x) 
#provides the min, 1st quadrant, median, mean, 3rd quadrant, and max
```

## random number seed

- a random seed is a number used to initialize a pseudorandom number generator (a starting point)
- ensure reproducibility of the sequence of random numbers
- setting the random number seed with set.seed()
    
    ```r
    set.seed(1) 
    rnorm(5) 
    ```
    

## simulating a linear model

- suppose we want to simulate the following model:
    
    > $y = ß_0 + ß_1x + e$
    $e$ ~ $N(0, 2^2)$
    > 
    > 
    > ```r
    > #set seed
    > set.seed(20)
    > 
    > #simulate predictor variable 
    > x <- rnorm(100) 
    > 
    > #simulate error term 
    > e <- rnorm(100, 0, 2) 
    > 
    > #compute the outcome via the model 
    > y <- 0.5 + 2 * x + e
    > summary(y) 
    > ```
    > 
- what if we wanted to simulate a predictor variable for a binary x?
    
    ```r
    set.seed(10)
    x <- rbinom(100, 1, 0.5) 
    str(x) #x is now 0s and 1s
    int [1:100] 1 0 0 1 0 0 0 0 1 0 
    
    e <- rnorm(100, 0, 2)
    y <- 0.5 + 2 * x + e
    plot(x, y)
    ```
    

## random sampling

- the sample() function draws randomly from a specified set of scalar objects allowing you to sample from arbitrary distributions of numbers
    
    ```r
    #sampling numbers
    set.seed(1)
    sample(1:10, 4) 
    
    #sampling letters
    sample(letters, 5) 
    
    #sample with replacement 
    sample(1:10, replace=TRUE)
    
    #random permutation
    sample(1:10)
    sample(1:10) 
    ```
    
- to sample more complicated things, such as rows from a data frame or a list, you can **sample the indices into an object** rather than the elements of the object itself

### example

- create the index vector indexing the rows of the data frame and sample directly from that index vector
    
    ```r
    set.seed(20) 
    
    #create index vector 
    idx <- seq_len(nrow(airquality)) # a vector from 1-53
    
    #sample from the index vector
    samp <- sample(idx, 6) #generates 6 random numbers
    
    #sample 6 rows according to the random numbers generated
    airquality[samp, ]
    ```
    

## case study

```r
pm0 <- read.table("RD_501_88101_1999-0.txt", comment.char="#", header=FALSE, sep="|", na.strings="")

#skip some commented lines in the beginning of the file
#do not read the header data
#fields are delimited with the | character
#missing values are coded as blank fieldspchs
```

```r
dim(pm0) #117421 28 --> 117421 data points with over 28 attributes
```

### fixing the headers

```r
cnames <- readLines("RD_501_88101_1999-0.txt", 1)
cnames <- strsplit(cnames, "|", fixed=TRUE)
names(pm0) <- make.names(cnames[[1]])
head(pm0[, 1:13]) 
```

![Screenshot 2023-03-13 at 1.09.46 PM.png](data%20analytics%2079658b3ada174ec3a3ccfdd7c1a881e5/Screenshot_2023-03-13_at_1.09.46_PM.png)

### checking missing values

```r
x0 <- pm0$Sample.Value
summary(x0)   

# Min.  1st Qu.  Median   Mean    3rd Qu.   Max.    NA's    
# 0.00   7.20    11.50    13.74   17.90    157.10   13217
 
mean(is.na(x0)) #0.11 
```

### do the same with 2012

```r
pm1 <- read.table("RD_501_88101_2012-0.txt", comment.char="#", header=FALSE, sep="|", na.strings="")
cnames1 <- readLines("RD_501_88101_2012-0.txt", 1)
cnames1 <- strsplit(cnames1, "|", fixed=TRUE)
names(pm1) <- make.names(cnames1[[1]])
x1 <- pm1$Sample.Value> summary(x1)   

#  Min.    1st Qu.   Median   Mean    3rd Qu.   Max.     NA's  
# -10.00    4.00     7.63     9.14    12.00    908.97   73133
```

## boxplot

```r
#first, need to fix negative values
negative <- x1 < 0
mean(negative, na.rm=T)
#[1] 0.0215034
```

```r
boxplot(log2(x0), log2(x1)) #extremely large
```

![Rplot.png](data%20analytics%2079658b3ada174ec3a3ccfdd7c1a881e5/Rplot.png)

### an individual monitor

```r
site0 <- unique(subset(pm0, State.Code==36, c(County.Code, Site.ID)))
site1 <- unique(subset(pm1, State.Code==36, c(County.Code, Site.ID)))

site0 <- paste(site0[,1], site0[,2], sep=".")
site1 <- paste(site1[,1], site1[,2], sep=".")

str(site0) 
#chr [1:33] "1.5" "1.12" "5.73" "5.80" "5.83" "5.110" "13.11" ...

str(site1) 
#chr [1:18] "1.5" "1.12" "5.80" "5.133" "13.11" "29.5" "31.3" ...

both <- intersect(site0, site1)
print(both) 
#[1] "1.5"     "1.12"    "5.80"    "13.11"   "29.5"    "31.3"    [7] "63.2008" "67.1015" "85.55"   "101.3"
```

```r
#choosing one that had a reasonable amount of data in each year 
#we need to find how many observations available at each monitor

pm0$County.site <- with(pm0, paste(County.Code, Site.ID, sep="."))
pm0$county.site <- with(pm0, paste(County.Code, Site.ID, sep="."))
pm1$county.site <- with(pm1, paste(County.Code, Site.ID, sep="."))
cnt0 <- subset(pm0, State.Code == 36 & county.site %in% both)
cnt1 <- subset(pm1, State.Code == 36 & county.site %in% both)
```

![Screenshot 2023-03-13 at 1.43.02 PM.png](data%20analytics%2079658b3ada174ec3a3ccfdd7c1a881e5/Screenshot_2023-03-13_at_1.43.02_PM.png)

```r
both.county <- 63
both.id <- 2008 
pm1sub <- subset(pm1, State.Code == 36 & County.Code == both.county & Site.ID == both.id) 
pm0sub <- subset(pm0, State.Code == 36 & County.Code == both.county & Site.ID == both.id)
```

## results

```r
dates1 <- as.Date(as.character(pm1sub$Date), '%Y%m%d')
x1sub <- pm1sub$Sample.Value
dates0 <- as.Date(as.character(pm0sub$Date), '%Y%m%d')
x0sub <- pm0sub$Sample.Value
rng <- range(x0sub, x1sub, na.rm = T)
plot(dates0, x0sub, pch = 20, ylim = rng, xlab = "", ylab = expression(PM[2.5]*" ("*mu*g/m^3*")"))s
```

![Rplot.png](data%20analytics%2079658b3ada174ec3a3ccfdd7c1a881e5/Rplot%201.png)

![Rplot.png](data%20analytics%2079658b3ada174ec3a3ccfdd7c1a881e5/Rplot%202.png)

- **observation 1**: median levels of PM have decreased
- **observation 2**: the variation spread in PM values in 2012 is much smaller than it was in 1999

## state-wide PM levels

```r
mn0 <- with(pm0, tapply(Sample.Value, State.Code, mean, na.rm=TRUE))
mn1 <- with(pm1, tapply(Sample.Value, State.Code, mean, na.rm=TRUE))
d0 <- data.frame(state=names(mn0), mean=mn0)
d1 <- data.frame(state=names(mn1), mean=mn1)
mrg <- merge(d0, d1, by = "state")
head(mrg)
```

```r
rng <- range(mrg[,2], mrg[,3])
with(mrg, plot(rep(1,52), mrg[,2], xlim=c(.5, 2.5), ylim=rng, xaxt="n", xlab="", ylab="State-wide Mean PM"))
with(mrg, points(rep(2, 52), mrg[,3]))
segments(rep(1,52), mrg[,2],rep(2,52), mrg[,3])
axis(1,c(1,2), c("1999", "2012"))

#xaxt: a character which specifies the x axis type, where "n" surpresses plotting of the axis
#segments(x0, y0, x1, y1): draws line segments between pairs of points
	#x0, y0: coordinates of points from which to draw
	#x1, y1: coordinates of points to which to draw 
#axis: adds an axis to the current plot 
```