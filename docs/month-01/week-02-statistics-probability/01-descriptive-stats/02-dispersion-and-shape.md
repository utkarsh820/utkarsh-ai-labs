# Dispersion and Shape

_While Central Tendency tells us where the data "lives", Dispersion tells us how "spread out" it is. Shape tells us if the data leans heavily to one side (Skewness) or has heavy tails (Kurtosis)._

---

## 🟢 Beginner (Foundations)

### 1. Range

The absolute difference between the largest and smallest values. It is completely susceptible to outliers.

- **Formula:** $Range = Max(x) - Min(x)$
- **Python Implementation:**

```python
import numpy as np
data = [10, 20, 30, 40, 50]
range_val = np.ptp(data) # ptp stands for "peak to peak"
```

### 2. Variance & Standard Deviation

Variance measures the average squared distance from the mean. Standard Deviation ($\sigma$) takes the square root of Variance to return the metric back to its original units (e.g., dollars² back to dollars).

- **Formula (Sample Variance):** $s^2 = \frac{\sum(x_i - \bar{x})^2}{n - 1}$
- **Python Implementation:**

```python
variance = np.var(data, ddof=1) # ddof=1 makes it a Sample Variance
std_dev = np.std(data, ddof=1)
print(f"Variance: {variance}, Standard Deviation: {std_dev}")
```

### 3. Skewness (Concept)

Skewness measures the _asymmetry_ of a distribution around its mean.

- **Positive Skew (Right-skewed):** Tail is on the right side. Mean > Median > Mode. (e.g., Household income)
- **Negative Skew (Left-skewed):** Tail is on the left side. Mode > Median > Mean. (e.g., Age of retirement)

---

## 🟡 Intermediate (Engineering)

### 1. Interquartile Range (IQR)

A robust measure of spread. It calculates the range of the middle 50% of the data, completely ignoring the top 25% and bottom 25% outliers.

- **Formula:** $IQR = Q_3 - Q_1$ (75th percentile minus 25th percentile)
- **Python Implementation:**

```python
q3, q1 = np.percentile(data, [75, 25])
iqr = q3 - q1
print(f"IQR: {iqr}")
```

### 2. Mean Absolute Deviation (MAD)

Instead of squaring distances like Variance does (which penalizes extreme outliers heavily), MAD simply takes the absolute value of the distances from the median. Highly robust.

- **Python Implementation:**

```python
median = np.median(data)
mad = np.median(np.abs(data - median))
print(f"Robust MAD: {mad}")
```

### 3. Kurtosis (Concept)

Kurtosis measures the "tailedness" of the data distribution compared to a Normal Distribution. High kurtosis indicates heavy tails (high likelihood of extreme outliers).

- **Mesokurtic:** Normal distribution behavior (Kurtosis ~3, Excess Kurtosis ~0)
- **Leptokurtic:** Heavy tails, sharp peak (Excess Kurtosis > 0)
- **Platykurtic:** Light tails, flat peak (Excess Kurtosis < 0)

---

## 🔴 Advanced / Elite (Optimization)

### 1. Coefficient of Variation (CV)

The ratio of the standard deviation to the mean. It allows you to objectively compare the "risk" or volatility of two completely different datasets (like comparing the volatility of a $10 stock vs. a $1000 stock).

- **Formula:** $CV = (\frac{\sigma}{\mu}) \times 100$
- **Python Implementation:**

```python
mean_val = np.mean(data)
std_val = np.std(data, ddof=1)
cv = (std_val / mean_val) * 100
print(f"Coefficient of Variation: {cv}%")
```

### 2. Robust Scale Estimators (Rousseeuw's Sn and Qn)

In quantitative finance and elite data science, standard deviation breaks instantly. IQR is better but inefficient. `Sn` and `Qn` are highly efficient, highly robust estimators of scale that survive up to a 50% contamination rate in your dataset.

- **Python Implementation (using `statsmodels`):**

```python
import statsmodels.robust.scale as robust
rc = robust.mad(data) # Normalized MAD
print(f"Robust Scale: {rc}")
```

### 3. Moment-Based Shape Analysis (Moments 1-4)

In probability theory:

- **1st Moment (Mean):** Location
- **2nd Central Moment (Variance):** Scale
- **3rd Standardized Moment:** Skewness
- **4th Standardized Moment:** Kurtosis

```python
from scipy.stats import moment, skew, kurtosis
m1 = moment(data, moment=1)
m2 = moment(data, moment=2)
# Fisher defined normal kurtosis as 0 (Excess Kurtosis)
kurt = kurtosis(data, fisher=True)
print(f"Skew: {skew(data)}, Excess Kurt: {kurt}")
```
