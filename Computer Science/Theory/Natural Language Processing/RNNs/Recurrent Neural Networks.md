> All information gathered from Udacity's Natural Language Processing Nanodegree

# Recurrent Neural Neworks

This type of neural networks rely on a memory element (past inputs being fed again into the neural network along with new inputs). This type of neural networks works for applications with temporal dependencies. 

![RNN graph's diagram](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/rnn.png)

Feedforward neural networks don't have the ability to capture dependencies that change over time.

- **1989**. An enhancement proposed were Time Delay Neural Networks (TDNN) which had a window of time represented by a set of inputs into the Neural Network which recollected past versions of the input. 
	- The disadvantage of this approach was the limit set by the size of the window selected
- **1990**. Then simple RNNs or Elman/Jordan Networks were introduced.

This types of neural networks have a flaw known as the **vanishing gradient** problem, in which contributions of information decay geometrically over time. Making contributions from more than  8 to 10 steps back was practically impossible.

- **Mid 90's**. Long Short-term memory (LSTM) were invented to address the vanishing gradient problem. The approach proposed that some signals (state variables) could be kept fixed using gates in the design, and this state variables could be reintroduced or not at an appropriate time in the future. This added the ability to represent arbitrary time intervals and to capture temporal dependencies.
- Gated Recurrent Networks are variations on LSTMs further refine the ability to represent arbitrary time intervals.

## Applications

- Speech recognition. Sequence of data samples extracted from an audio signal is continuously mapped to text. 
- Time series prediction. Prediction of pattern to suggest best possible solution.
- NLP. Machine translation, question answering, chatbots.
- Gesture recognition. Evaluating a sequence of data frames to identify gestures.

# Feedforward Neural Networks

Composed of three set of layers: 
- Input Layer
- n-Hidden Layers
- Output Layer

Usually uses backpropagation to adjust the weights between the network's nodes. 

## Vanishing Gradient Problem

TODO

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNDM5OTI5MjcsLTEyMTI4NzMwNDYsMT
MzNTk2NDg0MSw0MDIwMDk1MzEsLTc0NzkyNzA3LDIwODg3ODcx
ODEsMjA0MjY0OTE3XX0=
-->