# Visualization and Frequency

_Exploratory Data Analysis (EDA) relies on human visual perception to instantly detect shapes, modalities, and relationships that raw numbers obscure. Frequency tables structure those visual bins locally._

---

## 🟢 Beginner (Foundations)

### 1. Histograms vs. Bar Charts

- **Histograms:** Used for **Numerical/Continuous quantitative** data. They bin raw numbers together into ranges (e.g., Age 10-20, 20-30). Bars touch strictly because data is continuous.
- **Bar Charts:** Used for **Categorical/Discrete qualitative** data. Bars do not touch because categories are discrete (e.g., Red, Blue, Green).

```python
import matplotlib.pyplot as plt
import seaborn as sns

data = [12, 15, 14, 22, 28, 30, 31]
sns.histplot(data, bins=3)
plt.title("Continuous Data Binned")
plt.show()
```

### 2. Count & Simple Frequency Tables

Finding how many times distinct values occur.

```python
import pandas as pd
df = pd.DataFrame({"color": ["red", "blue", "red", "green", "blue", "blue"]})
print(df["color"].value_counts()) # Returns raw counts
```

---

## 🟡 Intermediate (Engineering)

### 1. Box Plots and Violin Plots

- **Box Plot:** A literal, visual manifestation of the 5-number summary (Min, Q1, Median, Q3, Max) and IQR. Dots outside the "whiskers" are mathematical outliers explicitly.
- **Violin Plot:** Combines a Box Plot with a Kernel Density Estimate (KDE). It solves the "bimodality" problem: A box plot can hide if a distribution has two distinct peaks, but a violin plot shows the exact curvature.

```python
sns.violinplot(x=data)
plt.title("Violin Plot displaying KDE Density Curve")
plt.show()
```

### 2. Relative and Cumulative Frequency

- **Relative Frequency:** Turns raw counts into percentages of the whole population. `count / total_count`.
- **Cumulative Frequency:** A running total. Adds percentages sequentially until 100% is reached.

```python
counts = df["color"].value_counts(normalize=True) * 100
cumulative = counts.cumsum()
print("Relative:\n", counts)
print("Cumulative:\n", cumulative)
```

---

## 🔴 Advanced / Elite (Optimization)

### 1. Empirical Cumulative Distribution Function (ECDF)

Rather than binning data like a histogram does (which forces you to subjectively choose the `bins=` parameter), an ECDF plots every single exact data point. It represents the proportion of items less than or equal to `x`. Fast, objective, and immune to binning bias.

- **Python Implementation:**

```python
sns.ecdfplot(data)
plt.title("Exact Cumulative Ratios")
plt.show()
```

### 2. Q-Q Plots (Quantile-Quantile)

The absolute best way to check if your data actually follows a Normal Distribution. It compares your data's quantiles against a theoretical perfect normal distribution. If the data points hug the 45-degree diagonal red line, your data is perfectly normal.

- **Python Implementation:**

```python
import scipy.stats as stats
stats.probplot(data, dist="norm", plot=plt)
plt.title("Q-Q Plot")
plt.show()
```

### 3. Cross-Tabulation & Contingency Tables

Used to quantify the interaction rate between two entirely different categorical variables simultaneously.

- **Python Implementation:**

```python
df["size"] = ["S", "M", "L", "S", "M", "L"] # Merging with colors
contingency = pd.crosstab(df["color"], df["size"], normalize='index')
print(contingency)
```
