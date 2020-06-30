> All information gathered from Udacity's Natual Language Processing Nanodegree

# Naive-Bayes for NLP

## Bayes Theorem

Bayes Theorem constructs a probability of the occurrence of an event by aggregating known probabilities on smaller events that build up to the one that we want to understand.

It compounds of two sets of probabilities called: Inferior and Posterior, named by the time of knowledge of the events' probabilities.

It stands on this premises to move from a Known probability to an Inferred probability

#### Known probabilities (These should be given)
$$ P(A) \\
P(B|A) $$

#### Inferred probability
$$
P(A|B)
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

The probability of event `P(R ∩ A)` is calculated by the multiplication of `P(A)*P(R|A)`

#### Scenarios

Therefore the previous probabilities for the events are the following. Here we are computing the probabilities `P(B|A)` using the naive bayes' form. This means 

$$
P(Alex|Red sweater) = P(Alex) * P(Red sweater|Alex) = 0.75 * 0.4 = 0.3 \\
P(Alex|Other sweater) = 0.75 * 0.6 = 0.45 \\
P(Brenda|Red sweater) = 0.25 * 0.6 = 0.15 \\
P(Brenda|Other sweater) = 0.25 * 0.4 = 0.1
$$
But as only the conditions having red are needed, is required to normalize both scenarios in order that they add to one.

#### Normalization
$$
P(A|R) = \frac{P(R|A)}{P(R|A)+P(R|B)}
$$
Results from examples
$$
P(Alex|Red sweater) = \frac{0.75 * 0.4}{0.75*0.4 + 0.25*0.6} = 0.67
$$
$$
P(Brenda|Red sweater) = \frac{0.25*0.6}{0.25*0.6 + 0.75*0.4} = 0.33 
$$

## Bayes Theorem Formula

Possible Scenarios for two sets of hypothesis

$$
P(R \cap A) = P(A)P(R|A) \\
P(R^c \cap A) = P(A)P(R^c) \\
P(R \cap B) = P(B)P(R|B) \\
P(R^c \cap B) = P(B)P(R^c|B)
$$

#### Normalization

$$
P(A|R) = \frac{P(A)P(R|A)}{P(A)P(R|A) + P(B)P(R|B)} \\
$$
$$
P(B|R) = \frac{P(B)P(R|B)}{P(B)P(R|B) + P(A)P(R|A)}
$$


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1Njc2OSwyMjc0ODMwOTYsNTE4MTM2NT
k3LDI1NTc3NjUwMiwtMjA3MDk0MTY5OSwtMTE2NzA4Mjg1OSwt
MTE3ODMxNjkyOCw0OTQzNzEzNTksNzEyMDM3MTE4LC0xODMxND
QyNjY3LC0yMDUyNzQ4NDU5LDk0OTY3MzA0Ml19
-->