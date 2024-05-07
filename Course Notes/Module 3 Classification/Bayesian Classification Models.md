# Bayesian Classification Models

---

# What are Bayesian Classification Methods?

- Bayesian classifiers are the statistical classifiers based on Bayes' Theorem
- Bayesian classifiers can predict class membership probabilities
    - i.e. the probability that a given tuple belongs to a particular class
- Bayesian model sees text as a latent (unobservable) phenomenon that emits observable features
- The frequency of which these observable features appear in the text is evidence for the label

# How do they work?

**Goal:** Classify $V^* \rightarrow \mathcal{L}$

- Where:
    - $V^*$ represents all possible strings or documents pulling from the vocabulary $V$
    - $\mathcal{L}$ represents the the label for the particular document or string

- We can express this using the Bayes Theorem. What is the probability of some label given the features?

$$
P(\mathcal{L}|\phi_1, \phi_2,...\phi_n) = \dfrac{P(\phi_1, \phi_2,...\phi_n|\mathcal{L})P(\mathcal{L})}{P(\phi_1, \phi_2,...\phi_n)}
$$

- However, we can apply the ***Naive Bayes Assumption*** (features are independent of each other), leading us to:

$$
P(\mathcal{L_+}|\phi_1, \phi_2,...\phi_n) = \dfrac{P(\phi_1|\mathcal{L_+})P( \phi_2|\mathcal{L_+})...P(\phi_n|\mathcal{L_+})P(\mathcal{L_+})}{P(\phi_1)P(\phi_2)...P(\phi_n)}
$$

- So if we want to compute this, we're going to need some information. first of all, we need to know what $P(ϕ_i|L_+)$ are
    - How often do you see the feature, $ϕ_i$ when you see a positive label in the training data?
        - This basically means how often do we see a particular feature or a word or bigram or whatever happens to be when we also happen to have a positive label in our training data
    - Figure out $P(L_+)$
    - Figure out $P(ϕ_i)$

## How do we turn probabilities into a classification prediction?

$$
P(\mathcal{L_+}|\phi_1, \phi_2,...\phi_n) - P(\mathcal{L_-}|\phi_1, \phi_2,...\phi_n)
$$

- Gives $\ge 0$ for $\mathcal{L_+}$ and $<$ 0 for $\mathcal{L_-}$
- This can be reduced to $sign(P(\mathcal{L_+}|\phi_1, \phi_2,...\phi_n) - P(\mathcal{L_-}|\phi_1, \phi_2,...\phi_n))$

### Normalization Constant

- The normalization constant $\alpha$ can often be safely regarded in NLP
    - It’s expensive to compute and really just a scaling factor which is applied to all labels

# Log Probabilities

- Using log probabilities in Natural Language Processing (NLP) has practical benefits that stem from numerical stability and computational efficiency. Here are the main reasons for using log probabilities in NLP:
    1. **Numerical Stability:**
        - **Underflow Prevention:** Multiplying many small probabilities (typically between 0 and 1) can lead to numerical underflow, where the product becomes too small to be accurately represented in a computer's floating-point arithmetic. Taking the logarithm helps prevent underflow, as products turn into sums, making the calculations more stable
        - When we're multiplying probabilities and we get zeros in these probabilities well multiplying zeros against anything else makes everything zero. So another way the thing that happens is that once things start to look like zeros everything becomes zeros
    2. **Computational Efficiency:**
        - **Simplifies Multiplicative Updates:** In many NLP models, probabilities are often multiplied together during the training process. Taking the logarithm transforms these products into additions, simplifying the computations. This can significantly speed up training algorithms
        - **Additive Updates:** Log probabilities allow for additive updates instead of multiplicative updates. This simplification is particularly beneficial in the context of optimization algorithms like gradient descent
    3. **Mathematical Convenience:**
        - **Conversion from Products to Sums:** Logarithms convert the product of probabilities into a sum, making it easier to work with and reducing the complexity of mathematical expressions.
        - **Negative Log-Likelihood:** In many machine learning tasks, including NLP, the objective function is often defined as the negative log-likelihood. Using log probabilities transforms this into a form that is more amenable to optimization, as minimizing the negative log-likelihood is equivalent to maximizing the likelihood.
    4. **Interpretability:**
        - **Log Odds:** Log probabilities can be interpreted as log odds, which can be more intuitive in certain contexts. For example, in sentiment analysis, the log odds of a positive class can be more easily interpretable than raw probabilities

## How do we solve this?

- Shift to the **log scale**
    - Normal probabilities run from 0 $\rightarrow$ 1 whereas the log scale goes from 0 $\rightarrow -\infty$
    - As our numbers get smaller and smaller the closer we are to zero the closer and closer we are to negative infinity. So now small numbers are very negative numbers but very large negative numbers
    - $Log(1) = 0$
    - $Log(0) = -\infty$
    - Now, we never have to worry about numbers zeroing out (though small probabilities can become very large)
- How does this change our math?
    - $P(A)P(B) = P(A) + P(B)$
    - $\prod_{i=1}^n P(\phi_i) = \sum_{i=1}^n log P(\phi_i)$
    - $\dfrac{P(A)}{P(B)} = logP(A) - log P(B)$
    

# Smoothing

- Even using log probabilities, zeros can still appear
- Suppose cheese is a feature but never appears in a positive movie review:
    - $P(\phi_{cheese} | \mathcal{L_+}) = 0$
        
        $$
        \begin{align}
        P(\mathcal{L_+}|\phi_1, \phi_2, \phi_{cheese},...\phi_n) &= \alpha P(\mathcal{L_+}) \prod_{i=1}^n P(\phi_i|\mathcal{L_+})
        
        \\
        
        &= \alpha P(\mathcal{L_+})P(\phi_1|\mathcal{L_+})P(\phi_2|\mathcal{L_+})....P(\phi_{cheese}|\mathcal{L_+})...P(\phi_n|\mathcal{L_+})
        \\
        &= 0
        \end{align}
        $$
        
- ***So, how do we deal with this??***
    - We can modify the equation so that we never encounter features with zero probability
    - We pretend there is never a non-zero count of features in a text. This gives us:
        
        $$
        P(\phi_i) = \dfrac{count(\phi_i)}{\sum_{j=1}^n count(\phi_j)}
        $$
        
        - Where:
            - $i$ is our target variable/feature
            - $j$ is all the features in our data
    - So, instead we can use this to ***smooth*** the probabilities:
        
        $$
        P(\phi_i) = \dfrac{1+count(\phi_i)}{1+\sum_{j=1}^n count(\phi_j)}
        $$
        
    
    # Parameter Learning
    
    - How do we learn the optimal set of parameters ($\theta^*$) such that the score function produces the correct classification for every input $x$?
        
        $$
        \theta^* = \argmax_{\theta \in R^n} \prod_{i=1}^n P(Y=y_i |X = x_i; \theta)
        $$
        
        - We need to search for the set of weights such that the probability of the label given the inputs is maximized
        - Across all $i = 1,…n$ examples in the training data
        - $P(Y=y_i |X = x_i; \theta)$ is the probability that the label for data point $i$ matches the input text for data point $i$ which should be high when the parameters are right and low when they are wrong
    - **We need a set of transforms for our score function**
        1. Switch to log probability space
            
            $$
            \theta^* = \argmax_{\theta \in R^n} \sum_{i=1}^n \log P(Y=y_i |X = x_i; \theta)
            $$
            
        2. Switch to to minimization (**Negative Log Loss**)
            - Since we want our loss function to be a measure of how bad our model is therefore we define loss function as $-\log(θ)$
            
            $$
            \theta^* = \argmin_{\theta \in R^n} \sum_{i=1}^n -\log P(Y=y_i |X = x_i; \theta)
            $$
            
            - Switching from maximizing the likelihood to minimizing the negative log-likelihood in binary logistic regression is largely a matter of ***mathematical convenience and compatibility with optimization algorithms***
            - Switching from log to negative log requires we also switch from a max to a min. Once we switch to a negative log we're now looking at numbers between infinity down to zero
                - And that means what we're trying to do is predict the label and predicting the label now means getting to zero from a very high number down to zero
                - So we're trying to compute the loss or the error or how wrong our parameters are means getting close to zero from a very high number
                - **So a high loss value means we are highly wrong**
                    - We have high loss when we have high error. If we are close to zero, this means we are minimally wrong
            - **Why???**
                - **Advantage of Minimization:** Optimization algorithms are often designed for minimization rather than maximization. Therefore, instead of maximizing the log-likelihood, practitioners minimize the negative log-likelihood
                - **Mathematical Convenience:** The negative log-likelihood provides a convenient and differentiable loss function for gradient-based optimization methods. This facilitates the use of optimization algorithms like gradient descent, which are designed for minimization
        3. Now let's take our negative log-likelihood and put this in terms of our scoring function
            
            $$
            \begin{align}
            
            \theta^* &= \argmin_{\theta \in R^n} \sum_{i=1}^n -\log (\sigma(y_i \cdot score(x_i;\theta))
            \\
            
            \theta^* &= \argmin_{\theta \in R^n} \sum_{i=1}^n \log (1 + \exp(y_i \cdot score(x_i;\theta)))
            
            \\
            
            \theta^* &= \argmin_{\theta \in R^n} \sum_{i=1}^n \underbrace{\log (1 + \exp(y_i \cdot \theta^T \phi(x_i)))}_{\text{Loss function for supervised learning}}
            \end{align}
            $$
            
            - So remember our probability of a particular label given the document and the parameters is equal to the logistic function multiplied by the score multiplied by that label which is a $+1$ or $-1$
    
    # Classification Models
    
    [Logistic Regression](https://www.notion.so/Logistic-Regression-f4424e638eb74609bba43c408d25d82d?pvs=21)
    
    # Resources
    
    ### Smoothing
    
    - [https://medium.com/@dancerworld60/demystifying-naïve-bayes-log-probability-and-laplace-smoothing-d6da61b0e70b](https://medium.com/@dancerworld60/demystifying-na%C3%AFve-bayes-log-probability-and-laplace-smoothing-d6da61b0e70b)
    - [https://repository.ubn.ru.nl/bitstream/handle/2066/227633/227633.pdf?sequence=1](https://repository.ubn.ru.nl/bitstream/handle/2066/227633/227633.pdf?sequence=1)

### Loss Functions

- [https://learningds.org/ch/19/class_loss.html](https://learningds.org/ch/19/class_loss.html)