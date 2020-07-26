> All information gathered from Udacity's Natural Language Processing Nanodegree

# Long Short-Term Memory Cells (LSTM)

This neural network structure allows to avoid the vanishing gradient problem. It does it by allowing certain inputs to be latched, or stored, for long periods of time in case they are needed in future steps of the training process.

![RNN cell structure](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/lstm1.png)

The main difference in the process of activation of the "cell" vs RNNs, is that LSTM cells are composed of four calculations. All of them are differentiable, which means a gradient function can be computed and allow to hold values over 1,000 previous iterations.

![LSTM cell structure](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/lstm2.png)

The operations inside the cell are used for the following processes. This functions are also trained through backpropagation to adjust to the data:
- What goes into the cell
- What is retained within the cell
- What passes to the output

## High-Level architecture LSTM

A LSTM works by conserving Long Term Memory (**LTM**) and Short-Term Memory (**STM**) and finding better predictions of the current event thanks to an ensemble of the two. At high-level it comprises four gates: 

> image lstmarch
> image lstmarch2


### Forget Gate
Takes Long Term Memory and it forgets everything that is not considered useful.

> image forgetgate

The output is calculated as $LTM_{t-1}f_t$, where:

$$
f_t = \sigma(W_f[STM_{t-1}, E_t] + b_f)
$$

### Remember Gate
Takes the information conserved from the Forget Gate and joins it with the information obtained in the Learn Gate. This outputs to an updated Long Term Memory.

> image remembergate

The output is calculated as $LTM_{t-1}f_t + N_ti_t$, where: 

$$
N_t = tanh(W_n[STM_{t-1}, E_t] + b_n)
$$
$$
i_t = \sigma(W_i[STM_{t-1}, E_t] + b_i)
$$
$$
f_t = \sigma(W_f[STM_{t-1}, E_t] + b_f)
$$

### Learn Gate
Takes the Short Term Memory and the current event and joins them, ignoring certain information.

> image learngate

The output is calculated as $N_ti_t$, where: 

$$
N_t = tanh(W_n[STM_{t-1}, E_t] + b_n)
$$
$$
i_t = \sigma(W_i[STM_{t-1}, E_t] + b_i)
$$


### Use Gate
Decides what to take from the information conserved from the Forget Gate and the information conserved from the Learn Gate. This outputs becomes an updated Short Term Memory and the prediction.

> image usegate

The output is calculated as $U_tV_t$, where:

$$
U_t = tanh(W_uLTM_{t-1}f_t + b_u)
$$
$$
V_t = \sigma(W_v[STM_{t-1}, E_t] + b_v)
$$

## Architecture of LSTMs

> image finalarch

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMDQ5MjY0MjksMzY5NjkwNDg2LC0xMT
Y1MjA2NDAsMTQxNjM0MzE4OSwxNzQyODQ3MDgxLDE5MDE1MTcz
MjUsMTYxMjczMTY2OSw3MTQzMjg1MTVdfQ==
-->