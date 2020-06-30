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

**Bag of words**
The basic idea of BoW is to take a piece of text and count the frequency of the words in that text. It is important to note that the BoW concept treats each word individually and the order in which the words occur does not matter.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxNzk3MTM1LDgyNTk4MjY1OCwxNTA1Mj
M5MDEzXX0=
-->