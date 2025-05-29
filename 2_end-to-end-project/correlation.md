### 📘 What is Correlation in Machine Learning?

**Correlation** is a **statistical measure** that expresses how strongly two variables are **related** to each other. In machine learning, understanding correlation is essential because it helps you:

* Detect **relationships between features** and the target variable.
* Identify **redundant features** that might not add value.
* Spot **multicollinearity**, which can affect model performance (especially in linear models).

---

## 📐 1. Types of Correlation

| Type                      | Meaning                                             | Value Range  |
| ------------------------- | --------------------------------------------------- | ------------ |
| **Positive**              | As one variable increases, the other also increases | `0 < r ≤ 1`  |
| **Negative**              | As one variable increases, the other decreases      | `-1 ≤ r < 0` |
| **Zero / No correlation** | No clear relationship                               | `r ≈ 0`      |
| **Perfect correlation**   | One variable changes exactly as the other does      | `r = ±1`     |

---

## 🔢 2. Pearson Correlation Coefficient (`r`)

This is the **most commonly used** measure. It evaluates **linear relationships** between two numeric variables.

### 📄 Formula:

$$
r = \frac{\text{cov}(X, Y)}{\sigma_X \cdot \sigma_Y}
$$

Where:

* `cov(X, Y)` = Covariance between X and Y
* `σ_X`, `σ_Y` = Standard deviation of X and Y

### Interpretation:

| `r` value    | Interpretation                      |
| ------------ | ----------------------------------- |
| 1.0          | Perfect positive linear correlation |
| 0.7 to 0.9   | Strong positive                     |
| 0.4 to 0.6   | Moderate positive                   |
| 0.1 to 0.3   | Weak positive                       |
| 0            | No correlation                      |
| -0.1 to -0.3 | Weak negative                       |
| -0.4 to -0.6 | Moderate negative                   |
| -0.7 to -0.9 | Strong negative                     |
| -1.0         | Perfect negative                    |

---

## 📊 3. Correlation Matrix

In pandas:

```python
corr_matrix = housing.corr(numeric_only=True)
print(corr_matrix["median_house_value"].sort_values(ascending=False))
```

* This shows how every numerical feature in the dataset correlates with the target (`median_house_value`).
* Helps select **important features** for training.
* High correlation with target = good candidate predictor.

---

## 📉 4. Heatmap Visualization

```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(10,8))
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm")
```

* Color-coded view of the full correlation matrix.
* Dark red/blue = high positive/negative correlation.

---

## ⚠️ 5. Caveats & Misunderstandings

| Myth / Issue                     | Clarification                                                                                                                             |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Correlation ≠ Causation          | Just because X and Y move together doesn't mean one causes the other.                                                                     |
| Non-linear relationships         | Pearson only captures **linear** relationships. Other measures like **Spearman** or **mutual information** can handle nonlinear patterns. |
| Outliers can distort correlation | Strongly! Use scatter plots to visually inspect.                                                                                          |
| Only works on numerical data     | Categorical variables need **different metrics** like Cramér’s V.                                                                         |

---

## 🧠 Use of Correlation in ML

1. **Feature Selection**:

   * Drop features with low correlation to the target.
   * Drop features that are too strongly correlated with each other (redundancy).

2. **Model Interpretability**:

   * Understand which features are **driving predictions**.

3. **Data Understanding**:

   * Spot interesting patterns before training.

---

## ✅ Summary

* Correlation helps understand **how strongly two numeric variables move together**.
* Use `.corr()` and heatmaps to get a **quick overview of relationships**.
* Don’t blindly trust correlation — always visualize!

---

### 🔍 What Does the `.corr()` Method Do in Pandas?

The `.corr()` method in pandas is used to compute **pairwise correlation** of columns in a DataFrame that contain **numerical data**.

---

## ✅ Purpose:

It **quantifies the strength and direction** of relationships between **numeric features**. This helps in understanding how variables are related and is often used in **feature selection and exploratory data analysis (EDA)**.

---

## 🧠 Basic Usage:

```python
df.corr()
```

Returns a **correlation matrix**, where:

* **Rows and columns** represent numeric columns in your DataFrame.
* **Each cell** contains the correlation coefficient between the two corresponding columns.

---

## 📌 Default Behavior:

By default, `.corr()` uses the **Pearson correlation coefficient**, which measures **linear correlation**.

```python
df.corr(method='pearson')  # Default
```

---

## 🧮 Other Supported Methods:

| Method       | Description                                             |
| ------------ | ------------------------------------------------------- |
| `'pearson'`  | Measures linear correlation (default).                  |
| `'kendall'`  | Measures ordinal (rank) correlation.                    |
| `'spearman'` | Measures monotonic relationships (good for non-linear). |

---

## 📊 Example:

```python
import pandas as pd

data = {
    "height": [150, 160, 170, 180],
    "weight": [50, 60, 70, 80],
    "age": [30, 25, 45, 35]
}

df = pd.DataFrame(data)
print(df.corr())
```

Output:

```
           height    weight       age
height   1.000000  1.000000  0.377964
weight   1.000000  1.000000  0.377964
age      0.377964  0.377964  1.000000
```

* `height` and `weight` have a perfect correlation of `1.0`.
* `age` has moderate correlation with height and weight.

---

## 🧪 With `housing` Dataset:

```python
housing.corr(numeric_only=True)
```

This gives you the correlation between all numeric features — for example:

* How `median_income` correlates with `median_house_value`.
* How `housing_median_age` relates to `households`.

---

## 🛠️ Parameters:

| Parameter      | Description                               |
| -------------- | ----------------------------------------- |
| `method`       | `'pearson'`, `'kendall'`, or `'spearman'` |
| `numeric_only` | `True` to ignore non-numeric columns      |
| `min_periods`  | Minimum number of observations needed     |

---

## 🔎 Summary:

* `.corr()` is a fast way to **see how numeric variables relate**.
* It’s essential for **feature selection** and **EDA**.
* Combine it with **heatmaps** to visualize patterns in your dataset.

---

> - The correlation coefficient ranges from -1 and 1.
> - When it is close to 1, it means that there is a strong positive correlation.
> - For example: the median house value tends to go up when the median income goes up.
> - When the coefficient is close to -1, it means that there is a strong negative correlation.
> - We can see that there is a strong negative correlation between the latitude and the median house value.
> - Finaly, coefficients close to 0 mean that there is no linear correlation.

---

Another **powerful way** to check for correlation — especially **visually** — is using the `scatter_matrix()` function from **pandas.plotting** or **Seaborn pairplot**.

## 🔍 `scatter_matrix()` – Visualizing Attribute Correlation

### 📌 What It Does:

`scatter_matrix()` creates a **grid of scatter plots**, showing **pairwise relationships** between multiple numeric attributes.

* **Diagonal**: Usually histograms (distribution of each attribute).
* **Off-diagonal**: Scatter plots between pairs of attributes.

This helps you **see**:

* **Linear relationships**
* **Clusters or outliers**
* **Strength of correlation**

---

### 🧪 Example (using the `housing` dataset):

```python
from pandas.plotting import scatter_matrix
import matplotlib.pyplot as plt

attributes = ["median_house_value", "median_income", "total_rooms", "housing_median_age"]
scatter_matrix(housing[attributes], figsize=(12, 8))
plt.show()
```

### 🔍 Interpretation:

* If the scatter plot shows a **clear line/shape**, the correlation is likely strong.
* If it looks like **random dots**, there's weak or no correlation.
* **Median income vs median house value** usually shows a strong positive trend.

---

## 🧰 Alternatives: Seaborn `pairplot()`

```python
import seaborn as sns

sns.pairplot(housing[attributes])
plt.show()
```

* Does the same as `scatter_matrix`, with more control and styling.
* You can also color by categories using the `hue` parameter.

---

## ✅ When to Use:

| Tool               | Best for                                         |
| ------------------ | ------------------------------------------------ |
| `.corr()`          | Fast numeric correlation matrix (quantitative)   |
| `scatter_matrix()` | Visual inspection of relationships (qualitative) |
| `sns.pairplot()`   | Advanced and beautiful visual correlation plots  |

---

## 🧠 Summary

* `scatter_matrix()` (or `sns.pairplot()`) helps **visualize correlations** between attributes.
* It complements `.corr()` by showing **non-linear** and **visual patterns**.
* Especially helpful in **EDA** before feature selection or model training.

---
