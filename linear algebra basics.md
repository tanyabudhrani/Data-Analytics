# linear algebra basics

type: lecture

# vectors

- an ordered list of numbers
    
    ![Screenshot 2023-01-29 at 6.58.21 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-29_at_6.58.21_PM.png)
    
- seen as a directed line segment in n-dimensions
    - **count of entries**: dimension
    - **vectors of dimension** n: n-vector
    - **numbers are called**: scalar

### example

> word count vectors are used in computer based document analysis
> 

> word
in 
number
house
the 
document
> 

> 1
1
0
0
0
1
> 

## vector addition

- $n$-vectors $a$ and $b$ can be added/subtracted using the head-to-tail method
    
    ![Screenshot 2023-01-29 at 7.02.53 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-29_at_7.02.53_PM.png)
    
    > 0   1   1
    7 + 2 = 9
    3   0   3
    > 

- **communicative**: $a+b = b+a$
- $a+0 = 0+a$

- **associative**: $(a+b) + c = a+(b+c)$
- $a-a = 0$

### example

> word count vectors are used in computer based document analysis 

each entry of the word count vector is the number of times the associated dictionary word appears in the document
> 

> word
in 
number
house
the
document
> 

> 1   2   3
1   1   2
0 + 0 = 1
0   0   0
0   4   4
1   1   2
> 

## scalar-vector multiplication

- scalar ß and $n$-vector $a$ can be multiplied
    - $ßa = (ßa_1, ßa_2,…,ßa_3)$
        
        > (-2)(1) = (-2)
             9     -18
             6     -12
        > 

![Screenshot 2023-02-08 at 1.21.25 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-02-08_at_1.21.25_PM.png)

### example

> word count vectors are used in computer based document analysis — **WEIGHT 0.75**

each entry of the word count vector is the number of times the associated dictionary word appears in the document — **WEIGHT 0.25**
> 

> word
in 
number
house
the
document
> 

> 1         2   1.25
       1         1   1
 (0.75)0 + (0.25)0 = 0.25
       0         0   0
       0         4   1
       1         1   1
> 

## inner product

- dot-product of $n$-vectors $a$ and $b$:
    - $a^Tb=a_1b_1+a_2b_2+…+a_nb_n$
    
    > (-1)$^T$ (1)
     2  *  0 = $-1*1+2*0+2*(-3)=-7$
     2    -3
    > 
- $a^T=b^Ta$
- $(ya)^Tb=y(a^Tb)$
- $(a+b)^Tc=a^Tc+b^Tc$
- $(a+b)^T(c+d)=a^Tc+b^Tc+a^Td+b^Td$

### example

> word count vectors are used in computer based document analysis 
****
each entry of the word count vector is the number of times the associated dictionary word appears in the document
> 

> word 0.1
in 0.8
number 0.2
house 0.1
the 0.9
document 0.1
> 

> 1  
1
0 * (0.1 0.8 0.2 0.1 0.9 0.1) = 1
0
0
1
> 

> 2
1
1 * (0.1 0.8 0.2 0.1 0.9 0.1) = 5
0
4
1
> 

# norm

- the euclidean norm of an n-vector x is:
    
    ![Screenshot 2023-01-29 at 7.23.25 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-29_at_7.23.25_PM.png)
    
- used to measure the length of a vector
- properties (for any n-vectors x, y and scalar ß)
    - **homogeneity** $||ßx|| = |ß|||x||$
    - **triangle inequality** $||x+y||≤||x||+||y||$
    - **non-negativity** $||x|| ≥ 0$
    - **definiteness** $||x|| = 0$ only if $x = 0$

# distance

- the euclidean distance of two n-vectors x and y is:
    
    ![Screenshot 2023-01-30 at 8.28.30 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_8.28.30_PM.png)
    
- length of the subtraction of the two vectors
    
    ![Screenshot 2023-01-30 at 8.29.26 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_8.29.26_PM.png)
    

# angle

- angle θ between two non-zero vectors a and b
    - $cosθ = a^Tb/||a||*||b||$ where $0≤θ≤π$

### cases of θ

| $θ=π/2 = 90º$ | a and b are orthogonal | $a⟂b$ |
| --- | --- | --- |
| $θ=0$ | a and b are aligned | $a^Tb=||a||*||b||$ |
| $θ=π=180º$ | a and b are anti-aligned | $a^Tb=-||a||$ |
| $θ ∈(0, π/2)$ | a and b make an acute angle | $a^Tb>0$ |
| $θ ∈(π/2, π)$ | a and b make an obtuse angle | $a^Tb>0$ |

### example - document similarity

- 5 wikipedia articles (veterans day, memorial day, academy awards, golden globe awards, super bowl)

![Screenshot 2023-01-30 at 8.31.02 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_8.31.02_PM.png)

### example - document dissimilarity

- 5 wikipedia articles (veterans day, memorial day, academy awards, golden globe awards, super bowl)

![Screenshot 2023-01-30 at 8.42.57 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_8.42.57_PM.png)

# clustering

- given $N$ $n$-vectors, $x_1, x_2, x_N$, partition (cluster) them into k clusters, letting vectors in the same cluster stay close to each other
    - **group assignment**: $c_i$ is the index of the group assigned to vector $x_i$ (i.e. $x_i∈G_c$$_i$)
    - **group representatives**: $n$-vectors $z_1, z_2,…z_k$
    - **clustering objective**: j[cluster] $= 1/N∑^N_1||x_i-z_c$$_i||^2$ — THE SMALLER THE BETTER

## k-means clustering

- alternatively updating the group assignment, then the representatives— j[cluster] goes down in each step

![Screenshot 2023-01-30 at 9.00.29 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.00.29_PM.png)

- iterations
    
    ![Screenshot 2023-01-30 at 9.01.11 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.01.11_PM.png)
    
    ![Screenshot 2023-01-30 at 9.01.21 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.01.21_PM.png)
    
    ![Screenshot 2023-01-30 at 9.01.32 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.01.32_PM.png)
    
    ![Screenshot 2023-01-30 at 9.01.43 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.01.43_PM.png)
    
    ![Screenshot 2023-01-30 at 9.01.52 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.01.52_PM.png)
    
    ![Screenshot 2023-01-30 at 9.02.14 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.02.14_PM.png)
    

### example — topic discovery

- N = 500 wikipedia articles
- dictionary size n = 4423
- run k-means algorithm with k = 9

> RESULTS:
top words in the cluster representatives, mean of word vectors in the cluster 

title of articles closest to the representatives
> 

# matrix

- a matrix is a rectangular array of numbers
    
    > 0    1  -2.3  0.1
    1.3  4  -0.1   0
    4.1  -1  0     7
    > 
    - its size is given by the **(row dimension) * (column dimension)** (i.e. 3*4 for the above example)
    - **elements** are also called **entries** (i.e. $b_i$$_,$$_j$ is the entry at the i-th row and j-th column)
    - two matrices are equal if they have the **same size** and **all corresponding entries are equal**

## matrix and vectors

- we consider a $n*1$ matrix to be an n-vector or **column vector**
- we consider a $1*1$ matrix to be a **number**
- a $1*n$ matrix is defined as a **row vector**
    - e.g. (1.2 -0.3  1.4  2.6) is different from (1.2 \n -0.3 \n 1.4 \n 2.6)

## column and rows of a matrix

- suppose A is an m*n matrix with entries $A_i$$_,$$_j$
- its j-th column is (an m-vector)
    
    > $A_1$$_,$$_j$
    $A_2$$_,$$_j$
    …
    $A_m$$_,$$_j$
    > 
- its i-th row is (an n-row-vector)
    
    > $A_i$$_,$$_1$ $A_i$$_,$$_2$ … $A_i$$_,$ $_n$
    > 

![Screenshot 2023-01-30 at 9.32.50 PM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-30_at_9.32.50_PM.png)

## column and row representation

- suppose A is an m*n matrix with entries $A_i$$_,$$_j$

- can express as block matrix with its (m-vector) columns $a_1, a_2, … a_n$
    - $A=(a_1 a_2 … a_n)$

can be expressed as block matrix with its (n-row vector) rows $b_1, b_2, … b_m$

- $A = (b_1$ \n $b_2$ \n $… b_m)$

### example — word count matrix

- we are examining n sentences with a dictionary size of m words— how can you represent the count of each word in the sentence?
    - we define an $m*n$ matrix A
    - $A_i$$_,$$_j$ denotes the count of the i-th word in the dictionary occurring in the j-th document

> word
in
number
house
the
document
> 

> 1
1
0
0
0
1
> 

> 2
1
1
0
4
1
> 

## transposing matrices

- the transpose of an $m*n$ matrix A is denoted as $A^T$, where $(A^T)_i$$_,$$_j = A_j$$_,$$_i$ for all possible i,j
- transposing converts columns to row vectors (and vice versa)— $(A^T)^T=A$
    
    > 0 4
    7 0 = 0 7 3
    3 1   4 0 1
    > 

## addition, subtraction, scalar multiplication

- we can **add or subtract** matrices of the same size:
    - $(A+B)_i$$_,$$_j = A_i$$_,$$_j + B_i$$_,$$_j$ for all i,j
    - $(A-B)_i$$_,$$_j = A_i$$_,$$_j - B_i$$_,$$_j$ for all i,j
- for **scalar multiplication**:
    - $(aA)_i$$_,$$_j = aA_i$$_,$$_j$

### **properties**:

- $A+B=B+A$
- $a(A+B)=aA+aB$
- $(A+B)^T = A^T+B^T$

## matrix-vector product

- matrix-vector product of m*n matrix A and n-vector x, denoted as $y=Ax$, with
    - $y_i=A_i$$_,$$_1x_1+…A_i$$_,$$_nx_n$

![Screenshot 2023-01-31 at 6.02.47 AM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-31_at_6.02.47_AM.png)

### example

> word count vectors are used in computer based document analysis 
****
each entry of the word count vector is the number of times the associated dictionary word appears in the document
> 

> word 0.1;1
in 0.8;0
number 0.2;0
house 0.1;0
the 0.9;0
document 0.1;1
> 

![Screenshot 2023-01-31 at 6.05.14 AM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-31_at_6.05.14_AM.png)

![Screenshot 2023-01-31 at 6.05.53 AM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-31_at_6.05.53_AM.png)

## matrix multiplication

- we can multiply m*p matrix A and p*n matrix B
    - C=AB where $C_i$$_,$$_j = ∑^P_1A_i$$_,$$_kB_k$$_,$$_j$ for any i,j— move along the i-th row of A and the j-th column of B

![Screenshot 2023-01-31 at 6.05.53 AM.png](linear%20algebra%20basics%20f3447aa89e8241a1a993c59e51720239/Screenshot_2023-01-31_at_6.05.53_AM%201.png)