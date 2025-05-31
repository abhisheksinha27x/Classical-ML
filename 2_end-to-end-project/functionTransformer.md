

## 🔄 **What Is `FunctionTransformer`?**

`FunctionTransformer` is a **scikit-learn transformer** that lets you **wrap any Python function** into a transformer object — **without writing a full class**.

It’s perfect when you want to:

* Apply a quick transformation (e.g., `np.log`, `np.sqrt`, etc.)
* Use a lambda or function in a pipeline

---

### ✅ Example: Apply `log1p` to a feature

```python
from sklearn.preprocessing import FunctionTransformer
import numpy as np

log_transformer = FunctionTransformer(np.log1p, validate=True)

X_transformed = log_transformer.fit_transform(X)
```

* `np.log1p(x)` is `log(1 + x)` (safe for zero/positive values)
* `validate=True` ensures input is array-like (ensures 2D if needed)

---

## 🛠️ How to Write a Custom Class Instead

Instead of `FunctionTransformer`, you can define your **own transformer class**.

Here’s a simple custom version that mimics what `FunctionTransformer` does:

```python
class MyLogTransformer:
    def fit(self, X, y=None):
        return self
    
    def transform(self, X):
        return np.log1p(X)
```

### 🧠 Why No Inheritance?

This class **does not inherit** from `BaseEstimator` or `TransformerMixin`.

Why does this still work?

---

## 🦆 Duck Typing in Python 🦆

> **“If it looks like a duck and quacks like a duck, it’s a duck.”**

* In Python, objects don’t need to inherit from a specific base class.
* If an object **implements the methods** that are expected (like `.fit()` and `.transform()`), it will work **as if** it were a scikit-learn transformer.

That's duck typing: **type behavior > class hierarchy**.

---

## 🧪 What Happens If You Inherit from `BaseEstimator` and `TransformerMixin`?

### `BaseEstimator` gives you:

* `get_params()` and `set_params()` for hyperparameter tuning (e.g., in `GridSearchCV`)
* Auto `__repr__` that prints readable model info

### `TransformerMixin` gives you:

* A default `.fit_transform()` implementation (so you don’t need to define it)

---

### ✅ Updated Example With Inheritance

```python
from sklearn.base import BaseEstimator, TransformerMixin
import numpy as np

class MyLogTransformer(BaseEstimator, TransformerMixin):
    def fit(self, X, y=None):
        return self
    
    def transform(self, X):
        return np.log1p(X)
```

Now it's:

* Pipeline-compatible ✅
* GridSearch-compatible ✅
* Cleaner and more flexible ✅

---

## 🧠 Summary

| Feature                         | No Base Class   | With BaseEstimator + TransformerMixin |
| ------------------------------- | --------------- | ------------------------------------- |
| Works in Pipelines              | ✅ (duck typing) | ✅                                     |
| Hyperparameter tuning           | ❌               | ✅                                     |
| `fit_transform()` shortcut      | ❌               | ✅                                     |
| Readable `__repr__`             | ❌               | ✅                                     |
| Good practice for real projects | ❌               | ✅ ✅ ✅                                 |

---

## 🚀 When to Use What?

| Situation                          | Use                                                   |
| ---------------------------------- | ----------------------------------------------------- |
| Quick function (log, square, etc.) | `FunctionTransformer`                                 |
| Reusable logic, with parameters    | Custom class with `BaseEstimator`, `TransformerMixin` |
| Testing ideas                      | Either                                                |

---
