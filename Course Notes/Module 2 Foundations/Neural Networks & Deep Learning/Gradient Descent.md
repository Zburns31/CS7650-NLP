# Gradient Descent

---

# What is Gradient Descent?

- Gradient descent is an iterative optimization algorithm commonly used in machine learning and mathematical optimization

# How it works

- The Gradient Descent Algorithm iteratively calculates the next point using gradient at the current position, scales it (by a learning rate) and subtracts obtained value from the current position (makes a step)
    - It subtracts the value because we want to minimize the function (to maximise it would be adding). This process can be written as:
    
    $$
    p_{n+1}= p_n - \nabla f(p_n)
    $$
    
    - Where:
        - $\nabla$ represents the gradient
- There’s an important parameter **η** which scales the gradient and thus controls the step size
    - In machine learning, it is called **learning rate** and have a strong influence on performance
    - The smaller learning rate the longer GD converges, or may reach maximum iteration before reaching the optimum point
    - If learning rate is too big the algorithm may not converge to the optimal point (jump around) or even to diverge completely

# High Level Process

- Its primary objective is to minimize a function by adjusting its parameters. Here's a high-level summary of how gradient descent works:
    1. **Initialization:** Start with an initial set of parameters for the function you want to minimize
    2. **Calculate Gradient:** Compute the gradient of the function at the current set of parameters
        1. The gradient is a vector that points in the direction of the steepest increase in the function
    3. **Update Parameters:** Adjust the parameters in the opposite direction of the gradient to move towards the minimum of the function
        1. The size of the step is determined by the learning rate, a hyperparameter that controls the size of the update
        2. make a scaled step in the opposite direction to the gradient
    4. **Repeat:** Repeat steps 2 and 3 until convergence or a predetermined number of iterations are reached
        1. Convergence occurs when the change in parameters becomes very small
    5. Terminate when one of the two conditions is satisfied:
        1. Maximum number of iterations is reached
        2. step size is smaller than tolerance (due to scaling or small gradient) 

## Example

- Here's a simple example to illustrate gradient descent:
    - Consider a function, $f(x)=x^2$, and we want to find the minimum value of this function. Gradient descent starts with an initial guess for $x$, let's say $x_0=4$
    - Steps:
        1. **Initialization:** $x_0=4$
        2. **Calculate Gradient:** 
            1. Compute the derivative of $f(x)=x^2$, which is $f'(x)=2x$
            2. At $x_0=4$, the gradient is $f'(4)=2×4=8$
        3. **Update Parameters:** Adjust $x$ in the opposite direction of the gradient. Let's choose a small learning rate, say $α=0.01$
            1. $x_1=x_0 − α×f’(x_0)$
            2. $x_1=4−0.01×8=4−0.08=3.92$
        4. **Repeat:** Repeat steps 2 and 3 until convergence. In each iteration, the value of $x$ gets closer to the minimum
            1. After a few iterations, $x$ approaches 0, and the algorithm converges

# Requirements

- Gradient descent algorithm does not work for all functions. There are ***two specific requirements***. A function has to be:
    1. **Differentiable**
    2. **Convex**
- What does it mean it has to be **differentiable**?
    - If a function is differentiable it has a derivative for each point in its domain — not all functions meet these criteria
- What does it mean to be **convex**?
    - A convex function is a mathematical function where, roughly speaking, the line segment between any two points on the graph of the function lies above the graph itself. In other words, if you pick any two points on the curve of a convex function and draw a straight line between them, that line will always be above the curve
    - [Good Resource](https://towardsdatascience.com/gradient-descent-algorithm-a-deep-dive-cf04e8115f21)

# Stochastic Gradient Descent (SGD)

---

- **How SGD works:**
    1. **Initialization:** Start with initial values for the model parameters
    2. **Shuffle Data:** Shuffle the training dataset
    3. **Iterative Process:** In each iteration:
        - Randomly select a mini-batch from the shuffled dataset
        - Compute the gradient of the loss function with respect to the model parameters using the selected mini-batch
        - Update the model parameters using the computed gradient and a learning rate
    4. **Repeat:** Repeat the process until convergence or a predefined number of iterations

## How does SGD and Normal GD Differ?

### Normal Gradient Descent (GD):

1. **Batch Processing:** GD computes the gradient of the entire dataset to update the model parameters in each iteration
2. **Slow on Large Datasets:** It can be computationally expensive, especially when dealing with large datasets, as it requires processing the entire dataset for each iteration
3. **Deterministic Updates:** The updates are deterministic and based on the average gradient over the entire dataset

### Stochastic Gradient Descent (SGD):

1. **Mini-Batch Processing:** SGD processes only a subset (mini-batch) of the dataset in each iteration to update the model parameters
2. **Faster Updates:** Because it only considers a small random subset, each iteration is computationally less demanding compared to GD
3. **Stochastic Updates:** The updates are more stochastic and noisy, as they are based on the gradient of a random mini-batch rather than the entire dataset
4. **Noisy Convergence:** Due to the randomness introduced by mini-batches, SGD may have more oscillations in the convergence path, but it can sometimes escape from local minima

# Key Terms & Concepts

---

- **Gradient** is a vector that is tangent of a function and points in the direction of greatest increase of this function
    - Gradient is zero at a local maximum or minimum because there is no single direction of increase
    - A gradient is the derivative of a tensor operation. It’s the generalization of the concept of derivatives to functions of multidimensional inputs:
- **Convex Functions**
    - Here are two key characteristics of convex functions:
        1. **Line Segment Above the Curve:** For any two points $x_1$ and $x_2$ in the domain of the function and any value $t$ between 0 and 1, the following condition holds:
            
            $$
            
            ⁍
            $$
            
        2. **Global Minimum:** Convex functions have a global minimum
            1. This means that there is a single point (or possibly a set of points) where the function takes its smallest value over the entire domain

# References

- [https://towardsdatascience.com/gradient-descent-algorithm-a-deep-dive-cf04e8115f21](https://towardsdatascience.com/gradient-descent-algorithm-a-deep-dive-cf04e8115f21)
- [https://towardsdatascience.com/an-introduction-to-gradient-descent-c9cca5739307](https://towardsdatascience.com/an-introduction-to-gradient-descent-c9cca5739307)
- [https://towardsdatascience.com/learning-process-of-a-deep-neural-network-5a9768d7a651](https://towardsdatascience.com/learning-process-of-a-deep-neural-network-5a9768d7a651)

## Videos

- [StatQuest Gradient Descent](https://www.youtube.com/watch?v=sDv4f4s2SB8)
- [Andrew Ng’s GD Overview](https://www.coursera.org/learn/neural-networks-deep-learning/lecture/A0tBd/gradient-descent)

## Blogs & Tutorials

- [Simple Intro to GD](https://medium.com/@hunter-j-phillips/a-simple-introduction-to-gradient-descent-1f32a08b0deb)
- [GD & Backprop Example Step by Step](https://hmkcode.com/ai/backpropagation-step-by-step/)
- [Single Layer NN & GD - Code + Visual Walkthrough](https://sebastianraschka.com/Articles/2015_singlelayer_neurons.html)