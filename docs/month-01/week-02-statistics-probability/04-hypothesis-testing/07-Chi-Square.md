# Chi-Square ($\chi^2$) Test

## 1. Intuition

Imagine you roll a die 60 times. You _expect_ each number (1 through 6) to come up roughly 10 times. However, in reality, you get twenty 6s and only three 1s. Is the die loaded, or was it just a wildly unlucky fluke?

T-tests deal with _continuous_ numbers (like height, weight, money). But what happens when your data is just grouping or counting _categories_ (like "Male/Female" or "Red/Blue/Green")? The **Chi-Square Test** was invented specifically to figure out if the categorical "counts" we observe are weirdly different from the counts we _expected_ to see.

## 2. Definition

The **Chi-Square ($\chi^2$) Test** is a non-parametric statistical hypothesis test used exclusively for _categorical_ data to determine if there is a significant association between two variables, or if a single variable follows an expected distribution.

There are two main types:

- **Goodness of Fit Test**: Tests if a single categorical variable matches an expected distribution (e.g., Is this die actually fair?).
- **Test of Independence**: Tests if _two_ categorical variables are related to each other (e.g., Is movie genre preference independent of gender?).

## 3. Formula

**Chi-Square Statistic:**
$$\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$$

Where:

- $O_i$ = Observed value (the actual count of a category in your data)
- $E_i$ = Expected value (what the count _should_ be if the null hypothesis is perfectly true)

_(The test simply calculates how far your observed counts deviate from the expected counts. If the sum is very large, the groups are statistically different)._

## 4. Examples & Code

### Theory Example: Customer Demographics

A store expects its customers to be 50% Men, 50% Women.
They randomly sample 100 people walking in.

- **Expected**: 50 Men, 50 Women.
- **Observed**: 30 Men, 70 Women.

$\chi^2 = \frac{(30 - 50)^2}{50} + \frac{(70 - 50)^2}{50} = \frac{(-20)^2}{50} + \frac{20^2}{50} = \frac{400}{50} + \frac{400}{50} = 8 + 8 = 16$.
A $\chi^2$ value of $16$ (with 1 degree of freedom) yields a tiny P-value. Conclusion: The store's audience is definitely skewed towards women.

### Code Example (Python/Scipy) - Test of Independence

_Are 'Eye Color' and 'Hair Color' related?_

```python
import numpy as np
import pandas as pd
from scipy.stats import chi2_contingency

# We survey 200 people.
# The table shows counts of [Black Hair, Blonde Hair].
# Row 1 = Brown Eyes [60, 20]
# Row 2 = Blue Eyes  [20, 100]
data = np.array([[60, 20],
                 [20, 100]])

# H0: Hair color and eye color are completely independent.
# H1: They are related/dependent.
chi2_stat, p_val, dof, expected = chi2_contingency(data)

print(f"Chi-Square Stat: {chi2_stat:.2f}")
print(f"P-Value: {p_val:.10f}")
print(f"\nExpected Frequencies if completely independent:\n{expected}")

if p_val < 0.05:
    print("\nReject Null: Hair and eye color are strongly associated!")
```

## 5. Case Study: E-Commerce Bug Detection (Goodness of Fit)

**Scenario**: An online retailer has four main product categories: Electronics, Clothing, Home, and Toys. Historically, organic search traffic lands exactly 25% evenly across all four categories.

**Application**: One day, the traffic numbers come in: Electronics (40%), Clothing (10%), Home (25%), Toys (25%).
A data scientist's automated monitoring script runs a **Chi-Square Goodness of Fit Test** on these daily categorical counts versus the highly reliable historical expectations.

Because the $\chi^2$ score is massively inflated by the sudden drop in 'Clothing.' The script immediately alerts the engineering team, rejecting the null hypothesis that traffic is normal. The engineers investigate and find a broken database link was preventing the 'Clothing' homepage from rendering correctly.
