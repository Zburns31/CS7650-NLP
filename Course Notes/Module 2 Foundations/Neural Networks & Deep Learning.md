# Neural Networks & Deep Learning

# What is Deep Learning?

- **Deep learning** is an approach to machine learning characterized by deep stacks of computations. This depth of computation is what has enabled deep learning models to disentangle the kinds of  complex and hierarchical patterns found in the most challenging
real-world datasets
- Through their power and scalability **neural networks** have become the defining model of deep learning
    - Neural networks are composed of neurons, where each neuron individually performs only a simple computation
- The power of a neural network comes instead from the complexity of the connections these neurons can form
- A neural network is just a composition of linear transformations and non-linear functions
    - Armed with these non-linearities, NN can approximate any function given enough hidden units
        - This is called the [Universal approximation theorem](http://neuralnetworksanddeeplearning.com/chap4.html) and has been proven with relatively weak assumptions
        - Intuitively, if a NN is able to represent a [step function](https://en.wikipedia.org/wiki/Step_function), which is a function made up of finitely many piecewise constant components, then it is able to approximate any other function with arbitrary accuracy given enough of these step components

# Neural Networks Overivew

- Neural networks are considered ***universal function approximators*** because, theoretically, they can learn to approximate any function, no matter how complex, given enough parameters (weights and biases) and sufficient training data
    - It states that a feedforward neural network with a single hidden layer containing a sufficient number of neurons can approximate any continuous function on a closed and bounded input space to any desired degree of accuracy

# Foundations: Neurons (Perceptrons)

---

- A neuron takes inputs, does some math with them, and produces one output
- There are multiple components which make up a neuron:
    1. **Inputs** (i.e. Feature Values)
    2. **Bias Weight:** Input Weight
    3. **Input (Transfer) Function:** Some form of aggregation for the inputs
        1. Typically a summation over the inputs (semi-linear)
    4. **Activation Function:** The activation function is used to turn an unbounded input into an output that has a nice, predictable form
        1. Activation functions are how we are able to approximate nonlinear functions
        2. Typically examples are: [Sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function), [Probit](https://en.wikipedia.org/wiki/Probit), [Step](https://iq.opengenus.org/binary-step-function/)
        3. [Good Reference](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/FNN/tutorial.html)
    5. Outputs

    ![Untitled](./Neural%20Networks%20&%20Deep%20Learning/Untitled.png)

    - Here:
        - Let $a_i$denote the output of neuron $j$ and $w_i$ let be the weight attached to the link from unit $i$ to unit $j$
        - $g_j$ is a nonlinear activation function associated with neuron $j$ and $in_i$ us the weighted sum of the inputs to neuron $j$

# Neural Network Building Blocks

- **Neurons:** Just a thing that holds a number. This number is also called the activation of a specific neuron
    - Neurons have many inputs, but only one output
    - Output is a ***weighted sum*** (affine transformation)
    - Threshold can be set (gives non-linear response)
- **Weights:**
    - Each weight is an indication of how its neuron in the first layer is correlated with this new neuron in the second layer
    - If the neuron in the first layer is on, then a **positive** weight suggests that the neuron in the second layer should also be on, and a **negative** weight suggests that the neuron in the second layer should be off
- **Layer:** The core building block of neural networks is the ***layer***, a data-processing module that you can think of as a filter for data
    - Some data goes in, and it comes out in a more useful form. Specifically, layers extract representations out of the data fed into them
    - Most of deep learning consists of chaining together simple layers that will implement a form of progressive data distillation
        - A deep-learning model is like a sieve for data processing, made of a succession of increasingly refined data filters—the layers
        - Layers break problems into bite sized pieces
        - A layer in which every neuron is connected to every other neuron in its next layer is called a **dense** **layer**
    - Typical Layers:
        - Input Layer
        - Hidden Layers
        - Output Layer
- **Activation Function**
    - These are what help introduce non-linearity into the network and allow for learning of arbitrarily complex functions
- L**oss function**
    - How the network will be able to measure its performance on the training data, and thus how it will be able to steer itself in the right direction
- **Optimizer**
    - The mechanism through which the network will update itself based on the data it sees and its loss function

# Notation & Math

---

[Notation & Math](./Neural%20Networks%20&%20Deep%20Learning/Notation%20&%20Math.md)

# Core Principles

- **Computing Decision Boundaries**
    - Minsky and Papert showed that a ***single layer FNN cannot solve problems in which the data is not linearly separable***, such as the XOR problem ([Newell 1969](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/FNN/tutorial.html#Newell780)). Adding one (or more) hidden layers to FNN enables it to solve problems in which data is non-linearly separable. Per ***Universal Approximation Theorem***, a FNN with one hidden layer can represent any function ([Cybenko 1989](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/FNN/tutorial.html#Cybenko1989)), although in practice training such a model is very difficult (if not impossible), hence, we usually add multiple hidden layers to solve complex problems
        - The Non-Linearity of the activation function allows each neuron to make it’s own contribution to the decision boundary
        - Additionally, the combination of multiple linear decision boundaries [can create non-linear boundaries](https://stats.stackexchange.com/questions/463716/how-can-a-neural-network-produce-non-linear-decision-boundary)

# How do Neural Networks Learn?

---

1. Typically, the weights of the networks are randomized initially
2. What comes next is to gradually adjust these weights, based on a feedback signal. This gradual adjustment, also called training, is basically the learning that machine learning is all about. This happens within what’s called a training loop, which works as follows:
    1. Repeat these steps in a loop, as long as necessary:
        1. Run for N epochs (until termination)
        2. Draw a batch of training samples $x$ and corresponding targets $y$
        3. Run the network on $x$ (a step called the forward pass) to obtain predictions $y_{pred}$
        4. Compute the loss of the network on the batch, a measure of the mismatch between $y_{pred}$ and $y$
        5. Update all weights of the network in a way that slightly reduces the loss on this batch
3. Repeat step 2 until the loss is minimized (but before overfitting the data)

## Gradient Descent

[Gradient Descent](./Neural%20Networks%20&%20Deep%20Learning/Gradient%20Descent.md)

## Back-Propagation

[Back-Propagation](./Neural%20Networks%20&%20Deep%20Learning/Back-Propagation.md)

- This process of updating the weights and summing the gradient updates for all of the training examples is a called an **epoch**

# Types of Neural Networks

### Fully Connected (Feed Forward) NN’s

- **Feedforward neural networks** are [artificial neural networks](https://brilliant.org/wiki/artificial-neural-network/) where the connections between units do not form a [cycle](https://brilliant.org/wiki/graphs/##graphs-basic)
- They are called *feedforward* because information only travels forward in the network (no loops), first through the input nodes, then through the [hidden nodes](https://brilliant.org/wiki/artificial-neural-network/#putting-it-all-together) (if present), and finally through the output nodes

[Fully Connected NN’s](./Neural%20Networks%20&%20Deep%20Learning/Fully%20Connected%20NN’s.md)

### Recurrent (Sequential) NN’s (RNN’s)

- Use cases: Speech, Time-Series

[RNN & LSTM](./Neural%20Networks%20&%20Deep%20Learning/RNN%20&%20LSTM.md)

### Convolutional NN’s

- Use Cases: Image

### Encoders & Decoders

[Encoders, Decoders, Autoencoders](./Neural%20Networks%20&%20Deep%20Learning/Encoders,%20Decoders,%20Autoencoders.md)

### Sequence-to-Sequence Models

[Sequence-to-Sequence Models (Seq2Seq)](./Neural%20Networks%20&%20Deep%20Learning/Sequence-to-Sequence%20Models%20(Seq2Seq).md)

### Transformers

[Transformers](./Transformers.md)

# Problem Spaces

[Deep Learning: Classification](./Neural%20Networks%20&%20Deep%20Learning/Deep%20Learning%20Classification.md)

# Activation Functions

[Activation Functions](./Neural%20Networks%20&%20Deep%20Learning/Activation%20Functions.md)

# Resources

## Books

- [DL Book (Goodfellow)](https://www.deeplearningbook.org/)
- [Understanding DL](https://udlbook.github.io/udlbook/)
- [Dive into Deep Learning](https://d2l.ai/index.html)

## MOOC’s

- [Linear Algebra for ML](https://www.coursera.org/learn/linear-algebra-machine-learning?specialization=mathematics-machine-learning)
- [Multivariate Calc for ML](https://www.coursera.org/learn/multivariate-calculus-machine-learning?specialization=mathematics-machine-learning)
- [Standford DL for CV](http://cs231n.stanford.edu/)
- [Deeplearning Specialization](https://www.coursera.org/specializations/deep-learning)
- MIT Intro to ML [Lectures](https://openlearninglibrary.mit.edu/courses/course-v1:MITx+6.036+1T2019/courseware/Week6/neural_networks/?activate_block_id=block-v1%3AMITx%2B6.036%2B1T2019%2Btype%40sequential%2Bblock%40neural_networks) & [Notes](https://openlearninglibrary.mit.edu/assets/courseware/v1/9c36c444e5df10eef7ce4d052e4a2ed1/asset-v1:MITx+6.036+1T2019+type@asset+block/notes_chapter_Neural_Networks.pdf)

# Tutorials

- [Neural Networks: 0 to Hero](https://karpathy.ai/zero-to-hero.html)
- [3Blue1Brown Deep Learning Series](https://www.youtube.com/watch?v=aircAruvnKk)
    - [Written Series](https://www.3blue1brown.com/topics/neural-networks)
- [Matrix Calculus](https://explained.ai/matrix-calculus/) & [Paper](https://arxiv.org/pdf/1802.01528.pdf)
- [Karpathy Makemore: Intro to NLP](https://www.youtube.com/watch?v=PaCmpygFfXo)
- [Intro to DL Kaggle](https://www.kaggle.com/learn/intro-to-deep-learning)
- [PyTorch Tutorials](https://uvadlc-notebooks.readthedocs.io/en/latest/tutorial_notebooks/tutorial2/Introduction_to_PyTorch.html)
- [Dissecting DL & RL](https://mpatacchiola.github.io/blog/2018/12/28/dissecting-reinforcement-learning-8.html)
- [Hands on DL - FeedForward NN’s](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/FNN/tutorial.html)

### NN Math

- [https://openlearninglibrary.mit.edu/assets/courseware/v1/9c36c444e5df10eef7ce4d052e4a2ed1/asset-v1:MITx+6.036+1T2019+type@asset+block/notes_chapter_Neural_Networks.pdf](https://openlearninglibrary.mit.edu/assets/courseware/v1/9c36c444e5df10eef7ce4d052e4a2ed1/asset-v1:MITx+6.036+1T2019+type@asset+block/notes_chapter_Neural_Networks.pdf)

# Component Specific Resources

### Activation Functions

- [https://en.wikibooks.org/wiki/Artificial_Neural_Networks/Activation_Functions](https://en.wikibooks.org/wiki/Artificial_Neural_Networks/Activation_Functions)