> All information gathered from Udacity's Natural Language Processing Nanodegree

# Deep Learning Attention

Attention started as an attempt to mimic human perception. "...humans focus attention selectively on parts of the visual space to acquire information when and where it is needed, and combine information from different fixations over time to build and internal representation..." (Recurrent Models of Visual Attention, 2014)

## Description

Deep Learning Attention incorporates a modification into sequence to sequence models to allow previously missing information, hidden states from the first up to the second last, to be sent to the decoder.

![Sequence to Sequence with attention](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Deep%20Learning%20Attention/s2sattention.png)

## The Attention Decoder

The decoder scores the hidden states that are sent from the encoder, applies a softmax function to the values to distribute the relative importance. And finally, it multiplies the values with each hidden state and sums them up into a Attention Context Vector. 
It is important to notice that for each timestep the Attention Context Vector is computed again with the corresponding hidden state.

![Description of the process within the Attention Decoder](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Deep%20Learning%20Attention/contextvector.png)


## Scoring functions

Scoring functions usually take two parameters, where $h_t$ is the current hidden state of the decoder, and $\bar{h}_s$ is a set of the hidden states received from the encoder: 
$$
score(h_t, \bar{h}_s)
$$
Where $t$ refers to the current time step of the decoder.

> image multiplicative

The scoring function can be evaluated using the following methods: 

**1. Dot Product**
 It is used to obtain the similarity measure between vectors by understanding the magnitudes and angles that separate each one. Formula: $|a||b|cos\theta$.

This means the output between two vectors is larger given a smaller angle $\theta$. Alternatively, the larger the angle $\theta$ is the smaller the resulting value will be.

The generalization for multiplying by the vectors $\bar{h}_s$  is: 

$$
h_t^T\bar{h}_s
$$
Where the current hidden state is transposed (to have dimensions $1 *n$) and multiplied against a matrix composed by the encoder vectors.

**2. Variation on Dot Product**

In case, the encoder and decoder work with different sized embedding vector spaces, there is a variation that can be applied to the dot product formula.

It introduces a weight matrix $W_a$, it's a linear transformation which allows input and output to use different embeddings.

$$
score(h_t, \bar{h}_s = h_t^TW
$$

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY2NjEyODg3Nyw0NzQ0NTA4NzYsNzAxMT
c1MDgzLC0xMDU0MDE2Mzk2LC0xOTk4NzkyMTgzLDEwNTc3Njg0
NCwtMTc0MjgzOTA4MCwtMTA3NTY0MDMyMSw3NDg1MjAxOTVdfQ
==
-->