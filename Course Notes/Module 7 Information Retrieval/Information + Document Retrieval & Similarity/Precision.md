# Precision

---

# Overview

[Classification: Model Evaluation](https://www.notion.so/Classification-Model-Evaluation-b9c7710e94044a50a54e943fa8d8b30e?pvs=21)

[Classic Information Retrieval](Classic%20Information%20Retrieval%20ffdb9f410fe0452cb8c490bbf5c54910.md)

# What is it?

**Precision or Weighted Precision (for Multi-Class Classification): True Positive / (True Positive + False Positive)**

- Precision is the ratio of the **correctly** labeled positive instances by our model compared to all instances labeled the as positive. For example, how many predictions that were identified to be a “Call” were actually a call? So basically, the less false positives a classifier gives, the higher is its precision
- **Focus on this if the cost of FP's is high**
- Also known as Positive Predictive Value

# Extension to IR

- Given a set of results documents, $R = [{d_1, d_2, …,d_n}]$
- **Precision:** of documents in R, what fraction are relevant