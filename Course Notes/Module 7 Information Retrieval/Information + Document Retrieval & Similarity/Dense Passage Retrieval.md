# Dense Passage Retrieval

---

# What is it?

# Significance of Dense Embeddings

- Dense embeddings play a pivotal role in information retrieval
    - Because it maps a given piece of text into a high dimensional space of real numbers, the advantage of this method is that it can consider semantic relationships and contextual information
    - These embeddings encode a rich representation of each passage, enabling more accurate matching and retrieval

# Architecture Overview

- DPR is a dual-encoder framework. Meaning there are two encoders present in this architecture
    - One encoder is used to encode a *question*, while the other encoder is used to encode the *passages* into **dense embeddings** as follows:

![Untitled](Dense%20Passage%20Retrieval%200815792a9e9241058e265af30a35ccfb/Untitled.png)

- The retriever ranks and selects the ***most promising candidate*** passages by calculating the ***similarity*** between the ***query*** and the ***passages***
    - This process significantly reduces the search space and improves efficiency

# How does it work?

![Untitled](Dense%20Passage%20Retrieval%200815792a9e9241058e265af30a35ccfb/Untitled%201.png)

# Resources

- [https://towardsdatascience.com/understanding-dense-passage-retrieval-dpr-system-bce5aee4fd40](https://towardsdatascience.com/understanding-dense-passage-retrieval-dpr-system-bce5aee4fd40)
- [https://sh-tsang.medium.com/brief-review-dpr-dense-passage-retrieval-for-open-domain-question-answering-9323cd8f85c4](https://sh-tsang.medium.com/brief-review-dpr-dense-passage-retrieval-for-open-domain-question-answering-9323cd8f85c4)