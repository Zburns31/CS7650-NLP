# Mean Average Precision (MAP)

---

# What is it?

- **Mean Average Precision (mAP)** is a widely used evaluation metric in information retrieval, search engines, recommendation systems, and object detection tasks.It assesses the quality of ranked retrieval or detection results by considering both the **precision** and **recall** of a system’s predictions

# **How It Works**

- Let’s break down the components of MAP:
    - **Average Precision (AP)**:
        - AP is calculated for each query or topic in the evaluation set
        - It combines precision and recall for ranked retrieval results
        - Specifically, AP is the **mean of precision scores** after each relevant document is retrieved
        - Higher AP values indicate better performance
    - **Mean Average Precision (MAP)**:
        - MAP takes the average of AP values across all queries or topics
        - It accounts for variations in performance across different information needs
        - The formula for mAP is as follows:
        
        where:
            - $n$ is the total number of queries or topics
            - $\text{AP}_i$ represents the average precision for query $i$
        
        $$
        \text{MAP} = \frac{1}{n} \sum_{i=1}^{n} \text{AP}_i
        $$
        
- **Interpretation**:
    - A higher MAP indicates that the system consistently retrieves relevant documents across various queries
    - It balances precision (accuracy of positive predictions) and recall (coverage of relevant documents)
- **Use Cases**:
    - In search engines, mAP helps evaluate the effectiveness of ranking algorithms
    - For recommendation systems, mAP assesses the quality of personalized recommendations
    - In object detection, mAP measures the accuracy of bounding box predictions

# Considerations

- If relevant document is not retrieved, precision is 0
- Assumes user is interested in multiple relevant documents
- Requires many relevance labels for each query

# Example

![Untitled](Mean%20Average%20Precision%20(MAP)%202250eb824c0a480281af8011d4ebb7aa/Untitled.png)

# Resources

- [https://www.v7labs.com/blog/mean-average-precision](https://www.v7labs.com/blog/mean-average-precision)
- [https://www.educative.io/answers/what-is-the-mean-average-precision-in-information-retrieval](https://www.educative.io/answers/what-is-the-mean-average-precision-in-information-retrieval)