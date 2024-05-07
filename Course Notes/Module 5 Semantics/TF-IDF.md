# TF-IDF

# What is it?

- It measures how important a term is within a document relative to a collection of documents (i.e., relative to a corpus)
- Words within a text document are transformed into importance numbers by a text vectorization process
    - There are many different text vectorization scoring schemes, with TF-IDF being one of the most common
- TF-IDF can be broken down into two parts *TF (term frequency)* and *IDF (inverse document frequency)*
    - ***Term frequency*** works by looking at the frequency of a *particular term* you are concerned with relative to the document
        - There are multiple measures, or ways, of defining frequency
    - ***Inverse document frequency*** looks at how common (or uncommon) a word is amongst the corpus
        - IDF is calculated as follows where $***t***$ is the term (word) we are looking to measure the commonness of and $***N***$ is the number of documents ($d$) in the corpus ($D$)
            - The denominator is simply the number of documents in which the term, $***t***$, appears in

# How does it work?

- As its name implies, TF-IDF vectorizes/scores a word by multiplying the word’s Term Frequency (TF) with the Inverse Document Frequency (IDF)
- Inverse Document Frequency (IDF) in TF-IDF is designed to give higher weights to terms that are rare across the entire document corpus
    - The idea is that terms that occur frequently across all documents in the corpus are less discriminative and, therefore, less informative
    - These common terms may not contribute significantly to distinguishing one document from another
- By taking the logarithm of the ratio between the total number of documents in the corpus and the number of documents containing a specific term, IDF penalizes common terms with lower values and rewards rare terms with higher values
- The term "inverse" in IDF indicates that the weight assigned to a term is inversely proportional to its document frequency. Rare words that occur in fewer documents receive a higher IDF score, making them more important in the overall TF-IDF score

### **Term Frequency**

- TF of a term or word is the number of times the term appears in a document compared to the total number of words in the document:

    $$
    \text{TF} = \dfrac{\text{Number of times the term appears in the document}}{\text{total number of terms in the document}}
    $$

- Can also be specified as:

    $$
    TF(w,d) = \log(1 + \text{frequency}(w,d))
    $$

    - Where:
        - $w$ is a word
        - $d$ is the document
        - $\text{Frequency}$ is how often $w$ occurs in document $d$
    - We add a 1 for smoothing

### Inverse Document Frequency

- **Inverse Document Frequency**: IDF of a term reflects the proportion of documents in the corpus that contain the term
    - Words unique to a small percentage of documents (e.g., technical jargon terms) receive higher importance values than words common across all documents (e.g., a, the, and)
        - So words that are common across all documents are not very important

    $$
    \text{IDF} = \log \left ( \dfrac{\text{number of documents in the corpus}}{\text{number of documents in the corpus that contain the term}} \right )
    $$

    - Can also be written as:

        $$
        IDF(w,D) = \log \left(\dfrac{1 + |D|}{1 + \text{count}(w,D)} \right) + 1
        $$

    - Where:
        - $|D|$ represents the number of documents
        - $\text{count}(w,D)$ represents how many documents in D contain $w$
        - $+1$ is a smoothing constant

### TF-IDF

- The TF-IDF of a term is calculated by multiplying TF and IDF scores: $\text{TF-IDF} = \text{TF}*\text{IDF}$

## Interpretation

- Importance of a term is high when it occurs a lot in a given document and rarely in others
- In short, commonality within a document measured by TF is balanced by rarity between documents measured by IDF
    - The resulting TF-IDF score reflects the importance of a term for a document in the corpus

# Resources

- [https://www.learndatasci.com/glossary/tf-idf-term-frequency-inverse-document-frequency/](https://www.learndatasci.com/glossary/tf-idf-term-frequency-inverse-document-frequency/)
- [https://www.capitalone.com/tech/machine-learning/understanding-tf-idf/](https://www.capitalone.com/tech/machine-learning/understanding-tf-idf/)
- [https://kmwllc.com/index.php/2020/03/20/understanding-tf-idf-and-bm-25/](https://kmwllc.com/index.php/2020/03/20/understanding-tf-idf-and-bm-25/)