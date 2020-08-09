# Sequence to Sequence


## Applications

Sequence to Sequence RNNs have architectures that allow to output a series of vectors that can contain from images, to words, to letters, from an input of sequence vectors.
It can be used for translation, summarization, Q&A answering model or a chatbot. 


## Architecture

The architecture for a sequence to sequence model consists of two RNNs. It has a:
- Encoder. Handles the input sequence and gives what was understood to the second RNN. It hands over a context, also represented as a fixed size tensor called the state or context.
- Decoder. Generates the output sequence.

*Note:* the bigger the size of the RNN cell, the more capacity it has to learn the patterns of the sequences and the more resource-intensive it will be.

> image s2s
> image s2sdetailed

### On detail

> image s2s2

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MjU4Nzg3MywxNDE5NjYyNjUyXX0=
-->