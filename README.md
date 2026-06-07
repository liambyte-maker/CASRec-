# CASRec: Confidence-Aware SASRec for Cold-Start Sequential Recommendation

## Overview

CASRec (Confidence-Aware SASRec) is a cold-start enhanced sequential recommendation framework built upon SASRec.

Traditional SASRec relies heavily on Item ID Embeddings. While popular items receive sufficient training signals, cold-start and long-tail items often suffer from poorly trained embeddings due to sparse interactions.

To address this issue, CASRec introduces a confidence-aware mechanism that dynamically balances Item ID representations and feature-based representations according to their reliability.

---

## Model Architecture

![CASRec Architecture](figures/casrec_architecture.png)

### Architecture Overview

CASRec consists of three key components:

* **Multi-Factor Confidence Network**: Estimates the reliability of Item ID Embeddings using interaction frequency, CTR, popularity, item age, and content quality signals.
* **Confidence-Aware Adaptive Fusion**: Dynamically combines ID Embeddings and Feature Embeddings according to the learned confidence score.
* **SASRec Encoder**: Models user behavior sequences through self-attention and predicts the next item.

### Key Idea

```text
Popular Item
→ Trust ID Embedding

Cold-Start Item
→ Trust Feature Embedding
```

---

## Method

### Multi-Factor Confidence Network

The confidence score is computed as:

```text
g = sigmoid(Wx + b)
```

where:

* g: confidence score
* x: item confidence features
* W, b: learnable parameters

A larger value of g indicates a more reliable Item ID Embedding.

---

### Confidence-Aware Fusion

The final item representation is:

```text
e = g × e_id + (1-g) × e_feat
```

where:

* e_id: Item ID Embedding
* e_feat: Feature Embedding

This allows the model to automatically adapt to both popular and cold-start items.

---

### Self-Attention

SASRec captures user interests through self-attention:

```text
Attention(Q,K,V) = softmax(QK^T / √d)V
```

The self-attention mechanism models both short-term and long-term user preferences.

---

## Training Objective

CASRec follows the original SASRec training strategy and uses Binary Cross Entropy (BCE) loss:

```text
L = -y log(ŷ) - (1-y) log(1-ŷ)
```

where:

* y: ground-truth label
* ŷ: predicted click probability

The objective is to assign higher probabilities to positive interactions and lower probabilities to negative interactions.

---

## Datasets

* Amazon Beauty
* Amazon Sports
* MovieLens-1M
* Taobao User Behavior

---

## Evaluation Metrics

* HR@10
* NDCG@10
* Recall@20

---

## Key Contributions

* Reproduced the original SASRec architecture.
* Designed a Multi-Factor Confidence Network for embedding reliability estimation.
* Proposed a Confidence-Aware Adaptive Fusion mechanism.
* Improved cold-start and long-tail recommendation performance.

---

## Tech Stack

* Python
* PyTorch
* Transformer
* SASRec
* NumPy
* Pandas
* Scikit-Learn

---

## Future Work

* [ ] Multimodal Recommendation
* [ ] CLIP-enhanced Item Representation
* [ ] Graph Neural Networks
* [ ] LLM-based Recommendation
* [ ] Agent Recommendation Systems

---

## Author

**Jinming Liu**

### Research Interests

* Recommendation Systems
* Sequential Recommendation
* Cold-Start Recommendation
* Transformer-based Recommenders
* Multimodal Recommendation
