# Continuous Probability Distributions

## 1. Intuition

Imagine measuring the exact height of every adult in your city down to the nanometer. No two people will have the _exact_ same height. The possible values aren't separate numbers like 1, 2, or 3 (like rolling dice), but instead form a smooth, continuous spectrum. **Continuous Distributions** model variables that can take on an infinite number of possible values within a given range (e.g., time, weight, height, temperature).

Two of the most essential continuous distributions are the **Normal (Gaussian) Distribution** and the **Uniform Distribution**.

## 2. Definition

**Normal Distribution (Gaussian Curve):** The famous "bell curve." It describes data that clusters around a central mean, with the occurrences tapering off symmetrically towards the extremes. It is foundational to statistics because of the Central Limit Theorem.

- **Parameters**: $\mu$ (mean, defining the center), $\sigma$ (standard deviation, defining the width/spread).

**Uniform Distribution (Continuous):** Describes an experiment where all outcomes between a minimum value ($a$) and a maximum value ($b$) are _equally likely_. The shape is a flat rectangle.

- **Parameters**: $a$ (minimum), $b$ (maximum).

## 3. Formula

Because continuous outcomes are infinite, the probability of any single exact value (like exactly 174.123 cm) is effectively 0. Instead, we use a **Probability Density Function $f(x)$ (PDF)** to find the probability of a value falling within a _range_ (by calculating the area under the curve).

**Normal PDF:**
$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$

_(Note: In practice, we never calculate this by hand; we use software or Z-tables)._

**Uniform PDF:**
$$f(x) = \begin{cases} \frac{1}{b - a} & \text{for } a \le x \le b \\ 0 & \text{otherwise} \end{cases}$$

## 4. Examples & Code

### Theory Example: Waiting for a Train (Uniform)

A train arrives exactly every 15 minutes. If you show up at the station at a random time, your wait time $T$ uniformly distributed between 0 and 15 minutes ($a=0, b=15$).

- The height of the rectangle is $1 / (15 - 0) = 1/15$.
- The probability you wait between 5 and 10 minutes: Area $= \text{width} \times \text{height} = (10 - 5) \times (1/15) = 5/15 = 33.3\%$.

### Code Example: Normal Distribution & Machine Learning (Scipy)

```python
import numpy as np
import scipy.stats as stats
import matplotlib.pyplot as plt

# Normal Distribution Example: IQ scores
# Mean (mu) = 100, Standard Deviation (sigma) = 15
mu, sigma = 100, 15

# What is the probability of having an IQ between 90 and 110?
# We use the Cumulative Distribution Function (CDF) for continuous ranges
# P(a < X < b) = CDF(b) - CDF(a)
prob_90_110 = stats.norm.cdf(110, loc=mu, scale=sigma) - stats.norm.cdf(90, loc=mu, scale=sigma)
print(f"Probability of IQ between 90 and 110: {prob_90_110:.4f}")

# Generate and Visualize the Bell Curve
x = np.linspace(mu - 4*sigma, mu + 4*sigma, 100)
plt.plot(x, stats.norm.pdf(x, mu, sigma), linewidth=2, color='blue')
plt.title('Normal Distribution of IQ Scores')
plt.xlabel('IQ Score')
plt.ylabel('Probability Density')
plt.grid(True, alpha=0.3)
plt.show()
```

## 5. Case Study: Quality Control in Manufacturing (Normal)

**Scenario**: A tech company manufactures computer processors. The "clock speed" of the chips is supposed to be 3.5 GHz. Due to microscopic variations in the silicon manufacturing process, the actual speed varies. Extensive data shows the speeds are _Normally Distributed_ with a mean ($\mu$) of 3.5 GHz and a standard deviation ($\sigma$) of 0.1 GHz.

**Application**: The company decides to bin its chips and sell them at different price points based on their actual speed.

- Using continuous distribution mathematics (specifically the Empirical Rule or 68-95-99.7 rule), they know automatically that approximately 68% of chips will land between 3.4 GHz and 3.6 GHz.
- If a chip measures above 3.7 GHz (which is $\mu + 2\sigma$), they know this is quite rare (only ~2.5% of chips). Instead of selling it for the standard price, they slap a "Gaming Processor" label on it and charge a $200 premium. This entire pricing architecture is built upon modeling the manufacturing variance as a continuous normal curve.
