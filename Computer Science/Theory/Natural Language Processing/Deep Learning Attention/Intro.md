> All information gathered from Udacity's Natural Language Processing Nanodegree

# Deep Learning Attention

Attention started as an attempt to mimic human perception. "...humans focus attention selectively on parts of the visual space to acquire information when and where it is needed, and combine information from different fixations over time to build and internal representation..." (Recurrent Models of Visual Attention, 2014)

## Description

Deep Learning Attention incorporates a modification into sequence to sequence models to allow previously missing information, hidden states from the first up to the second last, to be sent to the decoder.

> image s2sattention

## The attention decoder

The decoder scores the hidden states that are sent from the encoder, applies a softmax function to the values to distribute the relative importance. And finally, i


> image contextvector

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY3ODYyMDE3LC0xMDc1NjQwMzIxLDc0OD
UyMDE5NV19
-->