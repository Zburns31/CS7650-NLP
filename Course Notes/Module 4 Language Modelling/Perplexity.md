# Perplexity

---

# What is it?

- In general, [perplexity](https://en.wikipedia.org/wiki/Perplexity) is a measurement of how well a probability model predicts a sample
    - It is a measure of how surprised a model is by an input sequence
    - In other words, it quantifies how “surprised” the model is when it sees new data. The lower the perplexity, the better the model predicts the text
- A good language model is one that is good at guessing what comes next

# Why use it?

- The perplexity metric can be used to compare different language models, identify problems in a [chatbot dataset](https://www.surgehq.ai/blog/how-good-is-your-chatbot-an-introduction-to-perplexity-in-nlp), or fine-tune the parameters of a single model, among other uses

# Branching Factor

- **Branching Factor:** Number of things that are likely to come next
    - It all options are equally likely, then branching factor = number of options
    - But if different options have different probabilities then:
    
    $$
    \text{Branching Factor} = \dfrac{1}{P(option)}
    $$
    
    - Example:
        - $P(\text{heads)}$ = 0.5
        - $\text{Branching Factor} = \dfrac{1}{0.5} = 2$
        - $\text{Branching Factor} = \dfrac{1}{0.75} = 1.33$
            - Incorporates the weight of each branch
- So, the branching factor of a word is:
    
    $$
    ⁍
    $$
    
    - The more plausible alternatives, the more likely the model will make the wrong choice
    - But…longer sequences would have a smaller probability, so need to normalize by the length by taking the $n^{th}$ root:
        
        $$
        PP(W)=P(w_1,w_2,...,w_{t-1})^{\frac{1}{N}}
        $$
        
    - So the branching factor of a sequence of words is:
    
    $$
    \prod_{t=1}^n \dfrac{1}{P(w_t|w_1,w_2,...,w_{t-1})^{\frac{1}{N}}}
    $$
    

# How it works

1. **Probability Distribution:**
    - A language model assigns probabilities to sequences of words
    - Given a sequence of words, the model calculates the probability of the entire sequence based on its learned parameters
2. **Perplexity Calculation:**
    - The perplexity (PP) of a sequence of words is calculated as the inverse probability of the words, normalized by the number of words. It can be expressed mathematically as:
        
        $$
        Perplexity(w_1,w_2,...w_n) = \prod_{t=1}^n \sqrt[n]{\dfrac{1}{P(w_t|w_1,w_2,...,w_{t-1}; \theta)}}
        $$
        
        - where $N$ is the number of words in the sequence
    - Perplexity is just the branching factor for a sequence of words
3. **Interpretation:**
    - ***The perplexity value represents the average number of choices the model has for predicting the next word in the sequence***
        - A lower perplexity implies that the model is more confident and makes more accurate predictions. It can be interpreted as the "perplexity per word" or the average uncertainty associated with predicting each word in the sequence
4. **Training and Evaluation:**
    - During training, the goal is to minimize perplexity by adjusting the model's parameters
    - In the evaluation phase, perplexity is used to assess how well the model generalizes to unseen data. Lower perplexity values on a test set suggest better generalization

### Interpretation:

- **Lower Perplexity:** Indicates that the model is more certain and confident in its predictions. The model assigns higher probabilities to the correct words, resulting in better overall performance
- **Higher Perplexity:** Indicates greater uncertainty and less accurate predictions. The model struggles to assign high probabilities to the correct words, suggesting poorer performance
- $Perplexity(w_t) = x$ means the odds of getting the right token which is equivalent to rolling a 1 on an $x$-sided die
    - So if $Perplexity(w_t) = 45$, this means the model has a 1/45 chance of getting the right token

# Mathematical Trick

- Perplexity is also the per-word exponentiated, normalized cross-entropy:

$$
e^{\sum_t^n} - \frac{1}{n} \log P(w_t|w_1,w_2,...w_{t-1}; \theta)
$$

- See [video](https://gatech.instructure.com/courses/382338/pages/perplexity-part-2?module_item_id=3706284) for derivation
- RNN’s generate one slice at a time
- Perplexity is the exponentiated negative log likelihood loss of the neural network:
    
    $$
    perplexity(w_t) = e^{- \log P(w_t|w_1,w_2,...w_{t-1};\theta)} = e^{Loss(\hat y, target)}
    $$
    
    - Where:
        - $Loss(\hat y, target)$ represent sthe log softmax vector output by the neural network
        - $Target$ represents the which index to look at