# Machine Translation

## Using RNNs

**Basic Architecture**

**Input**. The input vector fed into the neural network should be one-hot encoded vectors for each token that is expected to be translated. If each training input (sentence) contains a different quantity of tokens, padding can be used to have same width vectors for all training values.

**Architecture**. The architecture composes of: 
- **Embedding Layer**. Helps enhance the representation of the word. It generates a more compact word vector. 
- **Recurrent Layer(s)**. They incorporate information from the whole sequence, modifying how each token affects or is affected by neighboring tokens.
	- Inside the layer: input vector $x_t$ is multiplied by matrix $W_x$
	- A bias is added $x_tW_x + b$
	- Previous state vector $h_{t-1}$ is multiplied by matrix $W_h$ to produce $h_{t-1}W_h$
	- To produce current hidden state $h_t$, the formula $activation(x_tW_x + b + h_{t-1}W_h)$ is applied. Where $activation$ can be ReLU, sigmoid or tanh.
	- Finally output $y_t$ is calculated by having $h_t$ multiplied to another matrix, bias and applied another activation function.

This two steps allow to maximize the information that can be gathered from similarities and differences between words in the current sequence. 

![RNN schema](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/Deep%20Learning%20Attention/rnnschmeatic.png)

- **Dense Layer(s)**. Produce a softmax output, that can be interpreted as one-hot encoded words in target language. Output is usually padded as well to obtain same sized vectors.


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTM1Mzk2MTEsMTkzMjAxMjkwNF19
-->