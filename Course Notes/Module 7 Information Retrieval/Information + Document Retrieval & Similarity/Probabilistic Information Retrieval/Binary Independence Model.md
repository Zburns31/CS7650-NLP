# Binary Independence Model

---

# What is it?

# How does it work?

1. **Binary Independence Assumption**:
    - Documents are represented as **binary vectors**, where only the presence or absence of terms is recorded
    - Terms are **independently distributed** within the set of relevant documents and also independently distributed within the set of irrelevant documents
    - Each document or query is represented by a vector of Boolean elements, with each element corresponding to a specific term
    - The assumption of independence allows the representation to be treated as an instance of a **Vector Space Model**
2. **Probability Estimation**:
    - The probability that a document is relevant is derived from the probability of relevance for its terms vector
    - Using Bayes’ rule, we get:
    
    $$
    P(\text{relevant} | x) = \frac{P(x | \text{relevant}) \cdot P(\text{relevant})}{P(x)}
    $$
    
    - Here:
        - $x$ represents the document’s representation (binary vector).
        - $P(x | \text{relevant})$ and $P(x | \text{nonrelevant})$ are the probabilities of retrieving a relevant or nonrelevant document, respectively
        - The exact probabilities are estimated from statistics about the collection of documents
3. **Query Terms Weighting**:
    - Given a binary query, the goal is to assign weights to its terms to improve retrieval effectiveness
    - Yu and Salton, who introduced the BIM, propose that the weight of a term is an increasing function of its probability of relevance
    - By assigning appropriate weights to query terms, BIM yields better retrieval effectiveness than equal weighting
    

# Assumptions

- Term independence
- Terms not in query do not affect ranking
- Boolean document/query representation
- Documents are sets of terms, i.e., binary term weights in {0,1}
    - Boolean notion of relevance
- Relevance of each document is independent

# Base Match 25 Model (Variant of BIM)

---

- Generative Document Model
    - Words are drawn i.i.d from a multinomial distribution
    - Term frequency is approximately ***poission***
        - Model as mixture of two possions (elite vs. non-elite words)
    - Log odds ration approximated by $\frac{\text{tf}}{k + \text{tf}}$

# Resources

- [https://resources.mpi-inf.mpg.de/d5/teaching/ws13_14/irdm/slides/irdm-3-3.pdf](https://resources.mpi-inf.mpg.de/d5/teaching/ws13_14/irdm/slides/irdm-3-3.pdf)