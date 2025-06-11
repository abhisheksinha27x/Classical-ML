

## 🧠 What Is Multiclass Classification?

> **Multiclass classification** is a type of classification task where the goal is to assign an input to **one of three or more classes**.

Unlike:

* **Binary classification** → only 2 possible classes (e.g., cat vs. dog)
* **Multiclass classification** → 3 or more possible, **mutually exclusive** classes (e.g., digits 0–9, flower species, types of fruits)

---

## 🔢 MNIST Dataset as an Example

The **MNIST dataset** is the **perfect example** of a multiclass classification task:

* Each input is a **28x28 grayscale image** of a **handwritten digit**
* The task is to classify the image as **one of 10 digits: 0 through 9**
* So the **number of classes = 10**

Every image belongs to **exactly one** class. There's no overlap — an image is either a "2" or a "5", never both.

---

## 📦 How Does Scikit-Learn Handle Multiclass Classification?

Scikit-learn’s classifiers like `SGDClassifier` are **binary by default**, but they automatically handle multiclass classification using **strategies** behind the scenes:

### 1. **One-vs-All (OvA)** a.k.a. One-vs-Rest:

* Train **one classifier per class**.
* Each classifier distinguishes **"this class" vs. "all others"**.
* At prediction time, each classifier gives a score → the class with the **highest score wins**.

📌 Default strategy in most scikit-learn classifiers.

### 2. **One-vs-One (OvO)**:

* Train one classifier for **every pair of classes**.
* For MNIST (10 classes), that's **45 classifiers** (10 choose 2).
* At prediction time, all classifiers vote, and the most-voted class wins.

📌 Used in `SVC()` (Support Vector Classifier) by default.

---

## ✅ Prediction Example (MNIST)

Let’s say you train a `SGDClassifier` on MNIST:

```python
from sklearn.linear_model import SGDClassifier
sgd_clf = SGDClassifier()
sgd_clf.fit(X_train, y_train)  # y_train contains digits (0 to 9)
```

Now when you run:

```python
sgd_clf.predict([some_digit])
```

Here’s what happens:

* Internally, **10 binary classifiers** are used (One-vs-All).
* Each says how confident it is that the image belongs to its digit.
* The digit with the **highest confidence** is selected as the final prediction.

---

## 🧪 Evaluating Multiclass Performance

You can still use:

* **Accuracy score**
* **Confusion matrix** → but now it’s a **10×10 matrix**
* **Precision / Recall / F1-score per class**

```python
from sklearn.metrics import confusion_matrix, classification_report

y_pred = sgd_clf.predict(X_test)
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

---

## 🎯 Summary

| Concept                       | Meaning                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| **Multiclass Classification** | Predict one of 3+ classes for each input                     |
| **MNIST**                     | Classic 10-class problem (digits 0–9)                        |
| **Strategy (OvA)**            | One classifier per class: "is it this class vs. all others?" |
| **Evaluation**                | Use confusion matrix and per-class precision/recall          |

---

Let's build on the concept of **multiclass classification** using the **MNIST dataset**, and explain how **`OneVsRestClassifier`** (OvR) fits into this process — including **when and why** you would use it.

---

## 🔁 Quick Recap: What is One-vs-Rest (OvR)?

**One-vs-Rest (a.k.a. One-vs-All)** is a strategy for converting a **binary classifier** into a **multiclass classifier**:

* For **K classes**, it trains **K separate binary classifiers**.
* Each classifier is trained to recognize **one class** vs. **all other classes**.

E.g., for MNIST:

* Classifier 0 → “Is this digit a 0?” vs. “Is this *not* a 0?”
* Classifier 1 → “Is this a 1?” vs. “Not a 1?”
* … up to classifier 9.

When predicting:

* All classifiers run in parallel on the input image.
* The classifier with the **highest confidence score** determines the final prediction.

---

## 🧰 What is `OneVsRestClassifier` in Scikit-Learn?

`OneVsRestClassifier` is a **wrapper** in `sklearn.multiclass` that **explicitly** forces this strategy.
It allows **you to wrap any binary classifier** and use it for **multiclass classification**.

> Even though many estimators like `SGDClassifier`, `LogisticRegression`, or `SVC` automatically apply OvR internally, using `OneVsRestClassifier` gives you **explicit control** and **transparency**.

---

### ✅ Example Using `SGDClassifier` with `OneVsRestClassifier` on MNIST:

```python
from sklearn.linear_model import SGDClassifier
from sklearn.multiclass import OneVsRestClassifier

# Wrap the SGDClassifier with OneVsRestClassifier
ovr_clf = OneVsRestClassifier(SGDClassifier(random_state=42))

# Fit on MNIST training data
ovr_clf.fit(X_train, y_train)

# Predict a digit
ovr_clf.predict([X_train[0]])  # Returns the predicted digit (0–9)
```

---

## 📦 What Happens Internally?

This command:

```python
ovr_clf = OneVsRestClassifier(SGDClassifier())
```

* Trains **10 binary classifiers** (for digits 0–9).
* Each is trained using:

  * **Positive samples**: all instances of one digit
  * **Negative samples**: all other digits
* During prediction, all 10 classifiers output a **confidence score**.
* The digit with the **highest score** is the predicted class.

---

## 💡 Why Use `OneVsRestClassifier` Explicitly?

| Use Case                                                  | Why it’s Helpful                                     |
| --------------------------------------------------------- | ---------------------------------------------------- |
| You’re using a **custom binary classifier**               | OvR lets you reuse it for multiclass problems        |
| You want **access to individual classifiers**             | You can inspect or tune each binary model separately |
| You want **full control** over the multiclass strategy    | e.g., try OvR vs. OvO manually                       |
| You want to combine with **pipelines** or **grid search** | OvR works cleanly with Scikit-learn’s tools          |

---

## 🔍 How to Access Scores from Each Classifier

```python
# Get confidence scores for each class
scores = ovr_clf.decision_function([X_train[0]])
print(scores)
```

This returns a list of **10 values**, one per class — the higher the value, the more confident that classifier is. The index with the **highest score** is the predicted digit.

---

## 🧾 Summary

| Term                    | Meaning                                                            |
| ----------------------- | ------------------------------------------------------------------ |
| **One-vs-Rest (OvR)**   | Strategy: one classifier per class vs. rest                        |
| **OneVsRestClassifier** | Scikit-learn tool to implement OvR manually                        |
| **SGDClassifier**       | Linear classifier (supports OvR natively, but can also be wrapped) |
| **Use with MNIST**      | Perfect for digit recognition (10 classes)                         |
| **Benefits**            | Full control, custom tuning, inspect each classifier’s behavior    |

---
