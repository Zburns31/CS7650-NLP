# Classic Information Retrieval

---

# What is it?

- An Information Retrieval (IR) system is a software-based framework designed to retrieve relevant information efficiently and effectively from a collection of data or documents in response to user queries
- *The Information Retrieval system enables you to quickly find relevant information about*
    - *It goes beyond simple keyword matching by understanding the context of your query and ranking documents based on their relevance to your information needs*

# Key Takeaways

- **Efficient Data Retrieval:** Information Retrieval in NLP ensures rapid access to pertinent information from massive datasets, enhancing user experience
- **Relevance Matters:** The system’s objective is to retrieve the most relevant data to a user’s query, often considering factors beyond keyword matching.
- **Structured Data:** IR systems organize unstructured data into a structured format, allowing for efficient indexing and retrieval
- **Multistep Process:** The IR process involves data preprocessing, indexing, query processing, and relevance ranking

# **Key features of Information Retrieval System**

- **Indexing:** Creating an organized structure maps terms (words or phrases) to the documents in which they appear. This structure allows for efficient lookup and retrieval of documents based on specific terms
- **Query Processing:** The system analyzes and processes user queries to identify the most relevant terms and concepts
    - This often involves techniques to handle synonymy (different words with the same meaning) and polysemy (a word with multiple meanings)
- **Relevance Ranking:** Documents retrieved from the index are ranked based on their perceived relevance to the user’s query
    - Various ranking algorithms, such as TF-IDF (Term Frequency-Inverse Document Frequency) and BM25, are used to determine the order in which documents are presented to the user
- **User Interaction and Feedback:** Some IR systems learn from user interactions to improve their performance over time
    - For instance, if a user clicks on a certain search result, the system might learn that similar results are likely to be relevant
- **Information Presentation:** The retrieved documents are typically presented to the user with additional information, such as document snippets, titles, and links, to help users quickly assess the relevance of each result
- **Query Expansion:** This technique involves automatically enhancing user queries with additional terms related to the original query
    - This can help retrieve more relevant results by accounting for different ways of expressing the same idea
- **Evaluation Metrics:** IR systems are often evaluated using precision, recall, and F1-score metrics, which measure how accurately the system retrieves relevant documents and avoids irrelevant ones
- **Scalability:** Modern IR systems must be scalable to handle large datasets efficiently given the vast data available today

# How it works

- A model of information retrieval predicts and explains what a user will find in relevance to the given query. IR model is basically a pattern that defines the above-mentioned aspects of retrieval procedure and consists of the following:
    - model for documents
    - A model for queries
    - A matching function that compares queries to documents
- Mathematically, a retrieval model consists of:
    - $**D**$ − Representation for documents
    - $**R**$ − Representation for queries
    - $**F**$ − The modeling framework for D, Q along with relationship between them
    - $**R (q,d_i)**$ − A similarity function which orders the documents with respect to the query
        - It is also called ranking

# Architecture

![Untitled](./Classic%20Information%20Retrieval/Untitled.png)

# Design Features

## **Inverted Index**

- An inverted index is an **index data structure** storing a mapping from content (content can be words or numbers) to its locations in a document or a set of documents
    - We can also say the inverted index is a **hashmap-like data structure** that directs the user from a word to a document or a web page
        - The inverted index is also the **primary** data structure of most information retrieval systems
    - ***Inverted index as a data structure lists for every word, all documents that contain it, and frequency of the occurrences in the document hence making it easy to search for hits of a query word***
- Types of inverted indexes: ***Mainly two types record level inverted index, and word level (positional) inverted index***
    - Record level inverted index contains a list of references to **documents for each word (main definition above)**
    - Word level inverted index additionally contains the **positions of each word within a document**
        - This form of the inverted index also offers more functionality but needs more processing power and space to be created
- **Positional Index**
    - In a real-life IR system, we not only encounter single-word queries (such as “dog”, “computer”, or “alex”) but also **phrasal queries** (such as “winter is coming”, “new york”, or “where is kevin”). To handle such queries, using an inverted index is not sufficient

    ![Untitled](./Classic%20Information%20Retrieval/Untitled%201.png)

    - **How it works:**
        - Store the index of each position a term appears in a document
        - Can use a two-stage merge algorithm to support phrase queries
        - Can also support proximity searches
    - **Properties**
        - Can be combined with bi-gram index
        - 2-4X larger than regular term-index (roughly 50% of original text size)
            - Frequent terms are especially expensive
            - Can use compression to reduce size

## **Stop Word Elimination**

- Stop words are high-frequency words that are **deemed unlikely to be useful** for searching inside the documents of the information retrieval system
- All the words in the corpus with **less semantic weights** are kept in a list called a stop list
- Example: Articles like a, an, the, and prepositions like in, of, for, at, etc. are examples of stop words
- **Size reduction of the inverted index using stop list**: One main pro of eliminating stop words is that the size of the inverted index can be significantly reduced by a stop list
    - As per Zipf’s law, a stop list covering a few dozen words reduces the size of the inverted index by **almost half**
    - One disadvantage of stop word elimination is that sometimes it may **cause the elimination of the term that is useful** for searching

## **Stemming (Normalization)**

- Stemming is the heuristic process of **extracting the base form of words** by chopping off the ends of words
    - It is the process of producing **morphological variants** of a root or base word
    - Stemming programs are commonly referred to as stemming algorithms or stemmers
    - Stemming is one of the important steps in information retrieval systems like search engines

# Metrics

## Precision

- Precision is the ratio of the number of relevant documents retrieved to the total number retrieved
    - Precision provides an indication of the **quality of the answer set**
    - ***Precision does not consider the total number of relevant documents***
        - A system might have good precision by retrieving ten documents and finding that nine are relevant (a 0.9 precision), but the total number of relevant documents also matters
    - Example: If there were only nine relevant documents, the system would be a huge success
        - However, if millions of documents were relevant and desired, this would not be a good result set

## Recall

- Recall considers the total number of relevant documents, it is the ratio of the number of relevant documents retrieved to the total number of documents in the collection that are **believed to be relevant**
- Computing the total number of relevant documents is non-trivial among the entire set of items

    ![Untitled](./Classic%20Information%20Retrieval/Untitled%202.png)


# Model Types

## Boolean Retrieval Model

- It is a simple retrieval model based on set theory and boolean algebra. Queries are designed as boolean expressions which have precise semantics. The retrieval strategy is based on binary decision criterion
    - The boolean model considers that index terms are present or absent in a document
- It is one of the application of the Term Document Incidence matrix where we can answer any query which is in the form of a ***Boolean expression*** of terms, that is, in which terms are combined with the operators ***and, or,*** and ***not***
- **Possible Improvements:**
    - Boolean Search with Inverted Index
        - ***Each document is a bag of words***
        - Process AND queries by merging lists
            - Linear in $L_1 + L_2$

# Key Concepts

- **Term Document Incidence Matrix:** The term-document incidence matrix is one of the basic techniques to represent text data where:
    - *We get the **unique words** across all the documents*
    - ***For each document, we add 1 if the term exists in the document otherwise fill 0 in the cell***
    - **Problem:** The term-document matrix can be too large even for moderate size collections
        - ***It is extremely sparse’***

# Resources

- [Intro to Information Retrieval](https://nlp.stanford.edu/IR-book/html/htmledition/irbook.html)
- [https://www.tutorialspoint.com/natural_language_processing/natural_language_processing_information_retrieval.htm](https://www.tutorialspoint.com/natural_language_processing/natural_language_processing_information_retrieval.htm)
- [https://www.scaler.com/topics/nlp/information-retrieval-nlp/](https://www.scaler.com/topics/nlp/information-retrieval-nlp/)
- [https://www.cl.cam.ac.uk/teaching/1516/InfoRtrv/lecture2-indexing.pdf](https://www.cl.cam.ac.uk/teaching/1516/InfoRtrv/lecture2-indexing.pdf)

### Model Types

**Boolean Retrieval Models**

- [https://www.geeksforgeeks.org/document-retrieval-using-boolean-model-and-vector-space-model/](https://www.geeksforgeeks.org/document-retrieval-using-boolean-model-and-vector-space-model/)