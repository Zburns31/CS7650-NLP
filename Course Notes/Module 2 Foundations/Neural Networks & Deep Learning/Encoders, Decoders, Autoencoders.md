# Encoders, Decoders, Autoencoders

---

# What are they?

- In neural networks, encoders and decoders are components often associated with autoencoder architectures, a type of neural network used for unsupervised learning
    - These components play specific roles in transforming and reconstructing input data
- **The idea** is to break the Neural Network into two parts:
    1. **Encoder**
        1. **Goal:** Send input through a smaller-than-necessary layer to force the neural network to find a small set of parameters that produced the intermediate activations that approximates the output
            1. I.e. Performs compression, which forces generalization
    2. **Decoder**
        1. **Goal:** Set of parameters that recovers information to produce the output
            1. We know we have a good compressor (encoder) if we can successfully decompress
    

![Untitled](Encoders,%20Decoders,%20Autoencoders%2009d4af88545b457480f873ad1e02f6b3/Untitled.png)

![Untitled](Encoders,%20Decoders,%20Autoencoders%2009d4af88545b457480f873ad1e02f6b3/Untitled%201.png)

# Why use them?

- In general sequence-to-sequence problems like machine translation ([Section 10.5](https://d2l.ai/chapter_recurrent-modern/machine-translation-and-dataset.html#sec-machine-translation)), inputs and outputs are of ***varying lengths that are unaligned***
    - The standard approach to handling this sort of data is to design an *encoder-decoder* architecture ([Fig. 10.6.1](https://d2l.ai/chapter_recurrent-modern/encoder-decoder.html#fig-encoder-decoder)) consisting of two major components:
        - an *encoder* that takes a ***variable-length sequence as input***
        - a *decoder* that ***acts as a conditional language model***, taking in the encoded input and the leftwards context of the target sequence and predicting the subsequent token in the target sequence

# Problems

- Need different architectures based on whether we have bigrams, trigrams, etc.
- We can’t remember any context or history outside of these n-grams

# Encoders

---

[Encoders](Encoders,%20Decoders,%20Autoencoders%2009d4af88545b457480f873ad1e02f6b3/Encoders%2032466e521ceb4eb6a7c4fda79069bf35.md)

## 

# Decoders

---

## High-Level Overview

- **Function:** The decoder is responsible for reconstructing the input data from the encoded representation produced by the encoder
- **High-Level Explanation:** The decoder takes the compressed representation and attempts to reconstruct the original input as closely as possible
- **Architecture:** Similar to the encoder, the decoder consists of one or more layers
    - It takes the encoded representation and transforms it back into the original dimensionality
- **Purpose:** The purpose of the decoder is to generate a meaningful reconstruction of the input based on the compressed representation
    - The reconstruction is ideally as close as possible to the original input

## Goals:

- 

# Auto-Encoder

---

## High-Level Overview

- **Combination of Encoder and Decoder:** An autoencoder combines an encoder and a decoder
    - The encoder compresses the input data, and the decoder reconstructs it
    - The training objective is to minimize the difference between the input and the reconstructed output
- **Unsupervised Learning:** Autoencoders are often used for unsupervised learning, where the network learns to represent the inherent structure in the data without explicit labels
- **Applications:** Autoencoders have applications in various domains, such as data compression, feature learning, and anomaly detection

# Encoder & Decoder Architecture

---

- There are three main blocks in the encoder-decoder model:
    1. Encoder
    2. Hidden Vector
    3. Decoder
- Encoder-Decoder models are jointly trained to maximize the conditional probabilities of the target sequence given the input sequence

- Consider a neural network that implements the identity function
    - The neural network is forced to make compromises
    - “King” produces a hidden state activation similar to regent

---

![Untitled](Encoders,%20Decoders,%20Autoencoders%2009d4af88545b457480f873ad1e02f6b3/Untitled%202.png)

# Encoder Only

---

- The *Encoder-only* architecture, on the other hand, is used when only encoding the input sequence is required and the decoder is not necessary
- Here the input sequence is encoded into a fixed-length representation and then used as input to a classifier or a regressor to make a prediction
- This output flexibility makes them useful for many applications, such as:
    - Text classification
    - Sentiment analysis
    - Named entity recognition

# Decoder Only

---

- In the *Decoder-only* architecture, the model consists of only a decoder, which is trained to predict the next token in a sequence given the previous tokens
    - The critical difference between the *Decoder-only* architecture and the *Encoder-Decoder* architecture is that the *Decoder-only architecture does* not have an explicit encoder to summarize the input information
    - Instead, the information is encoded implicitly in the hidden state of the decoder, which is updated at each step of the generation process
- This architecture is useful for applications such as:
    - Text completion
    - Text generation
    - Translation
    - Question-Answering
    - Generating image captions

# Implementation

**Linear Layer**

```python
Pytorch.nn.Linear(vocab_size, hidden_size)
```

- Takes a one hot vector (float) of length ***vocab_size***
- Map a vector to length of ***hidden_size***

**Embedding Layer**

```python
Pytorch.nn.Embedding(vocab_size, hidden_size)
```

- Takes a token id (integer) as input
- Converts to a one-hot vector of length ***vocab_size***
- Maps to a vector of length ***hidden_size***

# Resources

- [https://bastings.github.io/annotated_encoder_decoder/](https://bastings.github.io/annotated_encoder_decoder/)

### Implementation

- [https://d2l.ai/chapter_recurrent-modern/encoder-decoder.html](https://d2l.ai/chapter_recurrent-modern/encoder-decoder.html)
- [https://www.baeldung.com/cs/nlp-encoder-decoder-models](https://www.baeldung.com/cs/nlp-encoder-decoder-models)