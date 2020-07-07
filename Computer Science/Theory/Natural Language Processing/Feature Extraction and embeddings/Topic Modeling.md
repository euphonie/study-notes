> All information gathered from Udacity's Natural Language Processing Nanodegree

# Topic Modeling

Approach that classifies a document to a certain topic. 

## Bag of Words

- Should take into account a successful stemming and text processing to leave only relevant words for a document. 
	- For formula purposes, the document is denoted by $d$, the terms or words by $t$, and the probability of a word given a document is $P(t|d)$ which could be identified in the following manner: 
$$
P(t_i|d) = \frac{C(t_i)}{\sum{C(t_i, ..., t_n)}}
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjE0NDQ2NDUxNywtMTc5Njg4NjUwMSwtMT
c4MjcwNjYyMV19
-->