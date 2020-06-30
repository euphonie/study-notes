> Content obtained from Udemy's Probability for Statistics and Data Science course [Course link](https://telusinternational.udemy.com/course/probability-for-statistics-and-data-science)

# Bayes Theorem

Also known as Bayes' Rule or Bayes' Probability. 

Given conditional probability and the multiplication rule we have the following system of equations: 

$$
P(A|B) = \frac{P(A \cap B)}{P(B)} \\
P(A \cap B) = P(B|A) * P(A)
$$
We can conclude the following equation:
$$
P(A|B) = \frac{P(B|A) * P(A)}{P(B)}
$$
This allows us to find a relationship between the different conditional probabilities of two events.

### Independent cases

For indepdendent cases the theorem would generate the following equations:

$$
P(A|B) = \frac{P(A \cap B)}{P(B)} \\
P(A|B) = \frac{P(A)P(B)}{P(B)} \\
P(A|B) = P(A)
$$
And from Bayes' Theorem
$$
P(B|A) = \frac{P(A|B) P(B)}{P(A)} \\
P(B|A) = \frac{P(A)P(B)}{P(A)} \\
P(B|A) = P(B)
$$


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0OTg2NjcxNSwtMTQ4ODcxMTgyNSwtOT
Q2NjA0NjE3XX0=
-->