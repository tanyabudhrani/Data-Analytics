# calculus basics

type: lecture

# functions

- y is a function of x, written with $y = f(x)$
    - every value of x corresponds to one and only one value of y
    - x is the **independent variable** while y is the **dependent variable** (e.g. distance travelled per hour y is a function of velocity x)

## optimization of a function

- given a function f($x_1, x_2, …, x_n$) where $x_1, x_2,…,x_n$ are variables or parameters
- **optimization**: finding a set of variables $x_1, x_2, …, x_n$ that maximize or minimize f($x_1, x_2, …, x_n$)
    - example— you selected 3 classes this semester, each with different effects on the GPA (which you want to maximize via priorly knowing the number of hours you should spend on each class); here, the GPA is the **value of the function** while the number of hours is the **function variables**

## a recipe for machine learning

1. given training data: ${x_i, y_i}^N$$_i$$_=$$_1$
2. choose each of these: 
    1. decision function $(ŷ = fθ(x_i))$
        1. examples— linear regression, logistic regression, neural network
    2. loss function: **$ℓ(ŷ,y_i) ∈ ℝ$**
        1. examples— mean-squared error, cross entropy 

# derivatives

- the derivative of f(x) is the **slope of the tangent line** (instantaneous rate of change) at $(x, f(x))— dy/dx = f’(x)$
- the process of calculating the derivatives of a function is called **differentiation**
    - example— $y = x^2 = lim(2x+Δx) = 2x$ (also written as $dy = 2xdx$ or the differential $dy$ in terms of the differential $dx$)
- used to estimate the output difference $Δy$ in terms of the small input difference $Δx$

### some useful formulas

| rules  | formula  | example |
| --- | --- | --- |
| power rule  | $d(x^p)/dx = px^{p-1}$ <br> note— $dx/dx = 1$ (y = x has a slope of 1 everywhere)  | $d/dx (x^3) = 3x^{3-1} = 3x^2$ <br> $d/dx(1/2) = \frac{1}{2}x^{-1/2}$ |
| exponential rule  | $d(b^x)/dx = b^x \ln b$ | $d/dx (e^x) = e^x \ln e$ ($\ln e = 1$) → $e^x$ |
| logarithm rule  | $d(\log_b x)/dx = \frac{1}{x \ln b}$ | $d/dx (\ln x) = \frac{1}{x}$ |
| derivatives for constants | $dC/dx = 0 $ | $d/dx(6) = 0$ |

### properties of derivatives

- for any constant c and any differentiable function f(x), $d[cf(x)]/dx = C(d[f(x)]/dx)$
- for any two differentiable functions: f(x) and g(x)
    
    
    | sum and difference rules | $d[f(x) +- g(x)]/dx = df(x)/dx +- dg(x)/dx$ |
    | --- | --- |
    | product rule | $[f(x)g(x)]’ = f’(x)g(x) + f(x)g’(x)$ |
    | quotient rule | $[f(x)/g(x)]’ - f’(x)g(x) - f(x)g’(x)/[g(x)]^2 $ |
    | chain rule | $[f(g(x))]’ = f’(g(x))*g’(x)$ |
    - examples
       
## partial derivatives

- a function may have multiple variables (e.g. $f(x,y) = x^2y$ and $g(x_1,x_2,x_3) = x_1x_2x_3$)
- a partial derivative of a function of several variables is its derivative with respect to one of those variables, with the others held constant— **$∂f/∂x = df/dx$**
    - **example**: $f(x,y) = 100-x^2-y^2$ → **$∂f/∂a = -2x$** or ****$∂x/∂f = -2y$

# gradient

- given a function $f(x_1,x_2,…x_n)$ with multiple variables $x_1,x_2,…x_n$— how do we keep track of all the partial derivatives for each variable? a **gradient** is a **vector** holding all partial derivatives  $∇f = (∂f/∂c_1, ∂f/∂x_2,…,∂f/∂x_n)$
- ∇f points in the direction of the greatest rate of change or the “steepest ascent”
- **gradient descent algorithm** is used for the training of most machine learning models

### visualization

> **q**: given current w, should we make it bigger or smaller?
> 

> **a**: move w in the reverse direction from the slope of the function
> 
- the objective is to find the gradient of the loss function at the current point, and then moving in the opposite direction

### training example

- suppose we’re distinguishing cat from dog images
    1. we would build a model of what’s included in a cat image (e.g. whiskers, ears, eyes) then assign a probability to the images 
    2. then, do the same for the dog images 
    3. run both models and see which one fits better

## discriminative classifiers

- given input/output pairs ($x^i,y^i$):
    - a **feature representation** of the input— for each input observation $x^i$, a vector of features $[x_1, x_2,…x_n]$; feature $j$ for input $x^i$ is $x_j$, move completely $x_j$$^i$, or even $f_j(x)$
    - a **classification function** that computes $ŷ$, the estimated class, via $p(y|x)$, like the **sigmoid** or **softmax** functions
        - finds the outcome of the dependent variable in the model equation
    - an objective function for learning, like **cross-entropy loss**
        - metric used to measure how well a classification model performs by evaluating the loss or the error between 0 and 1— 0 being a perfect model
    - an algorithm for optimizing the objective function: **gradient descent**

### example of classification features

- for feature $x_i$, weight $θ_i$ tells us how important $x_i$ is
    - $x_i =$ “review contains ‘awesome’”: **$θ_i = +10$**
    - $x_j =$ “review contains ‘abysmal’”: **$θ_j = -10$**
    - $x_k =$ “review contains ‘mediocre;”: **$θ_k = -2$**


## a probabilistic classifier?

- $z = θ^T x$ is a number, and we want to use a function of z that goes from 0 to 1

- we need to formalize “sum is high” using a **principled classifier** that gives us a probability and can tell us:
    - $p(y = 1|x;θ)$
    - $p(y=0|x;θ)$
    - $y = s(z) = 1/1+e^-$$^z$
    

# logistic regression

> the equation, for anyone confused, begins with the transposition of θ and x, where θ represents the weight vector and x represents the feature vector— the result of their product is a scalar value which is then passed through the sigmoid activation function σ to produce the final probability
> 

## another recipe for machine learning

1. given training data: $\{(x_i, y_i)\}_{i=1}^N$
2. choose each of these: 
    1. **decision function** $(\hat{y} = f_\theta(x_i))$
        1. examples— linear regression, logistic regression, neural network
    2. **loss function**: **$\ell(\hat{y}, y_i) \in \mathbb{R}$**
        1. examples— mean-squared error, cross entropy 
3. define goal: $\theta^* = \arg\min \sum_{i=1}^N \ell(f_\theta(x_i), y_i)$
    1. using argmin to calculate the values of $\theta$ that result in the lowest possible value of the total loss— where the optimal parameters $\theta^*$ are learned from the training data and used to make predictions for new, unseen data 
4. train with SGD: $\theta^{(t+1)} = \theta^t - \eta_t \nabla \ell(f_\theta(x_i), y_i)$
    1. this is an update step— where $\theta^t$ is the current value of the model’s parameters, $\theta^{(t+1)}$ is the updated value of the model parameters, and $\eta_t$ is the learning rate or the size of the step 
    2. the gradient of the loss function,  $\nabla \ell(f_\theta(x_i), y_i)$, gives the direction of the steepest descent with respect to the model’s parameters— the loss function measures the difference between the model’s prediction $f_\theta(x_i)$ and the true label $y_i$ for $(x_i, y_i)$

## backpropagation

- a supervised learning algorithm used to train neural networks by calculating the loss function with respect to the model parameters, then allowing the model to be updated in a direction that minimizes the loss

| forward pass | input data is processed through the network to make a prediction— the prediction is then compared to the true label to compute the loss  |
| --- | --- |
| backward pass | the gradients of the loss, with respect to the model parameters, are calculated by computing the gradients at each layer then propagating backwards— this is done based on the CHAIN RULE OF DIFFERENTIATION  |
| weight update | after the gradients have been computed, the model parameters are updated using gradient descent by subtracting the gradient of the loss with respect to each weight and bias from their current value  |
| repeat | the forward and backward passes are repeated multiple times until convergence, until a maximum number of iterations is reached |

## areas under function graph

- given y = f(x), nonnegative (f(x) ≥ 0) and continuous (with no breaks or jumps)— $F(x) = ∫^x_af(t)dt$ [antiderivative] the area under the graph of $f(x)$ in the interval $[a,x]$
    - $F(x+∆x) - F(x) =$ area under the graph of $f(x)$  in $[z,x+∆x] = f(x)*∆x$
    - when $∆x → 0$, $z→x$
    - $f(

# integrals

- **definite integrals**: $F(x) = ∫^x_af(t)dt$
    - areas under $f(x)$ in the interval of $[a,x]$
    - in this context, $f(x)$ is called the **integrand**
    - F(x) is an **antiderivative** of f(x)

- **indefinite integrals**: ∫f(x)dx = F(x) + C [arbitrary constant]
    - $f(x) = 1/10x^1$$^0 + C$ is the general antiderivative of $f(x) = x^9$  OR $∫x^9dx = 1/10x^1$$^0+C$
    

### properties of integrals

- for any constant c and any integrable function f(x)— $∫[cf(x)]dx = c∫f(x)dx$
    
    
    | sum and difference rule | $∫[f(x)+-g(x)]dx$ $= ∫f(x)dx +-∫g(x)dx$ |
    | --- | --- |
    | power rule | $∫u^pdu = $
    
    if $p ≠ -1$, $u^p$$^+$$^1/p+1 + C$
    if $p = -1$, $ln|u| + C$ |
    | exponential rule | $∫e^udu = e^u+C$ |
    | chain rule | $∫(x^5+2)^95x^4dx$… |
   
