# Fine-Tuning, Instruction Tuning & RLHF

---

# What it is it?

- **Fine-tuning** is taking a pre-trained model and **training at least one internal model parameter** (i.e. weights)
    - In the context of LLMs, what this typically accomplishes is transforming a general-purpose base model (e.g. GPT-3) into a specialized model for a particular use case
- Reinforcement Learning (RL) should be better seen as a “fine-tuning” paradigm that can add capabilities to general-purpose pretrained models, rather than a paradigm that can bootstrap intelligence from scratch
- Pre-trained LLM’s are trained on a large, general corpus of text and are generally capable of generating fluent text
    - To specialize the output, one can fine-tune the model
    - Continue training the pre-trained model with a small, specialize corpus
    - Shifts the weights in the model, biasing it towards the new data

# When do we need to fine tune models?

- **Transfer Learning:** Fine-tuning is a key component of transfer learning, where a pre-trained model's knowledge is transferred to a new task
- **Limited Data Availability:** Fine-tuning is particularly beneficial when you have limited labeled data for your specific task
- **Time and Resource Efficiency:** Fine-tuning on top of a pre-trained model is often more efficient, as you can skip the initial training stages and converge faster to a solution
- **Task-Specific Adaptation:** Fine-tuning is necessary when you have a pre-trained language model, and you want to adapt it to perform a specific task
    - For example, you might fine tune a language model for sentiment analysis or text generation for a particular domain like medical or legal documents using domain specific data
- **Continuous Learning:** Fine-tuning is useful for continuous learning scenarios where the model needs to adapt to changing data and requirements over time
- **Bias Mitigation:** If you're concerned about biases present in a pre-trained model, fine-tuning can be used to reduce or counteract those biases by providing balanced and representative training data for the fine-tuning process
- **Data Security and Compliance:** When working with sensitive data that cannot leave a specific environment due to security and compliance concerns, you might need to fine tune a model locally on your secure infrastructure

# **Why RL fine-tuning over other alternatives?**

- Now, it’s natural to ask why don’t we just use prompts to discover capabilities ([Just ask for Generalization](https://evjang.com/2021/10/23/generalization.html)), or use supervised learning to fine-tune
- RL fine-tuning stands out in a few ways:
    - It can **directly optimize** a non-differentiable objective, instead of merely trying to mimic existing data, and thus does not have performance ceilings
    - [Other learning paradigms are about minimization; reinforcement learning is about maximization](https://arxiv.org/abs/2103.04047)
    - It should have (and has shown to have) **better scaling laws** compared to prompts or supervised learning
    - Meta-capabilities (such as having **agency**) just fit better in the RL fine-tuning paradigm
    - A model having agency will be better than a model without it. [Why Tool AIs Want to Be Agent AIs](https://www.gwern.net/Tool-AI)

# Types of Fine-Tuning

1. **Self-supervised learning:** consists of **training a model based on the inherent structure of the training data**
    1. Note: This is how most LLM’s are trained from scratch
2. **Supervised-Fine Tuning (SFT):** The concept of supervised fine-tuning in the context of AI pertains to the process of taking a pre-trained model and further training it on a new, labeled dataset, with the goal of adapting the model's parameters to perform a specific task more effectively
3. **RL from Human Feedback (RLHF)**

![Untitled](Fine-Tuning,%20Instruction%20Tuning%20&%20RLHF%207a4f561c451c430f97e7afdd78c5180c/Untitled.png)

# Types of Fine-Tuning

1. **Low Ranking Adaptation (LoRA):** LoRA is a technique to fine tune large language models
    1. It uses low-rank approximation methods to reduce the computational and financial costs of adapting models with billions of parameters, such as GPT-3, to specific tasks or domains
2. **Quantized LoRA (QLoRA):** QLoRA is an efficient finetuning approach for large language models (LLMs) that significantly reduces memory usage while maintaining the performance of full 16-bit finetuning
    1. It achieves this by backpropagating gradients through a frozen, 4-bit quantized pretrained language model into Low Rank Adapters
3. **Parameter Efficient Fine Tuning (PEFT):** PEFT is an NLP technique that adapts pre-trained language models efficiently to various applications by fine-tuning only a small set of parameters, reducing computational and storage costs
    1. It combats catastrophic forgetting, adjusting key parameters for specific tasks, and delivers comparable performance to full fine-tuning across modalities like image classification and stable diffusion dreambooth
    2. It's a valuable approach for high performance with minimal trainable parameters
4. **DeepSpeed:** DeepSpeed is a deep learning software library that accelerates the training of large language models. It includes ZeRO (Zero Redundancy Optimizer), a memory-efficient approach for distributed training
    1. DeepSpeed can automatically optimize fine-tuning jobs that use Hugging Face’s Trainer API, and offers a drop-in replacement script to run existing fine-tuning scripts
5. **ZeRO:** ZeRO is a set of memory
optimization techniques that enable effective training of large models with trillions of parameters, such as GPT-2 and Turing-NLG 17B
    1. A key appeal of ZeRO is that no model code modifications are required
    2. It’s a memory-efficient form of data parallelism that gives you access to the aggregate GPU memory of all the GPU devices available to you, without inefficiency caused by the data replication in data parallelism

# RLHF

---

## Using RL with Human Feedback for Fine-Tuning

- For fine-tuning LLMs using RL we need to frame the problem into a Agent-Environment setting where the agent ( policy ) can interact with the environment to get the reward for its actions. This reward is then used as feedback to train the model
- The mapping of the entities is as follows:
    - **Agent (Policy)**: LLM (Large Language Model)
    - **Environment**: In this case the environment is the reward function ( model ) which generates rewards
        - The reward function consumes the input as well as the output of the LLM to generate the reward
    - **Reward Model:** Before the reward model is trained data is collected from human labelers
        - For each input $*x$* several $*yᵢ*$ are generated by sampling from the LLM
        - The humans are then asked to rank these $*yᵢ*$ giving the highest rank to the best response
            - Using this as the label the reward model is trained to maximize the probability of the correct response using a loss of the type
    - **Loss Function**
- ***The reward is used in a loss function and the policy is updated***

## How it Works

- 

## Training Process Overview

![Untitled](Fine-Tuning,%20Instruction%20Tuning%20&%20RLHF%207a4f561c451c430f97e7afdd78c5180c/Untitled%201.png)

![Untitled](Fine-Tuning,%20Instruction%20Tuning%20&%20RLHF%207a4f561c451c430f97e7afdd78c5180c/Untitled%202.png)

# Instruction Tuning

---

[Instruction Tuning](Fine-Tuning,%20Instruction%20Tuning%20&%20RLHF%207a4f561c451c430f97e7afdd78c5180c/Instruction%20Tuning%20b2f3b6b20b4b4090b7c08474fe5e624f.md)

# Resources

- [RL & Fine Tuning](https://ankeshanand.com/blog/2022/01/08/rl-fine-tuning.html)
- [https://medium.com/@mlblogging.k/reinforcement-learning-for-tuning-language-models-how-chatgpt-is-trained-9ecf23518302](https://medium.com/@mlblogging.k/reinforcement-learning-for-tuning-language-models-how-chatgpt-is-trained-9ecf23518302)
- [https://cameronrwolfe.substack.com/p/understanding-and-using-supervised](https://cameronrwolfe.substack.com/p/understanding-and-using-supervised)
- [https://www.labellerr.com/blog/reinforcement-learning-from-human-feedback/](https://www.labellerr.com/blog/reinforcement-learning-from-human-feedback/)

### Fine-Tuning Methods

- [https://huggingface.co/blog/rishiraj/finetune-llms](https://huggingface.co/blog/rishiraj/finetune-llms)

### SFT

- [https://mantisnlp.com/blog/supervised-fine-tuning-customizing-llms/](https://mantisnlp.com/blog/supervised-fine-tuning-customizing-llms/)

### RLHF

- [https://medium.com/@mlblogging.k/reinforcement-learning-for-tuning-language-models-how-chatgpt-is-trained-9ecf23518302](https://medium.com/@mlblogging.k/reinforcement-learning-for-tuning-language-models-how-chatgpt-is-trained-9ecf23518302)
- [https://medium.com/@zaiinn440/reinforcement-learning-from-human-feedback-rlhf-empowering-chatgpt-with-user-guidance-95858592fdbb](https://medium.com/@zaiinn440/reinforcement-learning-from-human-feedback-rlhf-empowering-chatgpt-with-user-guidance-95858592fdbb)
- [https://gist.github.com/JoaoLages/c6f2dfd13d2484aa8bb0b2d567fbf093](https://gist.github.com/JoaoLages/c6f2dfd13d2484aa8bb0b2d567fbf093)
- [https://huyenchip.com/2023/05/02/rlhf.html](https://huyenchip.com/2023/05/02/rlhf.html)
- [https://archive.ph/Z390X](https://archive.ph/Z390X)