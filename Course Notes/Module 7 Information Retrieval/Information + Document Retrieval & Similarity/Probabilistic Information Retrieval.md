# Probabilistic Information Retrieval

# What is it?

- **Probabilistic information retrieval** is an approach used in **information retrieval (IR)** to estimate the relevance of documents to a given query based on probability theory
- The **probabilistic retrieval** model is based on the Probability Ranking Principle, which states that an information retrieval system is supposed to rank the documents based on their probability of relevance to the query, given all the evidence available
    - The principle takes into account that there is uncertainty in the representation of the information need and the documents
    - There can be a variety of sources of evidence that are used by the probabilistic retrieval methods, and the most common one is the statistical distribution of the terms in both the relevant and non-relevant documents

# Assumptions

- **Ranking assumption**: usefulness of a relevant document depends on the number of relevant documents the user has already seen the more documents we see - the less useful they are
- I**ndependence assumption**: relevance of $*D_i$* to $*Q$* is independent to other documents $*D_j$* from the collection therefore we can apply it for each document separately

# Goal

- We need estimate the probability of relevance of a document $*D$* w.r.t a query $*Q*$
- Need to find:
    - $*P(R=r∣D,Q)*$ - probability that $*D$* is relevant to $*Q*$
    - $*P(R=¬r∣D,Q)*$ - probability that $*D$* is not relevant to $*Q$*
- ***So we need to estimate (learn) $P(R∣D,Q)$***
    - How do we model $P$?

## Relevance Function

- $*R={r,¬r}*$ a binary random variable that indicates relevance
- let $*r$* represent the event that $*D$* is relevant
- $¬r$ **represent the event that $*D$* is not relevant

# Models

## **Binary Independence Model**

[Binary Independence Model](./Probabilistic%20Information%20Retrieval/Binary%20Independence%20Model%20f3595d7e476c4ccb8cd79250c59d44ca.md)

# Important Questions

- Longer documents likely to have higher term frequency. Does this mean it is more relevant?
    - Larger documents have larger scope
    - May just be verbose and repetitive, in which case no
    - Normalize to some degree:

    $$
    B = (1-b) + b \dfrac{dl}{\text{avrg } dl}, 0 \leq b \leq 1
    $$


# Models

## BM25

- BM25 works by calculating a relevance score for each document in the collection concerning a specific query. The algorithm considers the frequency of query terms in the document, the length of the document, and the average document length in the entire collection. The formula involves tuning parameters $*k1*$ and $*b*$ to control the impact of term frequency and document length normalization
- The key components of the BM25 formula are:
    - **Term Frequency (TF)**: The frequency of a term in the document. The more times a term occurs in a document, the higher its TF value
    - **Inverse Document Frequency (IDF)**: The [inverse document frequency](https://www.luigisbox.com/search-glossary/inverse-document-frequency/) of a term, which measures the rareness of the term in the entire collection of documents. Rare terms receive higher IDF values, encouraging the algorithm to prioritize them
    - **Document Length (DL)**: The number of words in the document. Longer documents are penalized to avoid favoring lengthy documents over concise ones
    - **Average Document Length (AVDL)**: The average document length across the entire collection. It helps in normalizing the document length across the corpus

# Resources

- [ML Wiki](http://mlwiki.org/index.php/Probabilistic_Retrieval_Model)
- [Stanford NLP](https://nlp.stanford.edu/IR-book/pdf/11prob.pdf)
- [Probabilistic Retrieval Models](https://resources.mpi-inf.mpg.de/d5/teaching/ws13_14/irdm/slides/irdm-3-3.pdf)
- [Slides](https://www.uni-mannheim.de/media/Einrichtungen/dws/Files_People/Profs/goran/5-Probabilistic-Retrieval-FSS20.pdf)
- [https://aspoerri.comminfo.rutgers.edu/InfoCrystal/Ch_2.html](https://aspoerri.comminfo.rutgers.edu/InfoCrystal/Ch_2.html)

### Blogs & Tutorials

- [https://medium.com/analytics-vidhya/nlp-lecture-series-from-basic-to-advance-level-additional-content-1c1e51c9f936](https://medium.com/analytics-vidhya/nlp-lecture-series-from-basic-to-advance-level-additional-content-1c1e51c9f936)

### BM25

- [https://www.luigisbox.com/search-glossary/bm25/](https://www.luigisbox.com/search-glossary/bm25/)
- [https://www.elastic.co/blog/practical-bm25-part-2-the-bm25-algorithm-and-its-variables](https://www.elastic.co/blog/practical-bm25-part-2-the-bm25-algorithm-and-its-variables)
- [https://pub.aimind.so/understanding-the-bm25-ranking-algorithm-19f6d45c6ce](https://pub.aimind.so/understanding-the-bm25-ranking-algorithm-19f6d45c6ce)