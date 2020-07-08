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


# Beta Distributions

Given an example of tossing a coin, being $a$ the times that it lands in heads and $b$ the times that it lands in tails, the Beta distribution is a curve that gives the certainty of the probability of an event occurring giving its trial's frequency values. 

This also means that computing a number of trials for $a$ and $b$ the value of the probability could be denoted as: 

$$
P(head) = \frac{favourable}{all} = \frac{a}{a+b}
$$

On top of this the beta distribution is a graph that indicates how likely is that $P(head)$ is the correct value. Being more narrow at the value $P(head)$ the more trials are executed. 

> image betadist

Its formula is: 

$$
\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1}y^{b-1} 
$$

To describe Gamma, if a is an integer then: $\Gamma(a) = (a-1)!$ The interesting part about Gamma is that it takes values in between integers, like $a = 5.5$, $\Gamma(5.5) = 52.35$. This is illustrated having direct probabilities for each event, as seen below.

> image betadist2



# Latent Dirichlet Allocation

Is based on matrix multiplication as a means to simplify computing a huge BoW modeled matrix. 
Then, the result of a given tuple of (word, document) could be calculated by multiplying the according row and column from much smaller matrixes. 

![LDA matric description](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/lda.png)

Another interesting feature of LDA is that the topics are not defined by the user. The topics are generated and posterior analysis on the associated words is needed to define the topic that was suggested by the model.

![Logic behind matrixes multiplication](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/lda2.png)


## Dirichlet distributions

To be able to define an algorithm to apply a modified matrix multiplication, it relies on a set of given distributions that are predefined. 
Having a triangle as a given space, with points inside of it. Assuming, each corner contains a probability value, the size of these probabilities determine which behavior is expected from the features in the diagram. It also determines which values are evaluated as good guesses for refining a model.

If the probability is high, it "pushes" the value away from the corner; and if the probability is low, it draws the value to the corner.

![Dirichlet Distributions graphical representation](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/dirichletDist.png)

![Dirichlet distributions 3D representation](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/dirichlet3d.png)

### Multinomial distribution 

A generalization of the binomial two-dimensional space to a higher dimension space. Having a three-dimensional space, for example as the one described above, the generalization of the rule computes the following formula: 

$$
\frac{\Gamma(a+b+c)}{\Gamma(a)\Gamma(b)\Gamma(c)}x^{a-1}y^{b-1}z^{c-1}
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgyMDAxNjM5MiwyMTQ0NDY0NTE3LC0xNz
k2ODg2NTAxLC0xNzgyNzA2NjIxXX0=
-->