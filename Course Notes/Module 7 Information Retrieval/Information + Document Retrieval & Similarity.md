# Information + Document Retrieval & Similarity

---

# What is it?

**Document Retrieval:** Given a word or a phrase (itself a document), compare the query to all other documents and return the most similar

- Given two documents, represented as vectors, how do we know how similar they are?

# Information Retrieval Methods

- [Classic Information Retrieval](./Information%20+%20Document%20Retrieval%20&%20Similarity/Classic%20Information%20Retrieval.md)
- [Ranked Retrieval](./Information%20+%20Document%20Retrieval%20&%20Similarity/Ranked%20Retrieval.md)
- [Probabilistic Information Retrieval](./Information%20+%20Document%20Retrieval%20&%20Similarity/Probabilistic%20Information%20Retrieval.md)
- [Dense Passage Retrieval](./Information%20+%20Document%20Retrieval%20&%20Similarity/Dense%20Passage%20Retrieval.md)

# Neural Information Retrieval

- [Neural Information Retrieval](./Information%20+%20Document%20Retrieval%20&%20Similarity/Neural%20Information%20Retrieval.md)

# Use Cases

## Document Embedding

- Embed each word in a document
- Add each word vector
- Word vectors pointing in the same direction strengthen the semantic concept
- Normalize the resultant vector
    - Value of any of the $d$ dimension is the relative strength of that abstract semantic concept
    - Necessary for cosine similarity

# Metrics & Evaluation

- A benchmark dataset consists of the following
    - **A** **document collection** (e.g. Wikipedia articles, news articles, etc.)
    - **A set of queries**
        - Ideally samples from real-user queries
    - **Relevance Labels** for each (q,d) pair
        - Could be binary or more nuanced
        - Infeasible to label all $(q,d)$ pairs, even with crowd sourcing
            - Instead, fetch likely candidates, only label those
            - Needs a working IR system (model bias)
            - There will be false negatives

## Metrics

### Binary IR Metrics

- [Precision](./Information%20+%20Document%20Retrieval%20&%20Similarity/Precision.md)
- [Recall](./Information%20+%20Document%20Retrieval%20&%20Similarity/Recall.md)

### Ranking Metrics

- [Precision @ K (Pr@K)](./Information%20+%20Document%20Retrieval%20&%20Similarity/Precision%20@%20K%20(Pr@K).md)
- [Mean Average Precision (MAP)](./Information%20+%20Document%20Retrieval%20&%20Similarity/Mean%20Average%20Precision%20(MAP).md)
- [Mean Reciprocal Rank (MRR)](./Information%20+%20Document%20Retrieval%20&%20Similarity/Mean%20Reciprocal%20Rank%20(MRR).md)
- [**Understanding Normalized Discounted Cumulative Gain (NDCG)**](./Information%20+%20Document%20Retrieval%20&%20Similarity/Understanding%20Normalized%20Discounted%20Cumulative%20Gain.md)

## Online Metrics (AB Testing)

- Rely on user clicks
    - Cheap & plentiful
- Two ranking algorithms: $A,B$
    - Interleave results from A & B (pick first system randomly)
    - Remove duplicates
    - System with more clicks wins

# Measures of Similarity

- [TF-IDF](./Information%20+%20Document%20Retrieval%20&%20Similarity/TF-IDF.md)

- [Cosine Similarity](./Information%20+%20Document%20Retrieval%20&%20Similarity/Cosine%20Similarity.md)

# Key Concepts & Terms

- A hard negative **refers to relevant texts that have a high semantic similarity with the query but are false positives**
    - This has been shown to improve the bi-encoder's capacity in discriminating between relevant and relevant text
    - By including hard negatives, the retrieval model learns to distinguish between relevant and irrelevant documents more effectively


# Resources

### Metrics and Evaluation

- [https://amitness.com/2020/08/information-retrieval-evaluation/](https://amitness.com/2020/08/information-retrieval-evaluation/)
- [https://www.pinecone.io/learn/offline-evaluation/](https://www.pinecone.io/learn/offline-evaluation/)
- [https://www.aporia.com/learn/a-practical-guide-to-normalized-discounted-cumulative-gain-ndcg/](https://www.aporia.com/learn/a-practical-guide-to-normalized-discounted-cumulative-gain-ndcg/)