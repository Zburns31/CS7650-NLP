# Decoder Block Internals

---

# Key Details

- The decoder block is similar to the encoder block, except it calculates the source-target attention
    - The source-target attention is another multi-head attention that calculates the attention values between the features (embeddings) from the input sentence and the features from the output (yet partial) sentence
- The decoder creates the query to be applied against the key and value from the encoder
    - Learn to select the most important hidden state from the input
    - Do this $n$ times
- Like Seq2Seq, the decoder will take the hidden state from the encoder
    - The Decoder takes the input $y$ tokens, as if deq2seq were teacher-forced
- The decoder output will be a log probability distribution over tokens
- **Masked multi-head attention** means the multi-head attention receives inputs with masks so that the attention mechanism does not use information from the hidden (masked) positions
    - The paper mentions that they used the mask inside the attention calculation by setting attention scores to negative infinity (or a very large negative number)
    - The softmax within the attention mechanisms effectively assigns zero probability to masked positions

# Architecture

![Untitled](Decoder%20Block%20Internals%200366097fbf9347d0a4e3c410c40ed004/Untitled.png)

# High Level Overview: Stages

- **Input**: The input to the Decoder block is the output from the final Encoder block and the target sequence offset by one position
    - The target sequence is offset because the model needs to predict the next word based on the previous words in the target sequence.
- **Masked Multi-Head Attention**: The first sub-layer in the Decoder block is a Masked Multi-Head Attention mechanism
    - The “mask” ensures that the predictions for each position can depend only on known outputs at positions less than the current one during training, preventing “future” information from being used
- **Add & Normalize (LayerNorm)**: The output of the Masked Multi-Head Attention sub-layer is then added to the original input (residual connection) and normalized using Layer Normalization
- **Multi-Head Attention**: The second sub-layer is a standard Multi-Head Attention mechanism, where the queries come from the previous sub-layer, and the keys and values come from the output of the Encoder stack
    - This allows the Decoder to focus on different parts of the input sequence for each word in the output sequence
- **Add & Normalize (LayerNorm)**: The output of the Multi-Head Attention sub-layer is then added to the output from the first sub-layer (residual connection) and normalized using Layer Normalization
- **Feed Forward**: The third sub-layer is a Pointwise Feedforward Neural Network, which is applied to each position separately and identically
- **Add & Normalize (LayerNorm)**: The output of the Feedforward network is added to the input of the Feedforward network (residual connection) and normalized using Layer Normalization
- **Output**: The output of the Decoder block is a sequence of vectors, where each vector corresponds to a word in the output sequence
    - This output can then be linearly transformed and softmaxed to produce a distribution over the vocabulary for each position (word prediction)

# How it Works

- The encoder start by processing the input sequence. The output of the top encoder is then transformed into a set of attention vectors $K$ and $V$
    - These are to be used by each decoder in its “encoder-decoder attention” layer which helps the decoder focus on appropriate places in the input sequence
        
        ![Untitled](Decoder%20Block%20Internals%200366097fbf9347d0a4e3c410c40ed004/Untitled%201.png)
        
- The following steps repeat the process until a special symbol is reached indicating the transformer decoder has completed its output
    - The output of each step is fed to the bottom decoder in the next time step, and the decoders bubble up their decoding results just like the encoders did
    - And just like we did with the encoder inputs, we embed and add positional encoding to those decoder inputs to indicate the position of each word
- The self attention layers in the decoder operate in a slightly different way than the one in the encoder:
    - In the decoder, the self-attention layer is only allowed to attend to earlier positions in the output sequence. This is done by masking future positions (setting them to `-inf`) before the softmax step in the self-attention calculation
    - The “Encoder-Decoder Attention” layer works just like multiheaded self-attention, except it creates its Queries matrix from the layer below it, and takes the Keys and Values matrix from the output of the encoder stack
- The decoder stack outputs a vector of floats. How do we turn that into a word? That’s the job of the final Linear layer which is followed by a Softmax Layer
    - The Linear layer is a simple fully connected neural network that projects the vector produced by the stack of decoders, into a much, much larger vector called a logits vector
        
        ![Untitled](Decoder%20Block%20Internals%200366097fbf9347d0a4e3c410c40ed004/Untitled%202.png)
        
    - 

# Resources

- [https://kikaben.com/transformers-encoder-decoder/](https://kikaben.com/transformers-encoder-decoder/)
- [https://bastings.github.io/annotated_encoder_decoder/](https://bastings.github.io/annotated_encoder_decoder/)