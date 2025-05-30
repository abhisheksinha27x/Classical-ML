
---

## 🔧 What is an Estimator 

In **Scikit-Learn**, an **estimator** is a **class** or **object** that **learns from data** using a `.fit()` method.

### 👉 Think of it like this:

An estimator is a **recipe** or **tool** that:

1. **Takes input data** (via `.fit()`).
2. **Learns something** from that data (like parameters, categories, mean/std).
3. **Uses that learning** to either:

   * Make **predictions** (if it’s a predictor),
   * **Transform** data (if it’s a transformer),
   * Or both (in some cases).

---

## 📂 Two Categories of Estimators

### 1. **Predictors**

* **Used for supervised learning** (classification or regression).
* Must implement:

  * `.fit(X, y)`
  * `.predict(X_new)`

**Example:**

```python
from sklearn.tree import DecisionTreeClassifier

clf = DecisionTreeClassifier()
clf.fit(X_train, y_train)  # learns patterns
y_pred = clf.predict(X_test)  # predicts labels
```

### 2. **Transformers**

* **Used for preprocessing / feature engineering**.
* Must implement:

  * `.fit(X)`
  * `.transform(X)`
* Or `.fit_transform(X)` for efficiency (fit + transform at once).

**Example:**

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
scaler.fit(X_train)          # learns mean and std
X_scaled = scaler.transform(X_train)  # standardizes data
```

---

## 🔄 Combined Estimators (e.g., Pipelines)

A **Pipeline** chains together multiple transformers and ends with a predictor.

```python
from sklearn.pipeline import Pipeline

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("model", LinearRegression())
])
pipeline.fit(X, y)  # scaler + model fit together
pipeline.predict(X_new)  # auto scales and predicts
```

---

## 🧠 Why Estimators Are Important

* ✅ **Consistency**: Every ML model, transformer, or tool follows the same `.fit()` interface.
* ✅ **Modularity**: You can plug-and-play any estimator into your pipeline.
* ✅ **Reusability**: You can apply the same trained estimator to new data (e.g., same scaler on test data).

---

## 📦 Summary Table

| Estimator Type | Purpose           | Key Methods                 | Example                           |
| -------------- | ----------------- | --------------------------- | --------------------------------- |
| Predictor      | Makes predictions | `.fit(X, y)`, `.predict(X)` | `LinearRegression`, `SVC`         |
| Transformer    | Transforms data   | `.fit(X)`, `.transform(X)`  | `StandardScaler`, `OneHotEncoder` |
| Combined       | Both              | `.fit_transform(X)`         | `Pipeline`, `TfidfVectorizer`     |

---
