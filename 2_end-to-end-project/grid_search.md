
## 🔍 What is Grid Search in Model Fine-Tuning?

**Grid Search** is a brute-force method for **hyperparameter tuning** — it systematically **tries every combination** of hyperparameter values you specify and **finds the one that gives the best performance** (e.g., lowest RMSE, highest accuracy).

It helps you **fine-tune** a model by optimizing the knobs you can’t learn from the data — like `n_estimators`, `max_depth`, `learning_rate`, etc.

---

### 📦 What Is Being Tuned?

You don’t tune **model weights** (those are learned during training). You tune **hyperparameters** — fixed settings **set before training**.

| Model            | Hyperparameters (Examples)                  |
| ---------------- | ------------------------------------------- |
| Random Forest    | `n_estimators`, `max_features`, `max_depth` |
| KMeans           | `n_clusters`, `init`, `max_iter`            |
| Ridge Regression | `alpha` (regularization strength)           |
| SVM              | `C`, `gamma`, `kernel`                      |

---

## ⚙️ How Grid Search Works

Let’s say you're tuning:

```python
param_grid = {
    "n_estimators": [50, 100],
    "max_features": [4, 6, 8]
}
```

### 🔁 Steps:

1. Grid search tries **all 2×3 = 6 combinations**:

   * (50, 4), (50, 6), (50, 8)
   * (100, 4), (100, 6), (100, 8)

2. For each combination:

   * Train the model (e.g., RandomForest)
   * Evaluate using **cross-validation**
   * Store the performance metric (e.g., RMSE)

3. Return the **best combination** based on average score.

---

## ✅ Code Example

```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestRegressor

param_grid = {
    "n_estimators": [50, 100],
    "max_features": [4, 6, 8]
}

grid_search = GridSearchCV(
    RandomForestRegressor(random_state=42),
    param_grid,
    cv=5,
    scoring='neg_root_mean_squared_error',
    n_jobs=-1
)

grid_search.fit(housing_prepared, housing_labels)

print("Best parameters:", grid_search.best_params_)
print("Best RMSE:", -grid_search.best_score_)
```

---

## 🎯 Why Use Grid Search?

| Benefit                      | Why It Matters                               |
| ---------------------------- | -------------------------------------------- |
| Optimizes model performance  | Better predictions, lower error              |
| Automated, exhaustive search | Removes guesswork from tuning                |
| Works with `Pipeline`s       | Can tune preprocessing and model hyperparams |
| Compatible with CV           | More reliable performance estimates          |

---

## ⚠️ Limitations

| Limitation                 | Workaround                                                |
| -------------------------- | --------------------------------------------------------- |
| Slow on large grids        | Use fewer combinations or trees                           |
| Wastes time on bad combos  | Use **`RandomizedSearchCV`** or **`HalvingGridSearchCV`** |
| Expensive for big datasets | Use subsampling while testing                             |

---

## 🧠 TL;DR

> **Grid Search = Try all hyperparameter combinations → Evaluate with CV → Pick the best.**
> It's an essential step in **fine-tuning a machine learning model** for optimal performance.

---
