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

![Different cases on learning rate](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/learningrate.png)

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

For choosing the number of epochs, the validation error can be used in a technique called **Early stopping**. This means the training should stop, when the error stops decreasing. As the validation error can jump from decreasing to increasing and back to decreasing, is best to apply this technique when it hasn't improved in the last 10 or 20 steps. 

## Model Hyperparameters

Are more involved in the structure of the model. This include: 

### Number of layers and hidden units*

The number of layers and hidden units should be proportional to the complexity of the function that the neural network is trying to learn. **This hyperpameter is the main measure for a model's learning capacity**. However, if the model has too much capacity it may tend to overfit.

According to the content, having more hidden units that inputs is a good starting value, and, three hidden layers is the most beneficial architecture to start with. Having as an exception, Convolutional Networks, as the more deeper they are the better they perform.

### Model specific hyperparameters for architectures like RNNs*.

In this case, vanilla RNNs tend to perform worse than LSTMs and GRUs. The recommendation is to test both when deciding between LSTMs and GRUs. 
In this matter, it is also recommended using a depth of 2 layers. 

[*] Recommendations given from papers presented in the course.

## Further Literature

- [Practical recommendations for gradient-based training of deep architectures](https://arxiv.org/abs/1206.5533)
- [Deep Learning Book - Chapter 11.4: Selecting Hyperparameters](http://www.deeplearningbook.org/contents/guidelines.html)
- [Neural Networks and Deep Learning book - Chapter 3: How to choose a neural network's hyper-parameters?](http://neuralnetworksanddeeplearning.com/chap3.html#how_to_choose_a_neural_network%27s_hyper-parameters)
- [Efficient BackProp](http://yann.lecun.com/exdb/publis/pdf/lecun-98b.pdf)
- [Visualizing and Understanding Recurrent Networks](https://arxiv.org/abs/1506.02078)

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc4NDEwNTQxNiwxMDg3MzU5MDAyLDg5Nj
c4ODMxMSwtODk5ODE0MDUzLC0xNzc5OTY1ODQsLTE0NDkxNzIx
NzddfQ==
-->