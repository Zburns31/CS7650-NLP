# Bag of Words Model (BOW), N-Grams & POS Tagging

---

# Overview

- The **bag-of-words** (BOW) model is a representation that turns arbitrary text into **fixed-length vectors** by counting how many times each word appears. This process is often referred to as **vectorization**
    - We lose contextual information when using Bag-of-Words models, such as where in the document these terms appear
        - It’s like a literal **bag**-of-words: it only tells you *what* words occur in the document, not *where* they occurred
        - I.e. The order or structure of words in the document is discarded
- A bag-of-words is a representation of text that captures the occurrence of words within a document. It involves two key components:
    - A vocabulary of known words
    - A measure of the presence of these known words
- **The goal** is to transform each document of free text into a vector that we can use as input for a machine learning model

# How does it work?

- Use a column vector of word counts, e.g., $x = [0, 1, 1, 0, 0, 2, 0, 1, 13, 0 . . .]$, where $x_j$ is the count of word $j$
    - The length of $x$ is $V$ , $|V|$, where $V$ is the set of possible words in the vocabulary
    - In linear classification, the classification decision is based on a weighted sum of individual feature counts, such as word counts
- To predict a label from a bag-of-words, we can assign a score to each word in the vocabulary, measuring the compatibility with the label
    - For example, for the label FICTION, we might assign a positive score to the word whale, and a negative score to the word molybdenum. These scores are called weights, and they are arranged in a column vector $θ$
- For each label $y ∈ Y$, we compute a score $Ψ(x, y)$, which is a scalar measure of the compatibility between the bag-of-words $x$ and the label $y$
    - In a linear bag-of-words classifier, this score is the vector inner product between the weights $θ$ and the output of a **feature function** $f(x,y)$:
    
    $$
    \Psi(\bold{x},y) = \theta \cdot f(\bold{x},y) = \sum \theta_j f_j(\bold{x}, y)
    $$
    
    - Where:
        - $x$ represents the word counts
        - $y$ represents the label

 

# High-Level Overview

1. **Determine the vocabulary**
    1. We first define our **vocabulary**, which is the set of all words found in our document set
2. **Create Document Vectors**
    1. To vectorize our documents, all we have to do is **count how many times each word appears**
3. **Managing Vocabulary**
    1. As the vocabulary size increases, so does the vector representation of documents
        1. As such, there is pressure to decrease the size of the vocabulary when using a bag-of-words model
            - There are simple text cleaning techniques that can be used as a first step, such as:
            - Ignoring case
            - Ignoring punctuation
            - Ignoring frequent words that don’t contain much information, called stop words, like “a,” “of,” etc
            - Fixing misspelled words
            - Reducing words to their stem (e.g. “play” from “playing”) using stemming algorithms
4. **Scoring Words**
    1. Scoring words is attaching a numerical value for marking the occurrences of the words. In the above example, scoring was binary: it means the presence or absence of the words. There are other methods as well:
        1. **Counts:** The number of times each word appears in a document
        2. **Frequencies:** Frequencies are the calculation of word frequency in a document in contrast to the total number of words in that document
        3. **Word Presence:** Does the word exist in the document or not?

## Why use it?

- Despite being a relatively basic model, BOW is often used for [Natural Language Processing](https://victorzhou.com/tag/natural-language-processing/) (NLP) tasks like Text Classification
    - Its strengths lie in its simplicity: it’s inexpensive to compute, and sometimes simpler is better when positioning or contextual info aren’t relevant

# Implementation

- While vector notation is used for presentation and analysis, in code the weights and feature vector can be implemented as dictionaries. The inner product can then be computed as a loop
- In python:

```jsx
def compute_score(x,y,weights): 
	total = 0 
	for feature,count in feature_function(x,y).items(): 
		total += weights[feature] * count 
	return total
```

- It is common to add an offset feature at the end of the vector of word counts $x$, which is always 1
    - The weight associated with this offset feature can be thought of as a bias for or against each label

# Time & Space Complexity

- The amount of memory required to represent a document is proportional to the number of possible words in the vocabulary

# N-Gram Word Models

- To improve on the BOW model by treating special phrases as if they were single words, we can use a Markov Chain that considers the dependence between ***n adjacent words***
    - Everything that the N-gram word model knows, it learned from counts of specific word sequences
    - The n-gram model misses generalization because it is an atomic model: ***each word is an atom, distinct from every other word, with no internal structure***
        - Factored or structured models allow for more expressive power and better generalization
- In an N-gram model, the probability of ***each word is dependent only on the n-1 previous words***. More specifically:
    
    $$
    ⁍
    $$
    

$$
P(w_{1:N}) = \prod_{j=1}^N P(w_j| w_{j-n + 1: j-1})
$$

## Why use N-Gram Models?

- Gram models work well for classifying newspaper sections, as well as for other classification tasks such as spam detection (distinguishing spam email from non-spam), sentiment analysis (classifying a movie or product review as positive or negative) and author attribution

## Smoothing N-Gram Models

- High-frequency n-grams like “of the” have high counts in the training corpus, so their probability estimate is likely to be accurate: with a different training corpus we would get a similar estimate
    - Low-frequency n-grams have low counts that are subject to random noise—they have high variance
        - Our models will perform better if we can smooth out that variance
- There is always a chance that we will be asked to evaluate a text containing an unknown or out-of-vocabulary word: one that never appeared in the training corpus
    - But it would be a mistake to assign such a word a probability of zero, because then the probability of the whole sentence would be 0

### How?

- We could replace unknown words to the model by modifying the training corpus by replacing infrequent words with a special symbol, traditionally, <UNK>
    - We could keep only the 50,000 most common words or words with a frequency greater than 0.0001%
    - When an unknown word appears in a test set, we look up its probability under <UNK>
- **Smoothing**
    - The problem is that some low-probability n-grams appear in the training corpus, while other equally low-probability n-grams happen to not appear at all. We don’t want some of them to have a zero probability while others have a small positive probability
        - We want to apply smoothing to all the similar n-grams which reserves some of the probability mass of the model for never-seen n-grams, ***to reduce the variance of the model***
    - **Backoff Model & Linear Interpolation Smoothing**
        - Start by estimating n-gram counts, but for any sequence that has a low (or zero) count, we back off to n - 1 grams
        - **Linear interpolation smoothing** is a backoff model that combines trigram, bigram and unigram models by linear interpolation
            - It defines the probability estimate as:
            
            $$
            \hat{P}(c_i|c_{i-2:i-1}) = \lambda_3P(c_i|c_{i-2:i-1}) + \lambda_2P(c_i|c_{i-1}) + \lambda P(c_i)
            $$
            
            - Where $\lambda_1 + \lambda_2 + \lambda_3 = 1$
                - The parameter values $\lambda_i$ can be fixed or they can be trained with an expectation-maximization algorithm
                - They could also depend on the counts: if we have a high count of trigrams, then we weigh them relatively more; if only a low count, then we put more weight on the bigram and unigram models

# Perplexity

[Perplexity](https://www.notion.so/Perplexity-e8a7bd7b009a41d4b866bdd3afb87bf2?pvs=21)

- [https://medium.com/nlplanet/two-minutes-nlp-perplexity-explained-with-simple-probabilities-6cdc46884584](https://medium.com/nlplanet/two-minutes-nlp-perplexity-explained-with-simple-probabilities-6cdc46884584)
- [https://surge-ai.medium.com/evaluating-language-models-an-introduction-to-perplexity-in-nlp-f6019f7fb914](https://surge-ai.medium.com/evaluating-language-models-an-introduction-to-perplexity-in-nlp-f6019f7fb914)
- 

# Resources

- [https://victorzhou.com/blog/bag-of-words/](https://victorzhou.com/blog/bag-of-words/)
-