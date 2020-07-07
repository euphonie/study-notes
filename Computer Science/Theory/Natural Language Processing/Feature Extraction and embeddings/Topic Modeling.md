> All information gathered from Udacity's Natural Language Processing Nanodegree

# Topic Modeling

Approach that classifies a document to a certain topic. 

## Bag of Words

- Should take into account a successful stemming and text processing to leave only relevant words for a document. 
	- For formula purposes, the document is denoted by $d$, the terms or words by $t$, and the probability of a word given a document is $P(t|d)$ which could be identified in the following manner: 
$$
P(t_i|d) = \frac{C(t_i)}{\sum{C(t_i, ..., t_n)}}
$$

## Latent Variables: Topics

Is used to reduce the size of the parameters that need to be feed into a ML model. It does this, by identifying which words "drive" the document's content. This introduces the concept of a topic, denoted by $z$. Then, to compute the model now there are two sets of probabilities that need to be taken into account. 

The probability of the document having an specific topic:
$$
P(z|d)
$$
and the probability of a given word or token being part of a topic: 
$$
P(t|z)
$$
This gives, the probability of word given a document:
$$
P(t|d) = \sum\limits{_z}\;P(t|z)P(z|d)
$$

# Latent Dirichlet Allocation

Is based on matrix multiplication as a means to simplify computing a huge BoW modeled matrix. 
Then, the result of a given tuple of (word, document) could be calculated by multiplying the according row and column from much smaller matrixes. 

> image lda1

Another interesting feature of LDA is that the topics are not defined by the user. The topics are generated and posterior analysis on the associated words is needed to define the topic that was suggested by the model.

> image lda2


## Dirichlet distributions

To be able to define an algorithm to apply a modified matrix multiplication, it relies on a set of given distributions that are predefined. 
Having a triangle as a given space, with points inside of it. Assuming, each corner contains a probability value, the size of these probabilities determine which behavior is expected from the features in the diagram. It also determines which values are evaluated as good guesses for refining a model.

If the probability is high, it "pushes" the value away from the corner; and if the probability is low, it draws the value to the corner.

> image dirichletdist

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDgzMTc2NzQ0LDIxNDQ0NjQ1MTcsLTE3OT
Y4ODY1MDEsLTE3ODI3MDY2MjFdfQ==
-->