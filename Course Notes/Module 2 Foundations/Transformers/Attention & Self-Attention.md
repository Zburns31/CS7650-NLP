# Attention & Self-Attention

---

# What is Attention?

- Attention is a fundamental mechanism in NLP transformer models that allows them to weigh the importance of different words in a sequence while processing each word. It enables the model to capture contextual relationships and dependencies among words, making it highly effective in understanding natural language
- By using self-attention, transformer models can efficiently capture long-range dependencies and contextual information in sequences, making them powerful tools for various NLP tasks like machine translation, text generation, sentiment analysis, and more
- Self-attention calculates **attention scores** between different sentence parts, enabling selective focus on the most relevant dependencies

# Attention Vs. Self-Attention

- **Self-attention**, on the other hand, refers to the ability of a transformer model to attend to different parts of the **input** sequence when making predictions
    - Self-attention is the method the Transformer uses to bake the “understanding” of other relevant words into the one we’re currently processing
- **Attention** refers to the ability of a transformer model to attend to different parts of **another sequence** when making predictions. This is often used in encoder-decoder architectures
- [Good Resource](https://medium.com/mlearning-ai/whats-the-difference-between-self-attention-and-attention-in-transformer-architecture-3780404382f3)
- The difference between attention and self-attention is that self-attention operates between representations of the same nature: e.g., all encoder states in some layer
    - Decoder-Encoder Attention is looking
        - **from:** one current decoder state
        - **at:** all encoder states
    - Self-Attention is looking
        - **from:** each state from a set of states
        - **at:** all other states in the same set

# How it works?

- Self-attention is the part of the model where tokens interact with each other
    - Each token "looks" at other tokens in the sentence with an attention mechanism, gathers context, and updates the previous representation of "self"
    
    [https://lena-voita.github.io/resources/lectures/seq2seq/transformer/encoder_self_attention.mp4](https://lena-voita.github.io/resources/lectures/seq2seq/transformer/encoder_self_attention.mp4)
    

# Example Walkthrough

[Self-Attention Example](Attention%20&%20Self-Attention%20b24598421f774178adeaebb3e2c26214/Self-Attention%20Example%20f53a531cbfe2438e9fddf1ec8284cf1a.md)

# Query, Key and Value Vectors in Self-Attention

- A normal hash table matches a query (**Q**) to a key (**K**) and retrieves the associated values (**V**)
    - Instead, we have a ***soft (approximate or fuzzy match)*** hash table in which we try to find the best match between a query and a key that gives us the best value
    - First we apply affine transformations to Q, K and V
        - ***Learning happens here -*** How can Q, K and V be transformed to make the retrieval work best (result in the best hidden state to inform the decoder)
- Formally, this intuition is implemented with a **query-key-value** attention. Each input token in self-attention receives three representations corresponding to the roles it can play:
    - **Query** - asking for information
        - The query is used when a token looks at others - it's seeking the information to understand itself better
    - **Key** - saying that it has some information
        - The key is responding to a query's request: it is used to compute attention weights
    - **Value** - giving the information
        - The value is used to compute attention output: it gives information to the tokens which "say" they need it (i.e. assigned large weights to this token)
    - [Good Explanation](https://stats.stackexchange.com/questions/421935/what-exactly-are-keys-queries-and-values-in-attention-mechanisms) on Querie, Key, and Value vectors
    
    ![Untitled](Attention%20&%20Self-Attention%20b24598421f774178adeaebb3e2c26214/Untitled.png)
    

# Self-Attention Output Formula

![Untitled](Attention%20&%20Self-Attention%20b24598421f774178adeaebb3e2c26214/Untitled%201.png)

# Self-Attention Mechanism

Here's a simple explanation of how self-attention works in NLP transformer models:

1. **Query, Key, and Value**: The **first step** in calculating self-attention is to create three vectors from each of the encoder’s input vectors (in this case, the embedding of each word)
    1. So for each word, we create a **Query vector, a Key vector, and a Value vector**
        1. These vectors are created by multiplying the embedding by three matrices that we trained during the training process (learnable weights)
        2. They are mimicking the retrieval process of the dataset by sending a query for a specific word and returning keys of all words (including itself) to retrieve their values
    - **Query Vector**: This vector is used to compare the similarity of the word with other words in the sequence
        - A vector of a specific word $i$ to calculate the attention score
    - **Key Vector:** This vector is used to represent the other words in the sequence and is compared with the query vector to compute attention scores
        - A vector of each word $j$ in the whole text to attend the dot product with the word $i$’s q for calculating their attention score and identify the most relevant word
    - **Value Vector:** This vector holds the information that the model will use to create the final output
        - A vector that represents the meaning of a word $j$ in another sense, but having a dimension that differs from the word embedding
2. **Attention Scores**: To calculate the attention scores, the model measures the similarity between the query vector and all the key vectors using a mathematical operation called the dot product. The dot product measures how much the query and key vectors align or correlate
3. **Softmax and Weights**: The attention scores are then passed through a softmax function, which converts them into weights. Softmax ensures that the weights sum up to 1, making it a distribution of importance across all words in the sequence.
4. **Weighted Sum**: The final step is to take a weighted sum of the value vectors using the computed attention weights. This weighted sum is the representation of the current word, taking into account the importance of all other words in the sentence with respect to it.
5. **Multiple Attention Heads**: In most transformer models, self-attention is performed with multiple sets of query, key, and value vectors, called attention heads. Each attention head learns to focus on different aspects of the relationships between words, and their results are combined to form a more robust representation

![Untitled](Attention%20&%20Self-Attention%20b24598421f774178adeaebb3e2c26214/Untitled%202.png)

# Masked Self-Attention: “Don’t Look Ahead” for the Decoder

- In the decoder, there's also a self-attention mechanism: it is the one performing the "look at the previous tokens" function
- In the decoder, self-attention is a bit different from the one in the encoder. While the encoder receives all tokens at once and the tokens can look at all tokens in the input sentence, in the decoder, we generate one token at a time
    - During generation, we don't know which tokens we'll generate in future
    - To forbid the decoder to look ahead, the model uses masked self-attention: future tokens are masked out. Look at the illustration
        
        [https://lena-voita.github.io/resources/lectures/seq2seq/transformer/masked_self_attn.mp4](https://lena-voita.github.io/resources/lectures/seq2seq/transformer/masked_self_attn.mp4)
        
- **But how can the Decoder look ahead?**
    - During generation, it can't - we don't know what comes next. But in training, we use reference translations (which we know)
    - Therefore, in training, we feed the whole target sentence to the decoder - without masks, the tokens would "see future", and this is not what we want
    - 

# Multi-Head Attention: **Independently Focus on Different Things**

- Usually, understanding the role of a word in a sentence requires understanding how it is related to different parts of the sentence
    - This is important not only in processing source sentence but also in generating target
- [Illustration here](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html#multi_head_attention)
- Formally, this is implemented as several attention mechanisms whose results are combined:

$$
\begin{align}
\text{MultiHead}(Q,K,V) &= \text{Concat}(\text{head}_1, ...\text{head}_n)W_0
\\
\\
\text{head}_i &= \text{Attention}(QW_Q^i, KW_K^i, VW_V^i)
\end{align}
$$

## Implementation Details

- Fold the K, Q and V tensors (reshape) so that the extra dimension is the number of heads
- Each $\dfrac{\text{embedding length}}{\text{number of heads}}$ elements of each embedding is dedicated to a different head
- Once folded, softmax will treat each new dimension as independent (will only softmax over $\dfrac{\text{embedding length}}{\text{number of heads}}$ elements)
- Each token position can select $***h$*** different token positions
- Each $h^{th}$ of each token embedding is a separate embed
- When unfolded, each row is now a combination of several other token embeddings
- ***Important because each token may be informed by the presence of several tokens instead of just one other token***

# Attention is All you Need Paper

- [https://arxiv.org/pdf/1706.03762.pdf](https://arxiv.org/pdf/1706.03762.pdf)

# Resources

- [https://medium.com/@yulemoon/detailed-explanations-of-transformer-step-by-step-dc32d90b3a98](https://medium.com/@yulemoon/detailed-explanations-of-transformer-step-by-step-dc32d90b3a98)
- [https://jalammar.github.io/illustrated-transformer/](https://jalammar.github.io/illustrated-transformer/)
- [https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html#main_content](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html#main_content)
- [https://theaisummer.com/transformer/](https://theaisummer.com/transformer/)
- [https://theaisummer.com/self-attention/](https://theaisummer.com/self-attention/)

### Attention

- [https://theaisummer.com/attention/](https://theaisummer.com/attention/)
- [https://jaketae.github.io/study/seq2seq-attention/](https://jaketae.github.io/study/seq2seq-attention/)
- [https://bastings.github.io/annotated_encoder_decoder/](https://bastings.github.io/annotated_encoder_decoder/)

### Slides

- [https://courses.cs.washington.edu/courses/cse543/22sp/schedule/lecture15_transformer.pdf](https://courses.cs.washington.edu/courses/cse543/22sp/schedule/lecture15_transformer.pdf)

### Blogs

- [https://medium.com/nerd-for-tech/gpt3-and-chat-gpt-detailed-architecture-study-deep-nlp-horse-db3af9de8a5d](https://medium.com/nerd-for-tech/gpt3-and-chat-gpt-detailed-architecture-study-deep-nlp-horse-db3af9de8a5d)
- 

### Key, Query & Value Vectors

- [D2L](https://d2l.ai/chapter_attention-mechanisms-and-transformers/queries-keys-values.html)
- [https://stats.stackexchange.com/questions/421935/what-exactly-are-keys-queries-and-values-in-attention-mechanisms](https://stats.stackexchange.com/questions/421935/what-exactly-are-keys-queries-and-values-in-attention-mechanisms)