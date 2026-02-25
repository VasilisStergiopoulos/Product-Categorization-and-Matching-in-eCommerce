# 🧠 Product Categorization & Matching using Transformer Models

### MSc Data Science Thesis — Two-Phase Deep Learning Framework for e-Commerce

📍 Author: **Vasileios Stergiopoulos**  
🎓 MSc in Data Science — School of Science & Technology  
📅 July 2025  

---

# 📌 Overview

Modern e-commerce platforms aggregate millions of product listings from different vendors. However, the same product is often described differently, creating inconsistent and duplicate records.

This project presents a **two-phase Deep Learning framework** that automatically:

1. **Categorizes products into predefined categories**
2. **Matches listings referring to the same real-world product**

This pipeline enables Product Comparison Platforms to maintain clean, structured, and reliable product catalogs while reducing manual effort. 

---

# 🚀 Key Results

| Task                   | Best Model | Accuracy | F1 Score |
| ---------------------- | ---------- | -------- | -------- |
| Product Categorization | DistilBERT | 99%      | 99%      |
| Product Matching       | DistilBERT | 96%      | 95%      |

DistilBERT achieved the best trade-off between:

* Performance
* Training time
* Computational cost

Making it ideal for real-world deployment.

---

# 🏗️ Framework Architecture

The system consists of two sequential phases:

```
Raw Product Titles
        │
        ▼
Phase 1: Product Categorization
(BERT-based classifier)
        │
        ▼
Grouped Products by Category
        │
        ▼
Phase 2: Product Matching
(Hard-Mining + Binary Classifier)
        │
        ▼
Matched Product Entities
```

Product Categorization acts as a **blocking strategy**, reducing computational complexity and improving matching accuracy. 

---

# 📂 Dataset

Source: **PriceRunner Mobile Phones dataset**

Contains:

* ~4,300 product titles
* Multiple vendors
* Cluster labels indicating identical products

Key dataset characteristics:

* Multiple titles per product
* High textual variation
* Noisy real-world labels requiring manual cleaning 

Example:

| Vendor Title                       | Actual Product          |
| ---------------------------------- | ----------------------- |
| iPhone 16 Pro Max 256GB            | Apple iPhone 16 Pro Max |
| Apple iPhone 16 Pro Max 5G 8GB RAM | Apple iPhone 16 Pro Max |

Challenges:

* High textual variation
* Missing attributes
* Vendor inconsistencies
* Annotation errors

---

# 🧹 Data Cleaning & Preparation

Manual inspection revealed:

* Incorrect cluster assignments
* Non-mobile products inside dataset
* Duplicate and noisy titles

These errors were manually corrected to improve model performance. 

---

# ⚒️ Hard-Mining Strategy

Product Matching requires labeled pairs.

This project introduces a **Hard-Mining sampling strategy**, selecting:

### Positive pairs

* Hard positives → least similar titles in same cluster
* Random positives → random titles in same cluster

### Negative pairs

* Hard negatives → most similar titles from different clusters
* Random negatives → random titles from different clusters

This improves the model’s ability to learn subtle differences. 

---

# 🤖 Models Implemented

## Product Categorization Models

Transformer classifiers:

* BERT
* RoBERTa
* DeBERTa
* DistilBERT

Architecture:

```
[CLS] Product Title → Transformer → Classification Head → Category
```

---

## Product Matching Models

Multiple architectures evaluated:

### Transformer Models

* BERT
* RoBERTa
* DeBERTa
* DistilBERT

### Neural Network

* Siamese LSTM

### Embedding Models

* Sentence-BERT

### Large Language Models

* GPT-4 (Zero-Shot Classification)

Each model predicts:

```
Product A [SEP] Product B → Match / No Match
```

---

# 🏆 Best Model: DistilBERT

DistilBERT achieved:

* High accuracy
* Fast training
* Lower computational cost

Making it ideal for real-world deployment. 

---

# 📊 Main Results

## Total Training Time per Model and Maximum Length in Product Matching

<p align="center">
  <img src="results/Product Matching/total-training-time-per-model-and-max-len.png" width="700">
</p>

---

## Comparative Analysis in Product Matching 

<p align="center">
  <img src="results/Product Matching/comparative-analysis.png" width="700">
</p>

---

# 📈 Conclusions
This thesis presented a comprehensive two-phase framework combining Product Categorization and Product Matching to address the challenges of identifying identical products across e-Commerce datasets.

The integration of these two tasks is essential for Product Comparison Platforms, as Product Categorization acts as an effective blocking condition. It organizes incoming product feeds into structured categories, significantly reducing the candidate space for matching and minimizing the workload for human annotators.

---

## Product Categorization

BERT-based models achieved excellent performance in categorizing products in the PriceRunner Aggregate dataset.

This step:

* Improves matching efficiency
* Enables scalable catalog organization
* Enhances real-world usability

Among all evaluated models:

* DistilBERT is recommended as the most efficient model
* It achieved 98.85% F1-score while requiring only 7.8 minutes training time

Although RoBERTa achieved the highest F1-score (99.21%), DistilBERT provides a significantly better balance between performance and efficiency.
RoBERTa is recommended only when maximum accuracy is required and computational resources are not limited.

## Product Matching

A wide range of models were evaluated:

* Transformer-based classifiers
* Siamese LSTM networks
* Sentence-BERT
* Large Language Models (GPT-4 and GPT-4o)

Results showed that:

* RoBERTa, DeBERTa, and DistilBERT achieved the highest performance
* These models performed effectively even on medium-sized datasets

Fine-tuned Sentence-BERT achieved 90% F1-score. This makes it a strong lightweight alternative.
Siamese LSTM networks provided a solid baseline but were outperformed by Transformer models.

## Large Language Models

GPT-4o demonstrated strong zero-shot performance:

* F1 Score: 0.8687
* Cost: $0.23 for 1210 product pairs

This highlights their potential when labeled data is limited.

## Overall Recommendation

Considering both performance and efficiency, DistilBERT is the recommended model for the proposed framework.

It provides:

* High accuracy
* Fast training
* Low computational cost
* Excellent scalability

## Final Conclusion

This thesis demonstrates that combining Product Categorization and Product Matching using efficient Transformer-based models provides a highly accurate, scalable, and cost-effective solution for real-world product identification.
This framework enables automation of product catalog management and significantly reduces redundant comparisons.
