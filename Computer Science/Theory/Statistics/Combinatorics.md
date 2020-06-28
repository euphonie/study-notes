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

Having a constant for translation would be: 

$$(n+k) ! = n! * (n+1) * (n+2) * ... * (n+k)! $$
$$
(n-k)! = \frac{n!}{(n-k+1) * (n-k+2) * ... * n}
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODU5NjE4ODA0LDE4MjM3MjkzNTgsMTQwNT
Q4NTkyMiwtMTk3NzQwNzU1MywtMTA3NDU4OTQ3NV19
-->