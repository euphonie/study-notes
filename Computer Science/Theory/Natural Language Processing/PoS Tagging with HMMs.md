> All information gathered from Udacity's Natual Language Processing Nanodegree

# Parts of Speech

This implementations are usually good for grammar or spelling checkers. It stands for identifying the part of speech that corresponds to every element of a sentence. 
Sentences can be formed of elements such as: 
- Nouns
- Verbs
- Modal verbs
- Adjectives
- Articles
- Pronouns, etc...

## Algorithms

### Lookup table

- We take the information from a given set of sentences and tag each word with its corresponding PoS. 
- Then a lookup table is filled, basically a frequency distribution matrix,
	-  with the columns being the possible PoS;
	-  the rows being each word in the sentences; 
	- and the row, column value being the frequency of usage in the corresponding PoS column. 
- This means there are words that could fall into two PoS categories/tags but would be identified by the highest frequency.

### Bigrams

In this approach, to avoid high frequency of a specific tag for a word to generalize its use, bi-grams can be used. These refer to combinations of neighbouring words.
The columns contain variations of tags and the rows contain the corresponding pair of words.

From 2 tags, the generalization of multiple PoS tags is called an n-gram.

![Bi-gram example](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/bigrams.png)

#### More complicated cases

Problem with n-grams is that not all possible variations exist in the lookup table. Therefore, certain ordered pair or n-tuples of words won't have a frequency to be evaluated.

# Hidden Markov Models

This approach works with probable grammatical structures in sentences. It uses:
-  **Transition probabilities** to move from one PoS to another one, and see how likely it is that these two could be neighbours. 



- And uses **emission probabilities** to identify which PoS corresponds to each word in a sentence. 

For calculating these, a lookup table is created and then the probabilities for each word and its corresponding PoS are computed. 



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODUzNDIzNjc0LC03MDU2NzczNDksNjgzOT
Y2MzY0XX0=
-->