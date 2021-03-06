> All information gathered from Udacity's Natural Language Processing Nanodegree

# Text processing

## Capturing data

Data can be obtained from several sources. To be able to process, first the origin and format should be known: 
	- E.g. comes from a HTTP request, comes in json/xml
	- Comes from a textfile separated by the newline (\n) character

## Cleaning data

Data should be clean according to the type of analysis that is needed. For example, `BeautifulSoup` is a python library that can be used to parse HTML content to find specific regions.

## Normalization

- **Case normalization**. In english, capitalization doesn't usually incur in a semantic difference, except for acronyms. So for basic analysis text can be normalized to lowercase. 
This however, won't be effective in languages as German where upper case words usually mean that the element is a subject.
- **Punctuation removal**. In low level detail analysis, as document classification or clustering punctuation can be removed as only content is used to determine what to do with the input.
- **Tokenization**. Obtaining a sequence of base segments from a text or string.

> ### NLTK 
> 
> Tokenization. The library comes with more specialized tokenization
> such as:
> 	- word_tokenize. Which holds punctuation semantics.
> 	- sent_tokenize. Which separates by sentences.
> 	- regex tokenizer
> 	- twitter tokenize

- **Stop word removal**. Removal of words that add no special meaning in basic text processing tasks.
- **Part-of-Speech Tagging**. Identification of each token in regards to which part of speech it is. Defining a grammar with POS sections sentences, even ambiguous, can be parsed to a POS tree.
	- **Named Entity Recognition**. Adds metadata to POS to identify them as higher-level entities.
- **Stemming**. Reduces complexity of parts-of-speech declination still conveying expected meaning. Might be a less memory-expensive option.
- **Lemmatization**. Reduces non-trivial inflection using a dictionary to reduce complexity. NLTK uses Wordnet to lemmatize words.

## Normal Processing Pipeline 

Normalization -> 
Tokenization -> 
Removal of stop words -> 
Lemmatization -> 
Stemming

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MjUyODIwNzAsLTM0MDI1MDU0NSwtMT
M0MjI1NDI2LDEyMzYwNDM1NDQsLTY1NTg5NDAzXX0=
-->