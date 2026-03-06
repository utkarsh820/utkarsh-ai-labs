# PowerTransformer (Forcing Normality)

**Level:** Advanced → Elite  
**Time to Complete:** 30 Minutes (Reading + Practice)

---

## 📘 Part 1: Why Do We Care About "Normality"?

In statistics, the **Normal Distribution** (the Bell Curve / Gaussian Distribution) is the holy grail.

Many of the most powerful and fundamentally sound machine learning algorithms—specifically **Linear Regression**, **Logistic Regression**, and **Linear Discriminant Analysis (LDA)**—carry a hidden mathematical assumption: _They assume your input features are normally distributed._

### The Real World is Skewed

Unfortunately, real-world data is almost never a bell curve. Things like **Income**, **House Prices**, and **Website Traffic** are usually "Right-Skewed." (Most people make $50k, fewer make $150k, and one guy makes $100 Billion). This long tail ruins regression models by dragging the "line of best fit" toward the extreme outliers.

We need a mathematical mechanism to squish the long tail inward, forcing a Bell Curve shape.

---

## 🟢 Level 1: The Basics (`PowerTransformer`)

Scikit-Learn provides the `PowerTransformer`. It applies mathematical power functions (like exponents and logarithms) to stabilize variance and minimize skewness.

```python
import numpy as np
import pandas as pd
from sklearn.preprocessing import PowerTransformer

# Generating a heavily right-skewed dataset
data = np.random.exponential(scale=2.0, size=(1000, 1))

# Initialize the PowerTransformer
# standardize=True means it automatically applies StandardScaler after transforming
pt = PowerTransformer(method='yeo-johnson', standardize=True)

# Transform the data
normal_data = pt.fit_transform(data)
```

---

## 🟡 Level 2: Yeo-Johnson vs. Box-Cox

The `PowerTransformer` supports two different mathematical methods. You must choose carefully.

### 1. Box-Cox

Invented in 1964. It is extremely powerful but has a fatal flaw: **It only works on strictly positive data ($X > 0$).** If your column contains `0` or negative numbers, Box-Cox will crash.

- **Math:** It searches for an optimal parameter $\lambda$. If $\lambda = 0$, it applies a pure natural log ($\ln x$). Otherwise, it applies $(x^\lambda - 1)/\lambda$.

### 2. Yeo-Johnson

Invented in 2000. It is a modification of Box-Cox that **handles positive, zero, and negative values.**

- **Rule of Thumb:** Use `yeo-johnson` (it is the default in Scikit-Learn). Use `box-cox` only if you explicitly know for a fact your data is strictly positive and you are following a rigorous academic paper.

---

## 🟠 Level 3: Proof (Q-Q Plots)

How do you know the Transformation actually worked? You could plot a histogram, but histograms can be deceiving based on how the bins are cut.

The elite statistical way to verify normality is a **Probability Plot** (or Q-Q Plot).

```python
import scipy.stats as stats
import matplotlib.pyplot as plt

# 1. Let's look at the original skewed data
plt.figure()
# The red line is a perfect Bell Curve. The blue dots are our data.
stats.probplot(data.flatten(), dist="norm", plot=plt)
plt.title("Before Transformation: Exponential Data")
plt.show() # The dots curve violently away from the red line.

# 2. Let's look at the transformed data
plt.figure()
stats.probplot(normal_data.flatten(), dist="norm", plot=plt)
plt.title("After PowerTransformer")
plt.show() # Magic! The blue dots now perfectly hug the red line!
```

---

## 🏁 Academy Exercise

**Task:**

1. Generate an array of 5,000 random samples from a Lognormal distribution: `np.random.lognormal(mean=0, sigma=1, size=(5000, 1))`.
2. Extract the data and plot its histogram (notice the intense skew).
3. Apply `PowerTransformer(method='yeo-johnson')`.
4. Plot the histogram of the new data. Notice the perfect bell shape!
