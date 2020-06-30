> All information gathered from Udacity's Natual Language Processing Nanodegree

# Spam Classifier
The objective is to build a SMS spam classifier.

The data comprises of a file that holds two columns. One describes if the message is spam or ham; and the second column, contains the SMS message.

Criteria| Message
-------- | -----
ham| Fine if thats the way...
spam | England v Macednoia - dont miss the goals...
ham | Is that seriously how you...

- Importing the dataset with pandas and bootstrapping the values from the column names

```python
import pandas as pd
# Dataset available using filepath 'smsspamcollection/SMSSpamCollection'
filename= 'smsspamcollection/SMSSpamCollection'
df = pd.read_csv(filename, sep=r'\t', engine='python', header=None, names=['output', 'message'])

# Output printing out first 5 rows
df.head()
```
- Converting categorical values into a numeric representation to feed them to scikit-learn

```python
df['output'] = df.output.map({'ham':'0', 'spam': '1'}) 
print(df)
```
- Convert the texts to a frequency distribution matrix using BoW

**Bag of words**
The basic idea of BoW is to take a piece of text and count the frequency of the words in that text. It is important to note that the BoW concept treats each word individually and the order in which the words occur does not matter.

**Bag of Words algorithm from scratch**
```python
# Step 1: Convert all strings to their lower case form.
documents = ['Hello, how are you!',
             'Win money, win from home.',
             'Call me now.',
             'Hello, Call hello you tomorrow?']

lower_case_documents = []
for i in documents:
    lower_case_documents.append(i.lower())
    
# Step 2: Removing all punctuations
sans_punctuation_documents = []
import string
import re

regex = re.compile('[%s]' % re.escape(string.punctuation))

for i in lower_case_documents:
    sans_punctuation_documents.append(regex.sub(' ', i))

# Step 3: Tokenization
preprocessed_documents = []
for i in sans_punctuation_documents:
    preprocessed_documents.append(i.split())

# Step 4: Count frequencies
frequency_list = []
import pprint
from collections import Counter
import itertools

frequency_list = Counter([i for i in itertools.chain.from_iterable(preprocessed_documents)])
pprint.pprint(frequency_list)
```

- BoW using scikit-learn

```python
documents = ['Hello, how are you!',
                'Win money, win from home.',
                'Call me now.',
                'Hello, Call hello you tomorrow?']
                
# import CountVectorizer and create an instance
from sklearn.feature_extraction.text import CountVectorizer
count_vector = CountVectorizer()

# Fit the documents dataset to the CountVectorizer object and get list of categorized features.
count_vector.fit(documents)
count_vector.get_feature_names()

# Create a matrix with the rows begin the documents and the columns being each word. The row, column values will have the frequency of occurrence of the word in the denoted document
doc_array = count_vector.transform(documents).toarray()
doc_array

# Convert the array into a dataframe
frequency_matrix = pd.DataFrame(doc_array, columns =count_vector.get_feature_names())
```
To mitigate the skewness due to word high frequency in certain languages CountVectorizer can be instantiated with a parameter named `stop_words` set to `english` for example. This will automatically ignore all words that are found in a built in list of English stop words in scikit-learn.

TF-IDF features could also be used for this. [TF-IDF Vectorizer - scikit-learn docs](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html#sklearn.feature_extraction.text.TfidfVectorizer)

- Training and testing the sets

```python
# split into training and testing sets
# USE from sklearn.model_selection import train_test_split to avoid seeing deprecation warning.
from sklearn.cross_validation import train_test_split

X_train, X_test, y_train, y_test = train_test_split(df['message'], 
                                                    df['output'], 
                                                    random_state=1)

print('Number of rows in the total set: {}'.format(df.shape[0]))
print('Number of rows in the training set: {}'.format(X_train.shape[0]))
print('Number of rows in the test set: {}'.format(X_test.shape[0]))
```

- Applying BoW to the dataset

```python
# Instantiate the CountVectorizer method
count_vector = CountVectorizer()

# Fit the training data and then return the matrix
training_data = count_vector.fit_transform(X_train)

# Transform testing data and return the matrix. Note we are not fitting the testing data into the CountVectorizer()
testing_data = count_vector.transform(X_test)
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjQyMDc3MTc0LDE3MzU0NDcwMDcsODI1OT
gyNjU4LDE1MDUyMzkwMTNdfQ==
-->