# Point Generator Networks

# What is it?

- A sort of sequence-to-sequence model called a pointer generator network creates summaries by using an attention mechanism
- **Pointer-Generator Networks** are a fascinating type of sequence-to-sequence model used for **text summarization**
    - [Unlike conventional abstractive summarization models, which generate summaries from scratch, pointer-generator networks have a unique ability: they can “point” to specific words from the input text when creating a summary](https://arxiv.org/abs/1704.04368)


# How do they work?

- A system of encoders and decoders is often the foundation of a pointer-generation network
    - The input text is processed by the encoder, which extracts its semantic meaning, and the decoder produces the summary step by step
    - The attention mechanism is the essential component that enables the model to concentrate on pertinent passages of the source text while producing the summary
- **Hybrid Architecture**: Pointer-generator networks combine elements of both extractive and abstractive summarization
    - They augment the standard sequence-to-sequence attentional model in two key ways:
        - **Copying Mechanism**: The network can **copy words directly from the source text** by “pointing” to them. This feature aids in **accurate reproduction of information** from the original text
            - **Word Generation**: Simultaneously, the network retains the ability to **generate novel words** using its internal language model (the “generator”)
        - **Coverage Mechanism**: To address the issue of repetition, pointer-generator networks use a concept called **“coverage”**
            - Coverage helps keep track of what has already been summarized, discouraging redundant phrases


![Untitled](./Point%20Generator%20Networks/Untitled.png)

# Resources

- [Research Paper](https://nlp.stanford.edu/pubs/see2017get.pdf)
- [https://medium.com/@isisjzua/get-to-the-point-summarization-with-pointer-generator-networks-132d1d5ad332](https://medium.com/@isisjzua/get-to-the-point-summarization-with-pointer-generator-networks-132d1d5ad332)