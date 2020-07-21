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
- Predicting next word in a sentence.
- Sentiment analysis.

## Explaining RNNs

- RNNs can reuse pieces of information for future parts of the process by variables called **states**. This is like this because most applications have dependencies over time.

> image states
>image temporaldep

- Inputs are fed with previous values of the sequence at the same time.

> image inputsfeeded

- In the topology of the NN a new set of inputs are added, these new inputs come from the latest result from the hidden layer. In this case, new inputs come to be named as the vector $\bar{y}_{t-1}$ (previous sequences) and the hidden layers $\bar{s}_t$ (memory state). The image below describes a simple RNN or Elman Network.

> image elmann

- In RNNs, previous inputs directly affect the result of the current training phase.

> image elmann2

**Folded model**, is known as the configuration for a RNN with input and output vectors $\bar{X}_t$ and $\bar{Y}_t$, weight matrices $W_x$, $W_y$ , $W_s$, and a state vector $\bar{S}_t$ which results from a previous training and is feed once again along with the inputs.

- $\bar{x}_t$ is the input vector at time $t$
- $\bar{y}_t$ is the output vector at time $t$
- $\bar{s}_t$ is the hidden state vector at time $t$

> image rnn4

When each phase of the training process is shown, it is called an **unfolded model**

> image rnn3


The activation function for inner layers has as inputs the linear combination of the inputs in the input vector multiplied by the weights in $W_x$, and the previous state values $\bar{s}_{t-1}$ multiplied by the weights in $W_s$. It is described as:

$$
\bar{s}_t = \phi(\bar{x}_tW_x + \bar{s}_{t-1}W_x)
$$

> image rnn5

As FFNN, RNNs can be stacked to form ensemble methods. 

> image rnn6

## Backpropagation Through Time (BPTT)

BPTT is the normal process used to train RNNs. While training RNNs, the network doesn't only learn by the input given at $t$, rather it


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjE1NTM1NzkyLC01NzY0NDMyOTAsLTE4Nj
AyMDU0NzMsMjM4Mzg2MDEsLTQwNDQxODQ0LC00OTE5Mzg3NDYs
LTExMDE0NTA5MDgsNDU4OTIwNDEzLDEwODUwMDg3NjgsMTQwMj
c1MjA1NywxOTg2Njc3NjQyLDEwMDMwNjE3OTMsLTEwNTIzOTU1
NjMsLTU5MzMxODUxNSw0NjcxMjAxMzcsMTA5MTYyNjg3OSwtMz
M5MzUyODI2LC0xMjEyODczMDQ2LDEzMzU5NjQ4NDEsNDAyMDA5
NTMxXX0=
-->