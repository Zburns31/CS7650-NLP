# Precision @ K (Pr@K)

---

# What is it?

- Represents the fraction of relevant documents in the top-k retrieved results
- Not sensitive to ranking within top-k
- **Precision at K** is an evaluation metric commonly used in information retrieval and recommendation systems
    - It measures the quality of ranked results by assessing the proportion of relevant items among the top **K** items recommended or retrieved by a system.In other words, it quantifies how many relevant items are present among the top **K** results

# How does it work

- **Mathematical Formulation**:
    - The formula for **Precision at K** is as follows:
    
    $$
    \text{Precision@K} = \frac{\text{True Positives@K}}{\text{True Positives@K} + \text{False Positives@K}}
    $$
    
    - Let’s break down the components:
        - **True Positives@K**: The number of relevant items correctly identified among the top **K** retrieved items
        - **False Positives@K**: The number of irrelevant items incorrectly included among the top **K** retrieved items
- **Example**:
    - Suppose we have a recommendation system that suggests movies to users. We want to evaluate its performance.
    - Let’s consider the top 10 movie recommendations (K = 10)
    - Among these 10 recommendations:
        - 6 movies are relevant (i.e., the user would like them)
        - 4 movies are irrelevant (i.e., the user would not like them)
    - Calculating Precision@10:
    
    $$
    \text{Precision@10} = \frac{6}{6 + 4} = 0.6
    $$
    
    - This means that 60% of the top 10 recommended movies are relevant
- **Interpretation**:
    - A higher Precision@K indicates that the system is better at providing relevant items within the top **K** results
    - However, Precision@K does not consider the positions of relevant documents among the top **K**
        - It treats all relevant items equally
- **Use Cases**:
    - Precision@K is valuable for scenarios where we care about the quality of recommendations within a limited set (e.g., displaying the top search results, suggesting products to users)
    - It helps balance relevance and efficiency by focusing on a specific subset of retrieved items
    

# Resources

- [https://www.evidentlyai.com/ranking-metrics/precision-recall-at-k](https://www.evidentlyai.com/ranking-metrics/precision-recall-at-k)