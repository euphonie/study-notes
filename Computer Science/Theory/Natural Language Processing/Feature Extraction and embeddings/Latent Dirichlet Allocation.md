# Latent Dirichlet Allocation

In the following steps, an LDA modal is proposed by generating fake documents related to each topic and then comparing them to the real documents to analyze.

> image sublda1

## Sample a topic

The first step to build the model is to build a dirichlet distribution space ($\alpha$) that gets map into a multinomial distribution matrix ($\theta$) for a set of documents and a set of topics. In the following image a probability is given for every pair (document, topic).

> image sublda2

## Sample a word

Now, a second dirichlet distribution space ($\beta$), in the case of the image is a 3-dimensional space),  is now mapped to another multinomial distribution matrix ($\phi$). $\phi$ represents the connections between the words and the topics.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM1OTA3NzEyNV19
-->