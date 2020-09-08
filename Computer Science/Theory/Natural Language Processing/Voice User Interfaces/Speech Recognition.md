
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

**Acoustic models and time **
- DTW calculates the similarity between two signals, even if their time lengths differ. This can be used in speech recognition, for instance, to align the sequence data of a new word to its most similar counterpart in a dictionary of samples.
	- Also HMMs can help with this task
	- With Deep Neural Networks the sequencing problem reappears, is better use a hybrid HMM/DNN system or with **Connectionist Temporal Classification (CTC)**

# HMMs in Speech Recognition

- HMMs can be trained with label time series sequences to create individual HMM models for each particular sound unit (phonemes, syllables, words, or even group of words)
- Training is easier with isolated units
	- With a set of words, an HMM model is created for each one, and finally the score of every model is evaluated to identify which words its in the audio segment
- Training continuous words or phrases (**utterances**)
	- When same utterances are part of many sentences, pairs of utterances can be trained into an individual HMM model. Ex. my brick walkway and a brick wall could have HMMs for the pairs
		- my-brick
		- a-brick
		- brick-walkway
		- brick-wall
	- This increases dimensionality as a HMM model exists for every word and every pair 
	- Applying this technique to phonemes the dimensionality stays manageable. With a set of 40 phonemes 1600 HMMs are needed
	- Once trained new utterances can be identify through chains of probable paths

# Language Models
- The job of a language model is to inject the language knowledge into the words to text step in speech recognition
- Provides a layer between words and text to solve ambiguity in spelling and context
- The likelihood of a word in a given order can be thought as a probability distribution over many different words. The likelihood that the particular word sequence could have been produced by the audio signal. 
$$
P(signal|w_1,w_2)
$$
- A statistical language model provides a probability distribution over sequences of words
$$
P(w_1,w_2)
$$
- Merging the acoustic model and the language model would be the most likely sequence 

# Tools
- Corpus 
	- TIMIT (1993) - 630 speakers voicing 10 phoneme-rich sentences
- Vocabulary sources
	- LDC Wall Street Journal Corpus - 73 hours of newspaper reading
	- LibriSpeech Corpus  - 1000 hours of reading from public domain books

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjg0OTU0MzksODE4OTM3MDUxLDkyMT
I4NjU1MSwtMTQ0NjE4MTQ1NSwxOTU4MDM5NzAsNDE1MzU0MDM3
LDIwMDc2NTA0NTBdfQ==
-->