# Embedding Based Retrieval (EBR)

---

# How does it work?

- **Embeddings**: In EBR, we use embeddings (dense vector representations) to encode the semantic meaning of text
    - These embeddings capture contextual information and relationships between words or sentences
    - ***Represent documents and queries as vectors***
        - High dimensional space (size of $|V|$ ~ millions)
        - Sparse
- **Nearest Neighbour Search**: EBR converts the retrieval problem into a **nearest neighbor search** problem in the embedding space
    - Given a query embedding and a set of document embeddings, the goal is to find the most similar documents to the query
        - Rank according to similarity

# Why?

- 1-hot vectors don’t capture word similarity
    - Similar words have similar embeddings
- Embeddings have useful structure
    - King - Man + Woman ~ Queen

# Naive Embedding Based IR Model

- Define query, document vectors as the mean of their word embeddings:
    
    $$
    \begin{align}
    Q &= \frac{1}{N_q} \sum_{i \in q} w_i
    \\
    \\
    D &= \frac{1}{N_d} \sum_{i \in d} w_i
    \end{align}
    $$
    
- Find the ***nearest*** document to query:

$$
f(d,q,w) = \text{cosine}(Q,D)
$$

- **Problem: $\text{min}_i cos(Q, D_i)$ -** Essentially KNN
- Pre-calculate and cache all document representations
- Still need N dot products, where $N$ is the number of documents
    
    $$
    C = O(N * \text{embedding dimension} * \text{arithmetic precision})
    $$
    
    - Infeasible beyond $10K+$ documents
- Embedding compression and quantization
    - Can lower embedding size, make each dot product much cheaper
    - But linear dependence on $N$ remains

# Fast Approximate Embedding Based Retrieval

- We can first cluster documents, then do 2-stage retrieval:
    1. First retrieve k closest clusters
    2. Do brute-force (dot-product) search over retrieved clusters
    3. Serve using Inverted File Index (IVF)
- With $C$ clusters, $N$ documents, run time is: $\sim O(C + kN/C)$ is clusters are balanced

# Dual Embedding Space Model (DESM)

- **Purpose:**
    - DESM aims to improve document ranking in information retrieval systems
    - It leverages word embeddings to enhance the understanding of query-document relationships
- **Word Embeddings**:
    - DESM uses **two sets of word embeddings**:
        - **Query Word Embeddings**: Represent the semantic meaning of query terms
        - **Document Word Embeddings**: Represent the semantic content of document terms
- **Vector Similarity**:
    - For each query term, DESM calculates the **cosine similarity** between the query word vector and all document word vectors
- **Dual Embeddings**:
    - DESM uses both **input matrix (IN)** and **output matrix (OUT)** embeddings from word2vec
        - IN-IN embeddings group similar words (typical relationships)
        - IN-OUT embeddings group co-occurring words (topical relationships)
- **Example**:
    - Suppose the query term is “Albuquerque”
    - Two passages:
        - (a) Contains “Albuquerque,” “population,” and “metropolitan”
        - (b) Contains only “Albuquerque”
    - DESM considers related terms, favoring passage (a) as being more about Albuquerque

# Resources