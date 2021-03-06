> All information gathered from Udacity's Natural Language Processing Nanodegree

# Sequence to Sequence


## Applications

Sequence to Sequence RNNs have architectures that allow to output a series of vectors that can contain from images, to words, to letters, from an input of sequence vectors.
It can be used for translation, summarization, Q&A answering model or a chatbot. 


## Architecture

The architecture for a sequence to sequence model consists of two RNNs. It has a:
- Encoder. Handles the input sequence and gives what was understood to the second RNN. It hands over a context, also represented as a fixed size tensor called the state or context.
- Decoder. Generates the output sequence.

*Note:* the bigger the size of the RNN cell, the more capacity it has to learn the patterns of the sequences and the more resource-intensive it will be.

![Sequence to Sequence architecture](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Sequence%20to%20Sequence/s2s.png)

![Detailed architecture](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Sequence%20to%20Sequence/s2sdetailed.png)

At the output of the decoder RNN theres is a layer that indicates which element from the vocabulary is chosen by analyzing the outputs. 

![Matrices within the sequence to sequence model](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Sequence%20to%20Sequence/s2s2.png)

![Logit process to determine currrent output from the vocabulary](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Sequence%20to%20Sequence/logi.png)

### Vocabulary

The vocabulary can contain position markers such as: 
- < PAD > 
- < EOS >, end of sentence
- < UNK >, unkown
- < GO >, start of sentence

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ4MDkwNTc1OCwtOTIyODU4ODkzLDE0MT
k2NjI2NTJdfQ==
-->