# Generative Sampling

---

# What is it?

- Generative sampling involves randomly selecting words or tokens based on the learned probability distribution
    - Sampling techniques can vary, including greedy sampling (selecting the most likely next word at each step) or stochastic sampling (sampling from the distribution to introduce randomness)

# Types of Sampling

- **Argmax (Greedy Search)**
- **Multinomial**
    - As opposed to greedy search that always chooses a token with the highest probability as the next token, multinomial sampling (also called ancestral sampling) randomly selects the next token based on the probability distribution over the entire vocabulary given by the model
    - Every token with a non-zero probability has a chance of being selected, thus reducing the risk of repetition
- **Temperature**
    - Lower temperatures make the model increasingly confident in its top choices, while temperatures greater than 1 decrease confidence
        - 0 temperature is equivalent to $\argmax$/max likelihood, while infinite temperature corresponds to a uniform sampling
- **Top K Sampling**
- **Beam Search**

# Why is it needed?

- **Problem:** Argmax can sometimes result in a local maximum
    - Generating long sequences can result in repeated words and nonsensical language
    - There is a strong likelihood of getting the same words and sequences happening over and over
- The activations scores for particular words just always were highly activated and therefore argmax was picking the same word over and over again
    
    
- **Solution: Multinomial Sampling**
    - We could do multinomial sampling which basically says pick a token pick a position pick a score based on how strong that probability distribution is
    - **Multinomial Sampling:**
        
        $$
        ⁍
        $$
        
        ![Untitled](Generative%20Sampling%2027487f15ed4849d395cf727434cc851d/Untitled.png)
        
    - This is all the words in our vocabulary and if we sort them according to their strength to the probability there'll be some words that have very high probability and some words that'll have really low probability
        - What we tend to see is that there's a cluster of really high it drops off quickly and then we have a long tail of very unlikely words
    - We select from the entire vocabulary proportional to the strength of the output
        - Which is basically saying with high likelihood I'll pick the word night with slightly less probability I'll pick the word disposition with slightly less probability sea storm and weather and there's a very small probability but non-zero probability that I might pick a word like pineapple
    - But sometimes our neural network isn't very certain about what it wants to do and we get a distribution that has a high probability over a much larger area of our vocabulary before hitting the long tail
        - And in this case if we sample probabilistically from our vocabulary we're probably not going to see words like pineapple very often but we're frequently going to see word night
        
- **Multinomial Sampling** **Problem:** Sometimes multinomial sampling can appear too random, especially when there are a lot of options with similar probabilities
- **Solution: Temperature**
    - Set a temperature $T$ variable $(0.0, 1.0]$
    - Sample from: $\text{norm} \left ( \Braket{\dfrac{\log P(w_1)}{T}, \dfrac{\log P(w_2)}{T}, \dfrac{\log P(w_n)}{T}}  \right )$
        - Temperature $T = 1.0$ means the distribution is unchanged
        - Dividing a number by $T < 1.0$ means all the numbers increase
            - Bigger numbers increase exponentially faster than smaller numbers
        - As temperature goes to 0.0, the highest scoring number goes to $\infty$
    - **How this works:**
        - We are just going to divide every probability score by this temperature value and then we'll renormalize this so everything comes back to be values zero and one
    
    ![Untitled](Generative%20Sampling%2027487f15ed4849d395cf727434cc851d/Untitled%201.png)
    

# Resources

### Implementation

- [Huggingface](https://huggingface.co/docs/transformers/v4.29.0/en/generation_strategies)
- [https://github.com/kmkarakaya/Deep-Learning-Tutorials/blob/master/Sampling_in_Text_Generation.ipynb](https://github.com/kmkarakaya/Deep-Learning-Tutorials/blob/master/Sampling_in_Text_Generation.ipynb)

### Blogs

- [https://towardsdatascience.com/how-to-sample-from-language-models-682bceb97277](https://towardsdatascience.com/how-to-sample-from-language-models-682bceb97277)
- [https://shivammehta25.github.io/posts/temperature-in-language-models-open-ai-whisper-probabilistic-machine-learning/](https://shivammehta25.github.io/posts/temperature-in-language-models-open-ai-whisper-probabilistic-machine-learning/)

### Sampling Methods

- [Temperature](https://lukesalamone.github.io/posts/what-is-temperature/)