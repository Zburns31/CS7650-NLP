# Part of Speech Tagging & Parsing

---

# POS Tagging

- One basic way to categorize words is by their part of speech (POS), also called lexical category or tag: noun, verb, adjective, and so on
    - The task of assigning a part of speech to each word in a sentence is called part-of-speech tagging
- POS Tagging takes a tokenized sequence of words, and returns a list of annotated tokens, where each token has a word class label. This is often disambiguated by looking at the context surrounding the token

# POS Parsing

- Each *sentence* gets assigned a structure (often a tree) which reflects how its components are related to each other
- Parsing commonly results in a [parse tree](https://en.wikipedia.org/wiki/Parse_tree) for a sentence; often there can be many possible trees in case of ambiguous sentences

# Parts of Speech

- This is only a simplified list of parts of speech

![Untitled](Part%20of%20Speech%20Tagging%20&%20Parsing%20eae63e82bd1643758bc170630dce0506/Untitled.png)

# Computing Parts of Speech

- **Dynamic Programming:** Compute the Most Likely Explanation (MLE): what sequence of latent values would most likely emit the observed sequence of words?
- Do not want to have to compute the probability distribution for every possible sequence of tags
- Assume that choosing the most liekly tag for each time slice results in the most likely explanation of the entire sequence