# Bidirectional Encoder Representations from Transformers (BERT)

---

# What is it?

- BERT, which stands for Bidirectional Encoder Representations from Transformers, is based on transformers, a [deep learning](https://www.techtarget.com/searchenterpriseai/definition/deep-learning-deep-neural-network) model in which every output element is connected to every input element, and the weightings between them are dynamically calculated based upon their connection
- It’s designed to pre-train deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers
- The purpose of BERT is to generate a language model that can understand the context of words in a sentence, not just the words in isolation
    - This is achieved by considering the words to the left and right of each word in the sentence, hence the term “bidirectional”
    - Addresses the need for ***contextual embeddings***

# How is it different?

- Historically, language models could only read input text sequentially -- either left-to-right or right-to-left -- but couldn't do both at the same time
    - BERT is different because it's designed to read in both directions at once
    - The introduction of transformer models enabled this capability, which is known as bidirectionality
    - ***Using bidirectionality, BERT is pretrained on two different but related NLP tasks: masked language modeling ([MLM](https://www.techtarget.com/searchenterpriseai/definition/masked-language-models-MLMs)) and next sentence prediction (NSP)***

# Use Cases

BERT can be used on a wide variety of language tasks:

- Can determine how positive or negative a movie’s reviews are [(Sentiment Analysis)](https://huggingface.co/blog/sentiment-analysis-python)
- Helps chatbots answer your questions. [(Question answering)](https://huggingface.co/tasks/question-answering)
- Predicts your text when writing an email (Gmail) [(Text prediction)](https://huggingface.co/tasks/fill-mask)
- Can write an article about any topic with just a few sentence inputs [(Text generation)](https://huggingface.co/tasks/text-generation)
- Can quickly summarize long legal contracts [(Summarization)](https://huggingface.co/tasks/summarization)
- Can differentiate words that have multiple meanings (like ‘bank’) based on the surrounding text. (Polysemy resolution)

***Generally, BERT is not suitable for text generation because it is bidirectional - it can look at future tokens***

# How does it work?

- **Masked Language Modelling:** MLM enables/enforces bidirectional learning from text by masking (hiding) a word in a sentence and forcing BERT to bidirectionally use the words on either side of the covered word to predict the masked word
- **NSP (Next Sentence Prediction)** is used to help BERT learn about relationships between sentences by predicting if a given sentence follows the previous sentence or not
    - **Next Sentence Prediction Example:**
        1. Paul went shopping. He bought a new shirt. (correct sentence pair)
        2. Ramona made coffee. Vanilla ice cream cones for sale. (incorrect sentence pair)
    - In training, 50% correct sentence pairs are mixed in with 50% random sentence pairs to help BERT increase next sentence prediction accuracy
- BERT uses self-attention, which means that the model can look at the words around the token (forward and backward) during inference time and factor those into the hidden state for the token
- BERT is trained by randomly masking the same word in the input and output and measuring the reconstruction loss (whether it can predict the true word)
- Attention means every token encoding is a mixture of the original token encoding (via residual) plus some portion of the other tokens that are being attended to

# High-Level Overview: Stages

1. **Input**: BERT takes as input a sequence of tokens, which are first embedded into vectors and then processed in the neural network
    1. The input also includes additional positional encoding to retain the order of words
2. **Tokenization**: ***BERT uses WordPiece tokenization***
    1. This method breaks words into subwords, which helps the model handle a wide range of words, including out-of-vocabulary words
3. **Embedding**: The tokenized words are then passed through an embedding layer to convert them into vector representations
    1. BERT combines token embeddings, segmentation embeddings (to distinguish different sentences), and positional embeddings
4. **Transformer Encoder Blocks**: The embedded vectors are then passed through a series of Transformer Encoder blocks
    1. Each block consists of a Multi-Head Attention mechanism and a Feed-Forward Neural Network with residual connections and Layer Normalization
5. **Bidirectional Context**: Unlike some other models that read the text input sequentially (left-to-right or right-to-left), BERT goes through the entire sequence of words at once, hence it is considered bidirectional
    1. This allows the model to learn the context of a word based on all of its surroundings (left and right of the word)
6. **Output**: The output of BERT can be used for a wide range of tasks
    1. BERT is a pre-training model: it is trained on a large corpus of text and then fine-tuned for specific tasks
    2. The fine-tuning step involves adding an additional layer based on the task (like classification, entity recognition, question answering, etc.), and training this layer on the specific task while slightly adjusting the pre-trained BERT parameters

# Resources

- [https://huggingface.co/blog/bert-101#1-what-is-bert-used-for](https://huggingface.co/blog/bert-101#1-what-is-bert-used-for)
- [https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270)