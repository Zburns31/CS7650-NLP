# Language Modelling

---

# What is Language Modelling?

- Language modelling is the task of predicting which word comes next in a sequence of words
    - More formally, given a sequence of words $𝑤_1, …, 𝑤_𝑡$, we want to know the probability of the next word, $𝑤_{𝑡+1}$:
        
        $$
        P(w_{t+1} | w_{1},....,w_t)
        $$
        
    - Here we are assuming that 𝑤𝑡+1 comes from a fixed vocabulary 𝑉
    - This allows language modelling to be treated as a classification task
- **Alternative View**
    - Rather than as predictive models, language models can also be viewed as models that assign probability to a piece of text
        - I.e. How likely is it that this piece of text is written in Swedish? French?
    - These two views are equivalent, as the probability of a sequence can be expressed as a product of conditional probabilities:
        
        $$
        P*(w_1,...w_n) = \prod_{i=1}^n P(w_t|w_1,...w_n)
        $$
        

### Use Cases:

- Autocomplete
- Text Summarization
- Translation
- Spelling and grammar correction
- Text generation

## Types of Language Models

- Statistical Language Models
    - N-Gram models (unigrams, bigrams, trigrams, etc.)
- Neural Language Models
    - Use neural networks to predict the likelihood of a sequence of words

# Pre-Processing

---

- Suppose each input is a word and each output is a different word from our vocabulary
    - One key issue is that there are ***many output classes***
    - Neural Networks require inputs to be real-valued numbers
    

[NLP: Pre-Processing](https://www.notion.so/NLP-Pre-Processing-fc3b9076e478488db81dc923439a439a?pvs=21)

# Neural Language Models

---

[Encoders, Decoders, Autoencoders](https://www.notion.so/Encoders-Decoders-Autoencoders-09d4af88545b457480f873ad1e02f6b3?pvs=21)

[RNN & LSTM](https://www.notion.so/RNN-LSTM-063950076f2d468b9a471dc5b235338b?pvs=21)

# Text Generation: Generative Sampling

[Generative Sampling](Language%20Modelling%20ee64895db0024e4d8a85a71c129be3b0/Generative%20Sampling%2027487f15ed4849d395cf727434cc851d.md)