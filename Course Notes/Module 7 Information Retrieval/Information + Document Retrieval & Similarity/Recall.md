# Recall

---

# Overview

[Classification: Model Evaluation](https://www.notion.so/Classification-Model-Evaluation-b9c7710e94044a50a54e943fa8d8b30e?pvs=21)

[Classic Information Retrieval](Classic%20Information%20Retrieval%20ffdb9f410fe0452cb8c490bbf5c54910.md)

# What is it?

**Recall (Sensitivity or TPR) or Weighted Recall (for Multi-Class Classification): True Positive / (True Positive + False Negative)**

- Recall summarizes how well the positive class was predicted. For example, of all the instances of a “Call”, how well did you predict those? Recall focuses on all relevant instances
- **Focus on this if the cost of FN's is high**

# Extension to IR

- Given a set of results documents, $R = [{d_1, d_2, …,d_n}]$
- **Recall:** of all documents which are relevant in the collection, what fraction appear in $R$?