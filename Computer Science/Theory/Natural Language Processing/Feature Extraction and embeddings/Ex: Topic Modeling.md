> All information gathered from Udacity's Natural Language Processing Nanodegree

# Topic Modeling: Lab

LDA is used to classify text in a document to a particular topic. It builds a topic per document model and words per topic model, modeled as Dirichlet distributions.

-   Each document is modeled as a multinomial distribution of topics and each topic is modeled as a multinomial distribution of words.
-   LDA assumes that the every chunk of text we feed into it will contain words that are somehow related. Therefore choosing the right corpus of data is crucial.
-   It also assumes documents are produced from a mixture of topics. Those topics then generate words based on their probability distribution.

# Analysis

#### Load dataset

Load the dataset from the CSV and save it to 'data_text'

```python
import pandas as pd
data = pd.read_csv('abcnews-date-text.csv', error_bad_lines=False);
# We only need the Headlines text column from the data
data_text = data[:300000][['headline_text']];
data_text['index'] = data_text.index
documents = data_text
print(len(documents))
documents[:5]
```
### Data pre-processing

-   **Tokenization**: Split the text into sentences and the sentences into words. Lowercase the words and remove punctuation.
-   Words that have fewer than 3 characters are removed.
-   All  **stopwords**  are removed.
-   Words are  **lemmatized**  - words in third person are changed to first person and verbs in past and future tenses are changed into present.
-   Words are  **stemmed**  - words are reduced to their root form.
```python
import gensim
from gensim.utils import simple_preprocess
from gensim.parsing.preprocessing import STOPWORDS
from nltk.stem import WordNetLemmatizer, SnowballStemmer
from nltk.stem.porter import *
import numpy as np
np.random.seed(400)
import nltk
nltk.download('wordnet')
## Lemmatizing example
print(WordNetLemmatizer().lemmatize('went', pos = 'v')) # past tense to present tense
## Stemming example
stemmer = SnowballStemmer("english")
original_words = ['caresses', 'flies', 'dies', 'mules', 'denied','died', 'agreed', 'owned', 'humbled', 'sized','meeting', 'stating', 'siezing', 'itemization','sensational', 'traditional', 'reference', 'colonizer','plotted']
singles = [stemmer.stem(plural) for plural in original_words]

pd.DataFrame(data={'original word':original_words, 'stemmed':singles })
```
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODI4OTkyMjA4LC0xNTk1NjAyMDA4XX0=
-->