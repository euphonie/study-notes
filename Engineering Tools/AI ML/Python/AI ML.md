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
features = np.zero
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Mzc0MTc4NTksOTI4MjgzMzM0XX0=
-->