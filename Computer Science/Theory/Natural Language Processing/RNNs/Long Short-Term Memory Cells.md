> All information gathered from Udacity's Natural Language Processing Nanodegree

# Long Short-Term Memory Cells (LSTM)

This neural network structure allows to avoid the vanishing gradient problem. It does it by allowing certain inputs to be latched, or stored, for long periods of time in case they are needed in future steps of the training process.

> image lstm1

The main difference in the process of activation of the "cell" vs RNNs, is that LSTM cells are composed of four calculations. All of them are differentiable, which means a gradient function can be computed and allow to hold values over 1,000 previous iterations.

> image lstm2

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzE0MzI4NTE1XX0=
-->