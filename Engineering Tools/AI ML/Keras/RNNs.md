# RNNs using Keras

There are three built-in RNN layers in Keras:

1.  [`keras.layers.SimpleRNN`](https://www.tensorflow.org/api_docs/python/tf/keras/layers/SimpleRNN), a fully-connected RNN where the output from previous timestep is to be fed to next timestep.
    
2.  [`keras.layers.GRU`](https://www.tensorflow.org/api_docs/python/tf/keras/layers/GRU), first proposed in  [Cho et al., 2014](https://arxiv.org/abs/1406.1078).
    
3.  [`keras.layers.LSTM`](https://www.tensorflow.org/api_docs/python/tf/keras/layers/LSTM), first proposed in  [Hochreiter & Schmidhuber, 1997](https://www.bioinf.jku.at/publications/older/2604.pdf).
    

In early 2015, Keras had the first reusable open-source Python implementations of LSTM and GRU.

Here is a simple example of a  `Sequential`  model that processes sequences of integers, embeds each integer into a 64-dimensional vector, then processes the sequence of vectors using a  `LSTM`  layer.

```python
model = keras.Sequential()
# Add an Embedding layer expecting input vocab of size 1000, and# output embedding dimension of size 64.
model.add(layers.Embedding(input_dim=1000, output_dim=64))
# Add a LSTM layer with 128 internal units.
model.add(layers.LSTM(128))

model.add(Dropout(.1))

# Add a Dense layer with 10 units.
model.add(layers.Dense(10))

model.summary()

# Compile
model.compile(loss="categorical_crossentropy", optimizer="adam", metrics = ["accuracy"])

# Train 

```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExNTQ4NzE5MCwtMTUzNTEzMzA5Niw3Mz
A5OTgxMTZdfQ==
-->