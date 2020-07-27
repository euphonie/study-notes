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

- Minibatch Size
- Number of Epochs

## Model Hyperparameters

Are more involved in the structure of the model. This include: 
- Number of layers and hidden units
- Model specific hyperparameters for architectures like RNMs.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3Nzk5NjU4NCwtMTQ0OTE3MjE3N119
-->