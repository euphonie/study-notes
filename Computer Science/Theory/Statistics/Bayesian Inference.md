> Content obtained from Udemy's Probability for Statistics and Data Science course [Course link](https://telusinternational.udemy.com/course/probability-for-statistics-and-data-science)

# Bayesian Inference

## Definitions
- Every event has a set of outcomes that identify (Favourable outcomes).
	- Notation indicates sets are written in upper case and elements in lower case.
- Set can be empty, thus being named empty set or null set: Ø.

## Sets

Sets can be finite or infinite. To denote an element belongs to a set we describe it as: 
$$x \in A | x \notin A$$
To denote contention:
$$A \ni x | A \notni x$$

- The inverted A can be used to make a reference about all elements within a set; is known as `for all`.
$$\forall$$
- To make statements about a specific group of elements within a set, `:` is used and described as `such that`.

Example, declaring a set of all even numbers

$$\forall x \in A : x\;is\;even$$

- A **subset** is a set that is fully contained in another set. This is described as: 
$$A \subseteq B$$

- Every set contains necessarily two subsets; itself and the null set. 
$$A \subseteq A \\
A \subseteq Ø$$

### Characteristics of sets
Considering two sets the description of two events:
- If the two sets have no related elements, the events can never happen simultaneously
	- Event A occurring guarantees that event B is not occurring and vice versa
- If the two sets intersect, the two events can occur at the same time.
- If a set is a subset of another event, it means that one event can only ever occur if the other event occurs as well.
	- Event B (subset) occurring guarantees event A
	- However, event A (greater set) occurring does not guarantee event B

#### Intersections

When two events intersect, it consists on all the outcomes that are favourable for both event A and event B simultaneously. 
$$A \cap B$$

Example, having two sets:
- $$
A = Cards\;having\;diamonds \\
B = Cards\;having\;hearts \\
A \cap B =  Ø
$$
- $$
A = Cards\;having\;diamonds \\
B = Card\;being\;queen \\
A \cap B = Queen\;of\;diamonds
$$

#### Unions

The union is the combination of all outcomes preferred for either A or B.
$$A \cup B \\ 
if \; A\cap B = Ø;\;A \cup B = A+ B \\
if \; A \cap B \ne Ø; \; A \cup B = A + B - A \cap B \\
if B \subseteq A; \; A \cup B = A + B - B = A
$$

### Mutually exclusive sets

Sets, which are not allowed to have any overlapping elements. This means:
$$A \cap B = Ø \\
A \cup B = A+B$$

Sets also have related complements. Which contain all the values in the sample space that are not part of the set. Complements are always mutually exclusive with their related sets. 
However, not all mutually exclusive sets are complements to each other.

## Independent/Dependent events

### Independent events

Events which its theoretical probability remains unaffected by other events.

### Dependent events

Events which its theoretical probability varies as conditions change

Example, expecting a favourable outcome of a Queen of spades while drawing a card from a deck. At first, the probability is 1/52. If, at the moment, we know that the card we draw is a spade, the sample space then reduces to 1/13; it would reduce to 1/4, in the case we know it's a queen.

Therefore, as the conditions change the event has a different probability due to its context.

**Notation**
The probability of getting A, if we are given that B has occurred. Read as the probability of A given B.
$$P(A|B)$$

Example
$$
P(A) = Probability\;of\;getting\;Queen\;of\;Spades \\
P(B) = Probability\;of\;getting\;a\;spade
$$
Then `P(A|B)` would be the probability of drawing the Queen of Spades if we know the card is a spade.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5MTIyNTQ0MSwxNjQzMjMyMDc2LC0xNT
M5MzQ1NTg5LC03MjQzNTQ0OTksLTE3MDUwOTUwODEsLTU5MTQw
OTUzMiwxOTcxNTUxMDg3XX0=
-->