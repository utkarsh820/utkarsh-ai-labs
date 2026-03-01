# Bivariate and Multivariate

_Moving beyond single variables (univariate) to explore how two or more variables interact with one another simultaneously._

---

## 🟢 Beginner (Foundations)

### 1. Scatter Plots

The fundamental plotting technique to see the raw visual relationship between two numerical variables.

- **Python Implementation:**

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

sns.scatterplot(x="total_bill", y="tip", data=df)
plt.title("Total Bill vs. Tip Amount")
plt.show()
```

### 2. Side-by-Side Bar Charts

Comparing continuous outputs across multiple different categories visually.

- **Python Implementation:**

```python
sns.barplot(x="day", y="total_bill", hue="smoker", data=df)
plt.title("Bill by Day and Smoker Status")
plt.show()
```

---

## 🟡 Intermediate (Engineering)

### 1. Covariance vs. Correlation

- **Covariance:** Measures the _direction_ of the relationship between two variables. Very difficult to interpret because the scale relies entirely on the original data units (e.g., measuring height in miles vs. inches changes covariance completely).
- **Correlation (Pearson's $r$):** The standardized version of covariance. It objectively bounds the relationship strictly between `-1` (perfect inverse) and `+1` (perfect positive). A value of `0` means absolutely zero _linear_ relationship.

```python
correlation = df[["total_bill", "tip"]].corr()
print("Pearson Correlation:\n", correlation)
```

### 2. Correlation Matrices and Heatmaps

Applying the underlying $r$-correlation formula to every single numerical column against every other numerical column simultaneously to build a matrix.

- **Python Implementation:**

```python
numeric_df = df.select_dtypes(include=['float64', 'int64'])
matrix = numeric_df.corr()

sns.heatmap(matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap")
plt.show()
```

### 3. Pair Plots

Creates a grid of scatterplots for every single pair of variables while drawing the histogram distributions diagonally.

```python
sns.pairplot(df, hue="sex")
plt.show()
```

---

## 🔴 Advanced / Elite (Optimization)

### 1. Pairwise Non-Linear Relationships (Spearman & Kendall)

Pearson only detects _linear_ relationships (straight lines). If `y = x^2` (an exponential curve), Pearson might read `0.0`.

- **Spearman's Rho:** Looks strictly at the _rank_ order of variables. If variable X goes up, does variable Y go up (regardless of how fast)?
- **Kendall's Tau:** Excellent for incredibly small sample sizes where ranking is critical.

```python
spearman_corr = df[["total_bill", "tip"]].corr(method="spearman")
print("Spearman Rank Correlation:\n", spearman_corr)
```

### 2. PCA (Principal Component Analysis) for EDA Exploration

When a dataset has 50 columns, you cannot possibly visualize 50 dimensions on a flat screen or find simple pair plots. PCA is an extremely powerful linear algebra technique (SVD) applied to rotationally project 50 dimensions flat onto a 2D or 3D graph (the "Components" capturing the maximum variance).

```python
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

# Standardize data strictly first before PCA
scaler = StandardScaler()
scaled = scaler.fit_transform(numeric_df)

pca = PCA(n_components=2)
principal_components = pca.fit_transform(scaled)

plt.scatter(principal_components[:, 0], principal_components[:, 1])
plt.xlabel("First Principal Component")
plt.ylabel("Second Principal Component")
plt.title("2D Projection of High-Dimensional Variance")
plt.show()
```
