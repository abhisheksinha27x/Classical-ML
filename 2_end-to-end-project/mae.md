

## 📘 **MAE Formula**

$$
\text{MAE}(X, h) = \frac{1}{m} \sum_{i=1}^{m} \left| h(x^{(i)}) - y^{(i)} \right|
$$

---

## 🧠 **Explanation of Each Notation (Book Style)**

| Symbol             | Term                                   | Meaning                                                                                                       |                |                                                                 |
| ------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------- | --------------------------------------------------------------- |
| $\text{MAE}(X, h)$ | Mean Absolute Error                    | The **average absolute error** between the predicted values and the true values for model $h$ on dataset $X$. |                |                                                                 |
| $X$                | Input dataset                          | The full input dataset (matrix of feature vectors).                                                           |                |                                                                 |
| $h$                | Hypothesis/model                       | The model used to make predictions, e.g. linear regression.                                                   |                |                                                                 |
| $m$                | Number of instances                    | The number of training examples in dataset $X$.                                                               |                |                                                                 |
| $i$                | Index of instance                      | Refers to the $i^\text{th}$ sample in the dataset.                                                            |                |                                                                 |
| $x^{(i)}$          | Feature vector of $i^\text{th}$ sample | Input features for the $i^\text{th}$ data point.                                                              |                |                                                                 |
| $y^{(i)}$          | True value (target) for $x^{(i)}$      | The actual output/label for the $i^\text{th}$ data point.                                                     |                |                                                                 |
| $h(x^{(i)})$       | Predicted value by model               | The model’s output (prediction) for input $x^{(i)}$.                                                          |                |                                                                 |
| ( \left            | h(x^{(i)}) - y^{(i)} \right            | )                                                                                                             | Absolute error | The absolute difference between the predicted and actual value. |
| $\sum_{i=1}^{m}$   | Summation                              | Adds up the absolute errors for all $m$ samples.                                                              |                |                                                                 |
| $\frac{1}{m}$      | Mean (average)                         | Divides the total absolute error by the number of samples to get the average.                                 |                |                                                                 |

---

## 🔍 **What Does MAE Measure?**

* It tells you the **average size of the errors** your model makes — in the **same units as the target variable**.
* Unlike RMSE, it **treats all errors equally** — **no squaring**, so large and small errors are weighted the same.

---

## 🧮 **Example Intuition**

Let’s say for a house price prediction:

| True Price (y) | Predicted Price (h(x)) | Absolute Error |
| -------------- | ---------------------- | -------------- |
| 200,000        | 210,000                | 10,000         |
| 300,000        | 290,000                | 10,000         |
| 400,000        | 390,000                | 10,000         |

MAE = $\frac{10,000 + 10,000 + 10,000}{3} = 10,000$

→ Your model is, on average, **\$10,000 off** in its predictions.

---

## 🧠 MAE vs. RMSE

| Metric   | Formula                                              | Penalizes Outliers?  | Unit           | When to Use                               |                |                                |
| -------- | ---------------------------------------------------- | -------------------- | -------------- | ----------------------------------------- | -------------- | ------------------------------ |
| **MAE**  | ( \frac{1}{m} \sum                                   | h(x^{(i)}) - y^{(i)} | )              | ❌ No                                      | Same as target | When outliers are not critical |
| **RMSE** | $\sqrt{ \frac{1}{m} \sum (h(x^{(i)}) - y^{(i)})^2 }$ | ✅ Yes                | Same as target | When large errors should be punished more |                |                                |

---

### ✅ Summary Diagram

```
[Predicted: h(x^{(i)})] ──► [Compare with y^{(i)}] ──► [|Error|] ──► [Mean] ──► MAE
```

---
