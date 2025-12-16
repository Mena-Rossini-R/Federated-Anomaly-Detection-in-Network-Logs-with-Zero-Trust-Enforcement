## 🔹 Overall Performance Summary of FIF-Based Hybrid Models

| Model                         | ROC-AUC    | Accuracy   | Precision  | Recall (TPR) | F1-Score   | FPR        | FNR        | Key Observations                                                            | Why It Underperformed                                                       |
| ----------------------------- | ---------- | ---------- | ---------- | ------------ | ---------- | ---------- | ---------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **F-IF + Autoencoder (AE)**   | **0.9439** | **0.9925** | **0.8182** | **0.8182**   | **0.8182** | **0.0038** | **0.1818** | Best overall performance; strong detection capability with low false alarms | — *(Best-performing model)*                                                 |
| **F-IF + Decision Tree (DT)** | 0.8440     | 0.9854     | 0.8824     | 0.4688       | 0.6122     | 0.0016     | 0.5312     | Good precision and low FPR; moderate attack detection                       | Struggles with generalization and subtle attack patterns due to hard splits |
| **F-IF + OC-SVM**             | 0.8479     | 0.9864     | 0.9091     | 0.4545       | 0.6061     | 0.0011     | 0.5455     | Very conservative model; excellent normal classification                    | One-class boundary too strict, leading to high missed attacks               |
| **F-IF + GBM**                | 0.7623     | 0.9833     | 0.8378     | 0.3196       | 0.4627     | 0.0014     | 0.6804     | High accuracy but weak anomaly recall                                       | Boosting favors majority (normal) class due to class imbalance              |
| **F-IF + K-Means**            | 0.7830     | 0.9782     | 0.5000     | 0.2222       | 0.3077     | 0.0050     | 0.7778     | Captures normal behavior well                                               | Assumes spherical clusters and fails to model complex attack distributions  |

---

###  Why Some Models Failed to Detect Attacks Effectively

* **Clustering-based models (K-Means)** assume simple distance-based separations and fail when attack patterns overlap with normal traffic.
* **One-Class models (OC-SVM)** prioritize minimizing false positives, which results in overly tight decision boundaries and high false negative rates.
* **Tree-based models (Decision Tree, GBM)** struggle with highly imbalanced intrusion datasets, biasing predictions toward normal traffic.
* **Boosting models (GBM)** amplify dominant class patterns, reducing sensitivity to rare attack instances.

###  Why Autoencoder Outperformed Others

> The Autoencoder effectively learns a compact representation of normal traffic and detects anomalies based on reconstruction error, enabling superior generalization to unseen and subtle attack patterns.

---

