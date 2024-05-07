# Multinomial Logistic Regression

---

# What is it?

- Multinomial logistic regression, also known as softmax regression, is a generalization of binary logistic regression to handle multiple classes
- In the context of neural networks, multinomial logistic regression is often implemented as a part of a larger neural network architecture

# Binary Vs. Multinomial Logistic Regression

- In binary logistic regression, we have:
    - **Sigmoid function**, which maps a real-valued input to the range 0 to 1
    - **Maximum likelihood estimation (MLE)**, which maximizes the probability of the data
    - **Gradient descent**, which attempts to find the minimum parameters of MLE
- In multinomial logistic regression, we have:
    - **Softmax function**, which turns all the inputs into positive values and maps those values to the range 0 to 1
    - **Cross-entropy loss function**, which maximizes the probability of the scoring vectors to the one-hot encoded Y (response) vectors
    - **Stochastic gradient descent**, which is just a gradient descent from a sample features

# Architecture:

1. **Input Layer:**
    - The input layer consists of neurons, each representing a feature of the input data
2. **Hidden Layers (Optional):**
    - There may be one or more hidden layers between the input and output layers
        - These hidden layers allow the network to learn complex representations of the input features
3. **Output Layer:**
    - The output layer uses a softmax activation function to produce a probability distribution over multiple classes
    - Each neuron in the output layer corresponds to a class, and the softmax function ensures that the output values sum to 1
        - I.e. If there are 10 classes, then the output layer has 10 heads

## Activation Function:

- **Softmax Function:**
    - The softmax function is used in the output layer to convert raw scores (logits) into a probability distribution over multiple classes. It is defined as:
    
    $$
    \text{softmax}(z_i) = \dfrac{e^{z_i}}{\sum_{j=1}^C e^{z_j}} 
    $$
    
    - where $z$ is the vector of raw scores for each class, and $C$ is the total number of classes

## Loss Function

- **Cross-Entropy Loss:**
    - The cross-entropy loss function is commonly used for training multinomial logistic regression models
    - In the context of neural networks, the categorical cross-entropy loss is applied
        - For a given example with true class y and predicted probability distribution y^, the loss is calculated as:
    
    $$
    ⁍
    $$
    
    - where $C$ is the number of classes

# Multinomial Logistic Classification as Probability

- How do we get the probability distribution over labels in a document. So we have:
    
    $$
    \begin{align}
    
    & P(Y | X=x;\theta) = softmax((score(x,y_1;\theta), score(x,y_2;\theta),...score(x,y_n;\theta)
    
    \end{align}
    $$
    
    - Where $y_i$ represents the class label
    - One of the numbers is going to be close to 1 and the rest will be close to 0
- However, what we really want to know is the conditional probability for a single class label, given a particular document and a set of parameters
    - Example: What is the probability that document $x$ is scifi (if my parameters are right)?
    
    $$
    \begin{align}
    
    P(Y = \ell | X = x;\theta) &= \dfrac{exp(score(x, \ell; \theta))}{\sum_{\ell' \in \ell} \exp(score(x, \ell';\theta))} 
    
    \\
    \\
    
    &= \dfrac{\exp(score(x, \ell;\theta)}{z(x;\theta)}
    \end{align}
    $$
    
    - Where:
        - $\ell$ represents only the label of interest
    - $z(x;\theta)$ is what makes multinomial logistic regression computationally expensive
        - To compute the probability even for a single label, one must sum across the scores for all labels and normalize

# Parameter Learning

---

- Recall from binary classification:

$$
\begin{align}

\theta^* &= \argmin_{\theta} \sum_{i=1}^n - \log P(Y = y_i|X=x_i;\theta)
\\

\end{align}
$$

- Same as before:
    - Find the parameters $\theta$ that minimize the log loss
    - The difference is that $P(Y=y_i|X=x_i;\theta)$ is defined differently
- For a single label:
    
    $$
    \begin{align}
    \theta^* &= \argmin_{\theta} \sum_{i=1}^n - \log \left [ \dfrac{\exp(score(x_i, y_i;\theta))}{z(x_i;\theta)} \right ]
    \\
    \\
    
    \theta^* &= \argmin_{\theta} \sum_{i=1}^n \left [ - \log(\exp(score(x_i, y_i;\theta))) - \log z(x_i;\theta) \right ]
    \\
    \\
    \theta^* &= \argmin_{\theta} \sum_{i=1}^n - score(x_i,y_i;\theta) + \log z(x_i;\theta)
    \\
    \\
    
    \theta^* &= \argmin_{\theta} \sum_{i=1}^n - \theta^T f(x_i, y_i) + \log \sum_{\ell \in \mathcal{L}} \exp(\theta^T f(x_i, \ell))
    \end{align}
    $$
    
    - Notes:
        - $f(x_i, y_i)$
            - Maximize the score (or minimize negative score) for features that correlate with correct label $y_i$
        - $\sum_{\ell \in \mathcal{L}} \exp(\theta^T f(x_i, \ell))$
            - Minimize the score for all other labels
        - **Goal:** Find the parameters that push up the score for the correct label but push down the scores for all other labels
            - Otherwise one can win by making parameters $\infty$

## Negative Log Likelihood Loss

![Untitled](Multinomial%20Logistic%20Regression%20f3ffd493ae5743c9b222e9c57e1c281b/Untitled.png)

- Negate the loss because we want high loss to be bad

# Resources

### Tutorials & Blogs

- [https://d2l.ai/chapter_linear-classification/softmax-regression.html](https://d2l.ai/chapter_linear-classification/softmax-regression.html)
- [http://deeplearning.stanford.edu/tutorial/supervised/SoftmaxRegression/](http://deeplearning.stanford.edu/tutorial/supervised/SoftmaxRegression/)
- [https://medium.com/ds3ucsd/multinomial-logistic-regression-in-a-nutshell-53c94b30448f](https://medium.com/ds3ucsd/multinomial-logistic-regression-in-a-nutshell-53c94b30448f)

### Cross Entropy Loss

- [https://www.educative.io/answers/what-is-cross-entropy-loss-in-pytorch](https://www.educative.io/answers/what-is-cross-entropy-loss-in-pytorch)