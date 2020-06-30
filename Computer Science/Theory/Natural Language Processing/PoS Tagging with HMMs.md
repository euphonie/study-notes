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
- This means there are words that could fall into two PoS categories but would be identified by the highest frequency.

### Bigrams

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjgzOTY2MzY0XX0=
-->