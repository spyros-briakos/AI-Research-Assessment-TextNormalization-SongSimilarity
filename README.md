# Text Normalization and Composition Writer Information Prediction: A Hybrid Approach

## Overview

I've opted for full implementation the Text Normalization Assesment, thus a brief report as this repo's README is provided! This project leverages a hybrid approach combining **rule-based models** and **Large Language Models (LLMs)** to improve text normalization, especially for ambiguous or non-English text. This approach enhances the accuracy and quality of text processing, making it more reliable for real-world applications.

A separate **PDF document** describing the approach for **song similarity prediction**.


## General Key Objectives

- **Normalize Text**: Correct inconsistent or ambiguous text for better prediction accuracy.
- **Handle Non-English Text**: Detect and process non-English characters and edge cases.
- **Hybrid Models**: Combine various approaches to boost prediction reliability and accuracy.


## Exploratory Data Analysis (EDA)

The goal of the **Exploratory Data Analysis (EDA)** was to understand the dataset's structure and inform our approach to preprocessing and model development. Key findings and action items include:

### Key Findings:
- **Missing Data**: ~1,400 missing values in the **Ground Truth** column, requiring imputation or handling.
- **Text Length**: The text length distribution was analyzed, revealing the average length, which will inform decisions on text normalization.
- **Language Distribution**: We identified a significant mix of Latin and non-Latin text, influencing preprocessing choices.
- **N-Gram Patterns**: Bigram, trigram, and 4-gram analysis revealed frequently occurring word pairs and sequences to enhance feature engineering.
- **Special Characters**: Special characters and punctuation were found to be prevalent in the **Original_Text**, guiding text cleaning processes.
- **Unique Word Count**: We observed diverse vocabulary in the text, indicating the need for robust tokenization and vocabulary management.

### Action Items:
- **Handle Missing Data**: Apply imputation or removal strategies for missing values in **Ground Truth**.
- **Text Normalization**: Remove special characters, handle non-Latin text, and ensure consistent formatting.
- **Feature Engineering**: Leverage N-grams to capture meaningful text patterns and enhance model performance.
- **Text Cleaning**: Standardize punctuation and symbols to reduce noise in text data.
- **Optimize Tokenization**: Focus on handling diverse vocabulary effectively to improve model generalization.

## Approaches Implemented

### 1. **Baseline Rules**
- **Rule-based text normalization** techniques. Simple but effective for certain tasks.
- **Challenges**: Struggles with ambiguous or complex cases, especially with non-English characters.

### 2. **Enhanced Rules**
- Refines baseline rules with added logic for edge cases, improving flexibility.
- **Challenges**: Limited compared to machine learning approaches.

### 3. **LLM-Assisted Approach**
- Utilizes **Large Language Models (LLMs)** to refine text based on a broader contextual understanding.
- **Challenges**: Computationally expensive and slower for large datasets.

### 4. **Voting Hybrid Approach**
- A hybrid approach combining different model outputs (e.g., Baseline, Enhanced, LLM) using a **voting mechanism** to decide the final prediction.
- **Challenges**: Can introduce noise if predictions vary significantly across models.

### 5. **RefineBoost Hybrid Approach**
- Combines rule-based models with **boosting techniques** to dynamically improve predictions.
- **Challenges**: More computationally demanding than simpler models.

### 6. **Conditional Hybrid Approach**
- Combines models based on text characteristics (e.g., text length, non-English content).
- **Challenges**: More time-consuming but balances accuracy and efficiency.

## Metrics Evaluated

- **Exact Match Percentage**: Measures the percentage of exact matches between predicted and true values.
- **Word Error Rate (WER)**: Measures errors at the word level.
- **Character Error Rate (CER)**: Measures errors at the character level.
- **Execution Time**: Time taken to process the dataset for each approach.

## Results and Findings

### **Subset Data Experimentation**

We conducted experiments on **10% of the dataset** (1000 rows) in different batches to evaluate the performance of various approaches. This allowed us to fine-tune the models, optimize execution times, and evaluate the effectiveness of different methods under controlled conditions.

| **Approach**           | **Exact Match** | **WER** | **CER** | **Execution Time (min)** |
|------------------------|-----------------|---------|---------|--------------------------|
| **Baseline Rules**     | 67%             | 0.25    | 0.05    | 0.01                     |
| **Enhanced Rules**     | 77%             | 0.22    | 0.04    | 0.10                     |
| **LLM-Assisted**       | 78%             | 0.12    | 0.03    | 0.60                     |
| **Voting Hybrid**      | 75%             | 0.16    | 0.04    | 0.25                     |
| **RefineBoost Hybrid** | 76%             | 0.14    | 0.04    | 0.50                     |
| **Conditional Hybrid** | **80%**         | **0.12**| **0.03**| **0.64**                 |

### **Comments on the Table**
- The **Conditional Hybrid** approach delivered the highest **Exact Match** (80%) and the lowest **WER** and **CER** (0.12 and 0.03, respectively), while balancing accuracy and **execution time** (0.64 minutes).
- **LLM-Assisted** models also showed strong performance, reducing word and character errors significantly, but with a longer execution time (0.60 minutes).
- **Baseline Rules** showed the fastest execution time but had the lowest accuracy compared to hybrid and LLM-assisted models.
- **Enhanced Rules** and **RefineBoost Hybrid** showed good results in terms of both **accuracy** and **execution time**, making them solid contenders for tasks requiring a balance between speed and precision.

## Insights

1. **Hybrid Models Perform Best**: The **Conditional Hybrid** approach achieved the highest **Exact Match** score while balancing **accuracy** and **computational efficiency**.
2. **LLM-Based Approaches Reduce Errors**: **LLM-Assisted** and **Conditional Hybrid** models performed exceptionally well in reducing **WER** and **CER**, albeit with a higher **execution time**.
3. **Rule-Based Models**: While **Enhanced Rules** provided a good compromise, **Baseline Rules** performed poorly in comparison to hybrid and LLM-assisted models.

## Performance Trade-offs

### **Latency vs. Accuracy**
- Moving from **Baseline Rules** to more advanced models like **LLM-Assisted** and **Conditional Hybrid** provides a significant increase in **accuracy**. However, there is a noticeable trade-off in **latency**:
  - **LLM-Assisted** and **Conditional Hybrid** models offer the best accuracy but at a cost of longer processing times.
  - **Baseline Rules**, while faster, lack the accuracy required for more complex tasks.

### **Cost vs. Performance**
- **LLM-Assisted** and **Conditional Hybrid** models are computationally more expensive but yield superior results in terms of **accuracy**. For environments with limited resources, **Voting Hybrid** or **Enhanced Rules** offer a better tradeoff without significant cost increases.

## Future Work

### **1. Experimentation with Heavier LLMs**
We plan to experiment with **heavier LLMs**, such as **GPT-4**, **T5**, and **PaLM** models, to further enhance accuracy, particularly for tasks requiring deep contextual understanding. These models come with increased **computational costs**, but their ability to handle more complex tasks is invaluable.

### **2. More Sophisticated Hybrid Approaches**
To further improve performance, we will investigate advanced hybrid techniques, such as:

- **Ensemble Learning**: Combining models through methods like **stacking**, **bagging**, and **boosting** to improve robustness and reduce overfitting. This technique will enhance the model's ability to generalize better to unseen data.
  
- **Fine-Tuned Models for Specific Tasks**: We plan to **fine-tune** heavier LLMs on **domain-specific** data (e.g., **Named Entity Recognition**, **sentiment analysis**, and **language translation**). This will allow the hybrid model to handle specific tasks more effectively, making it more optimized for real-world scenarios.

### **3. Integration of Pretrained Models**
Exploring **pretrained models** for tasks like **NER** or **language translation** will boost accuracy in those areas. Integrating these models into the hybrid framework will improve overall performance in specific domains.

### **4. Further Prompt Engineering and Temperature Tuning**
By refining **prompt engineering** for LLMs, we can guide models to produce more precise and relevant outputs. Additionally, experimenting with **temperature settings** will allow for better control over model behavior, balancing **deterministic outputs** and **creative variations**.

### **5. Scaling for Larger Datasets**
Expanding our dataset and testing the scalability of these approaches on larger data will be key to evaluating real-time feasibility and ensuring the methods hold up in production environments.

## Conclusion

This project demonstrates that **hybrid models**, particularly those combining **rule-based systems** and **LLMs**, provide the most reliable results for **text normalization** and **composition writer information prediction**. The **Conditional Hybrid** approach strikes the best balance between **accuracy** and **execution time**, making it ideal for complex text tasks.

Future work will focus on leveraging **heavier LLMs**, **ensemble learning**, **fine-tuning** for domain-specific tasks, and scaling to larger datasets. These developments will help further enhance the performance and scalability of our models for real-world applications.

After all the experiments and computational gymnastics performed, it turns out that *GPT-4o mini* only costs **X euros** to run... Well, if we don't count all the coffee and computational resources, that is! 😄
