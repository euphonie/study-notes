# Python Snippets


## Embedding vectors using Counter


```python
from collections import Counter
counts = Counter(words)
vocab = sorted(counts, key=counts.get, reverse=True)
voc
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NjMzNjIzNTJdfQ==
-->