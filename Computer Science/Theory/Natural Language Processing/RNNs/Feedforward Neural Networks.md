> All information gathered from Udacity's Natural Language Processing Nanodegree

# Feedforward Neural Networks

Composed of three set of layers: 
- Input Layer
- n-Hidden Layers
- Output Layer

Usually uses backpropagation to adjust the weights between the network's nodes.  A generalized version of a neural network can be described using: 

$$
\bar{y} = (\bar{x}, W) 
$$
Where $\bar{x}$ is the input vector, $\bar{y}$ is the output vector and W are the weights that make inner connections in the network.
Neural networks essentially work as non-linear function approximators, it searches to fit a smooth function between a given set of points given that a new point $x'$ a new output $y'$ can be found.
The two main types of applications neural networks have is: 
- Classification for a given input
- Regression for function approximation (through a supervised learning strategy)

The goal behind neural networks is to find the best set of weights $W$ to be able to produce a reliable output $\bar{y}$ given some known and unknown inputs. $W$ starts as a random set of weights that gets approximated, each execution, to a better approximation.

There are two main phases: 
- Training. A subset of all given points is used to adjust the weights to the best approximator function. 
	- Consists of two steps:
		- Feedforward. The input is feed through the weights and an output is generated.
		- Backpropagation. Output is compared to desired output and backpropagation adjusts the weights to correct the function in terms of the current input, value pair.
- Evaluation. The network is used to the testing set (the remaining points that are not part of testing phase but carry their desired output), to find how good is the neural network to generalize unknown data. 

![Feedforward network diagram](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/ffnn1.png)

In the graphical representation of a FFNN, the result of multiplying the input values with each corresponding weight is then applied to a summing function. Neurons can also contain a bias that affects the resulting value. The output of the summing function is run through an activation function which determines the obtained output.

#### Matrix multiplication

A neural network consists of a resulting vector $\bar{y}$ obtained from multiplying an input vector $\bar{x}$ by two matrices of edges $W_{n}$ (being $n$ the number of hidden layers) connected from an input to a hidden layer node or from a hidden layer node to an output. 
In the case, there is more than one hidden layer the number of matrices to compute the resulting $\bar{y}$ augments.

**Note:** *For having good approximations for an output $\bar{y}$, the network should consist of at least 10 hidden layers.*

#### Activation Functions

When multiplying each incoming node $i$ and a destination node $j$ inside of each layer, an activation function $\phi$ is applied to the result to ensure the resulting value stays within a certain limit. For $\phi$, there are several functions that can be used: 
- Hyperbolic tangent function $f(x) = tanh(x)$. Returns outputs between -1 and 1.
- Sigmoid function $\sigma(x) = \frac{1}{1+e^{-x}}$. Returns outputs between 0 and 1.
- ReLu function, Rectified linear unit. Negative values are nulled and positive values remain as they are.
$$
f(x) = 
\begin{cases}
0 for x < 0 \\
x for x \geq 0
\end{cases}
$$
This activation functions allow the network to represent non-linear relationships between inputs and outputs.

#### Softmax 

At the last step, when multiplying the corresponding hidden vector $h_n$ with the last matrix $W_n$ a softmax function can be used to limit results in outputs to values between 0 and 1. The formula for **softmax** is:

$$
\sigma(x)_j = \frac{e^{x_j}}{\sum{e^{x_k}}^k_1}
$$

#### Error functions

Finally, the adjustment of each matrix weights is done by comparing the output against the expected value. Error functions are used to calculate the difference between these values, and the goal is to minimize it below a specific threshold.
Some errors functions that are used:
- Mean Squared Error. Usually used in regression problems.
- Cross Entropy. Usually used in classification problems.

#### Overfitting

Overfitting is the quality of having a model that almost exactly represents the behaviour of the data. In this case, noise or random elements, are also taken into account to build the model and may affect the estimation on new and unknown data. The model will fail generalizing for new inputs. 
The two solutions for overfitting are:
- Stop the training process early. This can be done by selecting a subset from the training set, named the validation set, and use it to validate when is pertinent to stop.
- Using regularization. It means imposing a constraint on the training of the network to have better generalization. Dropout is a common used technique for this.

#### Mini batch training

Generalizing the gradient results from a set of N steps before applying them to the weights on the network. The benefits are:
- Reduces the complexity of the training process
- Noise reduction

$$
\delta = \frac{1}{N} \sum{\delta_{ij}}_k^N
$$



### Vanishing Gradient Problem

When the gradient applied to adjust the weight matrices connecting the layers within a network is too small, the contributions to the network are not as relevant, eventually stalling the process of learning.

### Exploding Gradient Problem

When the gradient grows uncontrollably. Usually a concept named Gradient Clipping is used to resolve this issue. 

The Gradient Clipping process works by, at a given timestep $t$, if the current gradient exceeds a given threshold, the successive gradient is normalized.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwNTMxNzE3NSwxOTUwOTU5NjA0LC0xMT
k5NjAwODkyXX0=
-->