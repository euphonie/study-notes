
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
- Cepstral analysis + Mel Frequency Analysis obtain between 12 and 13 MFCC features related to speech http://www.speech.cs.cmu.edu/15-492/slides/03_mfcc.pdf
	- To this, Delta and Delta-Delta MFCC features can optionally be appended to the feature set. It increases the number of features up to 39 and improves results. [http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/](http://practicalcryptography.com/miscellaneous/machine-learning/guide-mel-frequency-cepstral-coefficients-mfccs/)
- The benefits are
	- Reducing dimensionality of data
	- Reducing noise

# Phonetics
- Study of sound in human speech. A language can be defined by phonemes, which are small segments of distinct sounds. US english generally has between 33-44.
- In contrast, a grapheme is the smallest distinct unit in written language. A small grapheme set in US english could be 26 letters plus the whitespace.
- ARPABET is a phoneme set for US english created in 1971. It has 39 phonemes, 15 vowel sounds and 24 consonants, each represented as a one or two-letter symbol.
- If phonemes can be extracted from an audio signal the next step is matching the phonemes to the related words they comprise. This is called **Lexical Decoding**.
	- It is based on a lexicon or dictionary of the data set.
- A design choice could be transforming directly from the acoustic model into words, this can be useful when training with a limited vocabulary.


# Corpus 
- TIMIT (1993) - 630 speakers voicing 10 phoneme-rich sentences
- 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ1ODI0NjgzNSw5MjEyODY1NTEsLTE0ND
YxODE0NTUsMTk1ODAzOTcwLDQxNTM1NDAzNywyMDA3NjUwNDUw
XX0=
-->