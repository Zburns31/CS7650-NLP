# Bilingual Evaluation Understudy (BLEU)

# What is it?

- **BLEU** (Bilingual Evaluation Understudy) is a quantitative metric for measuring the quality of an output text based on multiple reference text
    - ***Measures the precision with Brevity Penalty***
- There can be more than one correct/reference for one candidate in Sequence to Sequence tasks
    - Hence, it is important that the references are chosen carefully and all the possible references are included. BLEU score is a precision based measure and it ranges from **0 to 1**
        - The closer the value is to 1, the better the prediction. It is not possible to achieve a value of 1 and usually a value higher than 0.3 is considered a good score

# How does it work?

To calculate the BLEU score, we need to be familiar with [N-grams](https://www.baeldung.com/cs/n-gram), precision, and clipped precision

## Precision

- [Precision](https://www.baeldung.com/cs/precision-vs-average-precision) refers to the number of words in the output text that are also in the reference text:

$$
\dfrac{\text{Number of words in the output text that occurred in the reference text}}{\text{Total number of words in the output text}}
$$

- **Example:**
    - Output = *She drinks the milk*
    - Reference = *She drank the milk*
    - The words “She”, “the”, and “milk” in the output text occurred in the reference text. Therefore, the precision is
        - But, there are two downsides to the above precision measure. First, it doesn’t catch repetition. For example, if the output text was “milk milk milk”, the precision would be $100$%
        - Second, it doesn’t take multiple reference texts into account. To address these issues, we use clipped precision

## Clipped Precision

- **Modified (Clipped) Precision:** For calculating Modified Precision, the count of an n-gram is clipped based on the maximum number of times it appears in the references
    - It is denoted by the Max_Ref_Count in the formula shown below:

    $$
    \text{Count}_{clip} = \min (\text{Count, Max Reference Count})
    $$


- Example:
    - Output text: *She She She eats a sour cherry*
    - Reference text 1: *She is eating a blueberry as she loves it*
    - Reference text 2: *She eats a fruit of her favourite*
    - In this example, the words “She”, “eats”, and “a” in the output text occur in at least one reference text. However, the word “she” is repeated three times
        - **In clipped precision, we bound the word count in the output text from above to the maximum count of the corresponding word in any of the reference texts:**

            $$
            \text{Clipped Precision} = \dfrac{\text{Clipped number of words in the output text that occurred in the reference text}}{\text{Total number of words in the output text}}
            $$

        - In our example, the maximum count of “She” in the reference texts is 2 (in the reference text 1). Therefore, the clipped number of “She” becomes 2
            - If we had more than three occurrences of “She” in the reference text, the clipped number would be cut to 3
            - Similarly, the output words “eats” and “a” have only one occurrence in the reference texts
            - So, their clipped number is 1
        - Since there are 7 words in the output text, the clipped precision is: $\frac{2+1+1}{7} = \frac{4}{7}$

## Brevity Penalty

- We penalize short output text to avoid high scores when they don’t make sense
- For example, if we have an output text with just one word that also occurs in the reference text, we’ll end up with $BLEU_1 = 1$
- To solve this issue, we need a new factor to penalize short output texts. That’s what the brevity penalty does:

    $$
    \text{BLEU Penalty} = \begin{cases}
       1 &\text{if } c > r \\
       e^{(1-\frac{r}{c})} &\text{if } c \leq r
    \end{cases}
    $$

    - Where:
        - $r$ is the number of words in the output text
        - $c$ is the number of words in the reference text

## BLEU Score Calculation

- The BLEU score is always defined with a particular $N$ in mind. It uses $K$-grams with $K = 1,2,…N$, and we denote it as:

    $$
    BLEU_N = (\text{Brevity Penalty}) \times (\text{Weighted Geometric Precision Score)}
    $$

- **The geometric mean precision score is a weighted geometric mean of the clipped N-gram precisions for $n=1,2,…N$, and the brevity penalty favours longer output texts**
- The formula for the clipped precision of N-grams is:

    $$
    CP_N = \dfrac{\text{Clipped number of n-grams in the output text that occur in the reference text}}{\text{Total number of n-grams in the output text}}
    $$


![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ec4217f4fa5fcd92a9edceba0e708cf7_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-ec4217f4fa5fcd92a9edceba0e708cf7_l3.svg)

- So the weighted geometric mean is:

    $$
    \text{Weighted Geometric Mean Precision} = \prod_{n=1}^N CP_n^{w_n}
    $$

    - The $w_n$ values are weights we give to each clipped precision. Typically, we use uniform weights

# Resources

- [https://www.baeldung.com/cs/nlp-bleu-score](https://www.baeldung.com/cs/nlp-bleu-score)
- [https://medium.com/@priyankads/evaluation-metrics-in-natural-language-processing-bleu-dc3cfa8faaa5](https://medium.com/@priyankads/evaluation-metrics-in-natural-language-processing-bleu-dc3cfa8faaa5)
- [https://medium.com/nlplanet/two-minutes-nlp-learn-the-bleu-metric-by-examples-df015ca73a86](https://medium.com/nlplanet/two-minutes-nlp-learn-the-bleu-metric-by-examples-df015ca73a86)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e975e655b68d040659228a944ff4255e_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-e975e655b68d040659228a944ff4255e_l3.svg)

![https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-9898801e86babf8e42c6c17afcf061c5_l3.svg](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-9898801e86babf8e42c6c17afcf061c5_l3.svg)