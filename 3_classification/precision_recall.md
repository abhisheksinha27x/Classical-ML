

## 🎯 1. Precision

### Definition:

> **Precision** tells you **how many of the items your model marked as positive are actually positive**.

### Formula:

$$
\text{Precision} = \frac{TP}{TP + FP}
$$

* **TP**: True Positives = model correctly predicted positive
* **FP**: False Positives = model predicted positive, but it was actually negative

### Example:

Imagine your model predicts whether an email is spam:

* **100 emails predicted as spam**
* **90 of them were actually spam**
  → So precision = 90 / 100 = **0.90 (90%)**

🔍 **High precision** means **low false positives**.

---

## 🔍 2. Recall (Sensitivity, True Positive Rate)

### Definition:

> **Recall** tells you **how many of the actual positive items your model was able to catch**.

### Formula:

$$
\text{Recall} = \frac{TP}{TP + FN}
$$

* **FN**: False Negatives = model predicted negative, but it was actually positive

### Example:

Suppose there are **100 spam emails in your inbox**:

* Your model correctly detects **80** of them
  → Recall = 80 / 100 = **0.80 (80%)**

🔍 **High recall** means **low false negatives**.

---

## ⚖️ 3. Precision vs. Recall Trade-Off

You often **can’t maximize both**.

* If you **increase precision**, you may miss some actual positives → **lower recall**
* If you **increase recall**, you may include more false positives → **lower precision**

### Example:

| Model says spam if score > X | Precision | Recall |
| ---------------------------- | --------- | ------ |
| Score > 0.9 (strict)         | High      | Low    |
| Score > 0.3 (lenient)        | Low       | High   |

---

## 🔁 4. F1 Score — The Balance

### Definition:

> **F1 Score** is the **harmonic mean** of precision and recall.
> It gives a **balanced measure** when both precision and recall matter.

### Formula:

$$
\text{F1} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}
$$

### Why Harmonic Mean?

* It penalizes extreme differences.
* If either precision or recall is **very low**, F1 score will also be low.

---

## 🔢 Example Walkthrough:

Let’s say:

* **Precision = 0.8**
* **Recall = 0.6**

$$
\text{F1} = 2 \cdot \frac{0.8 \cdot 0.6}{0.8 + 0.6} = \frac{0.96}{1.4} ≈ 0.686
$$

So F1 score = **68.6%**, which reflects the **balance**.

---

## 🧠 When to Use What?

| Metric    | Use When...                                                                   |
| --------- | ----------------------------------------------------------------------------- |
| Precision | You want to avoid false positives (e.g., spam filters, cancer diagnosis)      |
| Recall    | You want to catch as many positives as possible (e.g., crime/fraud detection) |
| F1 Score  | You need a **balanced view**, especially with **imbalanced classes**          |

---

## 🛠️ In Scikit-Learn

```python
from sklearn.metrics import precision_score, recall_score, f1_score

precision_score(y_true, y_pred)
recall_score(y_true, y_pred)
f1_score(y_true, y_pred)
```

---

## 🧾 Summary Table

| Metric    | Formula                | Tells You                                         |
| --------- | ---------------------- | ------------------------------------------------- |
| Precision | TP / (TP + FP)         | Of all predicted positives, how many were correct |
| Recall    | TP / (TP + FN)         | Of all actual positives, how many did you find    |
| F1 Score  | Harmonic mean of P & R | Balanced performance when both are important      |

---


# ⚖️ What Is the Precision/Recall Trade-Off?

> **You can't make your model perfect in both precision and recall at the same time.**
> If you try to make **precision better**, your **recall gets worse**, and if you try to make **recall better**, your **precision gets worse**.

This is like a **see-saw** — as one goes up, the other usually goes down.

---

## 🎯 Let’s First Recall:

* **Precision** = "Of the things I said were good (positive), how many were actually good?"
* **Recall** = "Of all the good things out there, how many did I find?"

---

## ✅ Real-Life Example 1: Safe Videos for Kids

You have a model that marks videos as “safe for kids.”

### ❗ Goal: You **don’t want to accidentally show any bad content**.

So, you care more about **precision**.

* It's **okay to miss some good videos** (low recall),
* But it's **not okay to show even one bad video** (so precision must be very high).

> Think: **Better safe than sorry**.

You might even add a **human reviewer** to double-check just to be sure.

---

## ✅ Real-Life Example 2: Detecting Shoplifters

You're training a system to detect shoplifters using cameras.

### ❗ Goal: You want to **catch all shoplifters**.

So, you care more about **recall**.

* Even if your system makes a few false accusations (low precision),
* It’s fine — because a guard can check before taking action.

> Think: **Catch all possible threats**, even if it means some false alarms.

---

## 🧮 Why Can't We Have Both?

Let’s say your model is trying to decide if something is “positive” (e.g., a video is safe or someone is a shoplifter) based on a **confidence score** from 0 to 1.

* If you set a **high threshold** (only mark things as positive when you're really sure):

  * ➕ Precision goes **up** (fewer false positives)
  * ➖ Recall goes **down** (you miss many actual positives)

* If you set a **low threshold** (mark things positive even when unsure):

  * ➕ Recall goes **up** (you catch more positives)
  * ➖ Precision goes **down** (more false positives)

---

## ⚖️ So the Trade-Off Is:

| If you want...     | You’ll get...          | But you sacrifice...                         |
| ------------------ | ---------------------- | -------------------------------------------- |
| **High precision** | Fewer false positives  | You’ll miss some real positives (low recall) |
| **High recall**    | Fewer missed positives | More false positives (low precision)         |

---

## 🎓 That’s Why We Choose Based on the Problem

* If **mistakes are costly**, go for **high precision**
* If **missing positives is costly**, go for **high recall**
* If you want a **balance**, use the **F1 score**

---
