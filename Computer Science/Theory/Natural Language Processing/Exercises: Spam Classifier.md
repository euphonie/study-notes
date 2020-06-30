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

- Bayes Theorem from scratch

Let us implement the Bayes Theorem from scratch using a simple example. Let's say we are trying to find the odds of an individual having diabetes, given that he or she was tested for it and got a positive result. In the medical field, such probabilies play a very important role as it usually deals with life and death situations.

We assume the following:

`P(D)`  is the probability of a person having Diabetes. It's value is  `0.01`  or in other words, 1% of the general population has diabetes(Disclaimer: these values are assumptions and are not reflective of any medical study).

`P(Pos)`  is the probability of getting a positive test result.

`P(Neg)`  is the probability of getting a negative test result.

`P(Pos|D)`  is the probability of getting a positive result on a test done for detecting diabetes, given that you have diabetes. This has a value  `0.9`. In other words the test is correct 90% of the time. **This is also called the Sensitivity or True Positive Rate.**

`P(Neg|~D)`  is the probability of getting a negative result on a test done for detecting diabetes, given that you do not have diabetes. This also has a value of  `0.9`  and is therefore correct, 90% of the time. **This is also called the Specificity or True Negative Rate.**

The Bayes formula is as follows:

![](https://view989a0867.udacity-student-workspaces.com/notebooks/images/bayes_formula.png)

-   `P(A)`  is the prior probability of A occurring independently. In our example this is  `P(D)`. This value is given to us.
    
-   `P(B)`  is the prior probability of B occurring independently. In our example this is  `P(Pos)`.
    
-   `P(A|B)`  is the posterior probability that A occurs given B. In our example this is  `P(D|Pos)`. That is,  **the probability of an individual having diabetes, given that, that individual got a positive test result. This is the value that we are looking to calculate.**
    
-   `P(B|A)`  is the likelihood probability of B occurring, given A. In our example this is  `P(Pos|D)`. This value is given to us.

Putting our values into the formula for Bayes theorem we get:

$$
P(D|Pos) = \frac{P(D) * P(Pos|D)}{P(Pos)}
$$

The probability of getting a positive test result  `P(Pos)`  can be calculated using the Sensitivity and Specificity as follows:

$$
P(Pos) = [P(D) * Sensitivity] + [P(D^c) * (1- Specificity)] \\
Sensitivity = P(Pos|D) \\
Specificity = P(Neg|D^c)
$$

```python
'''
Solution (skeleton code will be provided)
'''
# P(D)
p_diabetes = 0.01

# P(~D)
p_no_diabetes = 0.99

# Sensitivity or P(Pos|D)
p_pos_diabetes = 0.9

# Specificity or P(Neg|~D)
p_neg_no_diabetes = 0.9

# P(Pos)
p_pos = (p_diabetes * p_pos_diabetes) + (p_no_diabetes * (1-p_neg_no_diabetes))
print('The probability of getting a positive test result P(Pos) is: {}',format(p_pos))
```

** Using all of this information we can calculate our posteriors as follows: **

The probability of an individual having diabetes, given that, that individual got a positive test result:

$$
P(D|Pos) = \frac{P(D) * Sensitivity}{P(Pos)}
$$

The probability of an individual not having diabetes, given that, that individual got a positive test result:

$$
P(D^c|Pos) = \frac{P(D^c) * (1 - Specificity)}{P(Pos)}
$$

The sum of our posteriors will always equal  `1`.

```python
# P(D|Pos)
p_diabetes_pos = (p_diabetes * p_pos_diabetes) / p_pos
print('Probability of an individual having diabetes, given that that individual got a positive test result is:\
',format(p_diabetes_pos)) 

# P(Pos|~D)
p_pos_no_diabetes = 0.1

# P(~D|Pos)
p_no_diabetes_pos = (p_no_diabetes * p_pos_no_diabetes) / p_pos
print('Probability of an individual not having diabetes, given that that individual got a positive test result is:'\
,p_no_diabetes_pos)
```

- Define formula for Naive Bayes' Theorem

$$
P(y|x_1,...,x_n) = \frac{P(y)P(x_1,...,x_n|y}{P(x_1,...,x_n)}
$$

Here, `y` is the class variable or in our case the name of the candidate and `x1` through `xn` are the feature vectors or in our case the individual words. The theorem makes the assumption that each of the feature vectors or words (`xi`) are independent of each other.

**Copied from exercies point 4.2**
> This exercise tries to find the probability of a presidential candidate of saying specific words in a speech

To break this down, we have to compute the following posterior probabilities:

-   `P(J|F,I)`: Probability of Jill Stein saying the words Freedom and Immigration.
    
    Using the formula and our knowledge of Bayes' theorem, we can compute this as follows:  
$$
P(J|F,I) = \frac{P(J) * P(F|J) * P(I|J)}{P(F,I)}
$$
Here  `P(F,I)`  is the probability of the words 'freedom' and 'immigration' being said in a speech. 
$$
P(F,I) = P(F) \cap P(I)
$$

-   `P(G|F,I)`: Probability of Gary Johnson saying the words Freedom and Immigration.
    
    Using the formula, we can compute this as follows:  
$$
P(G|F,I) = \frac{P(G) * P(F|G) * P(I|G)}{P(F,I)}
$$

```python
# Find probability of Jill saying Freedom and immigration
# P(J)
p_j = 0.5

# P(F/J)
p_j_f = 0.1

# P(I/J)
p_j_i = 0.1

p_j_text = (p_j * p_j_f * p_j_i)

# Find probability of Gary saying Freedom and immigration
# P(G)
p_g = 0.5

# P(F/G)
p_g_f = 0.7

# P(I/G)
p_g_i = 0.2

p_g_text = (p_g * p_g_f * p_g_i)

p_f_i = p_j_text + p_g_text
print('Probability of words freedom and immigration being said are: ', format(p_f_i))

p_j_fi = p_j_text/p_f_i
print('The probability of Jill Stein saying the words Freedom and Immigration: ', format(p_j_fi))

p_g_fi = p_g_text/p_f_i
print('The probability of Gary Johnson saying the words Freedom and Immigration: ', format(p_g_fi))
```

- Naive Bayes' implementation using scikit-learn

Specifically, we will be using the **multinomial Naive Bayes** implementation. This particular classifier is suitable for classification with discrete features (such as in our case, word counts for text classification). It takes in integer word counts as its input. On the other hand **Gaussian Naive Bayes** is better suited for continuous data as it assumes that the input data has a Gaussian(normal) distribution.
```python
from sklearn.naive_bayes import MultinomialNB
naive_bayes = MultinomialNB()
naive_bayes.fit(training_data, y_train)
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ2Nzc1MTA0NiwxNjc2NjIyNTM4LDE3Mz
U0NDcwMDcsODI1OTgyNjU4LDE1MDUyMzkwMTNdfQ==
-->