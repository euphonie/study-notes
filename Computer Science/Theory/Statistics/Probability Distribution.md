> Content obtained from Udemy's Probability for Statistics and Data Science course [Course link](https://telusinternational.udemy.com/course/probability-for-statistics-and-data-science)

# Probability Distribution

- A distribution shows all the possible values a variable can take and how frequently they occur. 

Having $Y$ as the actual outcome of an event, and $y$ as one of the possible outcomes. $P(Y=y)\;or\;P(y)$  is the probability of the outcome being a particular $y$. $P(y)$ is also known as the **probability function**.

- A **probability frequency distribution**, measures the likelihood of an outcome given how often it is featured in the sample space. The possibilities can be finite or infinite according to the variable that is being measured.

### Distributions are defined by two characteristics: 
- **Mean**. That is the average value of the distribution. It is denoted by $\mu$.
- **Variance**. How spread out is the data from the center. The more disperse is the data, the higher the variance will be. It is denoted by $\sigma^2$. It has to be noted that the values of the variance are measured in squared units. E.g. $seconds^2$

### Types of data
- **Population data**. "All" the data of a topic.
- **Sample data**. A part of all the data.  The variables used to denote mean and variance change when using samples. These are: $\bar{x}$ for **sample mean** and $S^2$ for **sample variance**.

### Standard Deviation

Is calculated by the square root of variance. $\sqrt{\sigma^2}$. It is denoted by $\sigma$ when is a population and an $s$ when it is a sample. It holds the same units as the mean.

- It should be noted that everything between a distribution's boundaries $(\mu-\sigma, \mu+\sigma)$, is within 1 standard deviation $\sigma$ away from the mean.
	- If the percentage of data, within the standard deviation is high, the data is less dispersed.
	- If the percentage of data, within the standard deviation is low, the data is more dispersed.

### Mean and variance relation

A constant relationship between mean and variance is denoted by: 

$$
\sigma^2 = E((Y-\mu)^2) = E(Y^2) - \mu^2
$$

## Types of Distributions

### Discrete distributions

Are used on events that have a finite number of outcomes. Like rolling a dice or picking a card. Can be expressed as a table, a graph or a formula. 

- Is important to check that every unique outcome has a probability assigned to it.
- Is more interesting  to analyze the result of an interval rather than an individual value.
	- For this, all that it takes is adding up all the probabilities for all the values in the range

![Example of adding ranges](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/ex-add-ranges.png)

$$
P(Y \leq y) = P[Y < (y+1)]
$$
	

#### **Equiprobable (Uniform Distribution)**
Events where all outcomes are equally likely to occur. The distribution is denoted as: 

$$
U(a,b) \\
X \sim U(3,7)
$$

The last part means: variable X follows an uniform distribution ranging from 3 to 7.

For this types of distributions, it applies:
1. The mean and the variance are uninterpretable.
2. The mean and the variance present no predictive power.


#### **Benoulli Distribution**
Events that can only have true or false, or only two possible outcomes. Any event having two outcomes can be a Bernoulli event, it's just needed to assign which event falls for true and which one for false. This distribution is denoted as: 

$$
Bern(p) \\
X \sim Bern(p)
$$
Which means: variable X follows a Bernoulli distribution with a probability of success equal to $p$.

For this type of distributions, it applies: 
1. It comprises of 1 trial, and 2 possible outcomes
2. We either have the probability of $p$ or we have past data indicating some experimental probability.
3. Which event corresponds to 1 and which one to 0 has to be defined. Making $E(x) = p \;or\;E(x)= 1- p$
4. The higher probability is usually denoted with $p$ and the lower one $1 -p$. Having, $p > 1-p$.
5. Value of 1 is assigned to $p$ and 0 to $1-p$. That way the expected value expresses the likelihood of the favoured event. 
$$
E(X) = 1*p + 0*(1-p) = p
$$
and 
$$
\sigma^2 = (x_0 - \mu)^2 * P(x_0) + (x_1 - \mu)^2 * P(x_1) \\
\sigma^2 = (0-p)^2*(1-p) + (1-p)^2*p \\
\sigma^2 = p(1-p) \tag{always true}
$$

![Bernoulli distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/bernoullig.png)

#### **Binomial Distribution**

The outcomes of each iteration are two as in Bernoulli, but the experiment consists on many iterations. E.g. the likelihood of getting head two times, when making a 3-iterations coin toss. This distribution is denoted as: 

$$
B(n, p)  \\
X \sim B(10, 0.6) \\ 
\tag{n = No. of trials, p = Prob. of success e/trial}
$$
Which means, variable X follows a binomial distribution, with 10 trials and a likelihood of succeed of 0.6 in each individual trial.

For this type of distributions, it applies:
1. This type of distribution is a sequence of identical Bernoulli events.
2. A binomial distribution can be expressed as a Bernoulli distribution with a single trial. $Bern(p) = B(1,p)$
3. The expected value of a binomial event $E(Binomial\;event)$, is the number of times we expect to get a specific outcome.
4. Graph represents the outcome of obtaining an specific value a number of times.

![Binomial Distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/binomial.png)

5. The probability function of the binomial distribution $p(y)$, is used to obtain the likelihood of getting  given outcome a precise number of times.

$$
P(desired\;outcome) = p \\
P(undesired\;outcome) = 1-p
$$

Then to get how likely is to get $y$ desired outcomes from $n$-trials, the likelihood of $n-y$ also has to be computed, or else the result would be to compute the likelihood of a desired outcome **at least** $y$ times.

![Notice about probability function for binomial distributions](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/probfuncbino.png)

It can also be posed as, using the combinations notation: 

$$
{n \choose y} = C^n_y
$$

With this logic, the number of ways in which 4 out of 6 trials can be successful is the same as picking 4 elements out  of a sample space of 6.
Resulting in the formula: 
$$
P(y) = {n \choose y} * p^y * (1-p)^{n-y}
$$

and 

$$
E(Y) = p * n \\
\sigma^2 = n* p * (1-p)
$$

#### **Poisson Distribution**

Used to test how unusual an event frequency is for a given interval. E.g. Given a player that scores 35 points per game. What is the probability of the player scoring 12 points on the first quarter of the game. It is denoted as:

$$
Po(\lambda) \\
Y \sim Po(4)
$$

Which means: Variable Y follows a poisson distribution with $\lambda = 4$.

For this type of distributions, it applies:
1. Requires to know how often an event occurs for an specific period of time or distance.
	- E.g. A firefly might light up 3 times in 10 seconds. A poisson distribution could be used to determine how likely it is to light up 8 times during a 20 seconds interval.

![Poisson Distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/poissong.png)

E.g. An event that usually occurs 4 times a day, has an unusual behaviour one day when it occurs 7 times. To compute the likelihood of that event happening those 7 times during a day, it would be:
- $\lambda = 4$
- Interval = One day
- $y=7$
- $Po(4)$

Its probability function would be: 
$$
P(Y) = \frac{\lambda^y e^{-\lambda}}{y!}
$$

Adding the values from the example, it would be: 
$$
P(7) = \frac{4^7e^{-4}}{7!} \sim  0.06
$$

The expected value would be:
$$
E(y) = y_0\frac{\lambda^{y_0} e^{-\lambda}}{y_0!} + y_1\frac{\lambda^{y_1} e^{-\lambda}}{y_1!} + ...  \\
E(y) = \lambda
$$

and 
$$
\mu = \sigma^2 = \lambda
$$

Finally, for computing a poission distribution's interval, the joint probability is computed the same as in discrete distributions; using the joint probability of all individual elements.

### Continuous distributions

Are used on events that track time or distance. This are curves in comparison to bars used in discrete distributions.

- This distributions have infinite many consecutive outcomes.
- Sample space is infinite.
- Frequency for each distinct value cannot be recorded. Therefore, is usually represented with a graph; probability distribution function (**PDF**).
	- Is denoted as $f(y)$, as this function returns probability it holds that $f(y) \geq 0$.
	- The resulting curve from the function is called the **Probability distribution Curve (PDC)**
- Using the formula, $P(y) = \frac{favourable}{sample\;space}$, and given that $space = \infty$, probabilities can be considered extremely insignificant. 
- This means the probability of an event for a continuous distribution can be assigned as 0. $P(X) = 0$. 
- Therefore, is also accepted to assume $P(x > X) = P(x \geq X) = 0$.

Given this, a new function is described. The **Cumulative Distribution Function (CDF)**. This function describes all the values from below or equal to a defined outcome. Like $F(y) = P(Y \leq y)$.

Since no value of probability can be equal to $-\infty$,  $F(-\infty) = 0$. Equally if given $F(\infty)$ would be equal to $1$. As it comprises all possible outcomes.

CDFs are useful for estimating intervals from a continuous probability function. having $p(b > x > a)$. The area of the density curve is then found by: 

$$
\int_a^b p(x) dx
$$

Another way of describe this would be, that the Cumulative Distribution Function is the probability of the interval between $(-\infty; y)$.

Using this we can compute PDF from CDF and viceversa applying the formulas:
- PDF to CDF. $\int_{-\infty}^y p(y)dy = F(y)$
- CDF to PDF. $p(y) = F(y)\frac{d}{dy}$

Computing Expected values and variance would be:

$$
E(y) = \int_{-\infty}^\infty yp(y) dy
$$
$$
var(y) = E(y^2) - E(y)^2
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjU0NjUxOTYsMTM5NjIyOTM2LDQ2OD
kzNTA0NCwtMjA3MTU0NjU0Nyw2MjQxNDE4MDksLTg4MTM0NDgz
NywtMjExMjExMTkxOSwtMTAzOTAwNTIwNiw4MDg5NDgxMTMsLT
E2MjIyMzQyNDksLTE0MDczNjg2NjUsMjI3MTc5NTg0LC02MjQz
Mjg2LDExNTM0ODgxNDEsLTEyODA1MzM2NDhdfQ==
-->