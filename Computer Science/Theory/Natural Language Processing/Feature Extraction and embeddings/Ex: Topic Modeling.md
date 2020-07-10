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


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjcxNzU3NDI0LC0xNTk1NjAyMDA4XX0=
-->