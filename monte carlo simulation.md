# monte carlo simulation

type: lecture

# monte carlo simulation

- a method of estimating the value of an unknown quantity using the principles of inferential statistics
    - **population**: a set of examples
    - **sample**: a proper subset of a population

> a random sample tends to exhibit the same properties as the population from which it is drawn
> 

### coin flipping

- given a single coin, estimate fraction of heads you would get if you flipped the coin an infinite number of times
    - if you’ve flipped two coins, how certain will you be that the next will come up heads?
    - flipping 100 coins would give you a low confidence of guessing the next result

## difference in confidence

- confidence in our estimate depends on two things
    - size of sample (e.g. 100 vs 2)
    - variance of sample (e.g. all heads vs 52 heads)
- as variance grows, we need larger samples to have the same degree of confidence

# monte carlo principal

- in repeated independent tests with the same actual probability $p$ of a particular outcome in each test, **the chance that the fraction of times that outcome occurs differs from p converges to zero as the number of trials goes to infinity**
    - if deviations from expected behavior occur, these deviations are likely to be evened out by opposite deviations in the future

## sampling space of possible outcomes

- never possible to guarantee perfect accuracy through sampling
- the number of samples we need to look at before we can have a justified confidence on our answer depends on the **variability** in the underlying distribution

# estimating π

- what is the ratio of the area of the circle to the area of the square? $p = πr^2/(2r)^2 = π/4$
- randomly generating points (x, y)
    - generate 1000 points (x,y), -1 ≤ x,y ≤ 1
    - calculate the distance of each point from (0,0) and determine whether each point is inside the circle— multiply the ratio by 4 to estimate π

```r
no_of_points <- 1000 
#runif samples from a uniform distribution 
x <- runif(no_of_points, -1, 1)
y <- runif(no_of_points, -1, 1)

#complete the distance of each point from (0,0) 
distance <- sqrt(x^2 + y^2) 

#boolean vector to indicate if each point is within the circle 
within_circle <- ifelse(distance < 1, TRUE, FALSE) 

#compute proportion of points within circle/outside circle 
#table() counts the number of unique elements (TRUE/FALSE)
v <- table(within_circle) 

#compute and print PI 
pi <- v["TRUE"]/(v["TRUE"] + v["FALSE"]) *4 
print(pi) 
```

# product demand

- suppose the demand for a product is governed by the following discrete random variable:
    
    
    | demand (x)  | probability |
    | --- | --- |
    | 10,000 | 0.1 |
    | 20,000 | 0.35 |
    | 40,000 | 0.3 |
    | 60,000 | 0.25 |
- how to simulate daily demand for 100 days and sum them?
    
    ```r
    x <- c(10000, 200000, 40000, 60000)
    probability <- c(0.1, 0.35, 0.3, 0.25) 
    
    #sampling with replacement
    demand <- sample(x, 100, replace=TRUE, prob=probability)
    
    sum(demand) #3470000
    ```
    

# coin flipping

- given n = 100 flipping of a fair coin, what is the chance that we will get k = 4 heads-up or less?
    
    ```r
    n <- 10 #no. of coin flips 
    k <- 4 #no. of heads
    runs <- 10000 #number of trials 
    
    #one trial simulates the flipping of a coin for 10 times
    trial <- function() {
    	sum(sample(c(0,1), n, replace=TRUE)) # of heads
    	}
    
    #conduct 1000 trials 
    result <-replicate(runs, trial())
    t <- table(result) 
    print(t) 
    ```
    
- given n = 10 flipping of a fair coin, what is the chance that we will get k = 4 heads-up or less
    
    ```r
    #conduct trials 10000 times
    result <- replicate(runs, trial())
    t <- table(result) 
    print(t) 
    barplot(table(result))
    
    #normalize 
    barplot(table(result)/runs) 
    ```
    

## distributions

- **binomial**: the probability of getting k heads in n trials with the formula $(nCk)(p^k)(1-p^n$$^-$$^k)$

- **probability density**:
    
    ```r
    #dbinom(x, size, prob) probability density function
    #prob(3 head out of 10 coin flips) 
    dbinom(3, size=10, prob=0.5) 
    ```
    

- **cumulative**:
    
    ```r
    #pbinom(q, size, prob, lower.tail) calculates cumulative 
    
    #prob <= 3 heads out of 10 coin flips 
    pbinom(3, size=10, prob=0.5, lower.tail = TRUE) 
    
    #prob > 3 heads out of 10 coin flips 
    pbinom(3, size=10, prob=0.5, lower.tail = FALSE)
    ```
    

# stock price prediction

- the price of a stock today is $30
- in prior data, the price of the stock increases a factor of mean 1.001k with standard deviation of 0.005 (satisfies $N(1.001, 0.005^2)$)

```r
#generate the price change for 365 days 
days <- 365
changes <- rnorm(days, mean=1.001, sd=0.005) 

#returns a vector whose elements are the cumulative products of the elements of the argument 
price <- cumprod(c(30, changes)) #30*1st random no * 2nd random no...

#plot the line chart 
plot(price, type="l") 
```

# hits on a website

- we are interested in estimating the number of hits on a certain website during a fixed time interval with an average rate of 5 per minute

## poisson

- often used to model rare events that are extremely unlikely to occur within a very short period of time or simultaneously
    - also describes the probability of a given number of events occurring in a fixed interval of time and space
- these events occur independently with a known average rate of time since the last event
- poisson distribution has a single parameter λ > 0 being the average number of occurrences of the considered events ($e^λ(λ^k/k!)$**)**

### example

- find the probability that there will be exactly 17 hits in the next 3 minutes
    
    ```r
    dpois(17,15) #probability of 17 events with a rate of 15
    
    #cumulative probability distribution
    #ppois(x, lambda, lower.tail) 
    ppois(17, 15, lower.tail = TRUE)
    
    #average rate is 5 
    rate < 5
    x <- 1:20 
    p <- dpois(x, rate) 
    barplot(p, names.arg=x) 
    ```
    
- what if we want to estimate the waiting time for the next hit?

## exponential distribution

- used to model the time that elapses before an event occurs (e.g. the time between two events)

### exponential vs. poisson

- the inter-arrival times of events in a poisson process with rate λ is exponential and mean 1/λ
- what is the average time between two hits (5 hits/min)?
    
    ```r
    #generates n random numbers from exponential distribution with certain rate λ
    waitingTimeWebsite <- rexp(50, 5) 
    ```
    
- what if want to estimate the waiting time for the next hit?
    
    ```r
    hist(waitingTimeWebsite, breaks = 20)
    ```
    
# queueing system for atm

| we will model a simple queueing system that represents customers arriving at and using an atm |
| --- |
| customers arrive at an atm and perform a number of atm transactions  |
| one customer can use atm at a time— after completing their transactions, the customers take their cards and leave |
| when the atm is in use, the next customers have to wait until the previous customer has left |

- the first customer arrives at the ATM at 1 min and takes 1.3 minutes to complete his transactions

- the second customer arrives at 2 min and takes 0.5 minutes to complete his transaction
- a customer’s waiting time depends on his arrival time and the time at which the previous customer will leave the atm but there is no need for the first customer to wait
    - when determining if customer i should wait, we need to check when customer i-1 have completed his transactions when customer i arrives

## simulation

- suppose we want to simulate 100 customers coming to the atm
- the **service time** follows a normal distribution with a mean of 0.9 minutes and a standard deviation of 0.25 minutes $N(0.9 0.25^2)$
- the **inter-arrival time** of customers follows an exponential distribution with a rate of 1 customer per minute (λ=1)

```r
#service time can be sampled from the normal distribution
serviceTime <- rnorm(100, 0.9, 0.25) 
hist(serviceTime, breaks=50) 

#the inter-arrival time of customers can be sampled using rexp
interArrivalTime <- rexp(100,1)
hist(interArrivalTime, breaks=50)

#cumsum() computes the actual arrival time for 100 customers
arrivalTime <- cumsum(rexp(100, 1))
arrivalTime
```

```r
set.seed(2) #ensures reproduction  
serviceTime <- rnorm(100, mean = 0.9, sd = 0.25)

firstArrival <- 1.0 
interArrival <- rexp(99, 1)
arrivalTime <- cumsum(c(firstArrival, interArrival))

leaveTime <- 0.0
waitTime <- 0.0
waitTimeAll <- array(0, 100)

for(i in 1:100) {  
	waitTime <- max(0, leaveTime-arrivalTime[i])  
	leaveTime <- arrivalTime[i] + waitTime + serviceTime[i]  
	waitTimeAll[i] <- waitTime
}

plot(waitTimeAll, xlab = "Customer ID", ylab = "Wait time")
```
