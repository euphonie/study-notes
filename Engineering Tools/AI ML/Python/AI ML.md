# Python Snippets


## Embedding vectors using Counter

**Encoding features**
```python
from collections import Counter
counts = Counter(words)
# ordered by the frequency of words
vocab = sorted(counts, key=counts.get, reverse=True)
# as vocabulary is padded with 0, 0 would introduce noise
vocab_to_int = {word: ii for ii, word in enumerate(vocab, 1)}

reviews_ints = []
for each in reviews:
	reviews_ints.append([vocab_to_int[word] for word in each.split()])
```
**Encoding labels**
```python
labels = np.array([1 if each =='positive' else 0 for each in labels])
```

**Padding vectors**
```python
seq_len = 200
# make a 0s matrix of #reviews x seq_len
features = np.zeros( (len(reviews, seq_len), dtype=int)
# populate each row with the contents of each review
# populate the last segment (size len(row)) of the 0s array with the 
# contents of the len(row) from the current row
for i, row in enumerate(reviews_ints):
	features[i, -len(row):] = np.array(row)[:seq_len]
```

**Heatmap visualization of embedded vectors**

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Let's visualize our decoder hidden state
plt.figure(figsize=(1.5, 4.5))
sns.heatmap(np.transpose(np.matrix(dec_hidden_state)), annot=True, cmap=sns.light_palette("purple", as_cmap=True), linewidths=1)
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTY0NzUyNzksLTEyNDY4OTA5MjAsOT
I4MjgzMzM0XX0=
-->