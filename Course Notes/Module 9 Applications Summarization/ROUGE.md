# ROUGE

# What is it?

- **ROUGE**, which stands for **Recall-Oriented Understudy for Gisting Evaluation**, is a set of metrics and a software package specifically designed for evaluating automatic summarization
- Although its primary use is for summarization, it can also be applied to machine translation and other natural language processing (NLP) tasks
- Rouge assesses the output based on the summaries crafted by human experts (i.e., reference summary or ground truth)
    - It is designed to measure the similarity by comparing the system-generated summary to one or more reference summaries or translations. It ranges from **0–1**, 1 being the highest

# How does it work?

- Rouge mainly focuses on 2 key factors:
    1. **Precision** — Precision measures the accuracy of the system-generated summary
        1. It indicates how well the machine-generated summary matches the reference summary in terms of content
        2. A higher precision value implies that the machine-generated summary contains a significant amount of relevant information from the reference summary, minimizing unnecessary or irrelevant information

    $$
    \text{ROUGE Precision} = \dfrac{\text{Number of overlapping words}}{\text{Total words in system/candidate summary}}
    $$

    1. **Recall** — Recall is a measure that determines the completeness of the information captured by a machine generated summary. It helps you in understanding how much of the information in the reference summary is actually captured by the machine-generated summary
        1. A higher recall value indicates that your model has successfully managed to capture a large portion of the information from the reference summary
        2. However, there is a possibility that a high recall value might also include reductant information, leading to a decrease in precision value

    $$
    \text{ROUGE Recall} = \dfrac{\text{Number of overlapping words}}{\text{Total words in reference summary}}
    $$


# Variants

- **ROUGE-N:** Measures the number of matching n-grams (contiguous sequences of n words) between the model-generated text and a human-produced reference
- **ROUGE-2: Considers Bi-grams (pairs of consecutive words)**
- **ROUGE-L:** Based on the **longest common subsequence (LCS)** between the model output and reference
    - The LCS is the longest sequence of words (not necessarily consecutive) shared between both

# Problems With ROUGE

- Doesn’t consider the semantics and only looks at exact token match
- Candidate may be factually wrong, nonsensical, grammatically incorrect but still get a high ROUGE score
- Ignores the original document
    - Can be multiple valid summaries

# Resources

- [https://pub.aimind.so/unveiling-the-power-of-rouge-metrics-in-nlp-b6d3f96d3363](https://pub.aimind.so/unveiling-the-power-of-rouge-metrics-in-nlp-b6d3f96d3363)
- [https://www.freecodecamp.org/news/what-is-rouge-and-how-it-works-for-evaluation-of-summaries-e059fb8ac840/](https://www.freecodecamp.org/news/what-is-rouge-and-how-it-works-for-evaluation-of-summaries-e059fb8ac840/)