# Layer Normalization

---

# What is it?

- **Layer Normalization:** Layer normalization is a technique used in deep learning to stabilize the learning process and reduce the training time
    - It normalizes the inputs across the features instead of normalizing the features across the batch as in batch normalization

# Where is it Used?

- **Layer Normalization in Transformers:** In Transformers, layer normalization is used in both the encoder and 
decoder sub-layers, including self-attention and feed-forward neural networks
    
    ![Untitled](Layer%20Normalization%20f3c026ddeebf45f785ec8420084ad8ce/Untitled.png)
    
    - Learn to expand and compress the embeddings
        - Expansion gives capacity to spread concepts out
        - Compression forces compromises but in a different configuration

# How is it Used?

1. The input first goes through the **Multi-Head Attention** sub-layer
2. The output of the Multi-Head Attention sub-layer is then added to the original input in a process known as **residual connection** or **shortcut connection**
3. This sum is then normalized using **Layer Normalization**
4. The normalized output is then passed through the **Pointwise Feedforward Neural Network**
5. The output of the Feedforward network is added to the input of the Feedforward network (again, a residual connection)
6. This sum is then normalized again using **Layer Normalization**

[Residuals](Residuals%20387c0c6e17d946e9884e9bcbde0de959.md)

# How does it work?

- In layer normalization, for each feature in a layer, we subtract the mean and divide by the standard deviation, computed across all the features
    - This process ensures that the output of the normalization for each feature has a mean of 0 and a standard deviation of 1
- The formulas for layer normalization are as follows:
    
    $$
    \begin{align}
    \mu &= \frac{1}{H} \sum_{i=1}H x_i
    \\
    \\
    \sigma &= \sqrt{\frac{1}{H} \sum_{i=1}H (x_i - \mu)^2}
    \\
    \\
    \bar{x_i} &= \frac{x_i - \mu}{\sigma}
    
    \end{align}
    $$
    
    - Here, $x_i$ is the input to the layer, $H$ is the number of hidden units in the layer, $μ$ is the mean, and $σ$ is the standard deviation
        - The normalized input $\bar{x_i}$ is then scaled and shifted by two learnable parameters, usually denoted as $γ$ (scale) and $β$ (shift)
        

# Use in Transformers

- After normalizing, add trainable parameters $(W,b)$ so that the network can adjust the mean and standard deviation how it needs:

$$
x'' = Wx' + b
$$

# Resources

- [https://www.kaggle.com/code/halflingwizard/how-does-layer-normalization-work](https://www.kaggle.com/code/halflingwizard/how-does-layer-normalization-work)
- [https://lessw.medium.com/what-layernorm-really-does-for-attention-in-transformers-4901ea6d890e](https://lessw.medium.com/what-layernorm-really-does-for-attention-in-transformers-4901ea6d890e)
- [https://medium.com/@hunter-j-phillips/layer-normalization-e9ae93eb3c9c](https://medium.com/@hunter-j-phillips/layer-normalization-e9ae93eb3c9c)