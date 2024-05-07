# D Separation Example (1)

- The basic idea is that reasoning *flows along a path* from one variable to another. In the example of [figure 5.4](https://livebook.manning.com/book/practical-probabilistic-programming/chapter-5/ch05fig04), reasoning can flow from Size to Brightness along the path Size-Subject-Brightness
    - You saw a glimpse of this idea in [section 5.1.3](https://livebook.manning.com/book/practical-probabilistic-programming/chapter-5/ch05lev2sec3) on direct and indirect dependencies. **In an indirect dependency, reasoning flows from one variable to another variable via other intermediary variables**
    - In this example, Subject is the intermediary variable between Size and Brightness
        - In a Bayesian network, reasoning can flow along a path as long as the path isn’t *blocked* at some variable
        - In most cases, a path is blocked at a variable if the variable is observed. So if Subject is observed, the path Size-Subject-Brightness is blocked. This means that if you observe Size, it won’t change your beliefs about Brightness if Subject is also observed. Another way of saying this is that Size is conditionally independent of Brightness, given Subject
            
            ![Untitled](D%20Separation%20Example%20(1)%20279cea7b67b145afbcd29b645123aa66/Untitled.png)
            
        - 
        

## Bayes Network Quiz

- When we know C, the influence is cut off between A —> E
- **Given C, A and B become dependent due to the explaining away effect**
    - If we know C to be true, then knowledge of A will substantially effect what we believe about B
    
    ![Untitled](D%20Separation%20Example%20(1)%20279cea7b67b145afbcd29b645123aa66/Untitled%201.png)