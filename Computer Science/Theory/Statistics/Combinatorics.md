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

## Variations with repetition
Total number of ways we can pick and arrange some elements of a given set.

Given a set where a number of `p` values have to be assigned from a given set of `n` values into an ordered sequence, the resulting formula can be written as:

$$\overline{V}_p^n = n^p$$

Which can be translated to: "The number of variations with repetition when picking p-many elements out of n elements, is equal to n n to the power of p" (*Extracted from header's reference*)

## Variations without repetition

The number of variations without repetition when arranging p elements out of a total of n:
$$V_p^n = \frac{n!}{(n-p)!}$$

## Combinations

All the different permutations of a single combination are different variations. 
To obtain the formula, we have that the number of combinations equals the number of variations, over the number of permutations.

$$C_p^n = \frac{V_p^n}{P_p}  = \frac{n!}{p!(n-p)!}$$

### Symmetry
Picking more elements may result in fewer combinations.

We can pick p-many elements in as many ways as we can pick n minus p many elements
$$C_p^n = C^n_{n-p}$$

Symmetry can be used when:

$$p > \frac{n}{2} > n-p$$

![Symmetry in combinations](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Statistics/combsymmetry.png)

## Combinations with separate sample spaces



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDU3NjgyODAsLTg3MDk0Nzc4MCwtMT
E0NTI2MTczOSwyNzYwODA5NTEsLTQ4OTgxODcyNCwxMjc3OTI4
NzM2LDE4MjM3MjkzNTgsMTQwNTQ4NTkyMiwtMTk3NzQwNzU1My
wtMTA3NDU4OTQ3NV19
-->