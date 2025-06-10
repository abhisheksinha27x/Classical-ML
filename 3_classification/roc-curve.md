

# 🔍 What is the ROC Curve?

The **ROC (Receiver Operating Characteristic) curve** is a **visual tool** for evaluating the performance of a **binary classifier** across different **thresholds**.

Instead of using a fixed threshold (like 0.5), the ROC curve looks at how the classifier behaves as you adjust the threshold up or down.

---

## 📈 What Does the ROC Curve Plot?

It plots:

* **Y-axis** → **True Positive Rate (TPR)**
  Also known as **Recall** or **Sensitivity**

  $$
  TPR = \frac{TP}{TP + FN}
  $$

  → “Out of all actual positives, how many did we correctly predict?”

* **X-axis** → **False Positive Rate (FPR)**

  $$
  FPR = \frac{FP}{FP + TN}
  $$

  → “Out of all actual negatives, how many did we wrongly predict as positive?”

Now here's the connection:

* **FPR = 1 − Specificity**
* **Specificity (TNR)** = True Negative Rate

  $$
  TNR = \frac{TN}{TN + FP}
  $$

  → “Out of all actual negatives, how many did we correctly predict as negative?”

So the ROC curve essentially plots:

$$
\text{Sensitivity (Recall)} \quad \text{vs.} \quad 1 - \text{Specificity}
$$

---

## 🎯 What Does the ROC Curve Tell Us?

By plotting **TPR vs. FPR** at **every possible threshold**, we see:

* How well the model separates positives from negatives
* The **trade-off** between catching positives and avoiding false alarms

---

## 🧠 Interpreting the ROC Curve

* A **perfect classifier** hugs the **top-left** corner (TPR = 1, FPR = 0)
* A **random classifier** forms a **diagonal line** from (0,0) to (1,1)
* The **closer the curve is to the top-left**, the better the model

---

## 🧮 ROC AUC Score

* **AUC** = Area Under the ROC Curve
* Ranges from **0.5** (bad) to **1.0** (perfect)
* Higher = better classification performance

```python
from sklearn.metrics import roc_curve, roc_auc_score

y_scores = model.decision_function(X_test)
fpr, tpr, thresholds = roc_curve(y_test, y_scores)
auc_score = roc_auc_score(y_test, y_scores)
```

---

## ✅ When to Use the ROC Curve

| Use ROC Curve When…                        | Prefer Precision/Recall Curve When…                 |
| ------------------------------------------ | --------------------------------------------------- |
| Classes are **balanced**                   | Classes are **highly imbalanced**                   |
| You want to see **model behavior overall** | You care deeply about **false positives/negatives** |

---

## 🧾 Final Summary

| Term                    | Meaning                                    |
| ----------------------- | ------------------------------------------ |
| **True Positive Rate**  | Recall/Sensitivity = TP / (TP + FN)        |
| **False Positive Rate** | 1 – Specificity = FP / (FP + TN)           |
| **ROC Curve**           | Graph of TPR vs. FPR at all thresholds     |
| **ROC AUC Score**       | Area under the ROC curve (higher = better) |

---
