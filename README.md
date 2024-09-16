# NLP Class Imbalance: Classifying Student Responses with AI
![Static Badge](https://img.shields.io/badge/Jupyter%20Notebook-orange?style=for-the-badge&logo=Jupyter&labelColor=black)
![Static Badge](https://img.shields.io/badge/NLP-blue?style=for-the-badge&logoColor=black&labelColor=yellow)
![Static Badge](https://img.shields.io/badge/Prompting%20(Few--shot)%20(Chain--of--thought)-purple?style=for-the-badge&labelColor=black)



## Project Overview
I worked on this project during Fall 23 while working in the Innovative Educational Computing (IEC) lab headed by Dr. Noboru Matsuda.

This project focuses on **classifying student responses** from questions into three distinct categories:
1. **Passive**: The student is simply receiving information without interacting with or adding to it.
2. **Active**: The student manipulates or inputs information but does not generate new concepts or ideas based on prior knowledge.
3. **Constructive**: The student reflects on the information, provides reasoning, or thoughtful consideration based on prior knowledge.

The primary challenge faced in this project is the **class imbalance** in the dataset, with very few constructive labels available for training. The project explores **NLP techniques** using Large Language Models (LLMs) to address this imbalance.

---

## Problem Statement

The dataset contains **imbalanced labels** for student responses, making it difficult for the model to learn the **constructive class** effectively. The goal is to develop a system that can learn to classify the responses accurately despite this imbalance.
```The Dataset is hidden for research purposes and integrity```

### Dataset Structure
- **Features**: 
  1. **Questions** 
  2. **Student Responses**
  
### Example Label Issue:
- Question: “Analyze the examples you pasted above. Why do you think the feature is present in the unexpected type of reviews?”
- Student Response: “I think they are used to contradict expectations whether the person was disappointed or pleasantly surprised.”
- Label: **Passive**

Upon analysis, the response is **Active**, since it involves explanation and reasoning, which is a key challenge in the current dataset labeling.

---

## Approach: Leveraging Large Language Models

To handle the class imbalance, we experiment with **few-shot prompting** and **Chain-of-Thought (CoT)** reasoning using **GPT-3.5-turbo**. Additionally, we explore **assertions** to further guide the model's learning process.

### Key Techniques
1. **Few-shot prompting**: Demonstrating a small number of examples to guide the model.
2. **Chain-of-Thought (CoT)**: Breaking down complex tasks into smaller reasoning steps.
3. **Assertions**: Incorporating "do’s and don’ts" to refine model predictions.

---

## Experiments and Results

I conducted a series of experiments with different iterations of few-shot prompting and Chain-of-Thought (CoT) reasoning with a subset of the dataset:

1. **Pure Few-shot Specific CoT** 
2. **Few-shot Specific CoT + General CoT (step-by-step)**
3. **Few-shot Specific CoT + Assertions (Do’s and Don’ts)**
4. **Few-shot Specific CoT + General CoT (step-by-step) + Assertions**

### Results Summary:

| Model                    | Prompt                              | Accuracy |
|---------------------------|-------------------------------------|----------|
| GPT-3.5-turbo              | Pure Few-shot Specific CoT          | 0.60     |
| GPT-3.5-turbo              | Few-shot Specific CoT + General CoT | 0.73     |
| GPT-3.5-turbo              | Few-shot Specific CoT + Assertion   | 0.33     |
| GPT-3.5-turbo              | Few-shot Specific CoT + General CoT + Assertion | 0.73 |

**Observations**:
- General CoT and General CoT + Assertions performed well.
- Using assertions only caused all test samples to be predicted as "Constructive," leading to poor precision for Passive and Active labels.

### F1 Score, Precision, and Recall:

| Model                      | Class 0 (Passive) | Class 1 (Active) | Class 2 (Constructive) |
|-----------------------------|------------------|------------------|------------------------|
| Pure Few-shot Specific CoT   | Precision: 0.67  | Precision: 0.33  | Precision: 0.67        |
| Few-shot Specific CoT + General CoT | Precision: 1.00 | Precision: 1.00 | Precision: 0.56        |
| Few-shot Specific CoT + Assertion | Precision: NaN  | Precision: NaN  | Precision: 0.33        |
| Few-shot Specific CoT + General CoT + Assertion | Precision: 1.00 | Precision: 1.00 | Precision: 0.56        |

---


## References

- **Brown et al. (2020)** - Language models are few-shot learners.
- **Wei et al. (2022)** - Chain-of-thought prompting elicits reasoning in large language models.
- **Kojima et al. (2022)** - Large language models are zero-shot reasoners.
