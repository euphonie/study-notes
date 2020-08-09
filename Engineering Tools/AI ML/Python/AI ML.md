# Python Snippets


## Embedding vectors using Counter

**Encoding features**
```python
from collections import Counter
counts = Counter(words)
# ordered by the frequency of words
vocab = sorted(counts, key=counts.get, reverse=True)
vocab_to_int = {words: ii for ii, word in enumerate(vocab, 1)}

reviews_ints = []
for each in reviews:
	reviews_ints.append([vocab_to_int[word] for word in each.split()])
```
**Encoding labels**
```python

```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0Nzk5NDI1XX0=
-->