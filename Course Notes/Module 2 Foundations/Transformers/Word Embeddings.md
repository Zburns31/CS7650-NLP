# Word Embeddings

---

# What are Word Embeddings?

- A word embedding is a learned representation for text where words that have the same meaning have a similar representation
- An embedding is a dense vector of floating point values (the length of the vector is a parameter you specify)
    - Instead of specifying the values for the embedding manually, they are trainable parameters (weights learned by the model during training, in the same way a model learns weights for a dense layer)
    - It is common to see word embeddings that are 8-dimensional (for small datasets), up to 1024-dimensions when working with large datasets. A higher dimensional embedding can capture fine-grained relationships between words, but takes more data to learn
- Word embeddings are in fact a class of techniques where individual words are represented as real-valued vectors in a predefined vector space. Each word is mapped to one vector and the vector values are learned in a way that resembles a neural network
    - Each word is represented by a real-valued vector, often tens or hundreds of dimensions. This is contrasted to the thousands or millions of dimensions required for sparse word representations, such as a one-hot encoding
        - An embedding reduces the number of parameters needed by a tremendous amount. However, the fewer the dimensions in the embedded space, the more information about the original words gets discarded

# How it works?

Imagine each word in a language is like a unique puzzle piece, and we want to find a way to represent each piece as a set of numbers that captures its meaning and relationships with other pieces. Word embeddings help us do that.

Here's how it works in simple terms:

1. **Word-to-Vector Conversion**: First, we create a huge table of words, and for each word, we assign a unique numerical vector (a set of numbers). Think of this table like a dictionary where each word has its own page.
2. **Meaningful Relations**: Word embeddings are designed in such a way that words with similar meanings are represented by similar vectors. For example, the word "happy" and "joyful" would have vectors that are closer together, while "happy" and "sad" would be farther apart.
3. **Contextual Understanding**: Word embeddings also try to capture the context of a word by considering the words that usually appear around it. Words that have similar neighbors in sentences will have similar embeddings. For example, if "cat" and "dog" often appear together in sentences, their vectors would be closer.
4. **Vector Operations**: These word embeddings are not just random numbers; they hold meaningful information. We can perform mathematical operations on them to get interesting results. For example, if we take the vector for "king" and subtract the vector for "man" and then add the vector for "woman," the result would be close to the vector for "queen."

![Untitled](Word%20Embeddings%20158db28cfe0e462cb2338e122da08a9e/Untitled.png)

# Algorithms

- Embedding Layer
- Word2Vec
- GloVe

# Resources

- [https://e2eml.school/transformers.html#embeddings](https://e2eml.school/transformers.html#embeddings)
- [https://towardsdatascience.com/transformers-in-depth-part-1-introduction-to-transformer-models-in-5-minutes-ad25da6d3cca](https://towardsdatascience.com/transformers-in-depth-part-1-introduction-to-transformer-models-in-5-minutes-ad25da6d3cca)