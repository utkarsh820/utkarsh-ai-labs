# T-Test (Student's T-Test)

## 1. Intuition

Imagine a teacher testing whether a brand-new studying technique actually improves test scores. They only have a class of 15 students ($n = 15$). They don't know the "historical standard deviation of all students who have ever lived." They just have their small class data.

Because the sample is small and the true population standard deviation is entirely unknown, we cannot trust the strict, thin tail of a Normal Curve (Z-test). Instead, we use a **T-test**, which relies on a "fatter, wider" curve that accounts for the extreme uncertainty of small sample sizes.

_If Z-test is a surgical scalpel (precise but requires perfect population knowledge), the T-test is a Swiss Army Knife (works almost anywhere)._

## 2. Definition

A **T-Test** is an inferential statistical test that determines if there is a significant difference between the means of groups, specifically when the population variance is unknown and/or the sample size is small ($n < 30$).

There are three main types:

- **One-Sample T-test:** Compares a single sample mean to a known population mean.
- **Independent Two-Sample T-test:** Compares the means of two entirely unrelated groups (e.g., Men vs Women).
- **Paired T-test:** Compares means from the same group at different times (e.g., Before and After a drug trial).

## 3. Formula

**(One-Sample) T-Statistic:**
$$t = \frac{\bar{x} - \mu}{\frac{s}{\sqrt{n}}}$$

Where:

- $\bar{x}$ = Sample Mean
- $\mu$ = Population Mean
- $s$ = **Sample** Standard Deviation (We estimate $\sigma$ using $s$)
- $n$ = Sample Size

_Because we estimate the variance, we also must calculate **Degrees of Freedom (df)** $= n - 1$. The shape of the T-distribution changes depending on the df._

## 4. Examples & Code

### Theory Example: Energy Drinks

An energy drink claims to contain 150mg of caffeine. We buy 12 cans and test them ($n=12$). The average is 145mg ($\bar{x}$) with a sample standard deviation of 8mg ($s$).
$$t = \frac{145 - 150}{8 / \sqrt{12}} = \frac{-5}{2.31} \approx -2.16$$
Using a T-table at $11$ degrees of freedom ($12-1$), we can map this T-score to a P-value to determine if the company is lying about their caffeine content.

### Code Example (Python/Scipy) - Independent 2-Sample T-Test

_Does Diet A result in more weight loss than Diet B?_

```python
import numpy as np
from scipy import stats

np.random.seed(42)

# Weight loss (kg) for 20 people on Diet A
diet_A = np.random.normal(loc=5.5, scale=1.5, size=20)

# Weight loss (kg) for 20 people on Diet B
diet_B = np.random.normal(loc=4.0, scale=1.2, size=20)

# Independent 2-Sample T-Test
# Null Hypothesis: Diet A mean == Diet B mean
t_stat, p_value = stats.ttest_ind(diet_A, diet_B)

print(f"T-Statistic: {t_stat:.4f}")
print(f"P-Value:     {p_value:.6f}")

if p_value < 0.05:
    print("Reject Null: Diets have significantly different effectiveness.")
else:
    print("Fail to Reject: Diets perform statistically the same.")
```

## 5. Case Study: Website A/B Testing (Two-Sample T-Test)

**Scenario**: A tech startup is launching a new checkout flow. They want to know if "Checkout Flow B" yields a higher average order value (AOV) than the old "Checkout Flow A." They launch both flows on a Monday morning and collect 500 orders from each.

**Application**: They don't know the true population standard deviation of _all future customers_. Therefore, they must use the standard deviations derived directly from their two samples of 500.

A data analyst runs an **Independent Two-Sample T-Test**. The algorithm compares `Average_A` vs `Average_B`, punishing the math accordingly if the spread (variance) of the orders was wildly unpredictable. The resulting P-value tells the CEO whether the new checkout flow actually encouraged people to spend mathematically more money, or if the variance was just random daily noise.
