
## 🔍 1.3 Types of Machine Learning Systems

The chapter categorizes ML systems along several axes:

---

### 1.3.1 **Supervised Learning**

* **Definition**: Learn from labeled data (input-output pairs).
* **Goal**: Predict the output (label) for new inputs.

**Examples**:

* Spam detection
* Housing price prediction
* Sentiment analysis

**Algorithms**:

* Linear Regression
* Logistic Regression
* Decision Trees
* k-NN
* Support Vector Machines (SVM)
* Neural Networks

**Tasks**:
* Classification 
* Regression

---

### 1.3.2 **Unsupervised Learning**

* **Definition**: Learn from **unlabeled** data to find patterns or structure.
* **Goal**: Discover **underlying structure** in the data.

**Examples**:

* Customer segmentation
* Anomaly detection
* Topic modeling

**Algorithms**:

* k-Means Clustering
* DBSCAN
* Hierarchical Clustering
* PCA (Principal Component Analysis)
* Autoencoders

**Tasks**:
* Clustering
* dimensionality reduction
* anomaly detection
* novelty detection
* association rule learning

---

### 1.3.3 **Semi-Supervised Learning**

* **Definition**: Learn from a small amount of labeled data and a large amount of unlabeled data.

**Example**:

* Google Photos: Only a few photos are tagged, but the model learns to generalize.

---

### 1.3.4 **Reinforcement Learning (RL)**

* **Definition**: An agent learns to take actions in an environment to maximize a reward signal.

**Example**:

* Training an AI to play a game (e.g., AlphaZero).
* Robotics
* Autonomous vehicles

**Key components**:

* Agent
* Environment
* Actions
* Rewards

---

### 1.3.5 **Batch vs Online Learning**

| Batch Learning                  | Online Learning                         |
| ------------------------------- | --------------------------------------- |
| Trained using all data at once  | Trained incrementally from data streams |
| Requires retraining for updates | Learns continuously                     |
| Slower but more accurate        | Fast, scalable for real-time systems    |

---

### 1.3.6 **Instance-Based vs Model-Based Learning**

* **Instance-Based Learning**: Remembers data and generalizes using similarity (e.g., k-NN).
* **Model-Based Learning**: Learns a model from data and generalizes from it (e.g., linear regression, decision trees).

---
