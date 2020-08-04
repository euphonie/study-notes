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

y_train[:10] # -> [0,1] or [1,0] para Y, N
```

## Save a model

```python
# Save your model, so that you can quickly load it in future (and perhaps resume training)
model_file = "rnn_model.h5"  # HDF5 file
model.save(os.path.join(cache_dir, model_file))

# Later you can load it using keras.models.load_model()
#from keras.models import load_model
#model = load_model(os.path.join(cache_dir, model_file))
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MzM1NjQxMzksMTQ3MTAxODkwMiw2MD
Y2NDcwMThdfQ==
-->