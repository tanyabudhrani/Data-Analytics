# probability basic

type: lecture

### probability vs. data analytics

- in analytical processes, we usually use **random variables** to describe the data because we are,
    - turning mathematical processes into real-life problems
    - making the data computable
    - discovering the patterns and trends behind data
    - allowing the analysis of distribution and statistics
- probability helps us predict how likely it is that an event will occur

# probability

- a numerical description of how likely an event is to occur and/or how likely that a proposition is true
    - we run a random experiment $n$ times, during which an event $A$ occurs $m$ times, then we can say the frequency of $A$’s occurrence is $f_A = m/n$
    - when $n$ is large enough, $f_A$ will be very close to value $p$, which is defined as the probability of $A$ to occur (i.e. $lim [n → ∞] f_A = p(A) = p$)

| sample space | the set of all possible outcomes of an experiment  | coin flipping— the sample space is {$H, T$} which both have a 50% chance of happening |
| --- | --- | --- |
| event | subsets of the sample space | rolling a dice once— sample space is {$1, 2, 3, 4, 5, 6$}, each of which have a $1/6$ chance of happening

BUT the chance that event E {$1, 3, 4$} will occur is $1+1+1/6 = 1/2 $ |

## probability function

- assigns a real number (probability of E) to every event— function must satisfy the following basic properties:
    1. $0≤P(E)≤ 1$
    2. $P(S) = 1$
- for any disjoint events, $E_i(i=1,2,…n)$, we have $P(E_1UE_2U…E_n)=P(E_1)+ P(E_2) +… P(E_n)$
- **probability distribution:**
    - a listing of the probabilities for every possible value that the random variable might take
        
        **rolling a dice once** 
        
        | X | P(X) |
        | --- | --- |
        | 1 | 1/6 |
        | 2 | 1/6 |
        | 3 | 1/6 |
        | 4 | 1/6 |
        | 5 | 1/6 |
        | 6 | 1/6 |

### some notions

- $P(EUF)$: the probability that E or F occurs
- $P(E,F)$ or $P(EF)$: the probability that both E and F occurs
- $P(E^c)$: the probability that E does not occur

### more examples

- if the coin is flipped twice, what is the probability of two heads?
    - $P(H, H) = (1/2)(1/2) = 1/4$
- if the coin is flipped twice, what is the probability of two heads, given that we know the first toss was a head?
    - $P(H,H | H$$)$ $= 1/2$

## conditional probability

- if E and F are events, then P(E|F) is the conditional probability of E, given F— P(E|F) = P(E,F)/P(F)

### example one

- suppose we draw a card from a shuffled set of 52 playing cards

- what is the probability of drawing a queen, given that the card drawn is of suits hearts?
    - $P(Q|H) = P(Q,H)/P(H) = 1/52/1/4 = 1/13$

- what is the probability of drawing a queen, given that the card drawn is a face card?
    - $P(Q|F) = P(Q,F)/P(F) = 4/52/12/52 =1/3$
    

### example two

- it is well known that bob has two children, charlie and teddy— however, no one knows whether they are sons or daughters
    - one day you meet bob and he tells you that he has at least a daughter; what is the probability that both teddy and charlie are daughters?
        - if it is known that he has at least one daughter, the sample space will be {GG, GB, or BG}
        - $P(GG|GUG) = P(GG)/P(GUG) = (1/2)(1/2)/(3/4) = 1/3$
    - on another day, you meet bob again and he says that he was with his beautiful daughter and introduce that she was teddy; what is probability that both teddy and charlie are daughters?
        - since, you have observed that bob has a girl, you have more evidence that he may have two daughters— knowing that teddy is a girl, s = {GG, GB}
        - $P(GG|G) = P(GG)/P(T) = 1/4/1/2 = 1/2$

## law of total probability

- sometimes, the computation of P(E) will be easier if we condition E on another event F, namely from:
    - $P(E) = P(E(FUF^c)) = P(E,F) + P(E,F^c)$
    - also, $P(E,F) = P(E|F)P(F)$ and $P(E,F^c) = P(E|F^c)P(F^c)$ and $P(E) = P(E|F)P(F) + P(E|F^c)P(F^c)$

### example

- an insurance company holds the following data concerning the probability of an insurance claim— for people under 30, the probability is 0.04 and for people over 30, the probability is 0.02— if it is known that 30% of the targeted population is under 30, what is the probability of an insurance claim for a randomly chosen person?

## bayes’ formula

- sometimes, we need a formula that inverts conditions (e.g. predicts an event conditioned on some observations)
    - since $P(EF) = P(E|F)P(F)$ and $P(EF) = P(F|E)P(E)$ — $P(F|E) = P(E|F)P(F)/P(E|F)P(F) + P(E|F^c)P(F^c)$

### example

- suppose 1 in 1,000 persons has a certain disease
- for 99% of the diseased persons, a test will yield positive results | for 5% of the healthy persons, a test will also yield a positive result— what is the probability of a positive test?

## independent events

- two events E and F are independent if P(E,F) = P(E)P(F)— however, knowing that an event occurred, doesn’t change the probability of E

### example

- two different numbers are drawn at random from {1, 2, 3, 4}— if we don’t consider the order of the two numbers, then what is the sample space S?
    - S = {1, 2}, {1, 3}, {1, 4}, {2, 3}, {2, 4}, {3, 4}
- if $X = i+j$ and $Y = |i-j|$, which pairs are independent?
    - **Q1**: $X=5$ and $Y=2$— $P(X=5|Y=2) = P(X=5,Y=2)/P(Y=2) = 0$
        - $X=5 = 2/6 ≠ 0$ — DEPENDENT
    - **Q2**: $X=5$ and $Y=1$— $P(X=5|Y=1) = P(X=5,Y=1)/P(Y=1) =$ 1/6/3/6 = 1/3
        - $X=5 = 2/6 = 1/3$ — INDEPENDENT

## supervised machine learning

- **input**:
    - a document $d$
    - a fixed set of classes C = {$c_1, c_2, … c_j$}
    - a training set of m hand-labeled documents $(d_1,c_1)$,…,$(d_m,c_m)$

- **output**:
    - a learned classifier $y:d → c$
    

### bayes’ rule applied to documents and classes

- for a document $d$ and a class $c$— $P(c|d) = P(d|c)P(c)/P(d)$
    - our goal is to maximize $P(c|d)$ with a $cEC$

## naive bayes classifers

- **argmax**: the arguments of the maximum (e.g. find the optimal value of c which maximizes P(c|d))

## multinomial bayes

- **bag of words assumption**: assume position doesn’t matter
- **conditional independence**: assume the feature probabilities $P(x_i|c_j)$ are independent given the class $c$— $P(x_1, … x_n | c) = P(x_1 | c)P(x_2 | c)P(x_3 | c)$
  

### applying multinomial naive bayes to text classification

- position ← all word positions in the test document
- however, multiplying lots of probabilities can result in floating-point underflow— luckily, log(ab) = log(a) + log(b), so we can sum logs of probabilities instead of multiplying them

### log space

- the parameters (e.g. ($cj$) and ($x_i|c_j$)) will be estimated from the data
- we can do this since **log doesn’t change the ranking of the classes** (class with the highest probability still has the highest log problem)— the model is now just the max of the sum of the weights (a **linear function** of the inputs) which is why **naive bayes is a linear classifier**

# probabilistic language models

| machine translation | P(high winds tonight) > P(large winds tonight) |
| --- | --- |
| spell correction | P(about fifteen minutes from) > P(about fifteen minuets from)  |
| speech recognition | P(i saw a van) > P(eyes awe of an) |

## language model

- **the goal**: to compute the probability of a sentence or a sequence of words— $P(W) =$ P($w_1$, $w_2$, $w_3$, $w_4$,…$w_n$)

- **related task**: the probability of an upcoming word— $P(w_5 | w_1, w_2, w_3, w_4)$

## computing P(W)

- computing joint probability using the **chain rule**
    - **two variables**: $P(A,B) = P(A)P(B|A)$
    - **more variables**: $P(A,B,C,D) = P(A)P(B|A)P(C|A,B)P(D|,A,B,C)$
- **example**:
    - P(”its water is so transparent”) = P(its)*P(water|its) * P(is|its water) * P(so|its water is) * P(transparent|its water is so)— however, it is very complex to solve something like this, so we can actually simplify it with the markov assumption

## markov assumption

- if a word is **too far away** from the word we want to predict, then we can **disregard** that word— P(the|its water is so transparent that) = P(the|that) or P(the|its water is so transparent) = P(the|transparent that)

### unigram model

- model based on single words
- $P(w_1w_2…w_n) = IIP(w_i)$
    - using **frequent** words

### bigram model

- models based on compound words
- $P(wi|w_1w_2…w_i$$_-$$_1) = P(w_i|w_i$$_-$$_1)$
    - using the **co-occurences** of neighbors

> while we can extend the model to trigrams, 4-grams, 5-grams, etc, this is an insufficient model of language since language has long-distance dependencies (**ex**: the computer which i had just put into the machine room on the fifth floor crashed)
>
