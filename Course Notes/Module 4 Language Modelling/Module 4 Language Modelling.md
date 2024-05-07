# Module 4: Language Modelling

## Topics

- Language Modelling
- Neural Language Models

# Language Modelling Overview

- [Language Modelling](./Language%20Modelling.md)

## What makes a good language model?

- Model **fluency** of a sequence of words, not every aspect of language production
- **Fluent:** Looks like accurate language
- Does a sequence of words look like what we expect from fluent language?
- Can we choose words to put in a sequence such that it looks like fluent language

## Modelling Fluency

- **Vocabularly**
    - A set of words that our system knows
    - How many words does a system need to know?
        - E.g. English has > 600,000 words
    - What if we come across a word that isn’t in the dictionary?
    - Add special symbols to the dictionary to handle out-of-vocabulary words
        - UNK: an unknown word (sometimes also OOV)
    - Other special symbols
        - SOS: Start of sequence
        - EOS: End of sequence

## How to Model Fluent Language?

- What is the probability that a sequence of words $w_1, w_2, …, w_n$ would occur in a corpus of text produced by fluent language users?
- Fluence $\approx$ probability
- What is $P(w_1, w_2, w_3, ..w_n)$?
- Let’s create a bunch of random variables $W_1, W_2, W_3,..., W_n$such that each variable $W_i$ can take on the value of a word in the vocabularly $V$

## Modelling Fluency Examples

- Example Sentence: “The moles snuck into the garden last night”
    - $W_1$ = The
    - $W_2$ = moles
- Recall the chain rule from Bayesian Statistics

    $$
    \begin{align}
    & P(W_1 = w_1, W_2 = w_2,…W_n = w_n)

    \\

    &= P(w_1 = w_1) * P(W_2 = w_2 | W_1 = w_1) * P(W_3 = w_3 | W_2 = w_2,  W_1 = w_1) * P(W_n = w_n | W_1 = w_1, W_2 = w_2,....W_{n-1} = w_{n-1}
    \\
    \\
    &= \prod_{t=1}^n P(W_t = w_t | \underbrace{W_1 = w_1, W_2 = w_2, ... W_{t-1} = w_{t-1}}_{\text{This is the history of the } t^{th} \text{word. This is also called the context}})
    \\
    \end{align}
    $$

    - Basically the probability of each word $n$ is conditioned upon all of the words that came before it
    - One of the main challenges is figuring out how to squeeze the history (context) into a representation that makes an algorithm better at predicting the $t+1^{th}$ word
    - For an arbitrarily long sequence, it can be intractable to have a large (or infinite number of random variables)
    - Must limit the history/context by creating a fixed window of previous words
        - If we remove all of the context, then we arrive at a ***unigram model***
            - This seems obviously wrong because the words could be in any order but still predicted to be fluent

    [Bag of Words Model (BOW), N-Grams & POS Tagging](https://www.notion.so/Bag-of-Words-Model-BOW-N-Grams-POS-Tagging-eb89a4af5d5040098bff4ef389a8576a?pvs=21)




# Neural Language Models

- Suppose each input is a word and each output is a different word from our vocabulary
    - One key issue is that there are ***many output classes***
    - Neural Networks require inputs to be real-valued numbers

- [RNN & LSTM](/Course%20Notes/Module%202%20Foundations/Neural%20Networks%20&%20Deep%20Learning/RNN%20&%20LSTM.md)
- [Sequence-to-Sequence Models (Seq2Seq)](/Course%20Notes/Module%202%20Foundations/Neural%20Networks%20&%20Deep%20Learning/Sequence-to-Sequence%20Models%20(Seq2Seq).md)
- [Transformers](/Course%20Notes/Module%202%20Foundations/Transformers.md)
- [Generative Sampling](./Language%20Modelling/Generative%20Sampling.md)

# Different Token Representations

- Up to now, we’ve assumed a token is a word and the vocabulary is a large number of words
    - We could set the vocabulary to be a set of letters and numbers
        - The vocabulary size is much smaller but the language model has to learn how to spell one word at a time
- **Sub-Word Tokens:** Break complicated words into commonly recurring pieces
    - Example: Tokenize —> Token + ize
    - Vocabulary would contain common words, word roots, suffixes, prefixes, letters and punctuation
    - Neural network mostly works on tokens but occasionally has to use context to assemble a complex word
    - Sub-word vocabulary can cover most of English with fewer tokens (~50K tokens)
    - No need for out-of-vocab (UNK) tokens

# Perplexity

- How do we know if a language model is any good?
    - Probability $\sim$ fluency
- [Perplexity Overview](./Perplexity.md)

# Resources

- [https://web.stanford.edu/~jurafsky/slp3/7.pdf](https://web.stanford.edu/~jurafsky/slp3/7.pdf)