# BertSum

# What is it?

- Extractive summarization is basically a sentence classification task
    - Use Pre-Trained encoders such as BERT and RoBERTa
    - Inserting multiple [CLS] symbols to learn sentence representation
    - Train with binary classification loss
    - During inference, rank the sentences by their scores from highest to lowest and select the top-3 sentences as the summary
        - **Cons:** Sentences are scored independently

# How does it work?

- **Text Summarization**:
    - Text summarization aims to condense lengthy documents into shorter, more concise summaries
    - There are two main approaches:
        - **Extractive Summarization**: Selects sentences directly from the original text to form the summary
        - **Abstractive Summarization**: Generates new sentences that capture the essence of the content
- **BERT for Extractive Summarization (BERTSUM)**:
    - BERTSUM falls under the extractive category
    - It requires the model to “understand” the complete text, identify relevant keywords, and assemble them into coherent sentences
    - Unlike abstractive summarization, BERTSUM ensures no loss of information
- **Input Format**:
    - BERTSUM modifies the input format compared to the original BERT model
    - Each sentence begins with a `[CLS]` token to separate multiple sentences and collect features from the preceding sentence
    - Segment embeddings are assigned to each sentence (even or odd) to distinguish them
    - For example, if the sequence is `[s1, s2, s3]`, the segment embeddings are `[Ea, Eb, Ea]`
- **Scoring Sentences**:
    - BERTSUM assigns scores to each sentence, representing its value in the overall document
    - Given sentences `[s1, s2, s3]`, their scores are `[score1, score2, score3]`
    - The sentences with the highest scores are collected and rearranged to form the summary
- **Coverage Mechanism**:
    - To avoid repetition, BERTSUM incorporates a **coverage mechanism**
    - This mechanism keeps track of what has already been summarized, discouraging redundant phrases

# Resources

- [https://blog.paperspace.com/extractive-text-summarization-with-bertsum/#extractive-summarization-with-bert](https://blog.paperspace.com/extractive-text-summarization-with-bertsum/#extractive-summarization-with-bert)