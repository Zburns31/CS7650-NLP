# Word2Vec

---

# What is it?

- Word2vec is a two-layer neural net that processes text by “vectorizing” words
    - Its input is a text corpus and its output is a set of vectors: ***feature vectors that represent words in that corpus***
- Word2Vec is a simple neural network with a single hidden layer, and like all neural networks, it has weights, and during training, its goal is to adjust those weights to reduce a loss function
    - ***However, Word2Vec is not going to be used for the task it was trained on, instead, we will just take its hidden weights, use them as our word embeddings, and toss the rest of the model***
- Distributional Semantics: ***“A word is known by the company it keeps”***
    - Words that mean approximately the same thing tend to be surrounded by the same words
    - Word2Vec is trying to capture this

# **Why is it used?**

- The purpose and usefulness of Word2vec is to group the vectors of similar words together in vector space. That is, it detects similarities mathematically
    - Word2vec creates vectors that are distributed numerical representations of word features, features such as the context of individual words
- Given enough data, usage and contexts, Word2vec can make highly accurate guesses about a word’s meaning based on past appearances.
    - ***Those guesses can be used to establish a word’s association with other words (e.g. “man” is to “boy” what “woman” is to “girl”), or cluster documents and classify them by topic.*** Those clusters can form the basis of search, sentiment analysis and recommendations in such diverse fields as scientific research, legal discovery, e-commerce and customer relationship management

# How it works

Here’s a simplified explanation of how it works:

1. **Corpus**: Word2Vec starts with a text corpus, which is just a large collection of text data. This could be anything from a single book to the entire internet
2. **Window**: The algorithm then slides a window of a certain size (say, 5 words) across this corpus. The word in the middle of the window is the target word, and the words surrounding it are the context words
3. **Prediction**: The goal of Word2Vec is to either predict the context words given the target word (this is called the  Skip-Gram model), or to predict the target word given the context words (this is called the Continuous Bag of Words, or CBOW, model)
4. **Vectors**: Each word is represented by a vector
    1. Initially, these vectors are random, but through the process of prediction and adjusting for errors, these vectors gradually adjust to capture the semantic meanings of the words.
5. **Training**: The training process involves going through each window in the corpus, making predictions, and adjusting the word vectors based on the prediction errors
    1. This is done using techniques from machine learning and optimization, such as stochastic gradient descent

# Word2Vec Output

- The output of the Word2vec neural net is a vocabulary in which each item has a vector attached to it, which can be fed into a deep-learning net or simply queried to detect relationships between words
- The input to this network is a one-hot vector representing the input word, and the label is also a one-hot vector representing the target word, however, the network’s output is a probability distribution of target words, not *necessarily* a one-hot vector like the labels

# Word2Vec Implementations

- **Continuous-Bag-of-Words (CBOW) Model**
    - CBOW predicts target words (e.g. ‘mat’) from the surrounding context words (‘the cat sits on the’)
    - Statistically, it has the effect that CBOW smoothes over a lot of the distributional information (by treating an entire context as one observation)
        - For the most part, this turns out to be a useful thing for smaller datasets
- **Skip-Gram Model**
    - Skip-gram predicts surrounding context words from the target words (inverse of CBOW)
    - Statistically, skip-gram treats each context-target pair as a new observation, and this tends to do better when we have larger datasets
    - **SparkML uses this implementation**
    

![Untitled](Word2Vec%20957714fc843f453ca60e1316e6573bde/Untitled.png)

# Implementation

---

## CBOW

- [https://datascience.stackexchange.com/questions/81249/construct-word2vec-cbow-training-data-from-beginning-of-sentence](https://datascience.stackexchange.com/questions/81249/construct-word2vec-cbow-training-data-from-beginning-of-sentence)
- [https://github.com/udacity/deep-learning-v2-pytorch/blob/master/word2vec-embeddings/Negative_Sampling_Exercise.ipynb](https://github.com/udacity/deep-learning-v2-pytorch/blob/master/word2vec-embeddings/Negative_Sampling_Exercise.ipynb)

# Resources

- [The Illustrated Word2Vec](https://jalammar.github.io/illustrated-word2vec/)
- [https://www.tensorflow.org/text/tutorials/word2vec](https://www.tensorflow.org/text/tutorials/word2vec)
- [https://gist.github.com/aparrish/2f562e3737544cf29aaf1af30362f469](https://gist.github.com/aparrish/2f562e3737544cf29aaf1af30362f469)

### Blogs & Tutorials

- [https://towardsdatascience.com/word2vec-explained-49c52b4ccb71](https://towardsdatascience.com/word2vec-explained-49c52b4ccb71)