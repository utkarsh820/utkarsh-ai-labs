# Introduction to Distributions

## 1. Intuition

Imagine a classroom of 100 students taking a 100-point exam. If you plotted their scores on a graph where the horizontal axis is the score (0-100) and the vertical axis is the number of students who got that score, you would get a visual shape. This shape shows you how the scores are "distributed" or spread out across the possible range. **Probability Distributions** are simply mathematical models that describe the overall "shape" of data in the real world, allowing us to predict the likelihood of different outcomes.

## 2. Definition

A **Probability Distribution** is a mathematical function or a table that describes all the possible values and likelihoods that a random variable can take within a given range.

Every probability distribution has a set of **parameters** that dictate its shape (e.g., mean and standard deviation) and an associated equation (probability mass function for discrete variables, or probability density function for continuous variables).

## 3. Formula

There is no single formula for "all distributions," but the central concept revolves around the **Probability Density Function (PDF) $f(x)$** (for continuous distributions) or the **Probability Mass Function (PMF)** (for discrete distributions).

For any valid distribution:

1. All individual probabilities must be $\ge 0$.
2. The sum of all probabilities across the entire sample space must equal exactly 1.
   - For discrete: $\sum P(X=x) = 1$
   - For continuous: $\int_{-\infty}^{\infty} f(x) dx = 1$ (The area under the entire curve is 1)

## 4. Examples & Code

### Theory Example: A Loaded Die

If a six-sided die is loaded so the number "6" comes up half the time, and the other 5 numbers split the remaining probability equally (10% each), the distribution is:

- $X = \{1, 2, 3, 4, 5, 6\}$
- $P(X) = \{0.1, 0.1, 0.1, 0.1, 0.1, 0.5\}$
  This table is entirely enough to define the distribution of our random variable $X$.

### Code Example: Visualizing a Simple Uniform Distribution

```python
import numpy as np
import matplotlib.pyplot as plt

# Simulate rolling a fair 6-sided die 10,000 times
np.random.seed(42)
rolls = np.random.randint(1, 7, 10000)

# Plot a histogram to visualize the 'Empirical' Distribution
plt.hist(rolls, bins=6, range=(0.5, 6.5), density=True, rwidth=0.8, alpha=0.7)
plt.title("Distribution of 10,000 Fair Die Rolls")
plt.xlabel("Die Face Value")
plt.ylabel("Probability / Frequency")
plt.grid(axis='y', alpha=0.75)
plt.show()

# You will see the bars are relatively flat,
# indicating a 'Discrete Uniform Distribution'.
```

## 5. Case Study: Inventory Management

**Scenario**: A warehouse manager of a large retail store needs to decide how many flat-screen TVs to order before Black Friday.

- Too few: They lose out on potential sales (stockouts).
- Too many: Excess money is tied up in inventory that won't sell, costing storage fees.

**Application**: The manager doesn't just guess a single number. They analyze historical sales data to determine the _probability distribution_ of demand for the TV. They realize the demand follows a specific distribution curve with a mean of 500 units and a variance of 50. By understanding the shape of this distribution, they can mathematically optimize their order quantity to minimize the total expected costs (ordering costs + holding costs + stockout costs)—a classic algorithm known as the Newsvendor Model.
