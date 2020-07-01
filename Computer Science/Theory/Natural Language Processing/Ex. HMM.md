# Building Hidden Markov Models


```python
import matplotlib.pyplot as plt
import numpy as np

from helpers import show_model
from pomegranate import State, HiddenMarkovModel, DiscreteDistribution
```
𝜆=(𝐴,𝐵) specifies a Hidden Markov Model in terms of an emission probability distribution 𝐴 and a state transition probability distribution 𝐵.
At each time 𝑡, 𝑋𝑡 represents the hidden state, and 𝑌𝑡 represents an observation at that time.

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0MTUzOTc4OF19
-->