
## 🔹 Chapter 3: Classification – Overview

Classification is one of the most common and important types of supervised learning tasks, where the goal is to predict a **category (class label)** for given inputs.

### 🧠 Key Concepts Covered:

#### 1. **Introduction to Classification**

* A classification task is when the target variable is categorical (e.g., spam vs. not spam).
* **Binary Classification**: Only two possible classes (e.g., digit ‘5’ or not ‘5’).
* **Multiclass Classification**: More than two classes (e.g., digits 0–9).

#### 2. **The MNIST Dataset**

* Modified National Institute of Standards and Technology (MNIST)
* A classic dataset of **70,000 handwritten digits** (28x28 grayscale images).
* Widely used for benchmarking classification models.
* You learn to **load and visualize** this dataset using `sklearn.datasets.fetch_openml()`.

#### 3. **Training a Binary Classifier**

* Task: Classify whether a digit is ‘5’ or not (‘5-detector’).
* Use **Stochastic Gradient Descent (SGD) Classifier** from Scikit-Learn.
* Key steps:

  * Training (`fit()`), prediction (`predict()`), and measuring accuracy.

#### 4. **Performance Measures**

* Accuracy alone is **not enough**, especially with **imbalanced datasets**.
* Introduces:

  * **Confusion Matrix**
  * **Precision and Recall**
  * **F1 Score**: Harmonic mean of precision and recall.
  * **Precision/Recall Trade-off**
  * **Decision thresholds**
  * **ROC Curve** and **AUC Score**

#### 5. **Multiclass Classification**

* Strategies:

  * **One-vs-All (OvA)**: Train a binary classifier for each class.
  * **One-vs-One (OvO)**: Train classifiers for each pair of classes.
* Scikit-Learn automatically chooses a strategy based on the algorithm.

#### 6. **Error Analysis**

* After evaluating metrics, it’s important to **look at what types of errors the model is making**.
* Use **confusion matrix visualizations** and **image plotting** to inspect misclassified digits.

#### 7. **Multilabel Classification**

* Predicting **multiple binary labels per instance**.
* Example: Classify if a digit is large (≥7) and odd → two labels.
* Use `KNeighborsClassifier` for multilabel tasks.

#### 8. **Multioutput Classification**

* Also called **multioutput–multiclass classification**.
* Predict **multiple classes for multiple outputs**.
* Example given: Remove noise from images (denoising task).

---

## ⚙️ Tools & Libraries Used

* Scikit-Learn: `SGDClassifier`, `cross_val_score`, `confusion_matrix`, `precision_score`, `recall_score`, `roc_curve`, `KNeighborsClassifier`
* Matplotlib: Visualization of digits and errors

---
