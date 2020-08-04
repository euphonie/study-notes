# RNNs using Keras

There are three built-in RNN layers in Keras:

1.  [`keras.layers.SimpleRNN`](https://www.tensorflow.org/api_docs/python/tf/keras/layers/SimpleRNN), a fully-connected RNN where the output from previous timestep is to be fed to next timestep.
    
2.  [`keras.layers.GRU`](https://www.tensorflow.org/api_docs/python/tf/keras/layers/GRU), first proposed in  [Cho et al., 2014](https://arxiv.org/abs/1406.1078).
    
3.  [`keras.layers.LSTM`](https://www.tensorflow.org/api_docs/python/tf/keras/layers/LSTM), first proposed in  [Hochreiter & Schmidhuber, 1997](https://www.bioinf.jku.at/publications/older/2604.pdf).
    

In early 2015, Keras had the first reusable open-source Python implementations of LSTM and GRU.

Here is a simple example of a  `Sequential`  model that processes sequences of integers, embeds each integer into a 64-dimensional vector, then processes the sequence of vectors using a  `SimpleRNN`  layer.

The process of sequence padding allows having a same size vector as input for the RNN

```python
from keras.preprocessing import sequence
from keras.preprocessing.text import Tokenizer

# Set the maximum number of words per document (for both training and testing)
max_words = 500

# TODO: Pad sequences in X_train and X_test
X_train_padded = sequence.pad_sequences(X_train, maxlen=max_words)
X_test_padded = sequence.pad_sequences(X_test, maxlen=max_words)

print(len(X_train_padded[0]), len(X_test_padded[0]))


print(X_train_padded[22500])
y_train[:10]
print ('...')
print (X_train_padded.shape)
print(y_train.shape, y_train[1])
```

```python
from keras.models import Sequential
from keras.layers import Embedding, LSTM, Dense, Dropout, SimpleRNN

# TODO: Design your model
model = Sequential()

embedding_mat_columns=32
model.add(Embedding(input_dim=vocabulary_size, output_dim=embedding_mat_columns, input_length=max_words))

model.add(SimpleRNN(units=embedding_mat_columns))
model.add(Dropout(.2))
model.add(Dense(1, activation='sigmoid'))


print(model.summary())

from keras.optimizers import Adam
# TODO: Compile your model, specifying a loss function, optimizer, and metrics

optimizer = Adam(lr=0.001)

model.compile(
    loss="binary_crossentropy",
    optimizer=optimizer,
    metrics = ["accuracy"]
)

# TODO: Specify training parameters: batch size and number of epochs
batch_size = 60
num_epochs = 10

# TODO: Train your model
history = model.fit(X_train_padded, y_train, epochs=num_epochs, validation_split=0.5, verbose=1, batch_size=batch_size)
print(history.history)

# Evaluating a model
scores = model.evaluate(X_test_padded, y_test, verbose=1)  # returns loss and other metrics specified in model.compile()
print("Test accuracy:", scores[1])  # scores[1] should correspond to accuracy if you passed in metrics=['accuracy']
```

**Tip**: You can split off a small portion of the training set to be used for validation during training. This will help monitor the training process and identify potential over fitting. You can supply a validation set to `model.fit()` using its `validation_data` parameter, or just specify `validation_split` - a fraction of the training data for Keras to set aside for this purpose (typically 5-10%). Validation metrics are evaluated once at the end of each epoch.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgyMDA2ODA0Myw5NDMwNTcyNzMsLTE1Mz
UxMzMwOTYsNzMwOTk4MTE2XX0=
-->