# programming and statistics

type: lecture

### recap

- different types of data representation
    - vectors, matrices, array, data frames, and lists
- import data (from texts), viewing data, and exporting results (to texts)
- **data manipulation**:
    - control structures
    - arithmetic and logical operations
    - built-in functions (numeric, character, probability, statistics, etc)

## plotting a normal distribution graph

```cpp
x <- pretty(c(-3,3), 1000)
y <- dnorm(x, m=0, sd=1)
k <- dnorm(x, m=1, sd=0.8)

plot(x,k, type="b", pch=19, col="blue", xlab="z-scores", ylab="Density)
lines(x,y, type="b", pch=19, col="red") 
legend("topleft", c("N(0,1)", "N(1,0.64)"), fill=c("blue", "red"))
```

# ggplot2

- the r package extends the basic charting and graphing functions
- gets its name from leland wilkinson’s grammar of graphics, which provides a formal, structured perspective on how to describe data graphics
- it has attracted many users because of its versatility, clear and consistent interface, and beautiful output

### template

- to make a graph, replace the bracketed section with a data set (<DATA>), a geometry function (<GEOM_FUNCTION>), or a collection of mappings (<MAPPINGS>)

```r
ggplot(data = <DATA>) + <GEOM_FUNCTION>(mapping=aes(<MAPPINGS>)
```

## aesthetic mappings

- a third variable that can be added to the 2D scatterplot by mapping it to an aesthetic to convey additional information (aesthetics include things like size, shape, or color)

```r
ggplot(data=mpg) + geom_point(mapping=aes(x=displ, y=hwy, color=class))
```

> explanation of code: **`geom_point(mapping = aes(x = displ, y = hwy))`** adds a layer to the plot using the **`geom_point()`** function, which creates a scatterplot of points— the **`mapping`** argument specifies how the variables in the data frame should be mapped to the aesthetics (visual properties) of the plot (in this case, it uses the **`aes()`** function to map the **`displ`** variable to the x-axis and the **`hwy`** variable to the y-axis
> 

```r
ggplot(data=mpg) + geom_point(mapping=aes(x=displ, y=hwy, size=class))
#bases the size on the class
```

```r
ggplot(data=mpg) + geom_point(mapping=aes(x=displ, y=hwy, shape=class))
#bases the size on the shape
```

## facets

- useful for categorial variables, facets help you split your plot into subplots that each display one subset of the data

```r
ggplot(data=mpg), + geom_point(mappings=aes(x=displ, y=hwy)) + facet_wrap(~class, nrow=3)
```

```r
ggplot(data=mpg) + geom_point(mapping=aes(x=displ, y=hwy)) + facet_grid(drv~cyl)
```

> **`facet_wrap()`** creates a grid of plots, where each plot is a subset of the data based on a single categorical variable— the plots are arranged in a "wrap" fashion, meaning that the plots are arranged in a single row or column and wrap around to a new row or column when the maximum number of plots per row or column is reached
> 
> 
> **`facet_grid()`** is similar to **`facet_wrap()`**, but it allows you to create a grid of plots based on two categorical variables. The rows and columns of the grid represent the levels of the two variables— empty cells in a **`facet_grid()`** plot can occur when there are no observations in the data that correspond to a particular combination of levels of the two categorical variables used to define the grid
> 

## geometric objects

- the same data can be represented in different visual objects to provide different views of the data

```r
ggplot(data=mpg) + geom_point(mapping=aes(x=displ, y=hwy) #left
```

```r
ggplot(data=mpg) + geom_smooth(mapping=aes(x=displ, y=hwy))
```

- a geom is the geometrical object that a plot uses to represent data
    - bar charts use **bar geoms**, line charts use **line geoms,** box plots use **box plot geoms**
- we can set the group aesthetic to a categorical variable to draw multiple objects— ggplot2 will draw a separate object for each unique value of the grouping variable

```r
ggplot(data = mpg) +
geom_smooth(mapping = aes(x = displ, y = hwy)) # left

ggplot(data = mpg) +
geom_smooth(mapping = aes(x = displ, y = hwy, group = drv)) # middle

ggplot(data = mpg) +
geom_smooth(mapping = aes(x = displ, y = hwy, color = drv), show.legend = FALSE)

#the mapping argument sets the aesthetics of the layer, with x as the independent variable (displ), y as the dependent variable (hwy), 
#and color as the grouping variable (drv)-- this means that a separate smoothed curve will be drawn for each level of the drv variable, 
#he show.legend argument is set to FALSE, which means that the legend for the color grouping variable will not be shown in the plot
```

- multiple geom functions can also be added to ggplot to display in the same plot

```r
ggplot(data = mpg) +
geom_point(mapping = aes(x = displ, y = hwy)) + #geom_point creates a scatterplot
geom_smooth(mapping = aes(x = displ, y = hwy)) #gexaom_smooth creates a line 
```

## statistical transformations

- many graphs plot raw values of the data set while other graphs calculate new values (statistical transformation) to plot (e.g. bar charts, histograms, etc)
- override the default mapping from transformed variables to aesthetics

```r
ggplot(data = diamonds) +
geom_bar(mapping = aes(x = cut, y = after_stat(prop), group = 1))

#the mapping argument sets the aesthetics of the layer, with x as the variable to be plotted (cut) and y as the relative frequency of each cut level
#the after_stat(prop) function calculates the proportion of each level of the cut variable in the data
#he group argument is set to 1, which means that all the bars are treated as belonging to the same group, so they are all plotted in the same color
#this argument is necessary because the y aesthetic is computed using a summary statistic, so each bar has its own unique value of y
```

## position adjustment

- the stacking is performed automatically by the position adjustment specified by the position argument

```r
ggplot(data = diamonds) +
geom_bar(mapping = aes(x = cut, fill = clarity))
```

- position = “identity” will place each object exactly where it falls in the context of the graph
    - the **`position`** argument is set to **`"identity"`**, which means that the heights of the bars represent the actual values of the data, rather than some summary statistic like counts or proportions

- position = “fill” works like stacking, but makes each set of stacked bars the same height

- position = “dodge” places overlapping objects directly beside one another

- position = “jitter” adds a small amount of random noise to each point— adding randomness makes your graph less accurate at small scales, but more revealing at large scales

## coordinate systems

- the default coordinate system in ggplot2 is the cartesian coordinate system where the x and y positions act independently to determine the location of each point

```r
bar <- ggplot(data=diamonds) + 
	geom_bar(
		mapping=aes(x=cut, fill=cut),
		show.legend = FALSE,
		width = 1
	) + 
	theme(aespect.ratio = 1) + 
	labs(x=NULL, y=NULL)

bar + coord_fil() #switches the x and y axes
bar + coord_polar() #uses polar coordinates
```

> the **aspect ratio** is the ratio of the width of the plot to the height of the plot— by default, **`ggplot2`** tries to set the aspect ratio to be appropriate for the type of plot you are creating, but you can use the **`aspect.ratio`** argument to override the default and set a specific aspect ratio for your plot
> 

- `coord_quickmap()` sets the aspect ratio correctly for maps which is very important for plotting spatial data with ggplot 2
    
    ```r
    nz <- map_data("nz")
    
    ggplot(nz, aes(long, lat, group = group)) +
    geom_polygon(fill = "white", colour = "black")
    
    ggplot(nz, aes(long, lat, group = group)) +
    	geom_polygon(fill = "white", colour = "black") +
    	coord_quickmap()
    ```
    

### final template
- barplots, histograms, scatterplots
    
    # barplot
    
    ```r
    quiz <- c(100, 80, 70, 20, 80)
    exam <- c(80, 30, 90, 40, 90)
    name <- c("Peter", "Kenny", "Tom", "Tiffany", "Susanna")
    gender <- c("Male", "Male", "Male", "Female", "Female") 
    student_id <- c(1:5) #same as c(1,2,3,4,5) 
    
    record <- data.frame(student_id, name, gender, quiz, exam) 
    
    chart <- ggplot(record, aes(x=gender)) #defining the plot
    bars <- geom_bar(fill="blueviolet", color="black")
    chart+bars
    ```
    
    - `ggtitle: chart title; xlab, ylab: label for x-axis/y-axis`
        - xlabel ← xlab(”student’s gender”)
        - ylabel ← ylab(”frequency”)
        - title ← ggtile(”frequency distribution of students’ gender”)
        - chart + bars + xlabel + ylabel + title
    
    ```r
    ggplot(record, aes(x=name, y=quiz)) + 
    	geom_bar(fill="blueviolet", color="black", stat="identity")
    	+ xlab("Student") + ylab("Quiz Mark") + ggtitle("Quiz marks for student")
    
    # identity makes the heights of the bars to represent the values in the data
    ```
    
    - what if we want to color the bars depending on a certain feature?
    
    ### stacked bar
    
    ```r
    	ggplot(record, aes(x=gender, y=quiz, fill=name)) + 
    		geom_bar(color="black", stat="identity") + 
    		xlab("Student") + ylab("Quiz Mark") + ggtitle("Quiz marks for student")
    
    #fill allows us to breakdown the data into different students 
    ```
    
    ### interleaved bar
    
    ```r
    ggplot(record, aes(x=gender, y=quiz, fill=name)) + 
    		geom_bar(color="black", stat="identity", position="dodge") + 
    		xlab("Student") + ylab("Quiz Mark") + 
    		ggtitle("Quiz marks for student")
    #position also us to create interleaved bars
    ```
    
    # histograms
    
    - histogram consists of parallel vertical bars that graphically shows the frequency distribution of a quantitative variable— we can use them to visualize data distributions
    
    ```r
    ggplot(record, aes(x=quiz)) + geom_histogram(binwidth=20, fill="pink", color="black")
    ```
    
    # scatterplot
    
    - add the points using a `geom` layer called `geom_point` with the ‘+’ operator
    
    ```r
    scatter <- ggplot(record, aes(x=quiz, y=exam, color=gender, shape=gender)) 
    + geom_point(size=3) + xlab("Quiz") + ylab("Exam") + ggtitle("Exam vs. Quiz marks")
    ```
