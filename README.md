# Federated Anomaly Detection In Network Logs With Zero Trust Enforcements

## About

This project implements a privacy-preserving **Federated Learning (FL)** framework for network anomaly detection using the **UNSW-NB15** dataset.
Instead of centralizing raw network traffic logs—which poses privacy, compliance, and security risks—the system trains models locally on distributed nodes and shares only model outputs.

The goal is to create a scalable, secure, privacy-aware anomaly detection engine that fits modern **Zero Trust Architecture (ZTA)** principles.

Traditional NIDS pipelines rely on collecting packet data from all clients, leading to overhead and exposure of sensitive information. This project eliminates that dependency using federated anomaly detection.

---

## Features

* Six centralized baseline ML models:

  * **Supervised:** XGBoost, MLP, Random Forest
  * **Unsupervised:** Autoencoder, Isolation Forest, One-Class SVM
* Fully simulated **Federated Learning** pipeline across 3 clients
* **FedAvg-style** aggregation of Isolation Forest anomaly scores
* No raw data ever leaves the client (full data privacy)
* Real-time anomaly scoring for **Zero Trust policy decisions**
* Scales to IoT, Edge, and multi-branch environments

---

## Requirements

### **System Requirements**

* Windows 10/11 or Ubuntu (64-bit recommended)
* Python **3.8+**

### **Libraries**

* `numpy`, `pandas`
* `scikit-learn`
* `xgboost`
* `tensorflow` / `keras` (for Autoencoder, MLP)
* `matplotlib` / `seaborn` *(optional)*

### **Development Tools**

* Jupyter Notebook / VSCode
* Git (version control)
* Optional GPU support for deep learning models

---

## System Architecture

```
        +----------------------+
        |  Central Server      |
        | (Aggregates Scores)  |
        +----------+-----------+
                   ^
                   | FedAvg (scores only)
                   |
     +-------------+-------------+  
     |                           |
+----+-----+               +-----+----+
| Client 1 |               | Client 2  |
| Local IF |               | Local IF  |
+----------+               +-----------+
          \                 /
           \               /
            +-------------+
              Client 3
              Local IF
```

**Pipeline Summary**

1. Preprocess UNSW-NB15 → One-Hot Encode categorical features
2. Train all **centralized baseline models**
3. Split dataset into 3 partitions (clients)
4. Each client trains its own **Isolation Forest**
5. Server aggregates anomaly scores → **Global Federated IF**
6. Score feeds into **Zero Trust access rules**

---

## Output

### **Output 1 – Centralized Model Results**

*(Insert screenshot)*
Performance of MLP, XGBoost, Autoencoder, IF, etc.

### **Output 2 – Federated Learning Results**

*(Insert screenshot)*
Shows score aggregation + global ROC curve.

### **Key Metrics**

| Mode                 | ROC-AUC    | Notes                                    |
| -------------------- | ---------- | ---------------------------------------- |
| **Local-Only**       | **0.8903** | Highest accuracy; no global knowledge    |
| **Centralized**      | **0.8192** | Higher performance, but violates privacy |
| **Federated (F-IF)** | **0.8003** | Full privacy; small accuracy trade-off   |

---

## Results and Impact

This project demonstrates that **high-quality anomaly detection is achievable without centralizing sensitive network logs**. With a federated ROC-AUC of **0.8003**, the system provides reliable threat detection even under strict privacy constraints.

### **Impact Highlights**

* Real-time ZTA trust scoring enables dynamic access decisions
* Prevents data leakage by keeping traffic logs on-device
* Ideal for IoT, Edge, branch offices, and regulated environments
* Forms a strong foundation for future secure FL-NIDS implementations

---

## Articles / References

1. UNSW-NB15 Dataset – Moustafa & Slay (2015)
2. Kairouz et al., *Advances and Open Problems in Federated Learning* (2021)
3. A. A. Bin Zainuddin, *Enhancing IoT Security with ML + Blockchain* (2024)

---
