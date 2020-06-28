> Content obtained from Udemy's Probability for Statistics and Data Science course [Course link](https://telusinternational.udemy.com/course/probability-for-statistics-and-data-science)

# Combinatorics

Deals with combinations of objects from a specific finite set. It can contain repetition, order or other restrictions.

## Permutations

Number of different possible ways we can arrange a set of elements.

Given a set with `n` values defining an ordered list or configurations of these values would render this possible entries for each position: 

$$
n, n-1, n-2, n-3, ..., 1 \\
P_n = n * (n -1 ) * (n-2)*...*1 = n!
$$

### Factorials

Permutations can also be expressed as factorials `n!` which denote the product of the natural numbers from 1 to n.
- Notes:
	- Negative numbers don't have a factorial
	- `0! = 1`

Factorials can also be expressed in recursive means: 

$$n! = (n-1)! * n \\
(n+1)! = n! * (n+1) $$

Having a constant for computing segments of a factorial would be: 

$$(n+k) ! = n! * (n+1) * (n+2) * ... * (n+k)! $$
$$
(n-k)! = \frac{n!}{(n-k+1) * (n-k+2) * ... * n}
$$

Having two factorials in a fraction would have the following property (if `n > k`): 

$$\frac{n!}{k!} = (k+1) * (k+2) * ... * n$$

### Variations with repetition
Total number of ways we can pick and arrange some elements of a given set.

Given a set where a number of `p` values have to be assigned from a given set of `n` values into an ordered sequence, the resulting formula can be written as:

$$\overline{V}_p^n = n^p$$



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NDg1NjksMTgyMzcyOTM1OCwxNDA1ND
g1OTIyLC0xOTc3NDA3NTUzLC0xMDc0NTg5NDc1XX0=
-->