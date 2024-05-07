# Neural Information Retrieval

---

# What is it?

# ML for IR

---

## IR as Classification

- IR can be cast in the following form:
    - For each (q,d) pair, consider a function: $f(q,d) \rightarrow s, \text{where s is a relevance label}$
    - $s \in$ {0, 1}: Binary relevance (binary classification)
    - $s \in$ {0, 1, … $k$}: multi-relevance (multi-class classification)
    - $s \in$ {$R$}: relevance score (regression)
- Pick your classifier
    
    ![Untitled](Neural%20Information%20Retrieval%204ab8e4a8d66f425da6dbb887fe59cce5/Untitled.png)
    

## From Classification To Ranking

- Classification only defines an absolute notion of relevance
- Ranking: Consider not only whether document is “relevant”, but if it is more or less relevant than competing documents
- In practice, classification objective is good for discriminating random irrelevant documents, but not superficially relevant ones
    - Use pair-ranking objectives
    - “Hard Negatives”

# Re-Ranking Pipeline

- General ML formulation requires running inference for ***every (q,d) pair***
    - **Solution:** for each $**q$,** run fast (classical retrieval). Then run ML model on short-list of top-k candidates
    - Typically $10 < k \leq 10,000$
    - Can also have multiple re-rankers with increasing complexity

![Untitled](Neural%20Information%20Retrieval%204ab8e4a8d66f425da6dbb887fe59cce5/Untitled%201.png)

- There are four different families of Neural re-ranking models:
    - Representation-focused
    - Interaction-focused
    - All-to-all interaction(cross encoder)
    - Late interaction
- 

# Embeddings for IR

[Embedding Based Retrieval (EBR)](Neural%20Information%20Retrieval%204ab8e4a8d66f425da6dbb887fe59cce5/Embedding%20Based%20Retrieval%20(EBR)%20ad80e4e5c84b4aa89fa2626b2c2f5b21.md)

# Ranking Models

- RankNet
- LambdaRank

# Key Concepts

- **Vector Representations**: Neural IR models learn vector representations of text
- **Unsupervised Learning**: Some methods employ pre-trained neural vectors without end-to-end learning for the IR task
- **Learning to Rank (LTR)**: LTR frameworks use standard loss functions for ranking
- **Deep Neural Networks (DNNs)**: These architectures play a crucial role in neural IR
- **Supervised Learning**: Recent DNN architectures are trained end-to-end for ranking tasks

# Resources

- [https://www.microsoft.com/en-us/research/uploads/prod/2017/06/fntir2018-neuralir-mitra.pdf](https://www.microsoft.com/en-us/research/uploads/prod/2017/06/fntir2018-neuralir-mitra.pdf)

### Overview of Models

- [https://medium.com/@mhammadkhan/neural-re-ranking-models-c0a67278f626](https://medium.com/@mhammadkhan/neural-re-ranking-models-c0a67278f626)

### Re-ranking Models

- [https://medium.com/@mhammadkhan/neural-re-ranking-models-c0a67278f626](https://medium.com/@mhammadkhan/neural-re-ranking-models-c0a67278f626)