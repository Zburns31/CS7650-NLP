# Mean Reciprocal Rank (MRR)

---

# What is it?

- The **Mean Reciprocal Rank (MRR)** is a statistic used to evaluate processes that generate a list of possible responses to a set of queries
    - It provides insight into how well a system ranks relevant results

# How it works

1. **Reciprocal Rank (RR)**:
    - For each query, consider the ranked list of responses
    - The reciprocal rank of a correct answer is the **inverse of its position** in the list
    - Specifically:
        - First correct answer: Reciprocal rank = 1
        - Second correct answer: Reciprocal rank = 1/2
        - Third correct answer: Reciprocal rank = 1/3
        - And so on…
    - If no correct answer is found, the reciprocal rank is 0
2. **Mean Reciprocal Rank (MRR)**:
    - Calculate the reciprocal rank for each query
    - Take the **average** of these reciprocal ranks across all queries
    - The MRR value ranges from 0 (no correct answers) to 1 (all answers correct)
    - It provides a single metric to assess the overall performance of a system

# Use Cases

- Useful when only one relevant document is enough
    - Navigational queries
    - Factual queries (question answering)

# **Example**

- Suppose we have a system that translates English words to their plurals. Here are three sample queries and their proposed results:
    1. Query: “cat”
        - Proposed results: “catten,” “cati,” “cats”
        - Correct response: “cats”
        - Reciprocal rank: 1/3
    2. Query: “torus”
        - Proposed results: “torii,” “tori,” “toruses”
        - Correct response: “tori”
        - Reciprocal rank: 1/2
    3. Query: “virus”
        - Proposed results: “viruses,” “virii,” “viri”
        - Correct response: “viruses”
        - Reciprocal rank: 1
        - The mean reciprocal rank is calculated as:
    
    $$
    \text{MRR} = \frac{1/3 + 1/2 + 1}{3} = \frac{11}{18} \approx 0.61
    
    $$
    
- Remember that only the rank of the **first relevant answer** is considered, ignoring any further relevant answers
    - [If you’re interested in additional relevant items, the **mean average precision** is an alternative metric to explore](https://en.wikipedia.org/wiki/Mean_Reciprocal_Rank)

# Resources

- [https://www.gabormelli.com/RKB/Mean_Reciprocal_Rank_(MRR)_Measure](https://www.gabormelli.com/RKB/Mean_Reciprocal_Rank_%28MRR%29_Measure)
- [https://medium.com/data-science-at-microsoft/search-and-ranking-for-information-retrieval-ir-5f9ca52dd056](https://medium.com/data-science-at-microsoft/search-and-ranking-for-information-retrieval-ir-5f9ca52dd056)