# Bayesian Networks

# What are Bayes Networks?
- Bayesian networks, also known as Bayesian belief networks or probabilistic graphical models, are a type of graphical representation used to model and analyze relationships between variables in a probabilistic framework
    - Bayesian networks combine graph theory and probability theory to model the conditional dependencies between variables and make probabilistic inferences
- In a Bayesian network, variables are represented as nodes in a directed acyclic graph (DAG), where edges between nodes indicate probabilistic dependencies
    - Each node represents a random variable, and the edges specify the direct influence of one variable on another
    - The strength and nature of the relationship are typically described using conditional probability tables (CPTs), which quantify the conditional probabilities of a variable given its parents in the graph
- **Bayes networks define probability distributions over graphs of random variables**
    - Each nodes probability distribution is only conditioned by the incoming arcs
    - The compact representation of Bayes networks allow for scalability
        - The joint distribution over any five variables requires $2^5 -1 = 31$ probability values. The Bayes network only requires 10
            - Joint Distribution of Nodes $\equiv$ Product ($\prod)$ of Conditional Distributions + Markovian Property
                - Markovian Property: The Dependence on a node given another node is only through the immediate parents

    ![Untitled](./Bayesian%20Networks/Untitled%205.png)


# How it works

- A Bayesian network is a directed graph in which each node is annotated with quantitative probability information. The full specification is as follows:
    - Each node corresponds to a random variable, which may be discrete or continuous
    - Directed links or arrows connect pairs of nodes. If there is an arrow from node X to Y node X is said to be a parent of Y
        - The graph has no directed cycles and hence is a directed acyclic graph, or DAG
    - Each node $X_i$ has associated probability information $P(X_i | Parents(X_i))$ that quantifies the effect of the parents on the node using a finite number of **parameters**
        - The intuitive meaning of an arrow is typically that X has a direct influence on Y, which suggests that causes should be parents of effects
        - Each arc in the Bayesian network has a conditional probability
    - A Bayesian network is really just an equation. If we have variables $X_1, X_2, X_3$, then:
        - $P(X_1, X_2, X_3) = \prod_{i=1}^n P(X_i|Parents(X_i))$
    - Given the below figure, we would say A causes B or B is a consequence of A

    ![Untitled](./Bayesian%20Networks/Untitled%201.png)

- The independence of two nodes in a DAG depends on their relative position in the graph as well as on the knowledge of other nodes (conditioning)
- **Hard Evidence:** for a node A is evidence that the outcome of A is known
    - Hard evidence about nodes is the information that we bring to the network, and it affects the probabilities of other nodes

# Key Components

Key characteristics of Bayesian networks include:

1. **Directed Acyclic Graph (DAG):** The graph structure of a Bayesian network is acyclic, meaning it does not contain cycles
    1. This reflects the notion that causes precede their effects, as is often the case in real-world systems
2. **Nodes and Edges:** Nodes represent variables, and directed edges represent causal relationships or dependencies between variables.
3. **Conditional Probability Tables (CPTs):** Each node's conditional probability table describes the probabilities of its states given the states of its parent nodes
    1. These tables capture the conditional dependencies between variables
4. **Inference:** Bayesian networks enable probabilistic inference, allowing you to compute the probability distribution of one or more variables given evidence on other variables
    1. Inference can involve tasks such as predicting the probability of an event, finding the most likely explanation for observed data, or updating beliefs based on new information
5. **Learning:** Bayesian networks can be learned from data, allowing them to be constructed from observed relationships in real-world systems
    1. Learning can involve both structure learning (identifying the graph's topology) and parameter learning (determining the CPT values)
6. **Markovian Property:** The conditional distribution of any node depends only on its parental nodes

# Bayes Net Structure & Topology

- The local probability information attached to each node takes the form of a conditional probability table (CPT)
    - ***Only suitable for discrete variables***
- Each row in a CPT contains the conditional probability of each node value for a conditioning case. A conditioning case is just a possible combination of values for the parent nodes
    - Each row must sum to 1, because the entries represent an exhaustive set of cases for the variable
- Notice that the network does not have nodes corresponding to Mary’s currently listening to loud music or to the telephone ringing and confusing John. These factors are summarized in the uncertainty associated with the links from Alarm to John Calls and Mary Calls
    - This shows both laziness and ignorance in operation since it would be too difficult to find out why those factors would be more or less likely in certain scenarios

![Untitled](./Bayesian%20Networks/Untitled%202.png)

[Bayes Network Topology](./Bayesian%20Networks/Bayes%20Network%20Topology.md)

# Construction of Bayesian Networks

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

## Algorithm

1. **Nodes:** First determine the set of variables that are required to model the domain. Now order them, $\brace X_1, X_2, ... X_n$. Any order will work, but the resulting network will be more compact if the variables are ordered such that causes precede effects
2. **Links:** For i = 1 to n do:
    1. Choose a minimal set of parents for Xi from $X_1,...X_{i-1}$
    2. For each parent, insert a link from the parent to Xi
    3. CPTs: Write down the conditional probability table, $P(X_i | Parents(X_i))$

### Algorithm Notes

- Intuitively, the parents of node Xi should contain all those nodes in that directly influence Xi
- It’s important to not include parents that have already been include previously. This method guarantees the network is acyclic

# Difference Between Causal and Diagnostic Models

- **Causal:** Causal knowledge is *𝑝*(*𝑧*∣*ℎ*), i.e. the probability that a certain state *ℎ* causes a certain state of the observable variable *𝑧*
    - $P(cause | effect)$
- **Diagnostic:** Diagnostic knowledge on the other hand refers to the knowledge we gain from inferring the probability of state *ℎ*
 from observation *𝑧*
    - $P(effect | cause)$
    - In this case, like a doctor, we are using an effect (symptom) to inference a cause which can be much more difficult
- **If we stick to a causal model, we end up having to specify fewer numbers, and the numbers will often be easier to come up with**

# D-Separation (Reachability)

- d-separation is a criterion for deciding, from a given a causal graph, whether a set *X* of variables is independent of another set *Y,* given a third set *Z.* The idea is to associate"dependence" with "connectedness" (i.e., the existence of a connecting path) and "independence" with "unconnected-ness" or "separation"
- Intuitively, a path is *active* if it carries information, or dependence. Two variables X and Y might be connected by lots of paths in a graph, where all, some, or none of the paths are active. X and Y are d-connected, however, if there is *any* active path between them. So X and Y are d-separated if *all* the paths that connect them are  *inactive*, or, equivalently, if no path between them is active
- **General Rule:** Any two variables are independent if they are not linked by just unknown variables
    - ***In general, if the centre variable is known, then the first and third variables become independent. If all are unknown, then the first and third variables are dependent***
    - It is sufficient to know that if a direct successor of a convergent variable is known, then the variable itself does not have to be known. This is because if we know the successor, this gives us knowledge about the predecessor
    - [How to determine which nodes are D-separated](https://web.mit.edu/jmn/www/6.034/d-separation.pdf)

    ![Untitled](./Bayesian%20Networks/Untitled%203.png)

    - Example:
        - If we know B, then everything downstream becomes independent of anything upstream of B
            - E is now independent of C conditioned on B
            - Knowledge of B does not render A and E independent

        ![Untitled](./Bayesian%20Networks/Untitled%204.png)

    - More examples in:

    [D Separation Example](./Bayesian%20Networks/D%20Separation%20Example.md)

- **How do we define an active or inactive path?**
    - A path is active when *every* vertex on the path is active. Paths, and vertices on these paths, are active or inactive *relative* to a set of other vertices Z

- **Example:**
    - $C \perp A$: No because the information feeds through from A —> C. A influences C by virtue of B
    - $C \perp A | B$: Yes because if we know the full value of B, then knowing A won’t add any further information
        - The only determinant of C is B if we know B
    - $C \perp D$: No because if we know D, we can infer more about C
    - $C \perp D | A$: If we do know A, then the knowledge of D won’t help add further information
    - $E \perp C | D$: If we know D, then E and C become independent

    ![Untitled](./Bayesian%20Networks/Untitled%205.png)

- **References:**
    - [https://yuyangyy.medium.com/understand-d-separation-471f9aada503](https://yuyangyy.medium.com/understand-d-separation-471f9aada503)
    - [http://bayes.cs.ucla.edu/BOOK-2K/d-sep.html](http://bayes.cs.ucla.edu/BOOK-2K/d-sep.html)
    - [https://medium.com/mlearning-ai/bayesian-networks-d-separation-e2a8f483b721](https://medium.com/mlearning-ai/bayesian-networks-d-separation-e2a8f483b721)
    - [https://web.mit.edu/jmn/www/6.034/d-separation.pdf](https://web.mit.edu/jmn/www/6.034/d-separation.pdf)


# Probabilistic Inference

- General inference queries will have the following attributes
    - **Evidence variables** are variables that we know the values of
        - I.e $E = e_1, e_2, ..., e_n$
    - **Hidden variables:** Are variables that are along for the ride but that we don't care about
        - I.e. $H = h_1, h_2, ..., h_n$
    - **Query variables:**  Are variables we wish to know the probability of
        - I.e. Q

    ![Untitled](./Bayesian%20Networks/Untitled%206.png)


# Important Properties & Concepts

- **Non-descendants Property:** Each variable is conditionally independent of its non-descendants, given its parents
- **Markov Blanket: A** variable is conditionally independent of all other nodes in the network, given its parents, children, and children’s parents
- **Context-Specific Independence:** A conditional distribution exhibits CSI if a variable is conditionally independent of some of its parents given certain values of others
    - Example: $P(Damage | Car \space Ruggedness, Accident)$ = if (Accident = false) then d1 else d2 (Ruggedness)
- **Explaining Away Effect:** "Explaining away" is a common pattern of reasoning in which the ***confirmation of one cause*** of an observed or believed event reduces the need to invoke alternative causes
    - Think of it another way.  The ground is shaking.  You observe *𝐵*, the giant is wandering around.  This explains away *𝐶*, so it seems unlikely that there is now an earthquake - you settle for the giant explanation.  But observing the giant was key - until you had this as the likely explanation of the earthquake, nothing had been  explained away
        - [https://stats.stackexchange.com/questions/54849/why-does-explaining-away-make-intuitive-sense](https://stats.stackexchange.com/questions/54849/why-does-explaining-away-make-intuitive-sense)
- **Consistency:** An  [estimator](https://www.statlect.com/glossary/estimator) of a given [parameter](https://www.statlect.com/glossary/parameter) is said to be consistent if it [converges in probability](https://www.statlect.com/asymptotic-theory/convergence-in-probability) to the true value of the parameter as the sample size tends to infinity

# References:

- [https://bayesian-intelligence.com/publications/bai/book/BAI_Chapter2.pdf](https://bayesian-intelligence.com/publications/bai/book/BAI_Chapter2.pdf)
- [https://medium.com/nerd-for-tech/the-chain-rule-of-conditional-probabilities-656d8d2dbc15](https://medium.com/nerd-for-tech/the-chain-rule-of-conditional-probabilities-656d8d2dbc15)
- [https://livebook.manning.com/book/practical-probabilistic-programming/chapter-9/31](https://livebook.manning.com/book/practical-probabilistic-programming/chapter-9/31)
- [https://livebook.manning.com/book/practical-probabilistic-programming/chapter-9/18](https://livebook.manning.com/book/practical-probabilistic-programming/chapter-9/18)
- [https://deepai.org/machine-learning-glossary-and-terms/chain-rule](https://deepai.org/machine-learning-glossary-and-terms/chain-rule)
- [https://machinelearningmastery.com/introduction-to-bayesian-belief-networks/](https://machinelearningmastery.com/introduction-to-bayesian-belief-networks/)
- [https://www.cse.unsw.edu.au/~cs9417ml/Bayes/Pages/Bayesian_Networks_Inference.html](https://www.cse.unsw.edu.au/~cs9417ml/Bayes/Pages/Bayesian_Networks_Inference.html)
- [https://www.bayesserver.com/docs/introduction/bayesian-networks/](https://www.bayesserver.com/docs/introduction/bayesian-networks/)
- [https://causalnex.readthedocs.io/en/latest/04_user_guide/04_user_guide.html](https://causalnex.readthedocs.io/en/latest/04_user_guide/04_user_guide.html)
- [https://www.youtube.com/watch?v=WqqpwDVeW10](https://www.youtube.com/watch?v=WqqpwDVeW10)
- [https://towardsdatascience.com/introduction-to-bayesian-networks-81031eeed94e](https://towardsdatascience.com/introduction-to-bayesian-networks-81031eeed94e)
- [https://www.ee.columbia.edu/~vittorio/Lecture12.pdf](https://www.ee.columbia.edu/~vittorio/Lecture12.pdf)
- [https://inst.eecs.berkeley.edu/~cs188/sp20/assets/lecture/lec-20-6up.pdf](https://inst.eecs.berkeley.edu/~cs188/sp20/assets/lecture/lec-20-6up.pdf)
- [https://www.bayesserver.com/docs/introduction/bayesian-networks/](https://www.bayesserver.com/docs/introduction/bayesian-networks/)
- [https://people.cs.pitt.edu/~milos/courses/cs2740/Lectures/class19.pdf](https://people.cs.pitt.edu/~milos/courses/cs2740/Lectures/class19.pdf)
- MH Sampling: [https://www.youtube.com/watch?v=OTO1DygELpY](https://www.youtube.com/watch?v=OTO1DygELpY)

## D Separation

- [https://livebook.manning.com/book/practical-probabilistic-programming/chapter-9/](https://livebook.manning.com/book/practical-probabilistic-programming/chapter-9/)
- [https://www.probabilisticworld.com/conditional-dependence-independence/#Conditional_dependence](https://www.probabilisticworld.com/conditional-dependence-independence/#Conditional_dependence)

## Sampling