# Sequence-to-Sequence Models (Seq2Seq)

---

# What are they?

- Sequence-to-sequence learning (Seq2Seq) is about training models to convert sequences from one domain (e.g. sentences in English) to sequences in another domain (e.g. the same sentences translated to French)
    - This can be used for machine translation or for free-from question answering (generating a natural language answer given a natural language question) - in general, it is applicable any time you need to generate text
- **Sequence Modelling problems refer to the problems where either the input and/or the output is a sequence of data**

# How do they work?

- The idea is to use one [LSTM](https://paperswithcode.com/method/lstm), the *encoder*, to read the input sequence one timestep at a time, to obtain a large fixed dimensional vector representation (a context vector), and then to use another LSTM, the *decoder*, to extract the output sequence from that vector
- The second LSTM is essentially a recurrent neural network language model except that it is conditioned on the input sequence

# Key Components

- **Encoder**
    - The encoder takes in the input sequence and processes it into a fixed-size context vector
        - This context vector aims to capture the essential information from the input sequence
        - The encoder can be a recurrent neural network (RNN), Long Short-Term Memory (LSTM) network, or another type of neural network
        - The hidden states of the encoder capture the contextual information at each time step of the input sequence
            - The final hidden state or a combination of hidden states serves as the context vector
- **Context Vector**
    - The context vector summarizes the input sequence and acts as the initial hidden state for the decoder
        - It contains the encoded information about the input sequence
- **Decoder**
    - The decoder takes the context vector as input and generates the output sequence step by step
    - Like the encoder, the decoder can be an RNN, LSTM, or another type of recurrent network
    - At each time step, the decoder produces an output based on its current hidden state and the previously generated outputs
        - The hidden state is updated using the context vector and the previously generated output
- **Attention Mechanism (Optional)**
    - In some Seq2Seq models, an attention mechanism is incorporated to allow the decoder to focus on different parts of the input sequence at each time step
    - This attention mechanism helps the model to better capture long-range dependencies in the input sequence.

# Architecture

![Untitled](Sequence-to-Sequence%20Models%20(Seq2Seq)%2030c54efad6e1425ca3929ac5f156fe20/Untitled.png)

# Model Training

# Key Terms & Concepts

- **Teacher Forcing:** Teacher forcing is a training technique used in recurrent neural networks (RNNs) and other sequence-to-sequence models, particularly for tasks such as language modelling, translation, and text generation
    - During the training process, instead of feeding the model’s own previous output as input to the next time step, the ground truth (actual) output from the training data is provided as input
    - This approach is intended to help the model learn the correct sequence of output tokens more efficiently and stabilize the training process
        - Early in training, decoder outputs will be very random, so each decoding produce an out-of-distribution (unlike the training data) response
        - Very hard to learn anything if the decoder never produces a low-loss output
    - [Reference](https://towardsdatascience.com/what-is-teacher-forcing-3da6217fed1c)

# Resources

### Tutorials

- [Keras Into](https://blog.keras.io/a-ten-minute-introduction-to-sequence-to-sequence-learning-in-keras.html)
- [Seq2Seq & Attention (Visual Walkthrough)](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)
- [https://medium.com/analytics-vidhya/encoder-decoder-seq2seq-models-clearly-explained-c34186fbf49b](https://medium.com/analytics-vidhya/encoder-decoder-seq2seq-models-clearly-explained-c34186fbf49b)

### Slides

- [Stanford NLP](https://nlp.stanford.edu/~johnhew/public/14-seq2seq.pdf)