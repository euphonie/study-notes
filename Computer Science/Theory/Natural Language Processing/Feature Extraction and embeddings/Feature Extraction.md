> All information gathered from Udacity's Natural Language Processing Nanodegree

# Feature Extraction

## Bag of words

This technique converts each document to a corresponding unordered collection of words (bag). One of the applications, could be checking multiple documents for plagiarism or sentiment analysis from a collection of tweets.

This approach has a limitation, **it treats every word as equally important**. When in accordance to the topic of the corpus, some words might inherently have higher frequencies.

### Document-Term Matrix
Vectorization of a set of documents can be accomplished to have a better reading than analyzing each separate document. In this approach, a corpus would be constructed from all the documents and a frequency table should be composed having a column for each pre-processed token. This can be known as a **Document-Term Matrix**.

![Document-term matrix](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/doctermmatrix.png)

**Possible analysis**
- Comparing similarity of term frequency between two rows (vectors) from the matrix.
	- This is obtained applying the dot-product on the vectors. **Note**: This ignores the differences between the vectors; pairs that are different might end up with the same product from identical ones. 

$$
a*b = \sum{a_0*b_0 + a_1*b_1+...+a_n*b_n}
$$

-  A better approach is using **cosine similarity**, where the dot-product is divided by the product of the magnitudes from the vectors. This is also known as their **euclidean norms**
$$
cos(\theta) = \frac{a*b}{ ||a|| * ||b|| }
$$
The value is then -1 (less similar), 0 or 1 (most similar). To demonstrate the similarity of the vectors.

## TF-IDF

For avoiding having a bias on the importance or inherent high frequency of certain words given a topic, a **document frequency** can be tracked along with the document-term matrix.

The idea is to use the document frequency as a sample space and divide each frequency by it, having then a value that normalizes higher frequency words. This highlights words that are more unique in a document.

The formula is:

$$
tfidf(t, d, D) = tf(t,d) * idf(t,D) \\
tf = term\;frequency \\
idf = inverse\;document\;frequency
$$
The formulas components are:
$$
tf(t,d) = \frac{count(t, d)}{|d|} \\
count(t,d) = count\;of\;word\;t\;in\;document\;d \\
|d| = total\;number\;of\;terms\;in\;d
$$
$$
idf(t,D) = log(\frac{|D|}{{d \in D: t \in d}}) \\
 |D| = total\;number\;of\;documents\;in\;the\;corpus \\
d \in D: t \in d = number\;of\;documents\;were\;t\;is\;present
$$

![TD-IDF matrix](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/tdidf1.png)

## One-Hot Encoding

This technique is used to assign a numerical representation for each word that is part of a document. Basically a BoW matrix is created in a categorical way. 
- Each row represents a word
- and each column represents each word.
- Having then a matrix of 1's in the diagonal.

Where every vector is a bag of words containing only 1 word.

This approach is not the ideal when the size of the corpus is too large, as a similar-sized matrix is required.

## Word2Vec

### Word embeddings

In this approach, the idea is to have a vector space where some properties apply for pair or n-tuples of words:
- Words with same meaning are close to each other 
- Words with different meanings are far from each other
- Words with opposite meaning are separated by the similar magnitudes

### Word2Vec algorithm
This approach transforms words into vectors. It derives from the idea that a model could be able to identify relation between words given two methodologies:
- Analizing neighbouring words, also called **Continuous Bag of Words (CBoW)**
- Analizing a middle word, also called **Skip-gram.**
	- It takes one word and one-hot encodes it into a vector
	- The vector gets feed into a Neural Network or a Probabilistic model that aims to look for most plausible surrounding words given the context
	- The output layers of the model become the corresponding vector

### Properties
- Is a robust, distributed representation for analyzing words.
- The vector size is independent of the vocabulary
- Memoization can be applied to training
- It works with deep learning architectures (input for RNNs)

### Distributional Hyphotesis

> Words that happen in the same context tend to have the same meanings.

According to the course, this might be the reason why arithmetic might be plausible on words.

#### Dimensions

Having a vector space, the idea behind introducing new dimensions relies on the fact that words apply meaning to the immediate context in which they are used. Therefore, the magnitude or meaning of a word may vary in different contexts or dimensions to other similar words in different contexts or dimensions.

The process of word embedding can also be incorporated into the training algorithm to produce a significant word vector to convert the one-hot encoding into. However, using a pre-trained word embedding algorithm could be applied for already defined plausible word vectors for a given corpus.

Word embedding need to have high-dimensionality in order to capture variations in natural language.

![Embedding words model process vs visual analysis model](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/flowmeaning.png)


## GloVe (Global Vectors for Word Representation)

- The probability of words `j,i` is computed to know given `j` what is the likelihood of `i` being part of the context. $P(j|i)$. This is also known as the **co-ocurrence probabilities** of `j` and `i`.
	- This simply means if the word `j` is present in the vicinity (next or a few words) of word `i`. E.g. `a cup (i) of coffee (j)`
- Two sets of probability vectors are computed
	- One set when `j` is the target of the desired probability $W_i$
	- Another set when `j` is the context of another target word $W_j$
- It looks for the occurrence of probability between $P(j|i)$ to be equals to the product of the vectors $W_i*W_j$
- The goal is a set of vectors that capture the similarities and differences between a given set of words

![Logic begind co-oc probabilities](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/coocprobs.png)

## t-SNE

Stands for t-Distributed Stochastic Neighbor Embedding.  Technique that looks to reduce dimensionality that lowers vectors to a representation with less dimensions. Similar to Principal Component Analysis (PCA).

It tries to maintain similarity across words when the process of dimension removal is done. Preserves the line structures that represent the word embedding results from the model. This helps identifying bugs in the process of training.

This technique can also be applied to labelled images. 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxMzQ4NDU2LC0xMjk2ODQ5NTUwLC0xOD
U5NzE5NjU5LC0xMTQ1MDk2ODAsMTA3Nzc4MzA2XX0=
-->