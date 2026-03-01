# Z-Test

## 1. Intuition

Imagine you own a bakery that has famously sold exactly 500-gram loaves of bread for decades. A new baker takes over, and suddenly customers complain the loaves feel suspiciously light. You want to test if the new baker is shortchanging customers. A **Z-test** helps you answer the question: _"Is this new sample I'm looking at statistically different from the historical population we already know everything about?"_

It only works perfectly if you have historical data running like clockwork (i.e. you strictly know the _true population variance_).

## 2. Definition

A **Z-Test** is a statistical hypothesis test used to determine whether two population means are different when the variances are known AND the sample size is large (usually $n \ge 30$).

Z-tests rely strictly on the standard normal distribution (Z-distribution) and dictate how many standard deviations ($Z$-score) a data point or sample mean is from the population mean.

## 3. Formula

**One-Sample Z-Test for a Mean:**
$$Z = \frac{\bar{x} - \mu}{\frac{\sigma}{\sqrt{n}}}$$

Where:

- $\bar{x}$ = Mean of your sample
- $\mu$ = Mean of the population
- $\sigma$ = Standard deviation of the population (Must be known!)
- $n$ = Number of observations in your sample

## 4. Examples & Code

### Theory Example: Factory Quality

A factory manufactures lightbulbs that last exactly 1000 hours on average ($\mu$), with a well-documented standard deviation of 50 hours ($\sigma$). You test a new batch of 100 bulbs ($n$) and their average lifespan is 985 hours ($\bar{x}$).
$$Z = \frac{985 - 1000}{50 / \sqrt{100}} = \frac{-15}{5} = -3$$
A Z-score of -3 means your sample is 3 standard deviations below typical performance. This is exceedingly rare, strongly implying the new batch of bulbs is systematically defective.

### Code Example (Python/Scipy)

_Note: Python's `scipy.stats` does not have a dedicated 1-sample Z-test function because T-tests are almost exclusively used in practice. We use `statsmodels`._

```python
import numpy as np
from statsmodels.stats.weightstats import ztest

# Simulate lifetimes of 100 recent lightbulbs (defect batch)
np.random.seed(42)
sample_lifetimes = np.random.normal(loc=985, scale=50, size=100)

# We know historical Population Mean = 1000
population_mean = 1000

# Perform the Z-test
# H0: Sample mean == 1000
# H1: Sample mean != 1000
z_score, p_value = ztest(sample_lifetimes, value=population_mean)

print(f"Z-Score: {z_score:.4f}")
print(f"P-Value: {p_value:.6f}")

if p_value < 0.05:
    print("Reject Null Hypothesis (Batch is defective!)")
else:
    print("Fail to Reject (Batch is normal)")
```

## 5. Case Study: Algorithmic Trading (Pairs Trading Strategy)

**Scenario**: In algorithmic trading, quantitative analysts look for two stocks that historically move together (e.g., Coke and Pepsi). The price _difference_ between them usually hovers around \$0 on average (with a known standard deviation). They model this spread as a normal distribution.

**Application**: A trading bot constantly performs a rolling **Z-Test** on the price difference. If negative news hits Coke and the price spread suddenly yields a $Z$-score of $-2.5$ (meaning Pepsi is unusually expensive compared to Coke based on historical norms), the bot automatically rejects the null hypothesis that "everything is normal." Relying on mean reversion, the bot shorts Pepsi and buys Coke, betting they will drift back to their historical equilibrium.
