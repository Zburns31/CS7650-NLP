# Instruction Tuning

---

# What is it?

- [In instruction tuning, LLMs are further trained on a dataset consisting of (INSTRUCTION, OUTPUT) pairs in a supervised fashion](https://arxiv.org/pdf/2308.10792.pdf)
    - [The INSTRUCTION denotes the human instruction for the model, and OUTPUT denotes the desired output that follows the INSTRUCTION2](https://arxiv.org/pdf/2308.10792.pdf)
- The main difference between instruction tuning and standard supervised fine-tuning lies in the data that the model is trained on
    - Whereas supervised fine-tuning trains models on **input examples and their corresponding outputs**, instruction tuning **augments input-output examples with instructions**, which enables instruction-tuned models to generalize more easily to new tasks
- [This process bridges the gap between the next-word prediction objective of LLMs and the users’ objective of having LLMs adhere to human instructions](https://arxiv.org/pdf/2308.10792.pdf)
- [The benefits of instruction tuning are threefold](https://arxiv.org/pdf/2308.10792.pdf):
    - Fine-tuning an LLM on the instruction dataset bridges the gap between the next-word prediction objective of LLMs and the users’ objective of instruction following
    - Instruction tuning allows for a more controllable and predictable model behavior compared to standard LLMs
    - [It enhances the model’s ability to perform tasks it wasn’t specifically trained on, giving the model a range of applications](https://jasonwei20.github.io/files/FLAN%20talk%20external.pdf)

# How is this different than Fine-Tuning?

- Fine-tuning and instruction tuning are both techniques used to adapt pre-trained Large Language Models (LLMs) to specific tasks, but they differ in their objectives and the nature of the data they use
- **Fine-tuning** typically involves training the model on a task-specific dataset, where the model learns to predict the correct label for each input
    - The goal is to adapt the model’s parameters to perform well on the target task. The data used for fine-tuning is usually task-specific and labeled
- On the other hand, **instruction tuning** is a more recent technique that aims to make LLMs more controllable and better at following instructions
    - In instruction tuning, the model is trained on a dataset of (INSTRUCTION, OUTPUT) pairs
    - The goal is to make the model generate outputs that adhere to the given instructions
    - This technique is particularly useful when you want the model to generate specific types of responses based on the instructions

![Untitled](Instruction%20Tuning%20b2f3b6b20b4b4090b7c08474fe5e624f/Untitled.png)

# Resources

- [https://newsletter.ruder.io/p/instruction-tuning-vol-1](https://newsletter.ruder.io/p/instruction-tuning-vol-1)