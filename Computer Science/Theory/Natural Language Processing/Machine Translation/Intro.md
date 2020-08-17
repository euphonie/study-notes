# Machine Translation

## Using RNNs

**Basic Architecture**

**Input**. The input vector fed into the neural network should be one-hot encoded vectors for each token that is expected to be translated. If each training input (sentence) contains a different quantity of tokens, padding can be used to have same width vectors for all training values.

**Architecture**. The architecture composes of: 
- **Embedding Layer**. Helps enhance the representation of the word. It generates a more compact word vector. 
- **Recurrent Layer(s)**. 
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA2Nzk1MzI4XX0=
-->