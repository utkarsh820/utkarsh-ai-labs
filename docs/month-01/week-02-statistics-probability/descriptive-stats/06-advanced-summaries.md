# Advanced Summaries

_Transforming data shapes into workable ML structures, generating grouped aggregations, and standardizing values for modeling calculations._

---

## 🟢 Beginner (Foundations)

### 1. Simple Data Transformations (Log, Square Root)

Highly skewed data breaks linear assumptions in machine learning. We use static mathematical transformations to compress those massive outliers and force the distribution closer to a Bell Curve/Normal structure.

- **Log Transform:** $y = \log(x+1)$ (The $+1$ handles datasets with exact zeros).
- **Square Root Transform:** $y = \sqrt{x}$

```python
import numpy as np
import pandas as pd
import seaborn as sns

df = sns.load_dataset("diamonds")

# Log transform the heavily right-skewed price column
df["log_price"] = np.log1p(df["price"])
```

### 2. Basic Grouping and Tables

Aggregating numbers by discrete categories.

```python
mean_price_by_cut = df.groupby("cut")["price"].mean()
print(mean_price_by_cut)
```

### 3. Equal-width Binning

Slicing continuous numerical data into discrete categories by explicitly typing ranges (e.g. $[0 \to 10]$, $[10 \to 20]$).

```python
df["price_category"] = pd.cut(df["price"], bins=3, labels=["Low", "Med", "High"])
```

---

## 🟡 Intermediate (Engineering)

### 1. Standardization (Z-score)

Transforms continuous data so its `Mean = 0` and its `Standard Deviation = 1`. Vital for neural networks, SVMs, Ridge regression, and PCA visualization where large numbers mathematically overpower small numbers.

- **Formula:** $Z = \frac{x - \mu}{\sigma}$

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
df["scaled_price"] = scaler.fit_transform(df[["price"]])
```

### 2. Normalization (Min-Max)

Forcibly compresses the entire dataset perfectly between `0` and `1`. Highly sensitive to extreme outliers because the `Max` anchors all other values. Used heavily for Image/Pixel data in ConvNets.

- **Formula:** $X_{norm} = \frac{x - x_{min}}{x_{max} - x_{min}}$

### 3. Equal-frequency Binning (Quantile Binning)

Unlike equal-width binning, this ensures every single bin contains the _exact same number of samples_, avoiding massive class imbalances.

```python
# 4 bins (quartiles), each receiving 25% of the data exactly
df["price_quantile"] = pd.qcut(df["price"], q=4, labels=["Q1", "Q2", "Q3", "Q4"])
```

### 4. GroupBy Aggregations with Multiple Functions

```python
summary = df.groupby("cut").agg({
    "price": ["mean", "median", "std"],
    "carat": ["max"]
})
print(summary)
```

---

## 🔴 Advanced / Elite (Optimization)

### 1. Optimal Binning (Freedman-Diaconis Rule)

Instead of guessing `bins=30` subjectively in a histogram, mathematically optimize the bin width to perfectly represent the underlying density, adjusting rigidly for sample size and IQR to ignore extreme outliers plotting themselves.

- **Formula:** $Bin\_Width = 2 \times \frac{IQR(x)}{\sqrt[3]{n}}$

```python
import matplotlib.pyplot as plt

# Numpy's 'fd' string natively applies Freedman-Diaconis equation
plt.hist(df["price"], bins="fd")
plt.title("Freedman-Diaconis Optimized Bins")
plt.show()
```

### 2. Power Transformations (Box-Cox & Yeo-Johnson)

Instead of "guessing" whether to use Log or Square Root, these are advanced algorithms that rigorously hunt for the exact mathematical $\lambda$ exponent that transforms your specific arbitrary data point structure into a perfect Gaussian Normal Distribution.

- **Box-Cox:** Data strictly must be positive ( $> 0$).
- **Yeo-Johnson:** Elegantly handles negative numbers and exact zeros implicitly.

```python
from sklearn.preprocessing import PowerTransformer

# Defaults to Yeo-Johnson
pt = PowerTransformer()
df["gaussian_price"] = pt.fit_transform(df[["price"]])
print(f"Algorithm applied Lambda: {pt.lambdas_[0]}")
```

### 3. Rank Transformation (Non-Parametric)

For situations absolutely dominated by savage outliers where nothing fixes the skew, you abandon the values completely and sort the list. The smallest number becomes `1`, the second becomes `2`, the billion outlier becomes `3`. This permanently flattens the distribution into a uniform rectangle, erasing distances but guaranteeing model convergence stability.

```python
df["rank_price"] = df["price"].rank()
```
