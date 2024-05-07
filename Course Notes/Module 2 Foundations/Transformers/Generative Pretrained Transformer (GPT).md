# Generative Pretrained Transformer (GPT)

---

# What is it?

- Decoder models use only the decoder of a Transformer model
    - At each stage, for a given word the attention layers can only access the words positioned before it in the sentence
        - These models are often called ***auto-regressive models***
- GPT tweaks the transformer concept to make it suited for predicting the next word in a sequence
    - Outputs ($y$) are shifted to the left becasue we want to predict the next word
    - Future context is masked
- Utilizes a ***decoder-only architecture***

# Inputs & Outputs

- **The input** is a prompt (often referred to as context) fed into the transformer as a whole
    - There is no recurrence
- **The output** depends on the goal of the model
    - For GPT models, the output is a probability distribution of the next token/word that comes after the prompt
    - It outputs **one** prediction for the complete input

# How does it work?

1. **The embedding**: the input of the transformer model is a prompt. This prompt needs to be embedded into something that the model can use
2. **The block(s)**: This is the main source of complexity
    1. Each block contains a masked multi-head attention submodule, a feedforward network, and several layer normalization operations
    2. *Blocks are put in sequence* to make the model deeper
3. **The output**: the output of the last block is fed through one more linear layer to obtain the final output of the model (a classification, a next word/token etc.)
    
    ![Untitled](Generative%20Pretrained%20Transformer%20(GPT)%20db51557a209a430dbc62dc311f8144fa/Untitled.png)
    

# Resources

- [https://ai.stackexchange.com/questions/40179/how-does-the-decoder-only-transformer-architecture-work](https://ai.stackexchange.com/questions/40179/how-does-the-decoder-only-transformer-architecture-work)
- [https://medium.com/@ElGueddari/the-dual-worlds-of-decoder-only-transformers-training-vs-inference-1ea1c2aabaaa](https://medium.com/@ElGueddari/the-dual-worlds-of-decoder-only-transformers-training-vs-inference-1ea1c2aabaaa)