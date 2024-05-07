# Self-Attention Example

---

# Self-Attention at a High-Level

- **Goal:** Translate the following the input sentence: ****`The animal didn't cross the street because it was too tired`
    - What does “it” in this sentence refer to? Is it referring to the street or to the animal? It’s a simple question to a human, but not as simple to an algorithm
    - When the model is processing the word “it”, self-attention allows it to associate “it” with “animal”
    - As the model processes each word (each position in the input sequence), self attention allows it to look at other positions in the input sequence for clues that can help lead to a better encoding for this word
    - Self-attention is the method the Transformer uses to bake the “understanding” of other relevant words into the one we’re currently processing
        
        ![Untitled](Self-Attention%20Example%20f53a531cbfe2438e9fddf1ec8284cf1a/Untitled.png)