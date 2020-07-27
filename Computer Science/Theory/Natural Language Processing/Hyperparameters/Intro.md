> All information gathered from Udacity's Natural Language Processing Nanodegree

# Hyperparameters

A hyperparameter is a value that is need to be set before applying a learning algorithm into a dataset. Like

```python
learning_rate = 0.01
minibatch_size = 32
epochs = 12
```

This parameters widely vary and there is no definitive answer for setting them up. 
They can be separated into two categories: 

## Optimizer Hyperparameters

Related to the optimization and training process than to the model itself. They include:

###Learning Rate

The most important hyperparameter and also should be tuned up. A good starting point is $0.01$, and the recommended values are: 
- 0.1
- 0.01
- 0.001
- 0.0001
- 0.00001
- 0.000001

> image learningrate

A technique named **Learning Rate Decay** is good at moments where the gradient step applied to the weights keeps the error as far from the minima as in the previous step. It can be done by:
- Decreasing the learning rate by half every 5 epochs to do it linearly
- Decreasing the learning rate by a factor of 0.1 every 8 epochs to do it exponentially

There are algorithms that use **Adaptive Learning** that decreases or increases the learning rate according to the obtained results of each epoch.

### Minibatch Size

This parameter impacts in speed and the number of iterations. There are two ways of backpropagating the error to the weights of a neural network, it can be either: 
- Online (stochastic). Where for every input the process of backpropagation will calculate error and adjust the weights, or through
- Batch (Batch training). Where calculation of the error and adjustment of the weights will be executed per batch size.

In this case, online training can also be referred to minibatch training of size 1. 

Recommended values are as following: 
- 1
- 2
- 4
- 8
- 16
(Good Candidates)
- **32** 
- **64** 
- **128** 
- **256** 

Higher mini batch sizes requires more memory for the training process and, generally, more computational resources. While keeping the same learning rate, higher mini batch sizes decrease the accuracy of the model (This is according to the paper [Systematic evaluation of CNN advances on the ImageNet](https://arxiv.org/abs/1606.02228)); on comparison, if learning rate changes with minibatch size the decrease is less significant. 
Lower mini batch sizes permits to escape local minima for computing the error in training. 
*Note*: Some Out of Memory errors in TensorFlow can be eliminated by decreasing minibatch size.

### Number of Epochs

For choosing the number of epochs, the validation error can be used in a technique called **Early stopping**. This means the training should stop, when the error stops decreasing. As the validation error can jump from decreasing to increasing and back to decreasing, is best to apply this technique when it hasn't improve

## Model Hyperparameters

Are more involved in the structure of the model. This include: 
- Number of layers and hidden units
- Model specific hyperparameters for architectures like RNMs.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5Njg4NzY3MSw4OTY3ODgzMTEsLTg5OT
gxNDA1MywtMTc3OTk2NTg0LC0xNDQ5MTcyMTc3XX0=
-->