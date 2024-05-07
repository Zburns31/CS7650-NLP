# Probability

---

# Probability Notation

- The list of possible worlds are ***mutually exclusive and exhaustive***
- **Probability Model**: Associates a numerical probability $P(\omega)$ with each possible world
- **Events:** Probabilistic assertions and queries are not usually about particular possible worlds, but about sets of them
- **Unconditional (Prior) Probabilities:** Refers to the degree of belief in propositions in the absence of any other information
    - Most of the time, we have some information, usually called **evidence**, that has already been revealed
- **Conditional (Posterior) Probabilities:** A posterior probability, in Bayesian statistics, is the revised or updated probability of an event occurring after taking into consideration new information
    - In statistical terms, the posterior probability is the probability of event A occurring given that event B has occurred
- $\wedge$ and represents the conjunction or intersection of two sets
    - Event A happens and Event B happens
    - I.e. $P(a | b) = \dfrac {P(a \wedge b)} {P(b)}$
- $\vee$  represents the disjunction or union of two events
    - I.e. Either event A happens or event B happens
- $\Pi$ (capital pi) is a product operator
    - Analogous to the summation operator
- **Random Variables:** A random variable is a variable whose value is unknown or a function that assigns values to each of an experiment's outcomes
    - A random variable $Z$ can be divided into three classifications: 1) Discrete, 2) Continuous and 3) Mixed
        - If $Z$ is discrete, then its distribution is called a probability mass function which measures the probability that Z takes on the value k, denoted $P(Z=k)$
        - Note that the probability mass function completely describes the random variable $Z$
        - If $Z$ is continuous, then Z has a probability density function
            - ***It’s important to know that the value of the probability density function at a point does not equal the probability of that point***
- **Marginalization (Summing Out):** Marginalization is a method that requires summing over the possible values of one variable to determine the marginal contribution of another
- **Probability Density Function:** For continuous variables, it is not possible to write out the entire distribution as a vector, because there are infinitely many values
    - Instead, we can define the probability that a random variable takes on some value x as a parameterized function of x, usually called a probability density function
- **Joint Probability Distribution:** A joint probability distribution shows a [probability distribution](https://www.statisticshowto.com/probability-and-statistics/statistics-definitions/probability-distribution/) for two (or more) [random variables](https://www.statisticshowto.com/random-variable/)
    - Instead of events being labeled A and B, the norm is to use X and Y

# Conditional Probability

---

## Conditioning - The queen of spades

- Remember, by definition, independence means $P(AB) = P(A)P(B)$
    - Here we have a standard deck of 52 cards. There are 13 of each suit and 4 queens. Define Event A as drawing a spade and Event B as drawing a queen
    - $P(AB)$ is then the probability of drawing the queen of spades. This card is unique, so it occurs $\dfrac{1}{52}$ times
- If we multiply it out:
    - $P(A)P(B) = \frac{13}{52} \times \frac{4}{52} = \frac{1}{52}$
    - So $P(AB) = P(A)P(B)$ and the two events are independent
- ***But are they still independent if we first remove the two of diamonds from the deck? Let's see***
    - $P(AB) = \frac{1}{51}$
    - $P(AB) = P(A)P(B) = \frac{13}{51} \times \frac{4}{51} = \frac{52}{2601}$
    - $\frac{1}{51} \neq \frac{52}{2601}$
- **They are no longer independent!** It's easy to follow the math, but the intuition can take time to click. Think about it in terms of the information you have. If there are an equal number of cards left in the deck from each suit, any given suit has the same probability of being a queen
    - In the second case, if you draw a spade, heart, or club, the probability your card is a queen will be different than the probability of a queen given that you drew a diamond. You have slightly more information about diamonds since there are only 12 remaining in the deck
    - So now depending on the suit, a queen might be more likely. In other words, the probability of a queen is no longer independent of the suit

## Conditional Probability & Rules

---

**Addition Rule:**  $P(A \cup B) = P(A) + P(B)$

**Complementary Rule:**  $P(A) + P(A') = 1$

**Product Rule: $P(a\cap b) = P(a|b)*P(b)$**

**Multiplication Rule: $P(A \cup B) = P(A)P(B|A)$**

**Conditional Probability Formula: $P(a | b) = \dfrac {P(a \cap b)} {P(b)}$**

**Inclusion Exclusion Rule: $P(a \vee b) = P(a) + P(b) - P(a \wedge b)$**

# The Law of Total Probability

- The Law of Total Probability is a fundamental concept in probability theory that provides a way to express the probability of an event in terms of its partitions or subsets
    - **The total probability rule lets you take a joint probability distribution over a set of variables and produce a distribution over a single variable**
    - It is a useful tool for decomposing a complex probability problem into simpler, more manageable parts. The Law of Total Probability states that for any event A and a partition of the sample space into mutually exclusive and exhaustive events B₁, B₂, ..., Bₙ, the probability of event A can be expressed as the sum of the probabilities of A given each partition element, weighted by the probabilities of those partition elements

    $$
    P(A)=P(A∩B_1)+P(A∩B_2)+…+P(A∩B_n)
    $$

- Which is equivalent to:

$$
P(A) = \sum_{i=1}^{n} P(A \mid H_i) P(H_i)
$$

- The total probability rule states that by using the two conditional probabilities, we can find the probability of event A

# Joint Distributions

---

## Hidden Variables

---

- Conditional probability query doesn’t always reference all variables in the full joint distribution
    - Example: $P(Y=y | E = e)$
    - If there are more than 2 random variables, then $P(Y=y | E = e)$ is a partial joint distribution
- How do we convert partial joint distributions to a full joint distribution?
    - $P(Y=y|E=e) = \alpha \sum_{x\in H} P(Y=y, E=e, H = x)$
        - $\alpha$ is the normalization constant $\frac{1}{P(A)}$
        - $x$ is the hidden variable
- See [Module 2 (NLP)](https://gatech.instructure.com/courses/382338/pages/hidden-variables?module_item_id=3706184) for example

## Inference Using Full Joint Distributions

- **Marginal probability** is the probability of an event irrespective of the outcome of another variable
- **Marginalization (Summing Out):** Marginalization is a method that requires summing over the possible values of one variable to determine the marginal contribution of another
    - Marginalization tells us that we can calculate the quantity we want if we sum over all possibilities of countries (remember that the UK is made up of 3 countries: England, Scotland and Wales)
        - Example: i.e. P(happiness|weather) = P(happiness, country=England | weather) + P(happiness, country=Scotland | weather) + P(happiness, country=Wales | weather)

# Independence

---

- In probability, two [events](https://brilliant.org/wiki/uniform-probability/#definitions-of-key-terms) are **independent** if the incidence of one event does not affect the probability of the other event.  If the incidence of one event *does* affect the probability of the other event, then the events are **dependent**
    - Example: P(toothache, catch, cavity, cloud) = P(cloud | toothache, catch, cavity) * P(toothache, catch, cavity)
        - Because the weather is independent of dental issues, it seems safe to assume that weather doesn’t influence this. Therefore, we can make the following assertion: P(cloud | toothache, catch, cavity) = P(cloud)
- **Absolute independence does not imply conditional dependence**

## Rules

- Two random variables $A$ and $B$ are independent if $\Leftrightarrow P(AB) = P(A)P(B)$
- $P(A|B) = \dfrac{P(AB)}{P(B)}$
- By Symmetry $P(AB) = P(B|A)P(A)$
- $A,B$ independent
    - $P(A|B) = P(A)$
    - $P(B|A) = P(B)$

[Examples](Probability%20ea2edcaf2cad41b1924e0ae5e3a85051/Examples%2040f78658470b47829cdfafb0e488b1ef.md)

## Causal Vs. Logical Independence

- **Causal Independence:** refers to the absence of a direct causal relationship between two variables
    - In other words, two variables are causally independent if changes in one variable do not cause changes in the other
    - Causal independence is an important concept in understanding cause-and-effect relationships in various fields, such as epidemiology, economics, and social sciences. Establishing causal independence helps researchers identify whether changes in one variable can be attributed to changes in another variable, without a direct causal link
- **Logical Independence:** Logical independence, on the other hand, refers to the absence of a logical connection between two events or propositions
    - In statistics, logical independence is often used in the context of probability and probability distributions. Two events are said to be logically independent if the occurrence or non-occurrence of one event does not provide any information about the occurrence or non-occurrence of the other event
    - In terms of probability, if the probability of the joint occurrence of two logically independent events is equal to the product of their individual probabilities, then they are logically independent
- The suit of a card does not physically affect or cause any change in the probability of a queen. Neither does removing the two of diamonds, except for the fact that there are fewer cards to draw from
    - What we’re talking about here is logical independence, which is reflected in the state of our knowledge about the cards

# Bayesian Learning & Bayes Rule

---

- There are 4 components to the Bayes Rule:
    1. **Posterior probability** (updated probability after the evidence is considered)
    2. **Prior probability** (the probability before the evidence is considered)
    3. **Likelihood** (probability of the evidence, given the belief is true)
    4. **Marginal probability** (probability of the evidence, under any circumstance)

$$
\underbrace{P(H_i)}_{\text{prior prob}} \rightarrow  P(H_i|A) = \underbrace{\dfrac{P(A|H_i)}{P(A)}}_{\text{Posterior}} \cdot P(H_i)
$$

$$
\underbrace{P(A|B)}_{\text{posterior}} = \underbrace{P(A)}_{\text{Prior}} \space * \space \dfrac{\underbrace{P(B|A)}_{\text{likelihood}}}{\underbrace{P(B)}_{\text{marginal}}}
$$

- Other Notes
    - The posterior is sometimes known as the Bayes Factor
    - $P(A|H_i)$ is known as the likelihood
        - This is another conditional probability. It is the probability of the evidence being present, given the hypothesis is true
    - $P(A)$ here is also known as the query variable
    - $P(B)$ here is also known the evidence variable
    - If you need to find marginal probabilities, we can take advantage of the Law of Total Probability:
        - $P(B) = \sum_a P(B | A = a) *  P(B=b)$
        - This represents the sum of the probabilities over X

### Cause & Effect Relationships

- Often, we perceive as evidence the effect of some unknown cause and we would like to determine that cause. In that case, Bayes’ rule becomes: $P(cause | effect) = \dfrac {P(effect| cause)P(cause)} {P(effect)}$
- The conditional probability P(effect | cause) quantifies the relationship in the causal direction, whereas P(cause | effect) describes the diagnostic direction
    - In a task such as medical diagnosis, we often have conditional probabilities on causal relationship
    - Example: The doctor knows P(symptoms | disease) and wants to derive a diagnosis, P(disease | symptoms)
- Many problems have the form $P(\underbrace{Cause}_{\text{Unobservable}}|\underbrace{Effect}_{\text{Observable}})$
- What happens when the effects are independent?
    - We can use the ***Generalized Bayes Rule***
    - $\alpha P(\text{Cause}|\text{Effect}_1, \text{Effect}_2, ..., \text{Effect}_n)$
- **Naive Bayes Assumption:** Effect variables are always independent
    - Or that their causal effects are so small as to be negligible

## **Bayes Theorem Notes**

[Bayes Theorem & Ingredients For Inference](https://www.notion.so/Bayes-Theorem-Ingredients-For-Inference-8f83f2d1d66f4ae6b16f904deb1abaff?pvs=21)

## Bayes Rule with Multiple Evidence Variables

- **Chain Rule:** The chain rule, or general product rule, calculates any component of the [joint distribution](https://deepai.org/machine-learning-glossary-and-terms/joint-distribution) of a set of [random variables](https://deepai.org/machine-learning-glossary-and-terms/random-variable) using only conditional [probabilities](https://deepai.org/machine-learning-glossary-and-terms/probability)
    - **The chain rule is defined as: $P(X = x, Y = y) = P(X = x)P(Y = y | X = x)$**
    - Now, a possible world specifies a value for each of the variables Subject, Size, and Brightness. *How do you get the probability of a possible world?*
        - For example, what’s P(Subject = People, Size = Large, Brightness = Dark)? **According to the chain rule, this is simple. *You find the correct entries in the CPD tables and multiply them together*. So, in this case:**
            - P(Subject = People) × P(Size = Large | Subject = People) × P(Brightness = Dark | Subject = People, Size = Large)
            - **This result is called a *joint probability distribution* over Subject, Size, and Brightness, because it specifies the probability of each joint value of these three variables**
    - **Chain Rule Steps using conditional probability formula:**
        - Given P(a,b,c), find P(c)
        - Step 1: $\dfrac {P(a,b,c)} {P(b,c)} \rightarrow P(a,b,c) = P(a|b,c)P(b,c)$
        - Step 2: $P(b|c) = \dfrac {P(b,c)} {P(c)} \rightarrow P(b,c) = P(b|c)P(c)$
        - Step 3: $P(a,b,c) = P(a|b,c)P(b|c)P(c)$
        - Step 3: $P(c) = \dfrac {P(a,b,c)} {P(a|b,c)P(b|c)}$
    - **Chain Rule: 3 Variables:**
        - $P(A,B,C) = P(A|B,C) * P(B,C) = P(B|A,C) * P(A,C) = P(C|A,B) * P(A,B)$

    - **Two Test Cancer Example**
        - $P(c) = 0.01$ & $P(\neg c) = 0.99$
        - $P(+|c) = 0.9$ & $P(- |c) = 0.1$
        - $P(- | \neg c) =0.2$   & $P(+ | \neg c)$ = 0.8
        - Use a trick to find the joint probability distribution
        - Conditional Probability Table

        |  | Prior | + | + | P’ (Non Normalized Probability) | Posterior |
        | --- | --- | --- | --- | --- | --- |
        | Cancer | 0.01 | 0.9 | 0.9 | 0.0081 | 0.1698 |
        | Not Cancer | 0.99 | 0.2 | 0.2 | 0.0396 | 0.8301 |
        |  |  |  |  | 0.0477 |  |

# Conditional Independence & Dependence

---

### Conditional Independence

- In probability, we say two events are independent if knowing one event occurred doesn't change the probability of the other event
    - **Two events**
        - A and B, are independent if P(A ∣ B) = P(A) and P(B | A) = P(B)
        - **Three Events:**
            - If A and B are conditionally independent then we can say that P(A|B, C) = P(A|C)
        - **Conditional Independence**
            - Consider three variables a, b, and c, and suppose that the conditional distribution of a, given b and c, is such that it does not depend on the value of b, so that $P(a | b, c) = P(a|c)$
                - We say that a is conditionally independent of b given c
                - In other words, A and B are conditionally independent if and only if, given knowledge of whether C occurs, knowledge of whether A occurs provides no information on the likelihood of B occurring, and knowledge of whether B occurs provides no information on the likelihood of A occurring
            - **An** **important lesson here is that, generally speaking, conditional independence neither implies (nor is it implied by) independence**
                - Thus, we can have two events that are conditionally independent but they are not unconditionally independent (such as *A* and *B* above). Also, we can have two events that are independent but not conditionally independent, given an event *C*
        - Two events *A* and *B* are **conditionally independent** given an event *C* with *P*(*C*)>0 if:
            - $P(toothace \cap catch | cavity) = P(toothache | Cavity) * P(catch | cavity)$
                - This equation expresses the conditional independence of toothache and catch given cavity
    - **References**
        - [https://www.probabilitycourse.com/chapter1/1_4_4_conditional_independence.php](https://www.probabilitycourse.com/chapter1/1_4_4_conditional_independence.php)

### Conditional Dependence

- Conditional dependence is **a relationship between two or more events that are dependent when a third event occurs**
- Example:
    - In the below example: S & R are independent without knowledge of H. When we don’t know H, the probability of R is unaffected by the the knowledge of S
        - This means R & S are independent
    - However, when we know H, R & S become dependent since the probabilities change
    - **Two variables that may be independent, may not be independent in certain cases conditionally independent**

    ![Untitled](Probability%20ea2edcaf2cad41b1924e0ae5e3a85051/Untitled.png)

- **References:**
    - [https://www.probabilisticworld.com/conditional-dependence-independence/#Conditional_dependence](https://www.probabilisticworld.com/conditional-dependence-independence/#Conditional_dependence)

# Probability: Coin Flip Examples:

- What’s the probability of seeing at least 3 Heads across 4 flips?
    - $2^4 = 16$ total outcomes
    - 5 ways to achieve at least 3 Heads
        - H, H, H, H
        - H, H, H, T
        - H, H, T, H
        - H, T, H, H
        - T, H, H, H
    - 5 / 16 = 0.3125
- Given $P(X_1 = H) = 1/2$, what is the probability of X2 being Heads given $P(X_2 = H | X_1 = H) = 0.9$ and $P(X_2 = T | X_1 = T) = 0.8$
    - Using the theorem of total probability, we get:
        - $P(X_2 = H) = P(X_2 = H | X_1 = H) * P(X_1 = H) \space + P(X_2 = H | X_1 = T) * P(X_1 = T)$
        - This is equal to: $0.9 * \frac {1} {2} + 0.2 * \frac {1} {2} == 0.45 + 0.1 = 0.55$


# Probability Cheatshet

[probability_cheatsheet.pdf](Probability%20ea2edcaf2cad41b1924e0ae5e3a85051/probability_cheatsheet.pdf)

# References

- [https://www.mathsisfun.com/data/probability-events-conditional.html](https://www.mathsisfun.com/data/probability-events-conditional.html)
- [https://www.khanacademy.org/math/ap-statistics/probability-ap/stats-conditional-probability/v/testing-independence-from-experimental-data](https://www.khanacademy.org/math/ap-statistics/probability-ap/stats-conditional-probability/v/testing-independence-from-experimental-data)
- [https://www.seas.upenn.edu/~cis520/papers/Bishop_8.2.pdf](https://www.seas.upenn.edu/~cis520/papers/Bishop_8.2.pdf)
- [https://link.springer.com/referenceworkentry/10.1007/978-1-4419-9863-7_452](https://link.springer.com/referenceworkentry/10.1007/978-1-4419-9863-7_452)
- [https://www.probabilitycourse.com/chapter1/1_4_4_conditional_independence.php](https://www.probabilitycourse.com/chapter1/1_4_4_conditional_independence.php)
- [https://towardsdatascience.com/conditional-independence-the-backbone-of-bayesian-networks-85710f1b35b](https://towardsdatascience.com/conditional-independence-the-backbone-of-bayesian-networks-85710f1b35b)
- [https://betterexplained.com/articles/an-intuitive-and-short-explanation-of-bayes-theorem/](https://betterexplained.com/articles/an-intuitive-and-short-explanation-of-bayes-theorem/)