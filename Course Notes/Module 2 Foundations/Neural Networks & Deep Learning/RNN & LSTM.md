# RNN & LSTM

---

# What are they?

- Recurrent Neural Networks (RNNs) are a type of neural network architecture designed for sequential data processing
    - RNN remembers past inputs due to an internal memory which is useful for predicting stock prices, generating text, transcriptions, and machine translation
- They are particularly effective in tasks where the input data has a temporal or sequential structure, such as time series analysis, natural language processing, and speech recognition
- To prevent forgetting, it summarizes the state of the text in a vector (hidden state) and passes along an updated vector

# Why use them?

- Text sequences can have different history lengths
- **Recurrence:** Process each time-slice recursively

# Overview

---

Here's a high-level explanation of what recurrent neural networks are and how they work:

1. **Sequential Processing:**
    - RNNs are designed to handle sequences of data, which could be sequences of words in a sentence, time steps in a time series, or any other ordered set of observations
2. **Memory and Feedback Loop:**
    - The key feature of RNNs is their ability to maintain a form of memory or context across time steps
        - Each RNN unit has a hidden state that captures information from previous time steps and carries it forward
    - This is achieved through a feedback loop, where the output at each time step becomes part of the input for the next time step
        - The hidden state acts as a memory that retains information about previous inputs
3. **Parameter Sharing:**
    - RNNs share the same set of parameters across all time steps
        - This parameter sharing allows the network to learn to capture patterns and dependencies in sequential data, making them more efficient than standard feedforward neural networks for sequential tasks
4. **Architecture:**
    - The basic RNN unit takes an input at each time step, produces an output, and updates its hidden state
        - This hidden state serves as a kind of memory that carries information from the past into the future
5. **Long-Term Dependencies:**
    - One limitation of basic RNNs is the difficulty in capturing long-term dependencies
    - As the network processes more time steps, the influence of early inputs diminishes
        - This challenge is addressed by more advanced RNN architectures like Long Short-Term Memory (LSTM) networks and Gated Recurrent Units (GRUs), which are designed to better capture long-term dependencies

# Key Components

1. **Input Sequences:**
    - RNNs take input sequences, where each element in the sequence represents information at a specific time step
        - This can be sequences of words in a sentence, time steps in a time series, or any other ordered set of observations
2. **Recurrent Connection:**
    1. The key feature of an RNN is the recurrent connection, which allows information to persist across different time steps
        1. At each time step, the hidden state from the previous time step is used in combination with the current input to produce the output and update the hidden state
3. **Hidden State:**
    - It captures information about previous elements in the sequence and influences the processing of future elements
        - It is updated at each time step based on the current input and the previous hidden state
4. **Weights and Biases:**
    - RNNs have parameters (weights and biases) that are shared across all time steps
        - These parameters determine how information from the current input and hidden state influences the computation of the next hidden state and output
5. **Output:**
    - At each time step, the RNN produces an output based on the current input and hidden state
        - This output can be used for various tasks, such as predicting the next element in the sequence or classifying the sequence
6. **Backpropagation Through Time (BPTT):**
    - Training an RNN involves updating its parameters based on the error between predicted and actual outputs
        - Backpropagation Through Time (BPTT) is an extension of the standard backpropagation algorithm to handle sequences, allowing the network to learn from the temporal relationships in the data

# How do they work?

- The update equations for a basic RNN can be expressed as follows, where $h_t$ is the hidden state at time $t$, $x_t$ is the input at time step $t$, and $y_t$ is the output at time step $t$:
    
    $$
    \begin{align}
    h_t &= \text{activation}(W_{hh} *h_{t-1} + W_{xh} * x_t + b_h)
    \\
    y_t &= W_{yh} * h_t +b_t
    
    \end{align}
    $$
    
    - Where:
        - $W_{hh}$ and $W_{xh}$ are the weight matrices for the ***recurrent and input connections***, respectively
        - $W_{yh}$ is the weight matrix for the output layer
        - $b_h$ and $b_y$ are the bias vectors for the hidden state and output layer, respectively

- The figure below illustrates the computational logic of an RNN at three adjacent time steps. At any time step $t$, the computation of the hidden state can be treated as:
    1. Concatenating the input $X_t$ at the current time step $t$ and the hidden state $H_{t-1}$ at the previous time step $t_{t-1}$
    2. Feeding the concatenation result into a fully connected layer with the activation function $\phi$
        1. The output of such a fully connected layer is the hidden state $H_{t}$ of the current time step $t$
            1. In this case, the model parameters are the concatenation of $W_{xh}$ and $W_{hh}$, and a bias of $b_h$, all from [(9.4.5)](https://d2l.ai/chapter_recurrent-neural-networks/rnn.html#equation-rnn-h-with-state)
            2. The hidden state of the current time step $t$, $H_{t}$, will participate in computing the hidden state $H_{t+1}$ of the next time step $t+1$
            3. What is more, $H_{t}$ will also be fed into the fully connected output layer to compute the output $O_{t}$ of the current time step $t$

![Untitled](RNN%20&%20LSTM%20063950076f2d468b9a471dc5b235338b/Untitled.png)

# Training an RNN

- **Training Data**
    - $x$: Token ID of $\text{word}_{t-1}$
    - $y$: Token ID of $\text{word}_{t}$
- **Input:** $x$ + hidden state $t-1$
- **Output: $\Braket {\log P(w_1), \log P(w_2), ...\log P(w_i),..., \log P(w_{|V|})}$**
- **Cross Entropy Loss:** $\text{loss} = - \log P(w_i)$
    - Loss is how far away from 0.0 in the target index prediction
        - I.e. If its close to 0, we almost picked the right word

# Generating Text with an RNN

- Start with a word ($\text{word}_i$) and an empty hidden state (all zeros)
- Generate a distribution:
    
    $**\Braket {\log P(w_1), \log P(w_2), ...\log P(w_i),..., \log P(w_{|V|})}**$ 
    
- $\text{word}_{t+1}$ is the ***argmax*** of the distribution
    - The output token is the index of the vector with the highest score
- Feed the output back into the neural network for the next time slice $t+1$
    - Use generated $\text{word}_{t+1}$ plus the new hidden state as input to produce $\text{word}_{t+2}$
- Repeat until done

# Types of RNN’s

![Untitled](RNN%20&%20LSTM%20063950076f2d468b9a471dc5b235338b/Untitled%201.png)

# Challenges & Limitations

- **Vanishing and Exploding Gradients**
    - Basic RNNs can face issues with vanishing or exploding gradients, hindering their ability to capture long-term dependencies
        - LSTM and GRU architectures are designed to mitigate these problems
    - **Vanishing Gradient Problem:**
        - In RNNs, during the process of backpropagation through time (BPTT), gradients are computed and propagated back through the network to update the weights
            - The problem arises when the gradients become very small as they are backpropagated through many time steps
            - This results in the weights of the earlier layers getting updated by extremely small values or not getting updated at all
            - As a consequence, the RNN struggles to learn long-term dependencies because the influence of distant past inputs on the current prediction diminishes rapidly
                - The model ends up "forgetting" or being unable to effectively use information from earlier time steps
    - **Exploding Gradient Problem:**
        - On the flip side, exploding gradients can also occur. This happens when the gradients become extremely large as they are backpropagated through time
            - In this case, the weights can be updated by extremely large values, leading to unstable training and divergence
        - Exploding gradients make it difficult to train the network effectively, as large weight updates can cause the model to oscillate or diverge instead of converging to a solution
    - The vanishing and exploding gradient problems are more pronounced in RNNs due to the nature of their recurrent connections
        - In an RNN, the same set of weights is used across different time steps, and during backpropagation, the gradients are multiplied at each time step
        - If these multiplicative factors are consistently less than 1 (vanishing) or greater than 1 (exploding), the problems occur
- **Parallelization**
    - RNNs are inherently sequential, which can limit parallelization during training
        - This limitation has led to the development of parallelizable architectures like the Transformer for certain sequence-to-sequence tasks
- **Hidden State**
    - It’s hard to learn how to pack the information into a fixed-length hidden vector
    - Every time slice the RNN might re-use part of the vector, overwriting or corrupting previous information

# Long Short Term Memory Networks (LSTM)

---

[LSTM](RNN%20&%20LSTM%20063950076f2d468b9a471dc5b235338b/LSTM%20bf5ceb4b52764b5995a93d9a1905f9cd.md)

# Resources

- [Stanford Overview](https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks)
- [CS231 DL Course](https://cs231n.github.io/rnn/)
- [Datacamp](https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network)
- [D2L](https://d2l.ai/chapter_recurrent-neural-networks/)
- [Deep Learning Book](https://www.deeplearningbook.org/contents/rnn.html)
- [Vanilla RNN](https://calvinfeng.gitbook.io/machine-learning-notebook/supervised-learning/recurrent-neural-network/recurrent_neural_networks)
- [TDS](https://towardsdatascience.com/recurrent-neural-networks-rnns-3f06d7653a85)
- [Slides](https://slazebni.cs.illinois.edu/spring17/lec20_rnn.pdf)

### Blogs

- [Illustrated Guide](https://towardsdatascience.com/illustrated-guide-to-recurrent-neural-networks-79e5eb8049c9)

### Types & Overview

- [https://medium.com/@saba99/recurrent-neural-network-rnn-a56cef50d843](https://medium.com/@saba99/recurrent-neural-network-rnn-a56cef50d843)

###