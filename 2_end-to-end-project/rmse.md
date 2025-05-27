### 📏 What is **Root Mean Square Error (RMSE)**?

**Root Mean Square Error (RMSE)** is a commonly used **performance metric for regression problems**. It measures the **average magnitude of the error** between predicted values and actual (true) values.

---

## ✅ **Definition**

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2}
$$

Where:

* $\hat{y}_i$ = predicted value
* $y_i$ = true (actual) value
* $n$ = number of data points

---

## 🧠 **What Does RMSE Tell You?**

* How **far off** your model’s predictions are **on average**, in the same units as the target variable.
* RMSE **penalizes large errors more** than small ones due to squaring.
* A **lower RMSE** means a **better** model (closer predictions to real values).

---

## 📊 **Example**

If you're predicting house prices in thousands of dollars and RMSE = 50, that means:

> "On average, your predictions are about **\$50,000 off** from the actual price."

---

## 🔄 RMSE vs Other Metrics

| Metric   | Penalizes Large Errors | Sensitive to Outliers | Unit of Measure  |
| -------- | ---------------------- | --------------------- | ---------------- |
| **RMSE** | ✅ Yes                  | ✅ Yes                 | Same as target   |
| **MAE**  | ❌ No (linear)          | ❌ Less sensitive      | Same as target   |
| **R²**   | ❌ No (unitless)        | ❌ Less sensitive      | Proportion (0–1) |

---

## 📌 When to Use RMSE?

* When **large errors are especially bad** (e.g., pricing, forecasting).
* When you care about performance in the **same units as the target**.
* When **outliers matter** in your domain.

---


## 🎯 **Goal**

We want to measure how well our model's predictions $\hat{y}_i$ match the true values $y_i$ across all $n$ data points.

---

## 🧱 Step-by-Step Derivation of RMSE

### **Step 1: Compute Prediction Errors (Residuals)**

The **error** for a single prediction is:

$$
e_i = \hat{y}_i - y_i
$$

We want to summarize these errors over the whole dataset.

---

### **Step 2: Eliminate Negative Signs**

If we just average the errors, they might cancel out (positive and negative errors).
So we **square the errors** to make them all positive:

$$
e_i^2 = (\hat{y}_i - y_i)^2
$$

---

### **Step 3: Compute Mean of Squared Errors**

Now we average these squared errors across all predictions:

$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2
$$

This is called the **Mean Squared Error (MSE)**.

---

### **Step 4: Convert Back to Original Units**

MSE gives us squared units (e.g., squared dollars, squared meters), which are **hard to interpret**.

To fix that, we take the **square root**, giving us:

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2}
$$

Now the error is back in the **same units** as the original data (e.g., dollars).

---

## 🧠 Why RMSE?

* It **rewards smaller errors** and **penalizes large ones** more harshly (due to squaring).
* It’s **differentiable**, which makes it great for optimization in gradient-based learning.
* It’s a **standard metric** used in many regression problems.

---

## 📘 Summary

| Step | Concept                        | Formula                                          |
| ---- | ------------------------------ | ------------------------------------------------ |
| 1    | Raw error                      | $\hat{y}_i - y_i$                                |
| 2    | Square errors                  | $(\hat{y}_i - y_i)^2$                            |
| 3    | Mean squared error (MSE)       | $\frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2$ |
| 4    | Root mean squared error (RMSE) | $\sqrt{\text{MSE}}$                              |


---

## 📘 **Book's Version of RMSE Equation**

$$
\text{RMSE}(X, h) = \sqrt{ \frac{1}{m} \sum_{i=1}^{m} \left( h(x^{(i)}) - y^{(i)} \right)^2 }
$$

---

## 🧠 **Explanation of Each Notation (Book-Specific)**

| Symbol                                | Name                                          | Meaning                                                       |
| ------------------------------------- | --------------------------------------------- | ------------------------------------------------------------- |
| $\text{RMSE}(X, h)$                   | RMSE of hypothesis $h$ on dataset $X$         | Root mean square error calculated using model $h$ on data $X$ |
| $X$                                   | Input data matrix                             | Contains all feature vectors (i.e., inputs)                   |
| $h$                                   | Hypothesis / model function                   | The model that makes predictions (e.g., a linear model)       |
| $m$                                   | Number of instances                           | The total number of training (or test) examples               |
| $\sum_{i=1}^{m}$                      | Summation                                     | Add up the squared errors for each data point from 1 to $m$   |
| $x^{(i)}$                             | Input features for the $i^\text{th}$ instance | The input vector of features for example $i$                  |
| $h(x^{(i)})$                          | Prediction for input $x^{(i)}$                | The model’s predicted value for example $i$                   |
| $y^{(i)}$                             | True value (label) for example $i$            | The actual target/output for example $i$                      |
| $\left(h(x^{(i)}) - y^{(i)}\right)^2$ | Squared prediction error                      | Measures how far off the prediction is for each example       |

---

### ✅ TL;DR

* $h(x^{(i)})$ is the predicted value (same as $\hat{y}_i$).
* $y^{(i)}$ is the actual value (same as $y_i$).
* $m$ is the number of instances (same as $n$).

So the book is just using **machine learning notation**, especially from **mathematical learning theory**, where:

* $h$ stands for **hypothesis** (i.e., model),
* $x^{(i)}$, $y^{(i)}$ refer to the **$i^\text{th}$** training example,
* And RMSE is expressed as a **function** of the dataset and model.

---

## 📘 **Book's RMSE Formula**

$$
\text{RMSE}(X, h) = \sqrt{ \frac{1}{m} \sum_{i=1}^{m} \left( h(x^{(i)}) - y^{(i)} \right)^2 }
$$

---

## 🧠 **Explanation of Each Notation (Book Style)**

| Symbol                                | Term                                   | Meaning                                                                                                  |
| ------------------------------------- | -------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| $\text{RMSE}(X, h)$                   | Root Mean Square Error                 | The model's overall error across dataset $X$; it's a function of both the dataset $X$ and the model $h$. |
| $X$                                   | Input dataset                          | The full dataset of input feature vectors (e.g., matrix of shape $m \times n$).                          |
| $h$                                   | Hypothesis (model)                     | The predictive function or model being evaluated, such as a linear regression function.                  |
| $m$                                   | Number of training instances           | Total number of training examples (i.e., the dataset has $m$ rows or samples).                           |
| $i$                                   | Index of instance                      | Refers to the $i^\text{th}$ training example in the dataset.                                             |
| $x^{(i)}$                             | Input vector of $i^\text{th}$ instance | The features for the $i^\text{th}$ sample (e.g., \[area, bedrooms, age]).                                |
| $y^{(i)}$                             | True target value for $x^{(i)}$        | The actual output value (ground truth) for the $i^\text{th}$ sample.                                     |
| $h(x^{(i)})$                          | Predicted value                        | The prediction made by the model $h$ for input $x^{(i)}$.                                                |
| $\left(h(x^{(i)}) - y^{(i)}\right)^2$ | Squared error                          | The squared difference between prediction and actual value (individual error).                           |
| $\sum_{i=1}^{m}$                      | Summation over dataset                 | Add up the squared errors for **all** training instances from 1 to $m$.                                  |
| $\frac{1}{m}$                         | Mean (average)                         | Computes the average squared error (called MSE).                                                         |
| $\sqrt{\,}$                           | Square root                            | Converts the average squared error (MSE) back to original units to get RMSE.                             |

---

## 📌 Conceptually

* You’re comparing what the model **predicts** (using $h(x^{(i)})$) vs. what it **should predict** (actual $y^{(i)}$).
* Then you square that difference, average across the whole dataset, and take the square root to get a **single performance number**.

---

## ✅ Summary Diagram of Notation Flow

```
[Input Features X] ──► [Model h(x)] ──► [Predictions h(x^{(i)})]
                                 ↓
[Ground Truth y^{(i)}]           ↓
     └────────────────────────► [Compare → Square → Average → Root] ──► RMSE
```

---

