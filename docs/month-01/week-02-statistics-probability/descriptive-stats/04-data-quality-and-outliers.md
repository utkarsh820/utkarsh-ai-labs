# Data Quality and Outliers

_Before any machine learning model is trained, the data must be sanitized. Statistical tests must be deployed to handle null-values (missingness) and detect anomalies._

---

## 🟢 Beginner (Foundations)

### 1. Visual Inspection & Simple Counts

Before running algorithms, look at the data structure. Find missing (`NaN`) values and simple duplicates.

- **Python Implementation:**

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({"Age": [25, np.nan, 22, 25, 29, 300]}) # Exteme outlier and duplicate

print("Missing Values:\n", df.isnull().sum())
print("Duplicates:\n", df.duplicated().sum())
```

### 2. Basic Deduplication

Removing exact identical rows safely.

```python
df_cleaned = df.drop_duplicates()
```

---

## 🟡 Intermediate (Engineering)

### 1. Missingness Percentage & Matrix

Instead of raw counts (which are useless if you don't know the dataset size), calculate the percentage of missing values.

- **Python Implementation:**

```python
missing_percent = (df.isnull().sum() / len(df)) * 100
print(missing_percent, "% missing")
```

### 2. IQR Outlier Method (Tukey's 1.5× Rule)

Any data point outside the boundary of $(Q1 - 1.5 \times IQR)$ to $(Q3 + 1.5 \times IQR)$ is mathematically flagged as an outlier. Very robust for skewed data.

- **Python Implementation:**

```python
q1 = df["Age"].quantile(0.25)
q3 = df["Age"].quantile(0.75)
iqr = q3 - q1

lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

outliers = df[(df["Age"] < lower_bound) | (df["Age"] > upper_bound)]
print("Flagged Outliers:\n", outliers)
```

---

## 🔴 Advanced / Elite (Optimization)

### 1. The Z-Score Outlier Method

Mathematically calculates how many standard deviations away a data point is from the mean. Typically, any absolute Z-score $> 3$ is considered an anomaly.
_Note: Z-scores require your data to be Normally Distributed and are highly sensitive to extreme outliers because the mean is used in the calculation._

- **Python Implementation:**

```python
from scipy import stats
df_nomissing = df.dropna()
z_scores = np.abs(stats.zscore(df_nomissing["Age"]))
outliers_z = df_nomissing[z_scores > 3]
```

### 2. Statistical Missingness Classification (MCAR, MAR, MNAR)

You cannot simply "impute" missing data with the mean blindly. You must scientifically classify _why_ it is missing.

- **Missing Completely at Random (MCAR):** A true random glitch. Coin flip. (Safe to mean-impute or drop).
- **Missing at Random (MAR):** Missingness relies on a _different_ observed variable. (e.g., Men are less likely to fill out depression surveys than women. We can predict missingness using the "Gender" column). (Use Multiple Imputation, MICE).
- **Missing Not at Random (MNAR):** Missingness relies on the unobserved variable itself. (e.g., People with the lowest incomes leave the "Income" column blank because they are embarrassed). (Highly dangerous. Requires specialized domain knowledge).

### 3. Isolation Forest (Unsupervised Anomaly Detection)

Algorithms like Isolation Forests explicitly isolate anomalies by randomly partitioning trees. Anomalies travel shorter paths than standard observations. Very powerful for multivariable datasets.

- **Python Implementation:**

```python
from sklearn.ensemble import IsolationForest

model = IsolationForest(contamination=0.05)
predictions = model.fit_predict(df_nomissing[["Age"]])
# -1 indicates an outlier anomaly
df_nomissing["Anomaly"] = predictions
```
