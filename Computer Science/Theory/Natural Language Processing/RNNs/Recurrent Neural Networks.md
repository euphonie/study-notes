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

*Note* Take into account that temporal dependencies that may spam many time steps, more than 8 or 10 steps, might be affected by the vanishing gradient problem.  

![State layers](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/states.png)

![Temporal dependency description](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/temporaldep.png)

- Inputs are fed with previous values of the sequence at the same time.

![Previous input representation](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/inputsfeeded.png)

- In the topology of the NN a new set of inputs are added, these new inputs come from the latest result from the hidden layer. In this case, new inputs come to be named as the vector $\bar{y}_{t-1}$ (previous sequences) and the hidden layers $\bar{s}_t$ (memory state). The image below describes a simple RNN or Elman Network.

![Elman Nework](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/elmann.png)

- In RNNs, previous inputs directly affect the result of the current training phase.

![Elman Network with activation function](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/elmann2.png)

**Folded model**, is known as the configuration for a RNN with input and output vectors $\bar{X}_t$ and $\bar{Y}_t$, weight matrices $W_x$, $W_y$ , $W_s$, and a state vector $\bar{S}_t$ which results from a previous training and is feed once again along with the inputs.

- $\bar{x}_t$ is the input vector at time $t$
- $\bar{y}_t$ is the output vector at time $t$
- $\bar{s}_t$ is the hidden state vector at time $t$

![Elements of a RNN](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/rnn4.png)

When each phase of the training process is shown, it is called an **unfolded model**

![RNN unfolded model](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/rnn3.png)


The activation function for inner layers has as inputs the linear combination of the inputs in the input vector multiplied by the weights in $W_x$, and the previous state values $\bar{s}_{t-1}$ multiplied by the weights in $W_s$. It is described as:

$$
\bar{s}_t = \phi(\bar{x}_tW_x + \bar{s}_{t-1}W_x)
$$

![RNN activation functions](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/rnn5.png)

As FFNN, RNNs can be stacked to form ensemble methods. 

![Stacked RNNs](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/rnn6.png)

## Backpropagation Through Time (BPTT)

BPTT is the normal process used to train RNNs. While training RNNs, the network doesn't only learn by the input given at $t$, rather it uses $t$ and all previous instances to train the network.

To calculate the descent gradient for matrix $W_s$, a concept named **Accumulative Gradient** needs to be applied. This means gradients have to be added making the partial derivative calculation from the output error until the corresponding state $\bar{s}_t$ and its matrix $W_s$.

![BPTT equations](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/rnn7.png)

The formula behind this process is described as:
$$
\frac{\partial E_n}{\partial W_s} = \sum_{i=1}^N \frac{\partial E_N}{\partial \bar{y}_N} . \frac{\partial \bar{y}_N}{\partial \bar{s}_i} . \frac{\partial \bar{s}_i}{\partial W_s}
$$

The last step is to adjust weights that are connected to the input vector. For this step accumulative gradient is also applied following the trajectory from the ouput through the corresponding states given time $t$, all the way down to the corresponding input vector given time $t$. Having a formula described as:

$$
\frac{\partial E_n}{\partial W_x} = \sum_{i=1}^N \frac{\partial E_N}{\partial \bar{y}_N} . \frac{\partial \bar{y}_N}{\partial \bar{s}_i} . \frac{\partial \bar{s}_i}{\partial W_x}
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4MzQ5OTE5NCw4ODk0NTI0MjksLTIxMj
A2NzAyMjIsNjgwNjk1MDg3LDQwNTk0NzIzOSwtNTc2NDQzMjkw
LC0xODYwMjA1NDczLDIzODM4NjAxLC00MDQ0MTg0NCwtNDkxOT
M4NzQ2LC0xMTAxNDUwOTA4LDQ1ODkyMDQxMywxMDg1MDA4NzY4
LDE0MDI3NTIwNTcsMTk4NjY3NzY0MiwxMDAzMDYxNzkzLC0xMD
UyMzk1NTYzLC01OTMzMTg1MTUsNDY3MTIwMTM3LDEwOTE2MjY4
NzldfQ==
-->