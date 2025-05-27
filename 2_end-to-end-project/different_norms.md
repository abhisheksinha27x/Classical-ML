> Both the RMSE and MAE are ways to measure the distance between two vectors: the vector of predictions and the vector of target values. Various distance measures, or _norms_, are possible: 
---

# 🔢 Understanding Vector Norms in Machine Learning

In machine learning and mathematics, **norms** are functions that measure the **size (or length)** of a vector. In ML, they are used in:

* **Error metrics** (e.g. MAE, RMSE)
* **Regularization** (e.g. L1, L2)
* **Optimization**
* **Distance calculations**

The most commonly used norms are the **Lp norms**, where $p = 1, 2, 3, \infty$.

---

## 🧮 General Definition: **Lp Norm**

For a vector $\mathbf{v} = [v_1, v_2, ..., v_n]$:

$$
\| \mathbf{v} \|_p = \left( \sum_{i=1}^{n} |v_i|^p \right)^{\frac{1}{p}}
$$

Where:

* $p$: the order of the norm
* $|v_i|$: absolute value of the vector element
* $\| \cdot \|_p$: the Lp norm

---

## ① **L1 Norm (Manhattan Norm)**

### 🔹 Formula:

$$
\| \mathbf{v} \|_1 = \sum_{i=1}^{n} |v_i|
$$

### 🔹 Meaning:

* Measures the total **absolute** difference.
* Think of it as the **taxicab distance** in a grid-like city: you move in blocks, not diagonally.

### 🔹 Applications:

* **Mean Absolute Error (MAE)** in regression
* **L1 Regularization** (Lasso regression) — leads to sparsity by pushing some weights to **exact zero**
* Useful when **interpretability** and **feature selection** are important

### 🔹 Properties:

* Robust to outliers
* Promotes sparsity (zero values)

---

## ② **L2 Norm (Euclidean Norm)**

### 🔹 Formula:

$$
\| \mathbf{v} \|_2 = \sqrt{ \sum_{i=1}^{n} v_i^2 }
$$

### 🔹 Meaning:

* Measures the **straight-line (Euclidean)** distance from the origin to the point.
* It’s the **default notion of distance** in geometry and physics.

### 🔹 Applications:

* **Root Mean Squared Error (RMSE)** in regression
* **L2 Regularization** (Ridge regression) — discourages large weights but **doesn't zero them out**
* Common in most ML models when smooth error gradients are needed

### 🔹 Properties:

* Sensitive to large values / outliers
* Produces smooth optimization surfaces

---

## ③ **L3 Norm (Cubic Norm)**

### 🔹 Formula:

$$
\| \mathbf{v} \|_3 = \left( \sum_{i=1}^{n} |v_i|^3 \right)^{\frac{1}{3}}
$$

### 🔹 Meaning:

* A compromise between L1 and L2.
* Increases the penalty for large values more than L1 but less than L2.

### 🔹 Applications:

* Rarely used in standard ML
* Could be used in **custom loss functions** or **experimental regularization**
* Sometimes explored in **adversarial robustness** or **interpolation between L1 and L2**

### 🔹 Properties:

* Somewhat sensitive to outliers
* Smooth but not widely interpretable
* Good for tuning "error harshness" between L1 and L2

---

## 📊 Comparison Table

| Norm   | Formula             | Alias     | Sensitivity to Outliers | Sparsity            | Use Cases   |                       |                           |
| ------ | ------------------- | --------- | ----------------------- | ------------------- | ----------- | --------------------- | ------------------------- |
| **L1** | ( \sum              | v\_i      | )                       | Manhattan / Taxicab | Low         | High (promotes zeros) | MAE, Lasso                |
| **L2** | $\sqrt{\sum v_i^2}$ | Euclidean | High                    | No                  | RMSE, Ridge |                       |                           |
| **L3** | ( \left( \sum       | v\_i      | ^3 \right)^{1/3} )      | —                   | Medium      | Medium                | Custom loss, experimental |

---

## 📌 Visual Intuition

* **L1 Norm** → Diamond-shaped contours (sharp corners)
* **L2 Norm** → Circle-shaped contours (smooth, round)
* **L3 Norm** → Rounded shapes between L1 and L2 (less sharp than L1, less round than L2)

This matters when regularizing — the **geometry of the constraint** affects what the optimizer selects as the "best" solution.

---

## ✅ Summary

* Norms measure **how big a vector is** — often interpreted as **error**, **distance**, or **model complexity**.
* **L1 and L2** norms are used in nearly every ML model — especially for **loss functions** and **regularization**.
* **L3** and other Lp norms (like L0.5 or L10) are sometimes used for **custom tuning** of model behavior.

---


> - The higher the norm index \( p \), the more it emphasizes large errors and downplays smaller ones.
> - This is why **RMSE** (which uses the L2 norm) is more sensitive to outliers than **MAE** (which uses the L1 norm).
> - However, when outliers are **exponentially rare**, as in a **bell-shaped (Gaussian) distribution**, **RMSE** tends to perform well and is generally preferred.
