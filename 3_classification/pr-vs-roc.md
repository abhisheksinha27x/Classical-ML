The **ROC curve** and the **Precision/Recall (PR) curve** are both used to evaluate binary classifiers, especially when analyzing how they behave at **different thresholds**.

But they are **not interchangeable**, and choosing the right one depends on **your problem**, especially the **class imbalance** and **what you care about most** (false positives vs false negatives).

---

## ⚖️ Quick Comparison Table

| Criterion           | **ROC Curve**                                  | **Precision/Recall Curve**                                             |
| ------------------- | ---------------------------------------------- | ---------------------------------------------------------------------- |
| **Y-axis**          | True Positive Rate (Recall)                    | Precision                                                              |
| **X-axis**          | False Positive Rate                            | Recall                                                                 |
| **Focus**           | Balance between TPR and FPR                    | Focus on actual positive predictions                                   |
| **Best for**        | Balanced class distribution                    | Imbalanced datasets (e.g. rare events)                                 |
| **Misleading when** | Dataset is imbalanced                          | Generally more informative in imbalanced cases                         |
| **Preferred when**  | You want to understand **ranking performance** | You want to focus on **false positives vs false negatives** trade-offs |

---

## 🎯 When to Use ROC Curve

Use **ROC** if:

* Your **positive and negative classes are roughly balanced**
* You care about how well the model **ranks** positives over negatives overall
* You want a **general measure** of classifier performance (like ROC AUC)

### Example:

Email spam detection where spam and non-spam are roughly equal in volume.

---

## 🎯 When to Use Precision/Recall Curve

Use **PR Curve** if:

* You have a **highly imbalanced dataset** (e.g., 1% positive, 99% negative)
* You're more interested in the **quality of positive predictions** than overall accuracy
* You care a lot about **false positives** or **false negatives**

### Example:

* Medical diagnosis (few people have the disease — you want high recall and high precision)
* Fraud detection (fraud is rare)

---

## 📌 Why ROC Can Be Misleading with Imbalanced Data

In imbalanced datasets:

* The **false positive rate (FPR)** can be **very small** even if you have a lot of false positives (because the denominator TN is huge).
* This makes the **ROC curve look deceptively good**.

But **precision** will drop noticeably if your model makes many false positives — so the **PR curve will catch it**.

---

## ✅ Final Recommendation

| Scenario                                                    | Use...                     |
| ----------------------------------------------------------- | -------------------------- |
| Balanced classes                                            | **ROC Curve**              |
| Imbalanced classes (rare positive class)                    | **Precision/Recall Curve** |
| You care more about **ranking quality**                     | **ROC**                    |
| You care more about **correctness of positive predictions** | **PR Curve**               |

---
