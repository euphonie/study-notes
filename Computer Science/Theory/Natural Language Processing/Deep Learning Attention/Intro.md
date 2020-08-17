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
- Dot Product. In this 
- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk5MDc4NjY4OSwtMTk5ODc5MjE4MywxMD
U3NzY4NDQsLTE3NDI4MzkwODAsLTEwNzU2NDAzMjEsNzQ4NTIw
MTk1XX0=
-->