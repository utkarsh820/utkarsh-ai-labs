# Hypothesis Testing: Master Code Cheatsheet

This document serves as a one-stop-shop compiling the Python implementations for the most common statistical hypothesis tests using `scipy.stats` and `statsmodels`.

---

## 1. One-Sample T-Test

_Use Case_: Comparing your single sample against a known, historical population mean.

```python
import numpy as np
from scipy import stats

# 1. Generate Data
np.random.seed(42)
sample_data = np.random.normal(loc=98, scale=5, size=30)
known_population_mean = 100

# 2. Run Test
# H0: Sample Mean == 100
t_stat, p_value = stats.ttest_1samp(sample_data, known_population_mean)

print(f"One-Sample T-Test P-Value: {p_value:.4f}")
```

## 2. Independent Two-Sample T-Test

_Use Case_: Comparing the means of two distinctly different, independent groups (e.g., Men vs Women, Diet A vs Diet B).

```python
# 1. Generate Data
group_A = np.random.normal(loc=50, scale=10, size=50)
group_B = np.random.normal(loc=55, scale=10, size=50)

# 2. Run Test
# H0: Mean of Group A == Mean of Group B
t_stat, p_value = stats.ttest_ind(group_A, group_B, equal_var=False)
# Note: Welch's T-test (equal_var=False) is generally safer in reality!

print(f"Two-Sample T-Test P-Value: {p_value:.4f}")
```

## 3. Paired T-Test (Dependent)

_Use Case_: Comparing means of the _same_ subjects under two conditions (e.g., Before Treatment vs After Treatment).

```python
# 1. Generate Data (Subject numbers must line up perfectly by index)
before_scores = np.random.normal(loc=60, scale=15, size=40)
# 'After' scores get a +5 point bump, but same people
after_scores = before_scores + np.random.normal(loc=5, scale=2, size=40)

# 2. Run Test
# H0: Mean Difference (After - Before) == 0
t_stat, p_value = stats.ttest_rel(after_scores, before_scores)

print(f"Paired T-Test P-Value: {p_value:.4f}")
```

## 4. One-Way ANOVA

_Use Case_: Comparing the means of three or more independent groups simultaneously (e.g., Diet A vs Diet B vs Diet C vs Control).

```python
# 1. Generate Data
group_1 = np.random.normal(loc=5.0, scale=1.5, size=20)
group_2 = np.random.normal(loc=5.1, scale=1.5, size=20)
group_3 = np.random.normal(loc=7.5, scale=1.5, size=20) # Outperformer

# 2. Run Test
# H0: Mean 1 == Mean 2 == Mean 3
f_stat, p_value = stats.f_oneway(group_1, group_2, group_3)

print(f"ANOVA P-Value: {p_value:.4f}")
```

## 5. Chi-Square Test of Independence

_Use Case_: Checking if two Categorical variables are related (e.g., Is "Movie Genre Preference" independent of "User Gender"?).

```python
import pandas as pd
from scipy.stats import chi2_contingency

# 1. Setup Contingency Table (Counts of occurrences)
#               | Action | Comedy | Horror |
#         Men   |   50   |   30   |   20   |
#       Women   |   20   |   60   |   20   |
observed_counts = np.array([[50, 30, 20],
                            [20, 60, 20]])

# 2. Run Test
# H0: Gender and Genre Preference are completely independent
chi2_stat, p_value, dof, expected_counts = chi2_contingency(observed_counts)

print(f"Chi-Square P-Value: {p_value:.4f}")
```

## 6. Z-Test (For Means)

_Use Case_: You have a large sample ($n>30$) and, crucially, you know the absolute true _Population Standard Deviation_ ($\sigma$). Rarely used in practice over T-tests.

```python
from statsmodels.stats.weightstats import ztest

# 1. Generate Data
sample_data = np.random.normal(loc=102, scale=15, size=100)
population_mean = 100

# 2. Run Test
# H0: Sample Mean == 100
z_score, p_value = ztest(sample_data, value=population_mean)

print(f"Z-Test P-Value: {p_value:.4f}")
```
