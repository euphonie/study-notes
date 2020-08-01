> Content obtained from Udemy's Probability for Statistics and Data Science course [Course link](https://telusinternational.udemy.com/course/probability-for-statistics-and-data-science)

# **Normal distribution**

Often observed in most natural events. Extreme values in a distribution curve are called **Outliers** and don't feature frequently in this distributions.

![Student's-T distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/studentst.png)

Denoted as: 
$$
N(\mu, \sigma^2) \\
X \sim N(\mu, \sigma^2)
$$
Which means, variable $X$ follows a normal distribution with mean $\mu$ and variance $\sigma^2$. $\mu$ and $\sigma^2$ are usually known.

It applies that: 
- The graph is bell shaped
- Most of values are in the mean of the distribution
- Outliers are less likely to occur in the distribution
- The graph is equally symmetric
	- This means value in $\mu-\epsilon$ and $\mu+\epsilon$ are both equally likely to occur

![Normal Distribution Graph](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/normaldist.png)

The expected value and variance are: 

$$
E(X) = \mu
$$
and the variance $Var(X) = \sigma^2$ is usually given in the description. If it isn't it can be deduced from the expected value: 
$$
Var(X) = E(X^2) - E(X)^2
$$

## 68, 95, 99.7 Law
For any normal distribution: 
- 68% of all outcomes fall under 1 standard deviation from the mean, in the interval $(\mu-\sigma, \mu+\sigma)$
- 95% fall under 2 standard deviations. $(\mu-2\sigma, \mu+2\sigma)$
- 99.7% fall under 3 standard deviations. $(\mu-3\sigma, \mu+3\sigma)$

## Standardization

Works along with **transformations**. Which are a way in which every element of a distribution can be altered to get a new distribution. 

This means addition, subtraction, multiplication and division can be used to alter the values while conserving the type of distribution.

In standardizing, the goal is to make $E(X) = 0$ and $Var(X) = 1$. The distribution obtained would be a Standard Normal Distribution. It relates to a **z-table** as a similar calculation as the 68, 95, 99.7% rule, but for more values.

The process of standardizing is done by: 
- Moving the graph towards 0, such that $\mu  = 0$. This is done by subtracting the value of $\mu$ from each element $x$.
- Then, the standard deviation $\sigma = 1$. This is done by dividing each element $x-\mu$ by $\sigma$.
$$
y = f(\frac{x - \mu}{\sigma})
$$

**Note**. If the data is scarce, standardization could affect the analysis by introducing outliers as relevant values of the distribution (*in cases were there are less than 30 entries, normal distributions shouldn't be assumed*).


# **Student's-T distribution**
When there is limited data to an event, this type of distribution can be used as it is a small sample approximation of a normal distribution. It accommodates extremes values significantly better. It is denoted as: 
$$
t(k)  \\
Y \sim t(3)
$$
Where $k$ stands for **degrees of freedom**. If $k > 2$:
$$
E(Y) = \mu \\
Var(Y) = \frac{S^2*k}{k-2}
$$

It is similar to the shape of the normal distribution, however has higher-valued tails to accommodate the occurrence of values far away from the mean.

It also has a table with CDF values known as T-table.

![Student's-T distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/studentst.png)

# **Chi-squared**
 An asymmetrical distribution that only contains non-negative values. Is used in hypothesis testing and determining the goodness of fit. 

It is mostly featured in statistical analysis as few real life events follow this kind of distribution. It can be used in: 
- Hypothesis testing
- Computing confidence intervals

In general it can be used when determining the Goodness of fit of categorical values.

![Chi-squared distribution](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/chisquared.png)

Is it denoted as: 
$$
\Chi^2(k) \\
Y \sim \Chi^2(3)
$$
Where $k$ stands for **degrees of freedom**.

It can be interpreted as a transformation of the Student's T-distribution elevated to the second power:

$$
Y \sim t(k) \\
Y^2 \sim \Chi^2(k)
$$
and 
$$
x \sim \Chi^2(k) \\
\sqrt{X} \sim t(k)
$$

It also contains a table of known values (CDF table).  Having: 
$$
E(X) = k \\
Var(X) = 2k
$$

# **Exponential distribution**
Is used when dealing with events that are rapidly changing early on.E.g. the relevance of news articles, as time passes interest wears off. It is denoted by: 

$$
Exp(\lambda) \\
X \sim Exp(\frac{1}{2})
$$
Where $\lambda$ stands for a scale value. 



# **Logistic Distribution**
Is useful in forecast analysis. Like trying to determine a cut-off point for a successful outcome. E.g. It can be used to predict, in a competitive online game, how much of an in-game advantage is necessary to predict a victory. With forecasting, predictions would never reach true certainty.

## Notation
A notation to define the type of distribution from a sample or population can be expressed as (variable, type and characteristics): 
$$
X \sim N (\mu, \sigma^2)
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzU2OTI0MDU1LC0xMjcwMjA1OTIwLC0xNT
EwNjcwNDAsOTU4MTIzNzAzXX0=
-->