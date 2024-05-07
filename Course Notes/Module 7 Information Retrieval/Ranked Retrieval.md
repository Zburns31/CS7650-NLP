# Ranked Retrieval

---

# What is it?

- In a ranked retrieval approach, the system responds to a search query by ranking all documents in the corpus based on its estimate of their relevance to the query
- **Goal:** Return a ranked list of results, sorted according to relevance

# Why Ranked Retrieval?

- Boolean search often results in a feast (too many results) or famine (too few results)
- Good for experts where you know exactly how to formulate query to get manageable results
- Good for machines
    - Sift through 1000’s of results
- Manageable ***top-k*** list of results
- Uses free-text query vs. Boolean operators

# High-Level Overview

- Assign a ***relevance score*** to each (query, document pair)
- 

# How does it work?

- **Problem Statement**:
    - Given a **query** (a user’s search input) and a collection of **documents** (such as web pages, articles, or other textual content), the goal is to **rank** or **sort** the documents based on their relevance to the query
    - The objective is to ensure that the most relevant results appear early in the result list displayed to the user.
- **Scoring Documents**:
    - In ranked retrieval, each document is assigned a **score** based on its relevance to the query
    - The scoring process involves various techniques, such as term frequency-inverse document frequency (TF IDF), vector space models, and probabilistic models
    - These methods consider factors like the presence of query terms, their frequency, and the overall structure of the document
- **Ranking Algorithms**:
    - Search engines use different ranking algorithms to determine the order of documents in search results
    - Some common ranking models include:
        - **Boolean Models (BIR)**: Simple baseline models where documents either fully match the query (1) or don’t match at all (0). No ranking is involved
        - **Vector Space Models**: These models address partial matches by assigning weights to terms and representing documents and queries as vectors in a high-dimensional space. Cosine similarity is often used to measure relevance
        - **Probabilistic Models**: These models estimate the probability that a document is relevant given the query
            - Examples include the Okapi BM25 model
- **Evaluation**:
    - Ranking functions are evaluated using metrics like **precision**, which measures the proportion of relevant documents among the top-k results
    - Precision at different recall levels (e.g., precision@10) is commonly used to assess the quality of ranked retrieval

# Resources

- [https://web.stanford.edu/class/cs276/19handouts/lecture6-tfidf-6per.pdf](https://web.stanford.edu/class/cs276/19handouts/lecture6-tfidf-6per.pdf)