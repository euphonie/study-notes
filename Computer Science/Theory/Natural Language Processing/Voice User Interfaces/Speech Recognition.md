
# Speech Recognition

**ASR**. Automatic Speech Recognition. Has as goal to input any continuous audio speech and output the text equivalent.
**Sound signal** the data used in ASR.
- Models can be divided in 
	- Acoustic Model. Solves the problem of turning sound signals into some kind of phonetic representation.
	- Language Model. Houses the domain knowledge of words, grammar and sentence structure for the language.

**Challenges in ASR**
- Variability
	- Pitch 
	- Volume
	- Speed
- Ambiguity
	- Word boundaries
	- Spelling
	- Context

# Signal Analysis

- Speech can be thought to be created by sinusoidal waves in air. Higher pitches vibrate faster with a higher frequency than lower pitches.
- Acoustical energy carried in a sound wave can be transduced to electrical energy to be recorded as an audio signal
	- The amplitude of signal tells how loud or how much acoustical energy is in a specific region.
	- In a time slice from an audio sample, several frequencies conform the resulting sinusoidal wave identify in the sample. This is created by the sum of the multiple existing frequencies being recorded. 
	- Each **component frequency** could be used as a feature using a **Fourier Transform** to break the signal into the components
	- The FFT Algorithm (Fast Fourier Transform) can be used for this task.
- A spectogram can


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDAyNzU2NzgsMjAwNzY1MDQ1MF19
-->