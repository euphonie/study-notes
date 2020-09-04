
# Voice User Interfaces

Voice-enabled agents are common in phones, computers, cars. 
End-to-end usual pipeline:
- Audio waves are converted into language texts using ML algorithms and probabilistic models
- The resulting text is reasoned using AI logic to determine the meaning and formulate a response
- The response text must be converted back into understandable speech with ML tools

## Pipeline
- Voice to text (Speech Recognition)
	- Sound vibrations are converted to an audio signal
	- The signal is sample in some way and the samples can be converted into vectors of component frequencies **(Spectogram)**
		- The vectors represent features of sound in a data set (Feature extraction)
	- Decode series of vectors
		- Uses probabilistic models that go well with sampled data **(Acoustic model)**
			- Hidden Markov Models (HMMs) and Recurrent Neural Networks (RNNs) are good candidates
		- Gives a best guess as to what the words are
	- Adding a **Language Model**
		- Helps understand the common order of sequences probable in human language
		- It may also be needed an **Accent Model**
- Text to text 
	- Reasoning Logic. Understand what we want and mean when we speka

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzUzMDEzMTZdfQ==
-->