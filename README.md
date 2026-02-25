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

# 🧠 Key Contributions

This thesis introduces:

### Two-Phase Deep Learning Framework

Combining categorization and matching for improved accuracy

### Hard-Mining Strategy

Improves training data quality

### Real-World Evaluation

Tested on real e-commerce datasets

### Model Comparison

Evaluated:

* Transformers
* Siamese Networks
* Sentence Embeddings
* Large Language Models

### Efficient Production-Ready Solution

DistilBERT provides best performance-cost balance 

---

# 📁 Repository Structure

```
notebooks/

hard_mining.ipynb
product_categorization.ipynb
product_matching.ipynb

data/

raw/
processed/

images/

README.md
```

---

# 🎯 Real-World Applications

This system can be used in:

E-commerce platforms
Price comparison websites
Product recommendation systems
Catalog management systems

---
