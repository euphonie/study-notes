# Other Features

## One-hot encoding with Tokenizer


Example:

Binary encoding of words in a given text. 
[Keras Text Pre-processing](https://keras.io/api/preprocessing/text/)
```python
from keras.preprocessing.text import Tokenizer
# One-hot encoding the output into vector mode, each of length no_words
no_words = 1000
tokenizer = Tokenizer(num_words=no_words)
x_train = tokenizer.sequences_to_matrix(x_train, mode='binary')
x_test = tokenizer.sequences_to_matrix(x_test, mode='binary')
print(x_train[0])

# One-hot encoding the output
num_classes = 2
y_train = keras.utils.to_categorical(y_train, num_classes)
y_test = keras.utils.to_categorical(y_test, num_classes)
print(y_train.shape)
print(y_test.shape)

y_train[:10] # -> []
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjQ2NTY3MjYsNjA2NjQ3MDE4XX0=
-->