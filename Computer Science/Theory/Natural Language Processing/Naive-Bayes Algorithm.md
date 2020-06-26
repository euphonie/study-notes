> All information gathered from Udacity's Natual Language Processing Nanodegree

# Naive-Bayes for NLP

## Bayes Theorem

Bayes Theorem constructs a probability of the occurrence of an event by aggregating known probabilities on smaller events that build up to the one that we want to understand.

It compounds of two sets of probabilities called: Inferior and Posterior, named by the time of knowledge of the events' probabilities.

It stands on this premises to move from a Known probability to an Inferred probability

#### Known probabilities
$$ P(A) \\
P(R|A) $$

#### Inferred probability
$$
P(A|R)
$$

### Example

#### Priors (Probability of seeing someone)
Alex goes to office 3 times a week
$$P(Alex) = 0.75$$
Brenda goes to office 1 time a week
$$P(Brenda)=0.25$$

#### Posteriors (Probability of wearing a red sweater)
Alex wears red 2 times a week (from a 5-day week)
$$P(Red sweater|Alex) = 0.4 \\
 P(Other color sweater|Alex) = 0.6$$
Brenda wears red 3 times a week (from a 5-day week)
$$P(Red sweater|Brenda) = 0.6 \\
P(Other sweater|Brenda) = 0.4$$

## Using Conditional probability

The probability of event `P(A|R)` is calculated by the multiplication of `P(A)*P(R)`

Therefore the previous co



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwMzI5ODQzLC0yMDUyNzQ4NDU5LDk0OT
Y3MzA0Ml19
-->