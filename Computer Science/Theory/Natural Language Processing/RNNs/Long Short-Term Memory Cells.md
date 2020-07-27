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

![LSTM architecture](https://raw.githubusercontent.com/euphonie/study-notes/master/Computer%20Science/Theory/Natural%20Language%20Processing/RNNs/lstmarch.png)
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


## Other architectures

### Gated Recurrent Unit (GRU)

Combines the forget and learn gate into one Update Gate and then outputs the value into a combine gate. It only retains one working memory.

> image gru

### Peephole connections 

Regarding the Forget Gate, the value use to forget some elements from the LTM is defined by $f_t$. However, this vector does not take into account the LTM at all as is a result from $STM_{t-1}$ and $E_t$. 
In this case, peephole connections might add up LTM to modify the values of $f_t$ using a connection as shown in the following image, which would change $f_t$ to:

> image peephole1

$$
f_t = \sigma(W_f[LTM_{t-1}, STM_{t-1}, E_t] + b_f)
$$

This process can be replicated to all the forget gates to have a new LSTM architecture as follows:

> image peephole2


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDA1OTMwMjUsNTQwMjIwMjQ5LDM2OT
Y5MDQ4NiwtMTE2NTIwNjQwLDE0MTYzNDMxODksMTc0Mjg0NzA4
MSwxOTAxNTE3MzI1LDE2MTI3MzE2NjksNzE0MzI4NTE1XX0=
-->