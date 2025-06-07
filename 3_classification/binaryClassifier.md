A **binary classifier** is a machine learning model that is trained to **predict between two classes** — typically labeled as:

* **1 (positive class)**
* **0 (negative class)**

---

## 🔹 Definition:

A **binary classifier** answers a **yes/no**, **true/false**, or **class A/class B** type of question.

> **Example Questions:**

* Is this email **spam** or **not spam**?
* Is the digit a **5** or **not a 5**?
* Is the tumor **malignant** or **benign**?
* Will the customer **churn** or **stay**?

---

## 🧠 How It Works

### 📥 Input:

* Feature vector (e.g., pixel values, text features, sensor readings)

### ⚙️ Processing:

* The model learns to separate two classes using an algorithm (e.g., logistic regression, SVM, SGD, etc.)

### 📤 Output:

* Usually either:

  * A **binary prediction** (0 or 1)
  * A **probability score** (like 0.87 → likely to be positive)

---

## 🔄 Examples of Binary Classifiers

| Algorithm                         | Type                    |
| --------------------------------- | ----------------------- |
| `LogisticRegression`              | Linear                  |
| `SGDClassifier`                   | Linear (Online)         |
| `SVC` (with linear or RBF kernel) | Support Vector Machines |
| `RandomForestClassifier`          | Ensemble                |
| `KNeighborsClassifier`            | Non-parametric          |
| Neural networks                   | Deep learning           |

---

## 🧪 Training a Binary Classifier Involves:

1. **Labeling** the data as 1s and 0s
2. **Feeding** the labeled data to a classifier
3. **Evaluating** performance using:

   * Accuracy (for balanced data)
   * Precision, recall, F1-score (for imbalanced data)
   * ROC curve and AUC

---

## 🔍 Binary vs. Other Classification Types

| Type                      | Classes                | Example                               |
| ------------------------- | ---------------------- | ------------------------------------- |
| Binary classification     | 2                      | Spam vs. Not Spam                     |
| Multiclass classification | >2                     | Classify digits (0 to 9)              |
| Multilabel classification | Multiple binary labels | Detect emotions: \[happy, sad, angry] |

---

## 🎯 Objective of This Section

You learn to train a **binary classifier**: a model that decides whether an image is a particular class or not.
In this case, the task is:
**“Is this digit a 5 or not?”**

---

## 📥 Step 1: Load and Prepare the MNIST Data

```python
from sklearn.datasets import fetch_openml
mnist = fetch_openml('mnist_784', version=1, as_frame=False)
X, y = mnist.data, mnist.target.astype(int)
```

* `X`: Shape `(70000, 784)` — flattened 28×28 grayscale images
* `y`: Shape `(70000,)` — string labels → converted to integers with `.astype(int)`

---

## 🏷️ Step 2: Create the Target Vector for Binary Classification

The goal is to detect whether the digit is a **5** or not.

```python
y_binary = (y == 5)  # True for 5, False for all other digits
```

This gives a binary target:

* `True` (or `1`) for 5s
* `False` (or `0`) for all others

---

## 🔀 Step 3: Split the Dataset

To simulate real-world usage, you split the dataset into:

* Training set: 60,000 images
* Test set: 10,000 images

```python
X_train, X_test = X[:60000], X[60000:]
y_train, y_test = y_binary[:60000], y_binary[60000:]
```

---

## ⚙️ Step 4: Train the Binary Classifier with SGD

Use **Stochastic Gradient Descent (SGD)** because:

* It’s efficient with large datasets
* It supports online learning

```python
from sklearn.linear_model import SGDClassifier

sgd_clf = SGDClassifier(random_state=42)
sgd_clf.fit(X_train, y_train)
```

Now you have a trained model that can classify whether a digit is **5** or not.

---

## ✅ Step 5: Make Predictions

```python
sgd_clf.predict([X[0]])
```

This returns:

* `True` → model thinks it’s a 5
* `False` → model thinks it’s not a 5

---

## ❌ Step 6: Accuracy Isn’t Enough

Imagine only 10% of digits are 5s. A **dumb model** that always predicts "Not 5" will still be **90% accurate**!

So the book introduces better performance measures:

* **Confusion matrix**
* **Precision**
* **Recall**
* **F1 score**
* **ROC curve**

These are discussed in the next section: **Measuring Performance**.

---

## 📌 Summary

| Step           | Description                                          |
| -------------- | ---------------------------------------------------- |
| Load data      | Use `fetch_openml("mnist_784")`                      |
| Define task    | Binary classification: 5 vs. not-5                   |
| Prepare labels | `y_binary = (y == 5)`                                |
| Train model    | `SGDClassifier.fit()`                                |
| Predict        | `predict()` on test or training samples              |
| Learn          | Accuracy isn’t enough — need precision, recall, etc. |

---
