> All information gathered from Udacity's Natural Language Processing Nanodegree

# Long Short-Term Memory Cells (LSTM)

This neural network structure allows to avoid the vanishing gradient problem. It does it by allowing certain inputs to be latched, or stored, for long periods of time in case they are needed in future steps of the training process.

![RNN cell structure](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/lstm1.png)

The main difference in the process of activation of the "cell" vs RNNs, is that LSTM cells are composed of four calculations. All of them are differentiable, which means a gradient function can be computed and allow to hold values over 1,000 previous iterations.

![LSTM cell structure](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/lstm2.png)

The operations inside the cell are used for the following processes. This functions are also trained through backpropagation to adjust to the data:
- What goes into the cell
- What is retained within the cell
- What passes to the output



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0Mjg0NzA4MSwxOTAxNTE3MzI1LDE2MT
I3MzE2NjksNzE0MzI4NTE1XX0=
-->