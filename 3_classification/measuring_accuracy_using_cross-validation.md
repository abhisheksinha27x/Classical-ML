
# 📏 Measuring Accuracy Using Cross-Validation

In the previous steps, you trained a binary classifier to detect whether an image is a **5** or not. Now you want to **evaluate** how well your model performs.

> Evaluating a model means measuring how well our trained machine learning model performs -- usually on unseen data.

---


## ❓ Why Not Just Use `model.score(X_test, y_test)`?

Because:

* It tests performance **only on one split**.
* You risk **overfitting to that specific test set**.
* You may get **unreliable results**, especially with imbalanced classes like digit “5”.

To solve this, we use **cross-validation**.

---

## 🔁 What is Cross-Validation?

**Cross-validation** is a technique to evaluate model performance by **splitting the data multiple times** and averaging the results.

> In **k-fold cross-validation**, the training set is divided into `k` folds:

* Train on `k-1` parts
* Validate on the remaining part
* Repeat `k` times (each fold gets a turn as the validation set)
* Average the results

---

## 📦 Using Scikit-Learn: `cross_val_score`

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import SGDClassifier

sgd_clf = SGDClassifier(random_state=42)

cross_val_score(sgd_clf, X_train, y_train, cv=3, scoring="accuracy")
```

* `cv=3` → 3-fold cross-validation
* `scoring="accuracy"` → metric used to score each fold

#### Example output:

```python
array([0.95035, 0.96035, 0.9604])
```

➡️ This tells us:

* The model is \~95–96% accurate across all three validation folds

---

## ⚠️ Caveat: Class Imbalance Can Trick Accuracy

As mentioned earlier:

* If only 10% of labels are “5”, even a model that **never predicts “5”** can get 90% accuracy.

So here’s a neat trick…

---

## 🧪 Dummy Classifier Test (Sanity Check)

Let’s test a **dumb baseline model**: one that **always predicts “not 5”**.

```python
from sklearn.base import BaseEstimator

class Never5Classifier(BaseEstimator):
    def fit(self, X, y=None):
        return self
    def predict(self, X):
        return np.zeros((len(X),), dtype=bool)

never_5_clf = Never5Classifier()
cross_val_score(never_5_clf, X_train, y_train, cv=3, scoring="accuracy")
```

#### Output:

```python
array([0.91125, 0.90855, 0.90915])
```

➡️ Even this **dumb model** gets \~91% accuracy — because 5s are rare!

---

## ✅ What This Proves

* Accuracy alone is misleading with **imbalanced data**.
* A better model like `SGDClassifier` (\~95%) clearly outperforms the dumb one (\~91%), but we wouldn't know this without **cross-validation**.

---

## 📌 Summary

| Concept                     | Purpose                                      |
| --------------------------- | -------------------------------------------- |
| `cross_val_score()`         | Measures model performance reliably          |
| Dummy classifier (`Never5`) | Sanity check for class imbalance             |
| Accuracy ≠ enough           | Use with confusion matrix, precision, recall |

---

## 🧠 Key Takeaway

> Always **validate your model with cross-validation**, especially when class distribution is skewed. Then move to **precision, recall, and F1 score** for deeper evaluation.

---

## 🧩 What Is `StratifiedKFold`?

### ➤ It's a **cross-validation splitter** that **preserves the class proportions** (i.e., the target label distribution) in each fold.

---

## 🔍 Why Use StratifiedKFold?

In regular `KFold`, the data is split **randomly**, which can cause **class imbalance** in the folds.

> This is a problem when:

* You have **rare classes** (like digit "5" in MNIST)
* One fold might contain **more positives than others**, skewing metrics

---

### ✅ Example:

Imagine your training data has:

* 90% “not 5”
* 10% “is 5”

If you use regular `KFold`, a fold might get **8%** “is 5”, another \*\*12%”, etc.

With **StratifiedKFold**, **each fold gets 10% “is 5”**, preserving the original distribution.

---

## 🛠️ How to Use It in Scikit-Learn

```python
from sklearn.model_selection import StratifiedKFold
from sklearn.base import clone
from sklearn.metrics import accuracy_score

skfolds = StratifiedKFold(n_splits=3, shuffle=True, random_state=42)

for train_index, test_index in skfolds.split(X, y):
    clone_clf = clone(sgd_clf)  # Create a fresh copy of the classifier
    X_train_folds = X[train_index]
    y_train_folds = y[train_index]
    X_test_fold = X[test_index]
    y_test_fold = y[test_index]

    clone_clf.fit(X_train_folds, y_train_folds)
    y_pred = clone_clf.predict(X_test_fold)
    acc = accuracy_score(y_test_fold, y_pred)
    print("Fold accuracy:", acc)
```

---

### 🧠 What's Happening Here?

* `StratifiedKFold.split(X, y)` returns indices for each fold.
* `clone(sgd_clf)` ensures we start with a fresh model each time.
* We train on `k-1` folds and evaluate on the remaining fold.
* Accuracy is computed for each fold and printed.

---

## 🧪 When Should You Use It?

| Scenario                           | Use `StratifiedKFold`?           |
| ---------------------------------- | -------------------------------- |
| Class imbalance (e.g. 10% class 1) | ✅ Yes                            |
| Balanced classes                   | Optional (but still good)        |
| Multiclass classification          | ✅ Yes (it stratifies all labels) |

---

## ✅ Summary

| Feature     | Value                                       |
| ----------- | ------------------------------------------- |
| What        | Cross-validator that preserves label ratios |
| When to use | Anytime you have imbalanced data            |
| Benefit     | Fairer, more reliable performance estimates |

---

## 📦 Also Available:

If you want a **shortcut**, Scikit-Learn’s `cross_val_score()` uses `StratifiedKFold` **by default for classification problems**:

```python
from sklearn.model_selection import cross_val_score
cross_val_score(sgd_clf, X, y, cv=3, scoring="accuracy")
```

So unless you manually change it, you’re already getting the benefit of stratification.

---
