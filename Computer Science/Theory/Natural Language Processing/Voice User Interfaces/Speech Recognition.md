
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
- A **spectogram** can be generated from the audio signal plotted as frequency by time
	- To create one, first a time slice of the audio signal should be obtained
	- Then the time slice should be split into frequency components using FFT
	- This turns each time frame into a **One Time Frame Vector** of amplitudes at each frequency.
	- Finally plotting all the vectors ordered by time a chart containing the **Spectogram** can be visualized.
- To reduce noise, feature extraction can be applied 

# Feature Extraction with MFCC

- The frequencies of the spectograms can be categorized in bins that are relevant to human ears and filter out sound that can't be heard. This is using the **Mel Scale and Mel-Frequency Filters**
- A **source/filter model**  is a representation of human sound generation where the source is the source is unique to an individual and the filter is the articulation of words that we use when speaking. **Cepstral Analysis** relies on this model.
	- The source visualized in human anatomy is the throat and the filter is comprised by the nose, tongue and insides of the mouth and their interrelations while letting the sound out.
- There are already algorithms that can be used to extract the **Cepstrum**.
	- It drops the source that is unique to every individual and preserves the shape of the sound made by the filter.
- Cepstral analysis + Mel Frequency Analysis obtain between 12 and 13 MFCC features related to speech
	- To this, Delta and Delta-Delta MFCC features can optionally be appended to the feature set. It increases the number of features up to 39 and improves results. 
- The benefits are
	- Reducing dimensionality of data
	- Reducing noise


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1ODAzOTcwLDQxNTM1NDAzNywyMDA3Nj
UwNDUwXX0=
-->