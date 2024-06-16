# programming basics

type: lecture

# programming environment

## overview

- enter commands **one at a time** at the command prompt
- run **a set of commands** from a source file
- supports vectors (numerical, character, logical), matrices, data-frames, and lists
- to quit, use `>q()`

## workspace

- objects that you create during a session are held in memory
    - **workspace**: the collection of objects you currently have

### save

```r
getwd() #prints the current working directory 
ls() #lists the objects in the current workspace 
setwd(mydirectory) #changes to mydirectory 
	setwd("c:/docs/mydir")

```

### load

```r
load("C:\\Program Files\\R\\R-2.5.0\\bin\\.RData")

```

### help

```r
help.start() #general help
help(foo) #help re: function foo
?foo #^^
apropos("foo") #all functions with this string
example(foo) #shows an example of function
```

# commands

## naming

- results of calculations can be stored in objects using the assignment operators (an arrow (←) or an equal sign)
- these objects can be used in other calculations
- to print an object, simply enter its name
    - objects cannot contain symbols (e.g. !, +, -, #)
    - object names can contain a number but cannot start with one

### example

```r
> x <- c(1:10) #x=c(1:10)=[1,2,3,4,5,6,7,8,9,10]
> x #prints 1 2 3 4 5 6 7 8 9 10
> x>8 #prints F F F F F F F F T T 
> x<5 #prints T T T T F F F F F F
> x>8 | x<5 #prints T T T T F F F F T T 
> x[c(T,T,T,T,F,F,F,F,F,T,T)] #prints 1 2 3 4 9 10 
```

## ls

- to list the objects that you have in your current session, use the function `ls` or the *function objects*
    
    ```r
    > x2 = 9
    > y2 = 10
    > ls(pattern="x") #lists all objects starting with "x"
    #prints [1] "x2"
    ```
    

## rm

- if you assign a value to an object that already exists, then the contents of the object will be overwritten with the new value (without a warning)
- use the function rm to remove one or more objects from your session
    
    ```r
    > rm(x, x2) 
    ```
    

### example

- let’s create two small vectors with data and a scatterplot
    
    ```r
    x<- c(1, 2, 3, 4, 5, 6) 
    y<- c(6, 8, 3, 7, 1) 
    plot(x,y) 
    title("My first scattersplot) 
    ```
  
- solving for x in $Ax = b$
    
    ```r
    A <- matrix(c(1,2,4,1),ncol=2)
    > A
    #     [,1] [,2]
    # [1,]    1    4
    # [2,]    2    1
    
    > b <- c(2,1)
    > solve(A,b) #0.2857143 0.4285714
    ```
    

## conflicting objects

- r allows the user to give an object a name that already exists— which may result in problems when using names of objects that already exists in the base package
    
    ```r
    > mean = 10
    > conflicts # "body <-" "mean"
    ```
    
- you can safely remove the object with the function `rm()` without risking deletion of the base package function
    
    ```r
    > rm(mean)
    ```
    

# datasets

- r comes with some sample datasets that you can access using `> data()`

## packages

- the system allows you to write new functions and package those functions in a library— this package may also contain other r objects (e.g. datasets or documentation)
- to see a list of the packages already attached to the system, use `> search()`
- to attach another package, you can either:
    - use the menu → select r package installer (e.g. from packages&data)
    - or the library (e.g. `> library(MASS)`)
- the function can also be used to list all the available libraries on your system using `> library()`

---

# data types

## vectors

```r
> a <- c(1,2,5.3,6,-2,4) #numeric vector 
> b <- c("one", "two", "three") #character vector
> c <- c(TRUE, TRUE, FALSE) #logical vector 

#refer to elements using subscripts 
> a[c(2,4)] #2nd and 4th elements (2,6)
> a[2:4] #2nd to 4th elements (2,5.3,6)

#NOTE: STARTS AT INDEX 1!!
```

## dataframes

- more general than a matrix, in that different columns can have different modes

```r
d <- c(1,2,3,4)
e <- c("red", "white", "red", NA)
f <- c(TRUE,TRUE,TRUE,FALSE)
mydata <- data.frame(d,e,f)
names(mydata) <- c("ID","Color","Passed")

# ID Color Passed
#1  1   red   TRUE
#2  2 white   TRUE
#3  3   red   TRUE
#4  4  <NA>  FALSE

mydata[1:2] #columns 1,2 
mydata[c("ID","Passed")] #columns ID and Passed 
mydata$ID #variables ID 
```

## matrices

```r
#fills the matrices by columns by default
#provides optional labels for columns and rows

y <- matrix(1:20, nrow=5, ncol=4)
#      [,1] [,2] [,3] [,4]
#[1,]    1    6   11   16
#[2,]    2    7   12   17
#[3,]    3    8   13   18
#[4,]    4    9   14   19
#[5,]    5   10   15   20

y[,4] #4th column of matrix 
y[3,] #3rd row of matrix 
y[2:4,1:3] #rows 2,3,4 of columns 1,2,3
```

## arrays

- similar to matrices but can have more than two dimensions

```r
> array(data = NA, dim = length(data), dimnames = NULL)

#data = a vector
#dim = an integer vector of length one or more giving the maximal indices 
#dimnames = either NULL or the names of the dimensions in list form 

> y <- array(1:3, c(2,4))
#.     [,1] [,2] [,3] [,4]
#[1,]    1    3    2    1
#[2,]    2    1    3    2
```

## lists

- an ordered collection of objects (components) that allow you to gather a variety of (even unrelated) objects under one name

```r
w <- list(name="Fred", mynumbers=a, mymatrix=y, age=5.3)
v <- c(list1, list2) 

w[[2]] #2nd component of the list 
```

# import/export

- **import**

```r
#first row contains variable names
#assign the variable id to row names 
#note the / instead of \ 

mydata <- read.table("c:/mydata.csv", header=TRUE, sep=",", row.names="id")
```

- **export**

```r
write.table(mydata, "c:/mydata.txt.",sep"\t")

```

- **viewing**

```r
#list objects in the working environment 
> ls() 

#lists the variables in mydata 
> names(mydata) 

#list the structure of mydata 
> str(mydata) 

#dimensions of an object 
> dim(object)

#class of an object
> class(object) 

#print mydata
> mydata

#print first 10 rows of mydata
> head(mydata, n=10) 

#print last 5 rows of mydata
> tail(mydata, n=5) 

#create a dataframe from scratch 
> age <- c(25, 30, 56)
> gender <- c("male", "female", "male")
> weight <- c(160, 110, 220)
> mydata <- data.frame(age,gender,weight)

#   age gender weight
#1  25   male    160
#2  30 female    110
#3  56   male    220
```

## missing data

- missing values are represented by the symbol `NA` (not available)— impossible values, on the other hand, are represented by the symbol `NaN`
    
    ```r
    is.na(x) #return TRUE if x is missing 
    y <- c(1,2,3,NA) 
    is.na(y) #returns a vector (F F F T) 
    ```
    
- excluding missing values from analyses—arithmetic functions on missing values yield missing values
    
    ```r
    x <- c(1,2,NA,3) 
    mean(x) #returns NA
    mean(x, na.rm=TRUE) #returns 2 
    ```
    
- the function `complete.cases()` returns a logical vector indicating which cases are complete
    
    ```r
    #list rows of data that have missing values 
    mydata[!complete.cases(mydata),]
    ```
    
- the function `na.omit()` returns the object with list-wise deletion of missing values
    
    ```r
    #create new dataset without missing data 
    newdata <- na.omit(mydata) 
    ```
    

## creating new variables

```r
#3 examples for doing the same computations

mydata$sum <- mydata$x1 + mydata$x2 
mydata$mean <- (mydata$x1 + mydata$x2)/2

attach(mydata)
mydata$sum <- x1 + x2
mydata$mean <- (x1 + x2)/2
detach(mydata)

mydata <- transform(mydata, sum = x1 + x2, mean = (x1 +
x2)/2)
```

## arithmetic operators

| operator | description |
| --- | --- |
| + | addition |
| - | subtraction |
| * | multiplication |
| / | division |
| ^ or ** | exponentiation |
| x %% y | modulus (x mod y) 5%%2 is 1  |
| x %/% y | integer division 5%/%2 is 2 |

## logical operators

| operator | description |
| --- | --- |
| < | less than |
| <= | less than or equal to |
| > | greater than |
| >= | greater than or equal to |
| == | exactly equal to |
| != | not equal to |
| !x | not x  |
| x|y | x OR y |
| x&y | x AND y  |
| isTRUE(x) | test if x is TRUE |

## control structures

- `expr` can be multiple compound statements by enclosing them in braces {}— it is more efficient to use built-in functions rather than control structures whenever possible

```r
#transpose of a matrix 
mytrans <- function(x) {
	if(!is.matrix(x)) {
		warning("argument is not matrix: returning NA")
		return(NA_real_)}
	y <- matrix(1, nrow=ncol(x), ncol=nrow(x))
	for(i in 1:nrow(x)) {
		for(k in 1:ncol(x)) {
			y[j,i] <- x[i,j]
		}}
	return(y)}
```
