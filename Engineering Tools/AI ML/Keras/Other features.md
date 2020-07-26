# Other Features

## One-hot encoding with Tokenizer


```python
from keras.preprocessing.text import Tokenizer
# One-hot encoding the output into vector mode, each of length no_words
no_words = 1000
tokenizer = Tokenizer(num_words=no_words)
x_train = tokenizer.sequences_to_matrix(x_train, mode='binary')
x_test = tokenizer.sequences_to_matrix(x_test, mode='binary')
print(x_train[0])
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjA2NjQ3MDE4XX0=
-->