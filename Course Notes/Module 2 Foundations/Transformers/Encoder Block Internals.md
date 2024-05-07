# Encoder Block Internals

---

# Encoders

[Encoders, Decoders, Autoencoders](https://www.notion.so/Encoders-Decoders-Autoencoders-09d4af88545b457480f873ad1e02f6b3?pvs=21)

# What is it?

# High Level Overview: Stages

- **Inputs:** The inputs to the encoder block are the word embeddings of the input sequence, along with positional encodings
    - Word embeddings are vector representations of words, and positional encodings are added to provide information about the position of the words in the sequence
- **Self-Attention Layer:** The first layer in the encoder block is the self-attention layer. This layer allows the model to weigh the importance of each word in the input when producing the output
    - It does this by computing a weighted sum of the input vectors, where the weights are determined by the attention scores
    - The attention scores are computed using a softmax function applied to the dot product of the input vectors
    - This process is done multiple times (or “heads”) in parallel, allowing the model to capture different types of relationships between the words.
- **Normalization and Residual Connection:** After the self-attention layer, a normalization operation is performed on the output
    - This helps keep the network’s activations from becoming too large and destabilizing the learning process
    - Additionally, the original input is added back to the output of the self attention layer (this is the “residual connection”), which helps the model learn more effectively by combating the vanishing gradient problem
- **Feed-Forward Layer:** The next layer is a feed-forward neural network, which is applied to each position separately and identically
    - This consists of two linear transformations with a ReLU activation in between
- **Normalization and Residual Connection:** Similar to the self-attention layer, the output of the feed-forward layer is normalized, and the input to the layer (the output of the self-attention layer) is added back to it
- **Outputs:** The outputs of the encoder block are the transformed and contextualized word embeddings, which can then be fed into the next encoder block in the stack, or into the decoder if this is the final encoder block

# Encoder Block Structure

- The encoders are all identical in structure (yet they do not share weights). Each one is broken down into two sub-layers:
    
    ![Untitled](Encoder%20Block%20Internals%20736cf410ee444aba8b978d2165605da4/Untitled.png)
    
    - The encoder’s inputs first flow through a self-attention layer – a layer that helps the encoder look at other words in the input sentence as it encodes a specific word
    - The outputs of the self-attention layer are fed to a feed-forward neural network. The exact same feed-forward network is independently applied to each position

# How it works

- The embedding only happens in the bottom-most encoder
    - The abstraction that is common to all the encoders is that they receive a list of vectors each of the size 512
        - In the bottom encoder that would be the word embeddings, but in other encoders, it would be the output of the encoder that’s directly below
        - The size of this list is hyperparameter we can set – basically it would be the length of the longest sentence in our training dataset.
- After embedding the words in our input sequence, each of them flows through each of the two layers of the encoder
    
    ![Untitled](Encoder%20Block%20Internals%20736cf410ee444aba8b978d2165605da4/Untitled%201.png)
    
    - Here we begin to see one key property of the Transformer, which is that the word in each position flows through its own path in the encoder
        - There are dependencies between these paths in the self-attention layer
        - The feed-forward layer does not have those dependencies, however, and thus the various paths can be executed in parallel while flowing through the feed-forward layer
- The word at each position passes through a self-attention process. Then, they each pass through a feed-forward neural network -- the exact same network with each vector flowing through it separately

![Untitled](Encoder%20Block%20Internals%20736cf410ee444aba8b978d2165605da4/Untitled%202.png)

# Detailed Architecture

- One detail in the architecture of the encoder that we need to mention before moving on, is that each sub-layer (self-attention, ffnn) in each encoder has a residual connection around it, and is followed by a [layer-normalization](https://arxiv.org/abs/1607.06450) step
    
    ![Untitled](Encoder%20Block%20Internals%20736cf410ee444aba8b978d2165605da4/Untitled%203.png)
    

- If we’re to visualize the vectors and the layer-norm operation associated with self attention, it would look like this
    
    ![Untitled](Encoder%20Block%20Internals%20736cf410ee444aba8b978d2165605da4/Untitled%204.png)
    

# Implementation

- **Given:**a sequence of tokens $x_1,x_2,…x_n$ and a mask
- Stack the one-hots to create a matrix
    - This allows for parallelization since it’s creating set of independent inputs
- Embed the one-hots into a stack of embeddings

# Resources

- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)