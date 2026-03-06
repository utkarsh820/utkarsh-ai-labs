
## **The Feature Relationship Roadmap**

| Level | Method | Best For... | Logic | Interpretation |
| --- | --- | --- | --- | --- |
| **Basic** | **Pearson ($r$)** | Linear relationships | Straight-line correlation | **1.0** (Perfect line), **0** (No line) |
| **Intermediate** | **Spearman ($\rho$)** | Non-linear trends | Rank-based correlation | **1.0** (Always increases), **0** (No trend) |
| **Advanced** | **PPS** | Hidden patterns | Decision Tree prediction | **1.0** (Predicts perfectly), **0** (Naive guess) |
| **Elite** | **Mutual Info (MI)** | Complex dependency | Information Theory (Entropy) | **Higher is better** (Reduces uncertainty) |
| **State-of-Art** | **SHAP** | Feature Influence | Game Theory (Shapley values) | **+/- Value** (Impact on specific output) |

---

## **Implementation Guide & Interpretation**

### **1. Basic: Pearson Correlation**

**What it does:** Measures the strength of a linear "straight line" relationship between two numbers.

* **When to use:** First step in any EDA to find redundant features.
* **Code:** `df.corr(method='pearson')`
* **Interpretation:** If $r > 0.8$, the variables are nearly identical. If $r \approx 0$, it doesn't mean there's *no* relationship; it just means there's no *linear* one.

### **2. Intermediate: Spearman Rank**

**What it does:** Measures "monotonic" relationships—if $X$ goes up, does $Y$ *eventually* go up, regardless of the shape?

* **When to use:** When you have outliers or non-linear curves (like exponential growth).
* **Code:** `df.corr(method='spearman')`
* **Interpretation:** Better than Pearson for "curvy" data. It is less sensitive to extreme outliers.

### **3. Advanced: Predictive Power Score (PPS)**

**What it does:** Uses a single-variable Decision Tree to see if $X$ can predict $Y$.

* **When to use:** When you have mixed data (strings + numbers) or suspect "one-way" relationships.
* **Code:** ```python
import ppscore as pps
pps.matrix(df)
```

```


* **Interpretation:** **Asymmetric.** If $X \to Y$ is 0.8 but $Y \to X$ is 0.1, $X$ is a great predictor, but you can't work backward.

### **4. Elite: Mutual Information (MI)**

**What it does:** Measures how much "information" you gain about $Y$ by knowing $X$. It catches **any** relationship (circles, waves, patterns).

* **When to use:** The industry standard for feature selection in complex models (XGBoost/LightGBM).
* **Code:**
```python
from sklearn.feature_selection import mutual_info_regression
mi_scores = mutual_info_regression(X, y)

```


* **Interpretation:** It is "model-agnostic." A high MI score means the two variables are deeply linked, even if the pattern looks like total chaos on a standard graph.

---

## **Practical Workshop: Side-by-Side Comparison**

If you want to show your students the power of these tools, use this snippet to compare them on a **non-linear** relationship:

```python
import pandas as pd
import numpy as np
import ppscore as pps
from sklearn.feature_selection import mutual_info_regression

# Create a non-linear relationship (Parabola)
x = np.linspace(-10, 10, 100)
y = x**2  # Purely non-linear
df = pd.DataFrame({'X': x, 'Y': y})

# 1. Pearson (Will be 0 because it's not a line)
print(f"Pearson: {df.corr().iloc[0,1]:.2f}")

# 2. PPS (Will be high because it sees the pattern)
print(f"PPS: {pps.score(df, 'X', 'Y')['ppscore']:.2f}")

# 3. Mutual Info (Will be high)
mi = mutual_info_regression(df[['X']], df['Y'])[0]
print(f"Mutual Info: {mi:.2f}")

```