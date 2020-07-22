> Information gathered from Udacity's Natural Language Processing Nanodegree

# Keras

Python library for building deep neural networks.


# Code Intro

## Preparing data

### One-hot encoding

For categorical values, one-hot encoding is recommended. 

```python
# Make dummy variables for rank
one_hot_data = pd.concat([data, pd.get_dummies(data['rank'], prefix='rank')], axis=1)

# Drop the previous rank column
one_hot_data = one_hot_data.drop('rank', axis=1)

# Print the first 10 rows of our data
one_hot_data[:10]
```

### Scaling data

If data from inputs come in different ranges, the process of training might be affected. In this case is better to scale data in the range 0-1.

```python
# Copying our data
processed_data = one_hot_data[:]

# Scaling the columns
processed_data['gre'] = processed_data['gre']/800
processed_data['gpa'] = processed_data['gpa']/4.0
processed_data[:10]
```

### Splitting data

#### Training and testing data sets

```python
sample = np.random.choice(processed_data.index, size=int(len(processed_data)*0.9), replace=False)
train_data, test_data = processed_data.iloc[sample], processed_data.drop(sample)

print("Number of training samples is", len(train_data))
print("Number of testing samples is", len(test_data))
print(train_data[:10])
print(test_data[:10])
```

#### Features and targets

Now, as a final step before the training, we'll split the data into features (X) and targets (y).

Also, in Keras, we need to one-hot encode the output. We'll do this with the  `to_categorical function`.

```python
import keras
# Separate data and one-hot encode the output
# Note: We're also turning the data into numpy arrays, in order to train the model in Keras
features = np.array(train_data.drop('admit', axis=1))
targets = np.array(keras.utils.to_categorical(train_data['admit'], 2))
features_test = np.array(test_data.drop('admit', axis=1))
targets_test = np.array(keras.utils.to_categorical(test_data['admit'], 2))

print(features[:10])
print(targets[:10])
```

## Sequential Model

Keras uses a sequential model to implement the normal processes that are part of a neural network.

```python
from keras.models import Sequential

#Create the Sequential model
model = Sequential()
```

## Layers

The Keras Layer class provides a common interface for a variety of standard neural network layers. There are fully connected layers, max pool layers, activation layers, and more. You can add a layer to a model using the model's  `add()`  method. For example, a simple model with a single hidden layer might look like this:

```python
import numpy as np
from keras.models import Sequential
from keras.layers.core import Dense, Activation

# X has shape (num_rows, num_cols), where the training data are stored
# as row vectors
X = np.array([[0, 0], [0, 1], [1, 0], [1, 1]], dtype=np.float32)

# y must have an output vector for each input vector
y = np.array([[0], [0], [0], [1]], dtype=np.float32)

# Create the Sequential model
model = Sequential()

# 1st Layer - Add an input layer of 32 nodes with the same input shape as
# the training samples in X
model.add(Dense(32, input_dim=X.shape[1]))

#### Other ways of defining initial layers
model.add(Dense(128, activation='relu', input_shape=(6,)))
###

###
model.add(Dropout(.2))
###


# Add a softmax activation layer
model.add(Activation('softmax'))

# 2nd Layer - Add a fully connected output layer
model.add(Dense(1))

# Add a sigmoid activation layer
model.add(Activation('sigmoid'))
```
Only the first layer needs to be specifically indicated, as Keras, infers the succeeding layers.

We'll specify the loss function to be  `categorical_crossentropy`  which can be used when there are only two classes, and specify  `adam`  as the optimizer (which is a reasonable default when speed is a priority). And finally, we can specify what metrics we want to evaluate the model with. Here we'll use accuracy.

```python
model.compile(loss="categorical_crossentropy", optimizer="adam", metrics = ["accuracy"])
```

We can see the resulting model architecture with the following command:

```python
model.summary()
```

The model is trained with the  `fit()`  method, through the following command that specifies the number of training epochs and the message level (how much information we want displayed on the screen during training).

```python
model.fit(X, y, nb_epoch=1000, verbose=0)
```
*Note* For version 2 of Keras, **nb_epoch** is modified to **epochs**

Finally, the model is evaluated.
```python
model.evaluate()
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgwNjczNDY3NiwxMTgwNDA3OTAsLTE0NT
Y1MDg2MDhdfQ==
-->