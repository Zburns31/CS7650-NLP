# Positional Encoding

---

# What is it?

- In natural language processing tasks, the order of words in a sentence carries significant information
    - However, the self-attention mechanism in Transformers does not inherently capture the position of the words in a sequence. To address this, Transformers use a technique called positional encoding
- These positional encodings are added to the word embeddings before they are fed into the encoder, allowing the Transformer to consider the position of the words when processing the sentence
    - This is crucial for tasks like translation, where the order of the words carries important meaning

# How does it work?

- The positional encoding is a fixed-length vector **added to the word *i*** ‘s embedding ***xᵢ*** to enable **parallel** processing of input sequences **without disrupting the word order**
- The positional encodings are vectors that have the same dimension as the word embeddings, so they can be added together
- The values of the positional encodings are generated using a specific formula involving sine and cosine functions:
    
    $$
    \begin{align}
    & PE(pos,2i)=sin(pos/10000^{2i/d_{model}})
    \\
    & PE(pos,2i+1)=cos(pos/10000^{2i/d_{model}})
    \end{align}
    $$
    
    - Here, $pos$ is the position of the word in the sequence, and $i$ ranges from 0 to $d_{model}/2$, where $d_{model}$ is the dimension of the word embeddings
    - The $2i$ and $2i+1$ in the formulas ensure that each dimension of the positional encoding corresponds to a sinusoid of a different frequency
- The intuition behind these formulas is to create unique positional encodings that can capture both the absolute position of a word in a sentence (through the lower-frequency sinusoids) and the relative position of words (through the higher-frequency sinusoids)

# Resources

- [Good Resource](https://datascience.stackexchange.com/questions/51065/what-is-the-positional-encoding-in-the-transformer-model)
- [Mathematical Explanation](https://kazemnejad.com/blog/transformer_architecture_positional_encoding/#the-intuition)

# Resources

- [D2L](https://d2l.ai/chapter_attention-mechanisms-and-transformers/self-attention-and-positional-encoding.html)
- [https://towardsdatascience.com/understanding-positional-encoding-in-transformers-dc6bafc021ab](https://towardsdatascience.com/understanding-positional-encoding-in-transformers-dc6bafc021ab)