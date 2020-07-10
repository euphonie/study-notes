# Latent Dirichlet Allocation

In the following steps, an LDA modal is proposed by generating fake documents related to each topic and then comparing them to the real documents to analyze.

> image sublda1

## Sample a topic

The first step to build the model is to build a dirichlet distribution space ($\alpha$) that gets map into a multinomial distribution matrix ($\theta$) for a set of documents and a set of topics. In the following image a probability is given for every pair (document, topic).

> image sublda2

## Sample a word

Now, a second dirichlet distribution space ($\beta$), in the case of the image is a 3-dimensional space),  is now mapped to another multinomial distribution matrix ($\phi$). $\phi$ represents the connections between the words and the topics.

$\phi$ gets computed along with every topic to generate the following matrix.

> image sublda3

## Combining $\theta$ and $\phi$

> image sublda4

In this step, the objective is to find the best position for each word to be able to generate the corresponding topic. This is done by matrix multiplication between $\theta$ and $\phi$

# Example process

1. Choose a set of n-topics.
2. Generate a set of n-documents. 
	a. This is done using a dirichlet distribution on the n-topics. Probabilities of the relation between each document and a topic are generated in a matrix ($\theta$)
	b. A sample, the size defined by a poisson distribution, is generated for each topic with the corresponding probabilities.

> image sublda5

> image sublda6

3. Then, a set of n-words is selected. This will conform a dirichlet disitribution as well. 
	a. For each, word a probability distribution will be generated taking into account each topic.



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3NjYwMjI2NCw3MzYzMzYzMV19
-->