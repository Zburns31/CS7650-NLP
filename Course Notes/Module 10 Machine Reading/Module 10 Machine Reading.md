# Module 10: Machine Reading

# What is it?

- Extracting factual knowledge from unstructured text and placing it into a structured knowledgebase

# Information Extraction

- **Closed Information Extraction:** A fixed set of types of relations
    - Example: established, is_a, has_satellite, provost, etc.
    - Hand-authored rules
        - Example: look for a sentence with the word established and a date
    - Problems:
        - New ways of expressing information
        - New relations can emerge
        - Too many relations to anticipate
- **Open Information Extraction:** Extract structured knowledge from unstructured text without knowing what the entities or relations are in advance
    - Unsupervised acquisition task

# Approaches

- **Supervised Learning:**
    - Train a binary classifier to predict whether a sentence had a relation
    - Retrieve sentences from a document and test for each type of relation
- **Multinomial Supervised Learning:**
    - Train a classifier to pick a label from a set of relations
    - Requires a fixed set of relations
- **Distant Supervision:**
    - Instead of manually labelling, automatically derive labels from an existing knowledge base
    - Assume every entity that is related to another entity in a sentence is a positive example
    - Assume every entity that is unrelated to another entity in a sentence is a negative example
    - But how do you know whether two entities are related?


# **Open Information Extraction**

- Requires learning a way to recognize relations without labelling
- Syntax of sentences provide strong clues about relations
- **Goal:** From unstructured text to $\langle \text{subject, relation, object} \rangle$ triplets

# Part of Speech Parsing

- [Part of Speech Tagging & Parsing](./POS%20Tagging/Part%20of%20Speech%20Tagging%20&%20Parsing.md)

# Dependency Parsing

- [Dependency Parsing](./Dependency%20Parsing.md)

# Frames & Events

- Fact-based knowledge acquisition can help answer “who”, “what”, “where”, “when”
- “Why” questions are much harder
- **Events** are (descriptions of) changes in the state of the world
    - Events are rich semantic constructs that bring with them knowledge that is not literally in the text
- a word’s meaning cannot be understood without access to essential knowledge that relates to the word
    - Example:
        - “Sell” implies a seller, a recipient, and exchange of possession of items
- **A frame** is a system of related concepts such that understanding one concept requires the understanding of all concepts and their relationships
    - If you can identify the frame and the frame elements, you can make inferences about the relationships between frame elements that you might not be able to do from just the surface form of text

# Resources

- [Dependency Parsing](https://web.stanford.edu/~jurafsky/slp3/old_oct19/15.pdf)