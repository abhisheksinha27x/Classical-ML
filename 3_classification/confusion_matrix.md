
# 📊 What Is a Confusion Matrix?

### ✅ **General Idea:**

> A **confusion matrix** is a table that helps you understand how well a **classifier is performing** — by showing where it's getting things right **and** where it's making mistakes.

It **compares the actual labels vs. the predicted labels**.

---

## 🤔 Why Use a Confusion Matrix?

Because just looking at **accuracy** is often misleading — especially when classes are **imbalanced** (like detecting rare diseases or digit "5").

The confusion matrix tells you:

* **What kind of errors** your model is making
* **How many of each type of error**
* Whether it's **good at finding the positive class**

---

# 🧮 How to Compute a Confusion Matrix

### For a **binary classifier** (e.g., detecting “5” or “not 5”), the confusion matrix looks like this:

|                     | **Predicted: No (0)** | **Predicted: Yes (1)** |
| ------------------- | --------------------- | ---------------------- |
| **Actual: No (0)**  | True Negatives (TN)   | False Positives (FP)   |
| **Actual: Yes (1)** | False Negatives (FN)  | True Positives (TP)    |

Let’s break that down:

* **True Positive (TP)**: Model correctly predicts “yes” (e.g., “It is a 5” and it really is).
* **True Negative (TN)**: Model correctly predicts “no” (e.g., “Not a 5” and it isn’t).
* **False Positive (FP)**: Model predicts “yes” when it’s actually “no” (aka a **false alarm**).
* **False Negative (FN)**: Model predicts “no” when it’s actually “yes” (aka a **miss**).

---

## 🔢 How to Generate It in Code

```python
from sklearn.metrics import confusion_matrix

y_train_pred = sgd_clf.predict(X_train)
confusion_matrix(y_train_5, y_train_pred)
```

This compares:

* `y_train_5`: the **true labels**
* `y_train_pred`: your **model’s predictions**

### Sample Output:

```
array([[53892,   687],
       [ 1891,  3530]])
```

Interpretation:

* 53892 = TN
* 687   = FP
* 1891  = FN
* 3530  = TP

---

## 📈 What Does It Tell You?

From the matrix, you can compute:

* **Accuracy** = (TP + TN) / Total
* **Precision** = TP / (TP + FP) → *How many predicted “yes” are correct*
* **Recall** = TP / (TP + FN) → *How many actual “yes” were caught*
* **F1 Score** = Balance between precision and recall

---

## 📦 Visual Recap

```
                  Predicted
                0          1
Actual  0    [ TN        FP ]
        1    [ FN        TP ]
```

The diagonals (TN and TP) are **correct predictions**.
The off-diagonals (FP and FN) are **mistakes**.

---

## 🧠 Summary

| Metric           | Meaning                                       |
| ---------------- | --------------------------------------------- |
| Confusion Matrix | Full breakdown of predictions vs reality      |
| TP, TN, FP, FN   | Help you compute other performance metrics    |
| Best Use Case    | When accuracy is misleading (imbalanced data) |
| Computed using   | `confusion_matrix(y_true, y_pred)`            |

---
