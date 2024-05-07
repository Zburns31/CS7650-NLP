# Module 5: Semantics

# Document Semantics

- **Semantics:** What words and phrases mean
- **Problem:** Neural networks don’t know what words mean
    - By extension neural networks don’t know what a document is about
    - Words are just one-hot vectors
- ***How do we represent the meaning of a document?***
    - **Multi-Hot Vectors:** Set a 1 in each position for every word in a document
    - **Problem:** Places equal value on all words
    - If we want to figure out if two documents are related to each other you want to rely on words that are effective at distinguishing documents ****
    - Look for ways to determine which words are important in a document so we can compare documents

# TF-IDF

- Apply TF-IDF to every word $w$ in every document $d$ to get a vector
- [TF-IDF](./Module%205%20Semantics/TF-IDF.md)

# Document Retrieval & Similarity

- **Document Retrieval:** Given a word or a phrase (itself a document), compare the query to all other documents and return the most similar
- [Cosine Similarity](./Module%205%20Semantics/Cosine%20Similarity/Cosine%20Similarity.md)

# Word Embeddings

- [Embeddings](./Module%205%20Semantics/embeddings/Embeddings.md)
- [Word2Vec](./Module%205%20Semantics/word2vec/Word2Vec.md)

# Distributional Semantics

- Distributional Semantics: ***“A word is known by the company it keeps”***
    - Words that mean approximately the same thing tend to be surrounded by the same words