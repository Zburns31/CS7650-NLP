# Encoders

---

# High-Level Overview

- **Function:** The encoder is responsible for transforming the input data into a compressed or encoded representation, typically of lower dimensionality
- **High-Level Explanation:** Think of the encoder as a feature extractor. It takes raw input data and compresses it into a more compact and meaningful representation, capturing essential features or patterns
- **Architecture:** The encoder is usually composed of one or more layers of neurons (nodes), forming the encoding part of the autoencoder
    - The activation of these neurons represents the compressed representation of the input data
- **Purpose:** The goal of the encoder is to reduce the dimensionality of the input while retaining relevant information, facilitating efficient representation learning

# Goals

- A good set of parameters will:
    - Represent the input wth a minimal amount of corruption
    - Can be uncompressed to produce a prediction over the full range of outputs

# How do they work?

- Multiple RNN cells can be stacked together to form the encoder
    - RNN reads each inputs sequentially
- For every timestep (each input) $t$, the hidden state (hidden vector) $h$ is updated according to the input at that timestep $X_i$
- After all the inputs are read by encoder model, the final hidden state of the model represents the context/summary of the whole input sequence
- Example: Consider the input sequence “I am a Student” to be encoded
    - There will be totally 4 timesteps ( 4 tokens) for the Encoder model
    - At each time step, the hidden state $h$ will be updated using the previous hidden state and the current input

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a48361cdad743f51bd319a96b14f5820_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a48361cdad743f51bd319a96b14f5820_l3.svg)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a4f42eb1b1f90f3ca7a452331ceaf1e7_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a4f42eb1b1f90f3ca7a452331ceaf1e7_l3.svg)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e25b0812680a1e3b5ac148ec76d75332_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e25b0812680a1e3b5ac148ec76d75332_l3.svg)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-2103e5c98e40c343931f6f67fb89626f_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-2103e5c98e40c343931f6f67fb89626f_l3.svg)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e25b0812680a1e3b5ac148ec76d75332_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e25b0812680a1e3b5ac148ec76d75332_l3.svg)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-af64f1a114cc94a8d26d8f12f99f2222_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-af64f1a114cc94a8d26d8f12f99f2222_l3.svg)

# Encoder Vector

- This is the final hidden state produced from the encoder part of the model. It is calculated using the formula above
- This vector aims to encapsulate the information for all input elements in order to help the decoder make accurate predictions
- It acts as the initial hidden state of the decoder part of the model

# Example

- At the first timestep $t_1$, the previous hidden state $h_0$ will be considered as zero or randomly chosen
    - So the first RNN cell will update the current hidden state with the first input and $h_0$
    - ***Each layer outputs two things*** — updated hidden state and the output for each stage
    - The outputs at each stage are rejected and only the hidden states will be propagated to the next layer
- The hidden states $*h_i$* are computed using the formula:
    
    $$
    h_t = f(W^{hh} h_{t-1} + W^{hx} x_t)
    $$
    
- At second timestep $t_2$, the hidden state h1 and the second input $X_2$ will be given as input, and the hidden state $h_2$ will be updated according to both inputs
    - Then the hidden state $h_1$ will be updated with the new input and will produce the hidden state h2. This happens for all the four stages wrt example taken
    - A stack of several recurrent units (LSTM or GRU cells for better performance) where each accepts a single element of the input sequence, collects information for that element, and propagates it forward
    
    ![Untitled](Encoders%2032466e521ceb4eb6a7c4fda79069bf35/Untitled.png)
    

# Resources

- [https://medium.com/analytics-vidhya/encoders-decoders-sequence-to-sequence-architecture-5644efbb3392](https://medium.com/analytics-vidhya/encoders-decoders-sequence-to-sequence-architecture-5644efbb3392)
- [https://www.baeldung.com/cs/nlp-encoder-decoder-models](https://www.baeldung.com/cs/nlp-encoder-decoder-models)