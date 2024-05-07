# Notation & Math

---

# Notation

The actual function to get one neuron’s activation in terms of the activations in the previous layer is a bit cumbersome to write down

![Untitled](Notation%20&%20Math%20e6fb9c8cc3c54647a6c15de601fc352d/Untitled.png)

- Where:
    - $w_{0,0}$ represents the weight of the first neuron in the first layer
    - $a_{0,0}$ represents the activation (affine transformation - i.e. Summation $Ax + B$ - result of the neuron) in the first neuron in the first layer
    - $b_0$ represents the bias for the

# Learning Process

**Activations (Product from each Neuron)**

- Tracking all these indices takes a lot of effort, so let me show the more notationally compact way that these connections are represented
    - Instead of computing a bunch of weighted sums like this one-by-one, we’ll use matrix multiplication to compute the activations of all the neurons in the next layer simultaneously
    - Organize all activations from a layer into a column as a vector
        
        [https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/activation-vector.mp4#t=0.001](https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/activation-vector.mp4#t=0.001)
        

**Weights**

- Next, organize all the weights as a matrix, where ***each row of this matrix corresponds to all the connections between neurons in the first layer and a particular neuron in the next layer***
    - Then the product Wa(0)Wa(0) is a column vector containing all the weighted sums for the neurons in the next layer
    
    [https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/weight-matrix.mp4#t=0.001](https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/weight-matrix.mp4#t=0.001)
    

**Compute Matrix-Vector Product**

- This is just a summation (or any other affine transformation) between all the weights and activations
    
    [https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/weighted-sum.mp4#t=0.001](https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/weighted-sum.mp4#t=0.001)
    

**Bias**

- Instead of talking about adding the bias to each one of these values independently, we represent it by organizing all those biases into a vector, and adding the entire vector to the previous matrix-vector product
    
    [https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/bias-vector.mp4#t=0.001](https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/bias-vector.mp4#t=0.001)
    
    **Activation Function**
    
    - Finally, I’ll wrap a sigmoid on the outside here, which is meant to represent applying the sigmoid function to each component of the result
    
    [https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/sigmoid.mp4#t=0.001](https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/sigmoid.mp4#t=0.001)
    
    **Compact Representation**
    
    - So, once you write this weight matrix and these vectors as their own symbols, you can communicate the full transition of activations from one layer to the next in a neat little expression
        - This tiny expression represents the computation of all the neurons in the next layer based on all the neurons in the previous layer, using the chosen weights and biases
    
    [https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/final-equation.mp4#t=0.001](https://3b1b-posts.us-east-1.linodeobjects.com/content/lessons/2017/neural-networks/matrix-math-videos/final-equation.mp4#t=0.001)