

## 🎯 What is Randomized Search?

**Randomized Search** is an alternative to Grid Search for **hyperparameter tuning**.
Instead of trying **every** possible combination, it **samples random combinations** of hyperparameters from specified distributions.

This makes it **much faster**, especially when:

* You have many hyperparameters
* Some values don’t matter much
* You have limited compute time

---

## 🧠 Key Idea

Rather than trying all combinations like Grid Search:

```
Grid Search:       Try ALL 3×3×3 = 27 combos
Randomized Search: Try 10 random combos only
```

You **specify how many combinations** to try (e.g., `n_iter=10`), and it picks that many **at random**.

---

## ✅ Advantages of Randomized Search

| Advantage                    | Explanation                                               |
| ---------------------------- | --------------------------------------------------------- |
| 🚀 Much faster               | Doesn’t try every combo                                   |
| 📉 Often finds great results | Can find near-optimal solutions without exhaustive search |
| ⛳️ Focuses on large spaces   | Good for continuous or high-dimensional params            |
| 🧪 Supports distributions    | You can sample from uniform/log-uniform ranges            |

---

## ⚙️ How It Works

### Step-by-step:

1. **Define param distributions**, not full lists:

   ```python
   param_distributions = {
       "n_estimators": [50, 100, 150, 200],
       "max_features": np.arange(2, 10),
       "max_depth": [None, 10, 20, 30]
   }
   ```

2. **Set how many combinations** to try:

   ```python
   n_iter = 10  # Try only 10 random combinations
   ```

3. Run it like this:

```python
from sklearn.model_selection import RandomizedSearchCV
from sklearn.ensemble import RandomForestRegressor
import numpy as np

param_distributions = {
    "n_estimators": np.arange(50, 201, 10),
    "max_features": np.arange(2, 10),
    "max_depth": [None] + list(np.arange(10, 50, 10))
}

rnd_search = RandomizedSearchCV(
    RandomForestRegressor(random_state=42),
    param_distributions=param_distributions,
    n_iter=10,               # Try only 10 random combos
    cv=5,                    # 5-fold cross-validation
    scoring='neg_root_mean_squared_error',
    n_jobs=-1,
    random_state=42
)

rnd_search.fit(housing_prepared, housing_labels)

print("Best params:", rnd_search.best_params_)
print("Best RMSE:", -rnd_search.best_score_)
```

---

## 🆚 Grid Search vs. Randomized Search

| Feature                | Grid Search                    | Randomized Search                      |
| ---------------------- | ------------------------------ | -------------------------------------- |
| Strategy               | Try all combinations           | Try random combinations                |
| Speed                  | Slow for large grids           | Much faster                            |
| Ideal for              | Small param spaces             | Large param spaces                     |
| Flexible distributions | ❌ Fixed list of values         | ✅ Use distributions (uniform, etc.)    |
| Best use case          | Final tuning on narrowed range | Exploratory tuning or big search space |

---

## 🎯 When to Use RandomizedSearchCV

* When you have **lots of hyperparameters**
* When training is **slow** (e.g., Random Forests, Neural Nets)
* When you want **good-enough results quickly**

---

## 💡 Bonus Tip

For even more efficient search, look into:

* [`HalvingRandomSearchCV`](https://scikit-learn.org/stable/whats_new/v0.24.html#id15)
* `Bayesian optimization` (e.g., with `Optuna`, `scikit-optimize`)

---
