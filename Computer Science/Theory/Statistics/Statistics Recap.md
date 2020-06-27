# Statistics

## Probability

- Event. The outcome of a given event or more than one event that is likely or unlikely to happen.
- Probability of an event A. This is equal to the number of preferred (favourable) outcomes over the number of all possible (sample space) outcomes.

Probability of getting head while tossing a coin
$$P(A) = \frac{1}{2} = 0.5$$

Probability of getting an specific number while rolling a dice
$$P(A) = \frac{1}{6} \approx 0.167$$

- Probability of independent events. Probability of first event times the probability of the second event.
$$P(A \cap B) = P(A)P(B)$$
Probability of getting an ace of spades while playing cards
$$P(Ace \cap Spades) = P(Ace)P(Spades) $$

### Expected Values
The average outcome we expect if we run an experiment many times.

#### Experiment
To get the unknown probability of an event we can conduct an experiment which comprises several trials. A trial is taking a measure of the event and recording the resulting outcome. 
In this case, multiple trials could help having a certainty of probability of how likely is the preferred event to occur. Doing multiple trials is known as an experiment.

>  E.g. doing 20 coin tosses and recording the outcome of each would be considered as a Single experiment with 20 trials

#### Experimental probabilities
A probability obtained after performing an experiment.
The probability is then calculated as 
$$P(A) = \frac{successful\;trials}{all\;trials}$$
#### Theoretical (True) probabilities
Known probabilities

### Calculating Expected Values

`E(A)` is the outcome we expect to occur when we run an experiment.

For **categorical outcomes**, the formula is then calculated by multiplying the probability of the preferred event by the number of trials.
$$E(A) = P(A) * n$$

If we wanted to get the ace of spades from a deck of cards while executing 20 draws, the formula would be:
$$E(A) = 0.25 * 20 = 5$$
This means we would expect to get 5 times an A of spades running an experiment of 20 trials.

For **numerical outcomes**, the formula takes each of the values in the sample space and multiplies them by their probability. Then, all values are added up to get the expected value.

Having a sample space of three possible outcomes, the expected value would be calculated with:
$$E(X) = A*P(A) + B*P(B)+C*P(C)$$


### Probability Frequency Distribution

A collection of the probabilities for each possible outcome.

Using an example of throwing two dices and recording how many times is possible to obtain all results (1 to 12).

| Sum | Frequency | Probability |
|:--------:| -------------:| -------------:|
| 2 | 1 | 1/36
| 3 | 2 | 2/36
| 4 | 3 | 3/36
| 5 | 4 |3/36
| 6 | 5 |5/36
| 7 | 6 |6/36
| 8 | 5 |5/36
| 9 | 4 |4/36
| 10 | 3 |3/36
| 11 | 2 |2/36
| 12 | 1 |1/36

> Written with [StackEdit](https://stackedit.io/).

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5NjI2NDUzMywtNjY5NzM0MjA0LDE1Mj
k1NjIxMDYsLTk4MjQ0MzY3NiwxNjQ5MDUxMTU0LDE5MjU1MTQx
MzcsLTEyNTYwMjYzNTldfQ==
-->