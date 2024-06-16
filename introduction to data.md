# introduction to data

type: lecture

# data

- **individual units** of information (information pieces)
- a **single quality or quantity** of some object or phenomenon— data is represented by variables because we need to **compute the data**
- data is employed in virtually every form of **human organizational activity** (e.g. business management, finance, governance, research, etc)
- lots of data is being **collected and warehoused**

## data analytics

- a process of **inspecting, cleaning, transforming, and modeling the data** with the goal of discovering useful information, informing conclusions, and supporting decision making
    - data driven (the more the better)
    - interdisciplinary (mathematics + computer science)
        - math provides the **theoretical knowledge** while computer science provides the **practical knowledge**
    - discover knowledge regarding the data
- **examples**: weather prediction, physics research (supercollider data analytics), astronomy images (planet detection), medical research (drug interaction), etc

### example

- three students
    - continuous assessment grades (40%): D+, C+, A
        - **mean of continuous assessments**: (1.5+2.5+4.0)/3 = 2.67 = C+
    - final exam grades (60%): C, B, B
        - **mean of final exam**: (2.0+3.0+3.0)/3 = 2.67 = C+

- breakdown:
    - mean of student one — (1.5*0.4 + 2*0.6) = 1.8
    - mean of student two — (2.5*0.4 + 3*0.6) = 2.8
    - mean of student three — (4*0.4 + 3*0.6) = 3.4
        - **overall mean:** (2+3+3.5)/8 = 2.83 = B
- letter grade mapping system is may not be fair since all three students had higher letter grades than their numerical counterparts

### types of analytics in business

![Screenshot 2023-01-09 at 10.43.16 AM.png](introduction%20to%20data%208c0bf7631e7b49c496cd54f8dca14a6a/Screenshot_2023-01-09_at_10.43.16_AM.png)

[Untitled Database](introduction%20to%20data%208c0bf7631e7b49c496cd54f8dca14a6a/Untitled%20Database%20e458bd6eb0f64324b647843ea7f89a1a.csv)

### why is data science so successful?

- **better models**
    - with more variables to fit data
    - rule-based → statistical → deep learning

- **better computing resource**
    - more powerful RAM, CPU, GPU, etc
    

- **more data**
    - huge volume of data is available to do analytics and discover valuable information

## big data

- a collection of data sets so large and complex that it becomes difficult to process using on-hand database management tools or traditional data processing applications

### characteristics

| volume  | from terabytes to exabytes to zetabytes of existing data to process |
| --- | --- |
| velocity  | batch data, real-time data, streaming data, milliseconds to seconds to respond  |
| variety | structured, semi-structured, unstructured, text, pictures, multimedia |
| veracity | uncertainty due to data inconsistency & incompleteness, ambiguities, deception, model approximation |

### first big data challenge

- 1880 census
- 50 million people
- age, gender, occupation, education level, number of insane people in household

### first big data solution

- **hollerith tabulating system**
- punched cards with over 80 variables (used for 1890 census)
- 6 weeks as opposed to 7 years

- **manhattan project**
    - government wanted to develop more complex weapons for world war II— roughly 2 billion was allocated to this project
    - catalyst for “big science”

- **space program**
    - government wanted to compete with the soviet union (cold war) so they started a space program
    - began in late 1950s
    - an active area of big data now

## data mining

- discovery of patterns and models that are:
    - **valid**— hold on new data with some certainty (so that results can be reproducible)
    - **useful**— should be possible to act on the item
    - **unexpected**— non-obvious to the system
    - **understandable**— humans should be able to interpret the pattern

[Untitled Database](introduction%20to%20data%208c0bf7631e7b49c496cd54f8dca14a6a/Untitled%20Database%20780769e2e44e4b31afa0e105d372b46d.csv)

### relation between data mining and analytics

- analytics include both **data analysis (mining)** and **communication (guide decision making)**
- analytics is not so much concerned with individual analyses or analysis steps, but with the **entire methodology**