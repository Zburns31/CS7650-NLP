# Understanding Normalized Discounted Cumulative Gain (NDCG)

---

# What is it?

- **Normalized Discounted Cumulative Gain (NDCG)** is a commonly used metric in information retrieval (IR) and recommendation systems
    - It evaluates the quality of ranking models by assessing the effectiveness of an ordered list of results or predictions
- NDCG helps us evaluate how well a ranking model performs in terms of sorting items based on their relevance
    - [It’s a crucial metric for improving search engines and recommendation algorithms](https://en.wikipedia.org/wiki/Discounted_cumulative_gain)

# High-Level Summary

- Considers non-binary relevance ratings, {0,1,2,…}
- Highly relevant documents more useful than moderately relevant
- Lower ranked documents are less useful to the user
- Useful for queries with varying numbers of results

# How does it work?

**Discounted Cumulative Gain (DCG)**:

- DCG measures the usefulness or gain of a document based on its position in the result list
- It uses a graded relevance scale for documents (e.g., highly relevant, marginally relevant, non-relevant)
- The gain is accumulated from the top of the result list to the bottom
- However, the gain of each result is **discounted** at lower ranks
- The usual formula for DCG at a particular rank position is:

$$
\text{DCG} = \text{relevance}(1) + \sum_{i=2}^{n} \frac{\text{relevance}(i)}{\log(i)}
$$

- $n$ is the total number of results
- $\text{relevance}(i)$ represents the graded relevance of the result at position $i$

**Normalized DCG (NDCG)**:

- Different queries may have varying numbers of relevant results
- NDCG corrects for this by normalizing the DCG value
- It ensures that the metric is comparable across different queries
- The normalized version is often preferred over raw DCG
- The formula for NDCG is:

$$

\text{NDCG} = \frac{\text{DCG}}{\text{IDCG}}

$$

- Where:
    - $\text{IDCG}$ is the Ideal DCG, which represents the maximum achievable DCG for a given query

## **Assumptions**:

- Highly relevant documents are more useful when appearing earlier in the result list (higher ranks).
- Highly relevant documents are more useful than marginally relevant ones, which are in turn more useful than non-relevant documents

## **Interpretation**:

- NDCG values range from 0 to 1
- A higher NDCG indicates better ranking quality
- It considers both relevance and position in the list

# Resources

- [https://www.aporia.com/learn/a-practical-guide-to-normalized-discounted-cumulative-gain-ndcg/](https://www.aporia.com/learn/a-practical-guide-to-normalized-discounted-cumulative-gain-ndcg/)
- [https://www.evidentlyai.com/ranking-metrics/ndcg-metric](https://www.evidentlyai.com/ranking-metrics/ndcg-metric)
- [https://medium.com/data-science-at-microsoft/search-and-ranking-for-information-retrieval-ir-5f9ca52dd056](https://medium.com/data-science-at-microsoft/search-and-ranking-for-information-retrieval-ir-5f9ca52dd056)
- [https://kyle-dufrane.medium.com/normalized-discounted-cumulative-gain-what-it-does-and-how-it-works-b45c0f6624ec](https://kyle-dufrane.medium.com/normalized-discounted-cumulative-gain-what-it-does-and-how-it-works-b45c0f6624ec)