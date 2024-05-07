# Module 6: Modern Neural Architectures

---

# Transformers

- We are really combining three core concepts to work towards the transformers architecture:
    1. **Encoder/Decoder that operates on a large input window consisting of a sequence of tokens**
        1. Entire input and output sequence is provided at once (rather than one token or time slice at a time)
        2. Like Seq2Seq the decoder takes a hidden state and entire output sequence, which no longer needs to be generated token by token
    2. **Masking**
        1. Blacking out tokens so that the network has to guess the missing token
            1. Infilling: Guess a word in an arbitrary position in the middle of a sequence
            2. ContinuationL Guess the word at the end of the sequence (generation)
    3. **Self-Attention**
        1. Instead of collecting up hidden states from previous time steps, all time steps are flowing through the network in parallel
        2. Each time step can attend (softmax and dot product) to every other time slice
- Transformers are sometimes called ***masked language models***
- [Transformers Overview](/Course%20Notes/Module%202%20Foundations/Transformers.md)

# Fine-Tuning & Reinforcement Learning

- [Fine-Tuning, Instruction Tuning & RLHF](./Fine-Tuning,%20RLHF/Fine-Tuning,%20Instruction%20Tuning%20&%20RLHF.md)