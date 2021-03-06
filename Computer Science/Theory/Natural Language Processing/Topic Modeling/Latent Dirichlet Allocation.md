> All information gathered from Udacity's Natural Language Processing Nanodegree

# Latent Dirichlet Allocation

In the following steps, an LDA modal is proposed by generating fake documents related to each topic and then comparing them to the real documents to analyze.

![Main description](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Feature%20Extraction%20and%20embeddings/sublda1.png)

## Sample a topic

The first step to build the model is to build a dirichlet distribution space ($\alpha$) that gets map into a multinomial distribution matrix ($\theta$) for a set of documents and a set of topics. In the following image a probability is given for every pair (document, topic).

![Sample a topic](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Feature%20Extraction%20and%20embeddings/sublda2.png)

## Sample a word

Now, a second dirichlet distribution space ($\beta$), in the case of the image is a 3-dimensional space),  is now mapped to another multinomial distribution matrix ($\phi$). $\phi$ represents the connections between the words and the topics.

$\phi$ gets computed along with every topic to generate the following matrix.

![Sample a word](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Feature%20Extraction%20and%20embeddings/sublda3.png)

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
	a. For each, word a probability distribution ($\phi$) will be generated taking into account each topic.
4. Then, for each generated or fake document a topic is selected 
5. Finally, documents are compared are corrected.

> image sublda7

## Notes

- From $\alpha$, a set of documents is obtained. 
- From $\beta$, a set of topics is obtained
- $\alpha$ and $\beta$ are used to create fake articles or documents.
- Real articles are compared to take ones, expecting the probability of guessing correctly to be small.
- The idea is to maximize the arrangement of points in both spaces $\alpha$ and $\beta$ that gets the highest likelihood between fake and real articles.
	- This is executed by optimizing the error function that results from comparing fake and real articles.
	- The error then backpropagates to the distributions and sets a gradient to move each point in the space to reduce the error.
- When the best configuration for the points is obtained, $\alpha$ will indicate which articles are associated to the topics, and $\beta$ will indicate which words are associated to the topics.
- The backpropagation could even be passed up to the dirichlet distributions itself, generating $\alpha'$ and $\beta'$

> image sublda8

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Nzg4NDk4NTBdfQ==
-->