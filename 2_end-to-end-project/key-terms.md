
## 📘 **2. Key Terms & Definitions in Chapter 2**

| Term                               | Definition                                                      |
| ---------------------------------- | --------------------------------------------------------------- |
| **Regression**                     | Predicting a continuous numeric value                           |
| **Supervised Learning**            | Learning from labeled data                                      |
| **Test Set**                       | Held-out data to evaluate final model performance               |
| **Stratified Sampling**            | Sampling that preserves target distribution across subsets      |
| **Data Pipeline**                  | A sequence of preprocessing steps applied consistently          |
| **Imputation**                     | Filling in missing values                                       |
| **Feature Scaling**                | Normalizing/standardizing features                              |
| **One-Hot Encoding**               | Converting categorical variables into binary columns            |
| **Model Evaluation**               | Measuring model performance using metrics (e.g., RMSE)          |
| **Cross-Validation**               | Evaluating a model on multiple data splits for robustness       |
| **Grid Search**                    | Trying all combinations of hyperparameters                      |
| **Randomized Search**              | Sampling random combinations of hyperparameters                 |
| **Overfitting**                    | Model fits training data too closely, fails on new data         |
| **Underfitting**                   | Model is too simple to capture the data patterns                |
| **Feature Importance**             | Metric showing how much each feature contributes to predictions |
| **RMSE (Root Mean Squared Error)** | A popular regression evaluation metric                          |
| **Persistent Model**               | A model saved to disk for future inference                      |
| **Model Rot**                      | Degraded performance due to evolving data                       |

---


## 📌 **1. Univariate Regression**

* **Definition**: Regression with **one input (feature)** and **one output (target)**.
* **Goal**: Predict a single target using a single predictor.
* **Example**: Predict house price based only on square footage.

✅ **Format**:

$$
y = w_1x + b
$$

🧠 **Simple and easy to visualize** (2D line).

---

## 📌 **2. Multiple Regression**

* **Definition**: Regression with **multiple input features**, but still **one output**.
* Also called **multivariable regression** (NOT multivariate).
* **Goal**: Predict a single target using multiple predictors.
* **Example**: Predict house price using square footage, number of bedrooms, and age of the house.

✅ **Format**:

$$
y = w_1x_1 + w_2x_2 + \dots + w_nx_n + b
$$

🧠 This is the standard case in most ML models.

---

## 📌 **3. Multivariate Regression**

* **Definition**: Regression with **multiple output targets** (regress multiple variables at once).
* **Goal**: Predict **more than one dependent variable** at the same time.
* **Example**: Predict both house price **and** time-on-market using the same features.

✅ **Format**:

$$
\begin{bmatrix}
y_1 \\
y_2 \\
\vdots \\
y_k
\end{bmatrix}
= XW + b
$$

🧠 Useful in multi-task learning or joint modeling.

---

## ✅ Summary Table

| Type                        | Input Features | Output Targets | Example                                      |
| --------------------------- | -------------- | -------------- | -------------------------------------------- |
| **Univariate Regression**   | 1              | 1              | Price vs. square footage                     |
| **Multiple Regression**     | >1             | 1              | Price vs. square footage + bedrooms          |
| **Multivariate Regression** | >1             | >1             | Predict price and market time simultaneously |

---

