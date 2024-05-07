# Dependency Parsing

---

# What is it?

- Dependency Parsing is the process to analyze the grammatical structure in a sentence and find out related words as well as the type of the relationship between them
- Each relationship:
    1. Has one **head** **and a **dependent** that modifies the **head**
    2. Is labeled according to the nature of the dependency between the **head** and the **dependent**. These labels can be found at [Universal Dependency Relations](https://universaldependencies.org/u/dep/)

# Algorithms

---

## Shift-Reduce Parsing

- Shift-reduce parsing is based on a bottom-up parsing technique, where the parser starts with the input tokens and aims to construct a parse tree by applying a set of grammar rules
    - Process a sentence word by word from a buffer
    - Can place words in a stack if you don’t know what to do with them
    - **Shift:** Move a word to the stack
    - **Left:** The top of the stack is the child of the buffer’s next word
    - **Right:** The buffers next word is the child of the top of the stack
- The two main actions involved in shift-reduce parsing are “shift” and “reduce”:
    1. **Shift:** During the shift operation, the parser reads the next input token and pushes it onto a stack
        1. The parser maintains a buffer to hold the remaining input tokens
        2. The shift operation moves the parser’s current position to the right in the input stream
    2. **Reduce:** The reduce operation applies a grammar rule to the tokens on top of the stack
        1. If the tokens on the stack match the right-hand side of a grammar rule, they are replaced with the corresponding non-terminal symbol from the left-hand side of that rule
        2. The reduce operation moves the parser’s current position to the left in the input stream
    3. **Accept:** If the stack contains the start symbol only and the input buffer is empty at the same time then that action is called accept
    4. **Error:** A situation in which the parser cannot either shift or reduce the symbols, it cannot even perform accept action then it is called an error action
- Shift-reduce parsing continues until it reaches the end of the input stream and constructs a valid parse tree
    - It employs a parsing table, often generated using techniques like the LR(1) or LALR(1) parsing algorithm, to determine the shift or reduce action to take at each step
    

# Learning

- **How do you know whether to shift, left or right?**
- **Learn a classifier**
    - Given: a stack, a buffer, parts of speech tags
    - Output: shift, left, or right (and dependency type)
- **Data:**
    - Distant supervision
    - Annotate a lot of sentences with dependency graphs
    - Run stack-reduce, backtracking when necessary to find the known graph
    - **X:** Partial parses of sentences (buffer, stack, POS tags)
    - **Y:** Best shift-reduce action (shift, left or right)