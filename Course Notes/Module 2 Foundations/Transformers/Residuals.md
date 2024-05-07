# Residuals

---

# What are they?

- In the context of Transformer models, residuals refer to the concept of “residual connections” or “skip connections”, which are a key component of the model’s architecture
    
    ![Untitled](Residuals%20387c0c6e17d946e9884e9bcbde0de959/Untitled.png)
    
- 

# Why use them?

- The purpose of these residual connections is to help mitigate the problem of vanishing gradients, a common issue in deep neural networks where the gradients become increasingly small as they are propagated back through the layers during training
    - This can lead to slower convergence or the model failing to learn effectively
- Residual connections help to create more direct paths for the gradients to flow during backpropagation, making it easier for the model to learn and often leading to improved performance
- In Transformers, residual connections are used in both the encoder and decoder sub-layers, including self attention and feed-forward neural networks
    - After each sub-layer’s operation, the input to the sub-layer  (before the operation) is added to the output of the sub-layer
    - This combined result is then normalized and passed to the next sub-layer or used as the final output of the encoder/decoder block.

# How do they work?

- A residual connection works as follows: instead of sending the output of a layer directly to the next layer, the original input to the layer is added to the output
    - This sum is then passed to the next layer
        - In other words, the network is learning the residual function (hence the name) or the difference between the input and output, rather than the full output
- Mathematically, if we denote the input of a layer as `x` and the function of the layer as `F(x)`, a layer with a residual connection computes `F(x) + x` instead of just `F(x)` . This can also be stated as:
    
    $$
    x + \text{Sublayer}(x)
    $$
    

![Untitled](Residuals%20387c0c6e17d946e9884e9bcbde0de959/Untitled%201.png)

- Residual connections carry over the previous embeddings to the subsequent layers
    - As such, the encoder blocks enrich the embedding vectors with additional information obtained from the multi-head self-attention calculations and position-wise feed-forward networks

# Application of Residual

- Results of self-attention are added to the residual
- Important to retain the original embeddings in the original order
- Reinforcing or inhibiting embedding values (according to the transformation just before it)
- ***Now each embedding is some amount of the original embedding as well as some proportion of every other embedding attended to***

# Resources

- [https://kikaben.com/transformers-encoder-decoder/](https://kikaben.com/transformers-encoder-decoder/)