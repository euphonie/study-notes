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

> image ex-add-ranges

$$
P(Y \leq y) = P[Y < (y+1)]
$$
	

- **Equiprobable (Uniform Distribution)**. Events where all outcomes (more than 2) are equally likely to occur.



- **Benoulli Distribution**. Events that can only have true or false, or only two possible outcomes. Any event having two outcomes can be a Bernoulli event, it's just needed to assign which event falls for true and which one for false.
- **Binomial Distribution**. The outcomes of each iteration are two as in Bernoulli, but the experiment consists on many iterations. E.g. the likelihood of getting head two times, when making a 3-iterations coin toss.
- **Poisson Distribution**. Used to test how unusual an event frequency is for a given interval. E.g. Given a player that scores 35 points per game. What is the probability of the player scoring 12 points on the first quarter of the game.

### Continuous distributions

Are used on events that track time or distance. This are curves in comparison to bars used in discrete distributions.

- **Normal distribution**. Often observed in most natural events. Extreme values in a distribution curve are called **Outliers** and don't feature frequently in this distributions.
	- **Student's-T distribution**. When there is limited data to an event, this type of distribution can be used as it is a small sample approximation of a normal distribution. It accommodates extremes values significantly better.

![Student's-T distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/studentst.png)

- **Chi-squared**. An asymmetrical distribution that only contains non-negative values. Is used in hypothesis testing and determining the goodness of fit. 

![Chi-squared distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/chisquared.png)

- **Exponential distribution**. Is used when dealing with events that are rapidly changing early on.E.g. the relevance of news articles, as time passes interest wears off. 
- **Logistic Distribution**. Is useful in forecast analysis. Like trying to determine a cut-off point for a successful outcome. E.g. It can be used to predict, in a competitive online game, how much of an in-game advantage is necessary to predict a victory. With forecasting, predictions would never reach true certainty.

### Notation
A notation to define the type of distribution from a sample or population can be expressed as (variable, type and characteristics): 
$$
X \sim N (\mu, \sigma^2)
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NzMxMTE4MDMsLTE0MDczNjg2NjUsMj
I3MTc5NTg0LC02MjQzMjg2LDExNTM0ODgxNDEsLTEyODA1MzM2
NDhdfQ==
-->