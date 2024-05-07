# Fully Connected NN’s

---

# What are they?

- **Deep feedforward networks**, also often called **feedforward neural networks**, or **multilayer perceptrons** (MLPs), are the quintessential deep learning models
- [https://jermwatt.github.io/machine_learning_refined/notes/13_Multilayer_perceptrons/13_2_Multi_layer_perceptrons.html](https://jermwatt.github.io/machine_learning_refined/notes/13_Multilayer_perceptrons/13_2_Multi_layer_perceptrons.html)

# Goals

- The goal of a feedforward network is to approximate some function $f^*$
    - A feedforward network defines a mapping $y= f(x; \theta)$ and learns the value of the parameters $\theta$ that result in the best function approximation
- The function f is composed of a chain of functions: $f=f^{(k)}(f^{(k−1)}(…f^{(1)}))$, where $f^{(1)}$ is called the input layer, and so on. The **depth** of the network is $k$
- The final layer of a feedforward network is called the output layer

# Architecture

- The architecture of a network is an art:
    - How many layers the network should contain
    - How these layers should be connected to each other
    - How many units should be in each layer
    

## Network Design Choices

|  | Input Layer | Hidden Layer | Output Layer |
| --- | --- | --- | --- |
| Number of Layers | 1 | Design Choice | 1 |
| Size (# of Neurons) | Input Vector | Design Choice | Nature of Task |
| Input to Neurons | N/A | Size of the preceding layer | Size of last hidden layer |
| Output to Neurons | Size of 1st hidden layer | Size of the following layer | 1 |

## Tradeoffs

- **Number of Layers:**
    - The more hidden layers we have the more complex the network
        - It will take more time to train and a lot more difficult
- **Number of Neurons:**
    - Input Layer: Same shape as the input vector
    - Hidden Layer: Design Choice

# Resources

- [https://deeplearningmath.org/general-fully-connected-neural-networks.html](https://deeplearningmath.org/general-fully-connected-neural-networks.html)
- [https://jermwatt.github.io/machine_learning_refined/notes/13_Multilayer_perceptrons/13_2_Multi_layer_perceptrons.html](https://jermwatt.github.io/machine_learning_refined/notes/13_Multilayer_perceptrons/13_2_Multi_layer_perceptrons.html)