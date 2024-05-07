# Module 2: Foundations

# Review Topics

- [Probability](/Course%20Notes/Module%202%20Foundations/Probability.md)
- [Bayesian Networks](/Course%20Notes/Module%202%20Foundations/Bayesian%20Networks.md)
- [Neural Networks & Deep Learning](/Course%20Notes/Module%202%20Foundations/Neural%20Networks%20&%20Deep%20Learning.md)

# Language Example

- We can make use of the Generalized Bayes Theorem to assume independence between the words (evidence)

$$
P(\text{Sentiment} = +|w_1, w_2, ...., w_n) = \\ P(\text{Sentiment} =  +)P(\text{Sentiment} = + | w_1)P(\text{Sentiment} = + | w_2)...P(\text{Sentiment} = + | w_n)
$$

- We can rewrite this as:

$$
P(\text{Sentiment} = +) = \prod_{i=1}^n P(w_i|\text{Sentiment} = +)
$$

# Documents are Probabilistic Word Emissions

- Suppose we have a document and we want to determine the sentiment
    - We cannot directly observe the sentiment, but we can clearly parse the words and sentences
    - Furthermore we can learn to associate words with a sentiment
        - So for example "awesome" is generally associated with a positive sentiment, and "junk" is associated with a negative sentiment

![documents](./Module%202%20Foundations/documents.png)

# Neural Networks & Deep Learning

- Neural networks are a collection of modules
- Each module is a layer that stores weights and activations
- Each module knows how to update its own weights
- Modules keep track of who passes information (called a chain)
- Each module knows how to distribute loss to child modules
- Pytorch supports parallelization on GPU’s