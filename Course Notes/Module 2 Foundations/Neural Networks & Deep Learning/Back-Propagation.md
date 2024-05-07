# Back-Propagation

---

# High Level Overview

- **Forward Pass:**
    - Pass the entire batch into the NN
        - Each row is a sample and each column is a feature
    - Take these samples and pass them through the network until we get our prediction
- **Backward Pass (Backpropagation):**
    - Take the loss and use backpropagation which for every neuron, bias and weight, calculate the partial derivatives to determine which direction we need to move the parameters to minimize the loss

![Untitled](Back-Propagation%201a8f6befbb274d1bab9d105f4a261ef4/Untitled.png)

# High-Level Process

- Backpropagation starts with the final loss value and works backward from the top layers to the bottom layers, applying the chain rule to compute the contribution that each parameter had in the loss value
- It's used to minimize the error of the network's output by adjusting the weights of the connections between neurons. Here's a detailed step-by-step explanation of how the backpropagation algorithm works:
    
    ### 1. Forward Pass:
    
    - **Input:** Provide the neural network with an input example, and let it propagate through the layers to produce an output.
        1. **Input Layer:** Set the values of the input neurons to the features of the input example
        2. **Hidden Layers:** For each hidden layer:
            - Compute the weighted sum of inputs to each neuron
            - Apply an activation function to the sum to get the output of each neuron
            - Pass this output to the next layer as input
        3. **Output Layer:** Similar to hidden layers, compute the weighted sum and apply an activation function. The output is the prediction of the neural network
    
    ### 2. Compute Loss:
    
    **Objective:** Compare the predicted output with the actual target values to measure the error. The loss function quantifies this difference.
    
    ### 3. Backward Pass:
    
    **Objective:** Propagate the error backward through the network to adjust the weights and minimize the loss.
    
    **3.1. Compute Output Layer Gradients:**
    
    - **Gradient Descent:** Compute the derivative of the loss with respect to the output layer's weighted sum. This gradient guides how much the output should change to minimize the loss
    - **Chain Rule:** Use the chain rule to compute the gradient of the loss with respect to each weight and bias in the output layer
    
    **3.2. Update Output Layer Weights:**
    
    - **Gradient Descent Update:** Adjust the weights and biases of the output layer in the opposite direction of their gradients
        - The learning rate controls the size of the update
    
    **3.3. Backpropagate to Hidden Layers:**
    
    - **Error Backpropagation:** Propagate the gradient backward through the network. For each hidden layer:
        - Compute the derivative of the loss with respect to the weighted sum of each neuron
        - Use the chain rule to compute the gradients with respect to weights and biases
    
    **3.4. Update Hidden Layer Weights:**
    
    - **Gradient Descent Update:** Adjust the weights and biases of each hidden layer using the computed gradients
    
    ### 4. Repeat:
    
    **Objective:** Repeat the forward and backward passes for multiple iterations (epochs) until the network's performance converges or until a predetermined stopping criterion is met.
    

# How does it work?

1. Output Layer: Same as for single layer perceptrons
    1. Calculate our error looking at what the output should be and what it is for a training example
    2. $W_{i,j} \leftarrow W_{i,j} + \alpha \space X \space \alpha_j \space X \space \triangle_i$
        1. Where $\triangle_i = Err_i \space X \space  g^1(in_i)$
2. Hidden Layer: Back propagate the error from the output layer
    1. The idea here is that a hidden node ***j***, is responsible for some quantity of the error $\triangle_i$ in each of the output nodes in which it connects
    2. $\triangle_j = g^1(in_j) \sum_i W_{j,i} \triangle_i$
3. Update Rule for weights in the hidden layer
    1. $W_{k,j} \leftarrow W_{k,j} + \alpha \space X \space \alpha_k \space X \space \triangle_j$

# Resources

- [Andrej Karpathy Backprop Tutorial](https://www.youtube.com/watch?v=VMj-3S1tku0)
- [Backprop: Step by Step](https://hmkcode.com/ai/backpropagation-step-by-step/)
- [3Blue1Brown Backpro Overview](https://www.youtube.com/watch?v=Ilg3gGewQ5U)
- [Backprop for Dummies](https://medium.com/analytics-vidhya/backpropagation-for-dummies-e069410fa585)
- [Understanding Backprop](https://towardsdatascience.com/understanding-backpropagation-algorithm-7bb3aa2f95fd)
- [Step By Step Intro](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)
- [Stanford Tutorial](https://cs.stanford.edu/~quocle/tutorial1.pdf)

## Links

- [https://training.galaxyproject.org/training-material/topics/statistics/tutorials/FNN/tutorial.html](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/FNN/tutorial.html)
- [https://towardsdatascience.com/understanding-backpropagation-algorithm-7bb3aa2f95fd](https://towardsdatascience.com/understanding-backpropagation-algorithm-7bb3aa2f95fd)
- [https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)
- [https://towardsdatascience.com/learning-process-of-a-deep-neural-network-5a9768d7a651](https://towardsdatascience.com/learning-process-of-a-deep-neural-network-5a9768d7a651)
- [https://medium.com/data-science-365/overview-of-a-neural-networks-learning-process-61690a502fa](https://medium.com/data-science-365/overview-of-a-neural-networks-learning-process-61690a502fa)

### Tutorials & Examples

- [https://towardsdatascience.com/how-neural-network-learn-3b56c175b5ca](https://towardsdatascience.com/how-neural-network-learn-3b56c175b5ca)