# Cosine Similarity

---

# What is it?

- Cosine similarity is a mathematical metric used to measure the similarity between two vectors in a multi-dimensional space, particularly in high-dimensional spaces, by calculating the cosine of the angle between them
    - Cosine similarity is a mathematical way to measure how similar two sets of information are
    - In the simplest terms, it helps us understand the relationship between two elements by looking at the "direction" they are pointing in, rather than just comparing them based on their individual values

# How does it work?

- Cosine Similarity is a value that is bound by a constrained range of 0 and 1
- The similarity measurement measures the cosine of the angle between the two non-zero vectors A and B

    $$
    \text{similarity} = \cos(a) \dfrac{A \cdot B}{||A||\space ||B||} = \dfrac{\sum_{i=1}^n A_iB_i}{\sqrt{\sum_{i=1}^n A_i^2}\sqrt{\sum_{i=1}^n B_i^2}}
    $$

    - Where:
        - $||A|| = \sqrt{A_1^2 + A_2^2,...A_n^2}$
            - This represents the L2 Norm (Vector)
        - $A \cdot B$ is the dot product

## Interpretation

- The similarity can take values between $-1$ and $+1$
    - Smaller angles between vectors produce larger cosine values, indicating greater cosine similarity. For example:
        - When two vectors have the same orientation, the angle between them is 0, and the cosine similarity is $1$
        - Perpendicular vectors have a 90-degree angle between them and a cosine similarity of $0$
        - Opposite vectors have an angle of 180 degrees between them and a cosine similarity of $-1$


![Untitled](./Cosine%20Similarity/Untitled.png)

# Retrieval

- Create a $1 \times |V|$ normalized document vector for the query $q$
- Create a normalized vector for every document and stack to create a $|D| \times |V|$ matrix $m$
- Matrix multiply to get scores
- This is the same as computing the cosine similarity
- Take the $\argmax$ to get the index of the document with the highest score (or get top-k to return more than one)

![Untitled](./Cosine%20Similarity/Untitled%201.png)

# Resources

- [https://www.datastax.com/guides/what-is-cosine-similarity](https://www.datastax.com/guides/what-is-cosine-similarity)
- [https://studymachinelearning.com/cosine-similarity-text-similarity-metric/](https://studymachinelearning.com/cosine-similarity-text-similarity-metric/)
- [https://www.learndatasci.com/glossary/cosine-similarity/](https://www.learndatasci.com/glossary/cosine-similarity/)
- [https://towardsdatascience.com/two-most-common-similarity-metrics-39c37f3fe14d](https://towardsdatascience.com/two-most-common-similarity-metrics-39c37f3fe14d)