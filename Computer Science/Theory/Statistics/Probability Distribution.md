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


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1MzQ4ODE0MSwtMTI4MDUzMzY0OF19
-->