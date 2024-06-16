# statistic basics

type: lecture

## expectation of random variables

- the expected value (mean) for discrete random variable (X) is $E[X] = ∑_xx_kP(=x_k) = ∑_kx_kp_X(x_k)$ which represents the **weighted average sum of x**
    - **ex**: the expected value of rolling a dice is$E(X) = 1(1/6) + 2(1/6) +… (6)(1/6) = ∑^6$$_k$$_=$$_1 = 7/2$

**properties** 

- $E[aX] = aE[X]$
- $E[aX+b] = aE[X] + b$

### probability mass function

|  | $y=6$ | $y=8$ | $y=10$ | $p_x(x)$ |
| --- | --- | --- | --- | --- |
| $x=1$ | 1/5 | 0 | 1/5 | 2/5 |
| $x=2$ | 0 | 1/5 | 0 | 1/5 |
| $x=3$ | 1/5 | 0 | 1/5 | 2/5 |
| $p_Y(y)$ | 2/5 | 1/5 | 2/5 | 1 |

- E[X]

- E[Y]

- E[XY]
- are X and Y independent

## variance and standard dev

- the variance of $X$ is $Var(X) = E[(X-\mu)^2] = \sum_k (x_k - \mu)^2 p_x(x_k)$ which represents the **square distance from the mean** | variance can also be portrayed as $Var(X) = E[X^2] - \mu^2$
- standard deviation is simply $\sigma(X) = \sqrt{Var(X)}$ which represents the **weighted distance from the mean**
    - **ex**: the variance of rolling a dice is $Var(X) = \sum_{k=1}^6 \left[ \frac{k^2}{6} \right] - \mu^2 = \frac{1}{6} \cdot \frac{6(6+1)(2 \cdot 6 + 1)}{6} - \left( \frac{7}{2} \right)^2 = \frac{35}{12}$ — the standard deviation is $\sqrt{\frac{35}{12}} = 1.70$

---

# sampling

- **gathering random data** from a large population (e.g. measuring the height of randomly selected adults, measuring the starting salary of random CS students)

- **recording the** **results** of experiments (e.g. measuring the breaking strengths of randomly selected bolts, measuring the lifetime of randomly selected bolts)
- **assumptions**:
    1. the population is infinite (or very large) 
    2. the observations are independent 

## sample statistics

- a random sample from the population consists of independent, identically distributed random variables ($X_1, X_2, X_n$) where the values of $X_i$ are called the **outcomes** of the experiment
- a statistic is a function of $X_1, X_2, X_n$, thus a **statistic itself is a random variable**

## important statistics

- the **sample mean:** $x̄ = 1/n(X_1 + X_2 +… X_n)$
- the **sample variance:** $S^2 = \frac{1}{n-1} \sum_{k=1}^n (X_k - \bar{x})^2$
- the **sample standard deviation:** $S = √sample variance$
- the **sample median:**
    - the middle value of the **order statistic** (if [1] the observations are arranged in increasing order and [2] if n is odd)
    - the average of the two middle values (if n is even)
- the **sample range:** the difference between the largest and smallest observations

### example

- for 8 observations (0.737, 0.511, -0.083, 0.066, -0.562, -0.906, 0.358, 0.359)

| sample mean | $x̄ = 1/8(−0.737 + 0.511 − 0.083 + 0.066 − 0.562 −0.906 + 0.358 + 0.359) = −0.124$ |
| --- | --- |
| sample var | $S^2 = 1/8-1[(−0.737 + 0.124)^2 + 0.511 + 0.124)^2 +(−0.083 + 0.124)^2 + (0.066 + 0.124)^2 + (−0.562 +0.124)^2 + (−0.906 + 0.124)^2 + (0.358 + 0.124)^2 + (0.359 + 0.124)^2] = 0.297$ |
| sample sd | S = √0.297 = 0.545 |
| sample median | order statistics— -0.906, -0.737, -0.562, -0.083, 0.066, 0.358, 0.359, 0.511

$0.083+0.066/2 = -0.0085$ |
| sample range | $0.511 - (-0.906) = 1.417$ |

### sample mean vs. population mean

- expected value of $µ_x̄ = E[x̄] = E[1/n(X_1+X_2+…X_n)] = µ$

- variance of **$\sigma^2_x = Var(\bar{x}) = \frac{\sigma^2}{n} \rightarrow n \rightarrow +\infty$** and **$\sigma^2_x \rightarrow 0$**

> the expected value of the sample mean is the population mean
> 

## markov inequality

- for **discrete random** variables $X≥0$ and $e >0$:
    - $P(X≥e) ≤ E[X]/e$
        - $E[X] = ∑_x$$_≥$$_0 xp(x) ≥ ∑_x$$_≥$$_e$$xp(x) ≥ e∑_x$$_≥$$_ep(x) = eP(X≥e)$ which also holds for **continuous** random variables

## chebyshev’s  inequality

- for any random variables, we have:
    - $P(|X-µ|≥e) ≤ σ^2/e^2$
    - where $µ = E[X] = σ = √Var(x)$
    - $P(|X-µ|≥e) = P((X-µ)^2≥ e^2) ≤σ^2/e^2$

## law of large numbers

- chebyshev’s inequality— if $P(|X-µ|≥e) ≤ σ^2/e^2 (µ = E[X] and σ = √Var(x))$ then $P(|x̄-µ| ≤e) ≥1 - σ^2$$^/$$^x/e^2 = 1 - σ^2/ne^2$
    - for $n→ +∞, P(|x̄-µ| ≤e) =1$ for any $e>0$
    - **the sample mean approximates the population mean µ for very large n**
    

# central limit theorem

- suppose the population mean and standard deviation are $µ$ and $σ$
    - $µ_x̄ = E[x̄] = E[1/n(Xn)]=µ$
    - $σ^2$$^/$$^x = Var(x̄) = σ^2/n$
- **NOTE**— x̄ is approximately **general normal** (or satisfies normal distribution) for very large n and $x̄-µ_x̄/σ_x̄ = x̄-µ/σ/√n$ is approximately **standard normal** for very large n

## general normal

- $P(x≤X≤x+△x)/△x$ ****where $△x$ is very small ****

## standard normal

- $f(x) = 1/(√2π)e^-$$^1$$^/$$^2$$^x$$^2$, say $X$~$N(0,1)$
    - the cumulative distribution function is $f(x) = P(X≤x) = Φ(x)$

### general and standard normal

- for continuous random variable $X$, if for all $x e R$
    - $P(x≤X≤x+△x)/△x$, we can say $X$ is **general normal** or $X$~$N(µ, σ^2)$ where $E[x] = µ$ and $Var(x) = σ^2$
- when $µ = 0$ and $σ = 1$:
    - $f(x) = 1/(√2π)e^-$$^1$$^/$$^2$$^x$$^2$ where X is **standard normal** or $X$~$N(0,1)$ because
        

| $z$ | $Φ(z)$ | $z$ | $Φ(z)$ |
| --- | --- | --- | --- |
| 0.0 | .5000 | -1.2 | .1151 |
| -0.1 | .4602 | -1.4 | .0801 |
| -0.2 | .4207 | -1.6 | .0548 |
| -0.3 | .3821 | -1.8 | .0359 |
| -0.4 | .3446 | -2.0 | .0228 |
| -0.5 | .3085 | -2.2 | .0139 |
| -0.6 | .2783 | -2.4 | .0082 |
| -0.7 | .2420 | -2.6 | .0047 |
| -0.8 | .2119 | -2.8 | .0026 |
| -0.9 | .1841 | -3.0 | .0013 |
| -1.0 | .1587 | -3.2 | .0007 |

### difference between standard and general

- a general normal distribution can take on any value as its mean and standard deviation, however a standard normal distribution has a fixed mean and standard deviation

---

# confidence interval estimate

- $x̄-µ/σ/√n$ is approximately standard normal for very large n— the confidence interval estimate of µ is:

### example

- **population mean**: unknown

- **population sd**: $σ = 3$

- **sample size**: $n=25$

- **sample mean:** $x̄ =4.5$
- taking $z=2$, we have $P(µe[x̄-2.3/√25, x̄+3.2/√25]) = P(µe[3.3, 5.7]) = 1-2Φ(-2)=95%$% therefore, we can say that [3.3, 5.7] is the 95% confidence interval estimate of µ

# hypothesis testing

- how to test whether a hypothesis is **true** or **false**?
    1. gather data (samples)
    2. we hypothesize that a random variable has a given meaning
    3. we decide to accept or reject the hypothesis based on the data we collect

---

## descriptive vs. inferential

- **descriptive**: describes data you have but can’t be generalized beyond that (e.g. median)

- **inferential**: enables inferences about the population beyond our data (e.g. t-test)

### the differences

- **simple descriptive**: “who are the most profitable customers?”
- **hypothesis testing**: “is there a difference in value to the company of these consumers?”
- **segmentation/classification**: “what are the common characteristics of these customers?”
- **prediction**: “will this new customer become a profitable consumer? if so, how profitable?”

## statistics vs. data analytics

- always better to ask CORRELATIONAL questions

- **supervised**
    - naïve bayes, logistic regression, support vector machines, random forests, neural networks

- **unsupervised**
    - clustering, factor analysis, latent topic modeling, auto-encoders
    
> note that, unsupervised learning is **often used inside** a larger supervised learning problem
> 

---

## multinomial bayes model

- first attempt— maximum likelihood estimates using the **frequencies** in the data
    
## parameter estimation

- creating a mega-document for class j by concatenating all documents with the class label and using frequency of w in said document

## problem with maximum likelihood

- what if we have seen no training documents with the word fantastic and classified in the topic positive (thumbs-up)?
- zero probabilities cannot be conditioned away, no matter the lack of evidence!
    
# laplace (add-1)

- smoothing for naive bayes
  
## unknown words

- we **ignore** unknown words that appear in our test data but not our training data/vocab— building an unknown word model just would not help

## stop words

- other systems may also ignore very frequent words (e.g. the, a, and) by sorting the whole vocabulary by frequency in the training and calling the top 10 the stopword list and removing it
    - in some specific text classification applications, removing stop words will not help, so it is more common to NOT use a stopword list
    

# multinomial: learning

- from training corpus, extract ‘**vocabulary**’

- calculate $P(c_j)$ terms
    - for each $c_j$ in $C$ do $docs_j$ ← all docs with class $= c_j$ where $p(c_j) = |docs_j|$$/$$|$total # documents$|$

- calculate $P(w_k|c_j)$ terms for $text_j$ ← single doc containing all $docs_j$, for each word $w_k$ in vocabulary, and $n_k$ ← # of occurrences of $w_k$ in $text_j$, making $P(w_k|c_j)$ ← $n_k+a/n+a|$vocabulary$|$

### example

| cat |  | documents |
| --- | --- | --- |
| training | -
-
-
+
+ | just plain boring
entirely predicable and lacks energy
no surprises and very few laughs
very powerful
the most fun film of the summer |
| test | ? | predictable with no fun— drop “with” |

- **prior from training:**
    - P(-) = 3/5
    - P(+) = 2/5
    

- **likelihoods from training:**
    - P(”predictable”|-) = 1+1/14+20 | P(”predictable”|+) = 0+1/9+20
    - P(”no”|-) = 1+1/14+20 | P(”no”|+) = 0+1/9+20
    - P(”fun”|-) = 0+1/14+20 | P(”fun”|+) = 1+1/9+20
    
- **scoring the test set**:
    - $P(-)P(S|-) = 3/5(2*2*2/34^3) = 6.1*10^-$$^5$
    - $P(+)P(S|+) = 2/5(1*1*2/29^3)=3.2*10^-$$^5$

## estimating n-gram probabilities

> A. <s> I am Sam </s> 
B. <s> Sam I am </s>
C. <s> I do not like green eggs and ham </s>
> 

- P(I|<s>) = 2/3 = 0.67
    - A and C
- P(do|I) = 1/3
    - C
- P(Sam|<s>) = 1/3
    - B

- P(</s>|Sam) = 1/2
    - A — ignore whatever doesn’t have “Sam”
- P(Sam|am) = 1/2
    - B — ignore whatever doesn’t have “Sam”
