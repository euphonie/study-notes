
# Feature Extraction

## Bag of words

This technique converts each document to a corresponding unordered collection of words (bag). One of the applications, could be checking multiple documents for plagiarism or sentiment analysis from a collection of tweets.

This approach has a limitation, **it treats every word as equally important**. When in accordance to the topic of the corpus, some words might inherently have higher frequencies.

### Document-Term Matrix
Vectorization of a set of documents can be accomplished to have a better reading than analyzing each separate document. In this approach, a corpus would be constructed from all the documents and a frequency table should be composed having a column for each pre-processed token. This can be known as a **Document-Term Matrix**.

> image

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

The idea is to use the document frequency as a sample space and divide each frequency by it, having then a value that normalizes higher frequency words.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2NjUzNDg3OF19
-->