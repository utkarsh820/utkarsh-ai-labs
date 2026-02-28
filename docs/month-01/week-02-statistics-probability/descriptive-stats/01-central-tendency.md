# Central Tendency

_Central tendency measures describe the "center" or "typical" value of a dataset. Understanding these is the fundamental first step in any exploratory data analysis._

---

## 🟢 Beginner (Foundations)

### 1. Mean (Arithmetic Average)

The mean is the sum of all values divided by the number of values. It is highly sensitive to outliers.

- **Formula:** $\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i$
- **Python Implementation:**

```python
import pandas as pd
import numpy as np

data = [10, 20, 30, 40, 50, 1000] # 1000 is an outlier
mean_val = np.mean(data)
print(f"Mean: {mean_val}") # Output: 191.66
```

### 2. Median

The median is the middle value when the data is sorted. It is **robust** (not heavily affected by outliers).

- **Python Implementation:**

```python
median_val = np.np.median(data)
print(f"Median: {median_val}") # Output: 35.0
```

### 3. Mode

The mode is the most frequently occurring value. Useful specifically for categorical data.

- **Python Implementation:**

```python
from scipy import stats
mode_val = stats.mode([1, 2, 2, 3, 4], keepdims=True)
print(f"Mode: {mode_val.mode[0]}") # Output: 2
```

---

## 🟡 Intermediate (Engineering)

### 1. Weighted Mean

Used when certain data points contribute more "weight" or importance than others (e.g., calculating GPA from credits).

- **Formula:** $\bar{x}_w = \frac{\sum_{i=1}^{n}w_i x_i}{\sum_{i=1}^{n}w_i}$
- **Python Implementation:**

```python
values = [80, 90, 95]
weights = [0.2, 0.3, 0.5] # Exams weights
weighted_mean = np.average(values, weights=weights)
print(f"Weighted Mean: {weighted_mean}") # Output: 90.5
```

### 2. Trimmed Mean

A compromise between the mean and median. It involves discarding a certain percentage of the lowest and highest values before calculating the mean, explicitly removing outliers.

- **Python Implementation:**

```python
from scipy.stats import trim_mean
# Trim 10% from both ends
trimmed = trim_mean([1, 2, 3, 4, 5, 6, 7, 8, 9, 1000], proportiontocut=0.1)
print(f"Trimmed Mean: {trimmed}") # Output: 5.5
```

---

## 🔴 Advanced / Elite (Optimization)

### 1. Geometric Mean

Used for data that grows multiplicatively (e.g., compounding interest rates, investment returns, or biological cell growth). It answers: "What is the constant growth rate?"

- **Formula:** $GM = \sqrt[n]{x_1 \cdot x_2 \cdots x_n}$
- **Python Implementation:**

```python
from scipy.stats import gmean
returns = [1.05, 1.10, 0.95] # 5% gain, 10% gain, 5% loss
geom_mean = gmean(returns)
print(f"Geometric Mean: {geom_mean}")
```

### 2. Harmonic Mean

Used when calculating the average of rates or ratios (e.g., average speed given distance, or P/E ratios in finance).

- **Formula:** $HM = \frac{n}{\sum_{i=1}^{n}\frac{1}{x_i}}$
- **Python Implementation:**

```python
from scipy.stats import hmean
speeds = [60, 40] # Outward at 60mph, return at 40mph over same distance
har_mean = hmean(speeds)
print(f"Harmonic Mean (Average Speed): {har_mean}") # Output: 48.0
```

### 3. Winsorized Mean

Instead of trimming (removing) outliers, Winsorizing replaces extreme values with the nearest "acceptable" value (e.g., capping the 99th percentile). This retains the data point count but reduces variance explosion.

- **Python Implementation:**

```python
from scipy.stats import mstats
# Cap bottom 5% and top 5%
data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 100]
winsorized_data = mstats.winsorize(data, limits=[0.05, 0.05])
print(f"Winsorized Mean: {np.mean(winsorized_data)}")
```
