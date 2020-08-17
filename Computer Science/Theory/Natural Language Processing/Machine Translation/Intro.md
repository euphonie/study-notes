# Machine Translation

## Using RNNs

**Basic Architecture**

**Input**. The input vector fed into the neural network should be one-hot encoded vectors for each token that is expected to be translated. If each training input (sentence) contains a different quantity of tokens, padding can be used to have same width vectors for all training values.

**Architecture**. The architecture composes of: 
- **Embedding Layer**. Helps enhance the representation of the word. It generates a more compact word vector. 
- **Recurrent Layer(s)**. They incorporate information from the whole sequence, modifying how each token affects or is affected by neighboring tokens.

This two steps allow to maximize the information that can be gathered from similarities and differences between words in the current sequence. 

- Dense Layer
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNzY2NjMyNjddfQ==
-->