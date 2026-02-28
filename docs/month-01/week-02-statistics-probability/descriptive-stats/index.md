# Descriptive Statistics Essentials Index (0 → Elite)

| Topic Area | Beginner (Foundations) | Intermediate (Engineering) | Advanced / Elite (Optimization & Internals) |
| :--- | :--- | :--- | :--- |
| **Central Tendency** | Mean, Median, Mode | Weighted mean, Trimmed mean | Geometric mean, Harmonic mean, Winsorized mean |
| **Dispersion** | Range, Variance, Standard Deviation | Interquartile Range (IQR), MAD | Coefficient of Variation, Robust scale estimators |
| **Position** | Min, Max, Percentiles | Quartiles, Deciles | Quantile functions, Order statistics |
| **Shape** | Skewness (concept) | Kurtosis (concept) | Moment-based shape analysis, Jarque-Bera test |
| **Distribution Visualization** | Histogram, Bar chart | Box plot, Violin plot | ECDF, Q-Q plot, Ridge plots, Heatmaps |
| **Frequency Tables** | Count, Simple frequency | Relative frequency, Cumulative frequency | Cross-tabulation, Contingency tables |
| **Data Types** | Numerical vs Categorical | Discrete vs Continuous, Ordinal vs Nominal | Interval vs Ratio, Mixed-type handling |
| **Outlier Detection** | Visual inspection | IQR method (1.5× rule) | Z-score method, Modified Z-score, Isolation Forest |
| **Missing Data** | Count missing values | Missing percentage, Patterns | MCAR/MAR/MNAR classification, Missingness heatmap |
| **Data Quality** | Duplicate detection | Unique value counts | Data validation rules, Schema enforcement |
| **Aggregation** | Sum, Count, Mean | GroupBy aggregations | Multi-level aggregation, Custom agg functions |
| **Bivariate Analysis** | Scatter plot, Side-by-side bars | Covariance, Correlation matrix | Pairwise relationships, Conditional distributions |
| **Multivariate Analysis** | — | Pair plots, Correlation heatmaps | PCA for exploration, Parallel coordinates |
| **Time-Based Descriptives** | Time period counts | Trend lines, Moving averages | Seasonal decomposition, Lag features |
| **Categorical Summaries** | Frequency, Mode | Proportions, Percentages | Entropy, Diversity indices, Mode stability |
| **Numerical Summaries** | 5-number summary | Describe() output | Extended summaries, Custom summary stats |
| **Data Transformation** | Log, Square root | Standardization (Z-score), Normalization (Min-Max) | Box-Cox, Yeo-Johnson, Rank transformation |
| **Binning** | Equal-width bins | Equal-frequency bins | Optimal binning (Sturges, Freedman-Diaconis) |
| **Summary Tables** | Basic stat tables | Grouped summary tables | Multi-index summary, Styled reports |
| **Reporting** | Basic statistics output | Formatted tables (rounding) | Automated reports, APA-style tables, Dashboards |

---

### Quick Reference: Descriptive Stats by Data Type

| Data Type | Central Tendency | Dispersion | Visualization |
| :--- | :--- | :--- | :--- |
| **Numerical (Normal)** | Mean | Std Dev, Variance | Histogram, Box plot |
| **Numerical (Skewed)** | Median | IQR, MAD | Box plot, Violin plot |
| **Ordinal** | Median, Mode | Range, Percentiles | Bar chart, Cumulative freq |
| **Nominal** | Mode | Frequency, Proportion | Bar chart, Pie chart |
| **Time Series** | Moving average | Rolling std | Line plot, Area chart |

---

### Essential Python Libraries

| Library | Purpose | Key Functions |
| :--- | :--- | :--- |
| `pandas` | Data summarization | `describe()`, `agg()`, `groupby()`, `value_counts()` |
| `numpy` | Numerical operations | `mean()`, `std()`, `percentile()`, `histogram()` |
| `scipy.stats` | Distribution stats | `skew()`, `kurtosis()`, `describe()` |
| `matplotlib` | Basic visualization | `hist()`, `boxplot()`, `scatter()` |
| `seaborn` | Statistical visualization | `distplot()`, `boxplot()`, `pairplot()`, `heatmap()` |
| `pingouin` | Extended descriptives | `describe()`, `summary_stats()` |

---

### Key Formulas Reference

| Measure | Formula | Python Equivalent |
| :--- | :--- | :--- |
| **Mean** | Σx / n | `np.mean()` |
| **Median** | Middle value | `np.median()` |
| **Variance** | Σ(x - mean)² / (n-1) | `np.var(ddof=1)` |
| **Std Deviation** | √Variance | `np.std(ddof=1)` |
| **IQR** | Q3 - Q1 | `np.percentile(75) - np.percentile(25)` |
| **Skewness** | E[(x-μ)³] / σ³ | `scipy.stats.skew()` |
| **Kurtosis** | E[(x-μ)⁴] / σ⁴ - 3 | `scipy.stats.kurtosis()` |
| **CV** | (Std Dev / Mean) × 100 | `(std/mean)*100` |
| **Z-Score** | (x - mean) / std | `scipy.stats.zscore()` |

---

### 5-Number Summary Checklist

| Statistic | Description | Python |
| :--- | :--- | :--- |
| **Minimum** | Smallest value | `df.min()` |
| **Q1 (25th)** | Lower quartile | `df.quantile(0.25)` |
| **Median (50th)** | Middle value | `df.median()` |
| **Q3 (75th)** | Upper quartile | `df.quantile(0.75)` |
| **Maximum** | Largest value | `df.max()` |