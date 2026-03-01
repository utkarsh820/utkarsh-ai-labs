# Discrete Probability Distributions

## 1. Intuition

Imagine flipping a coin 10 times and counting the number of "Heads." The answer can only be whole numbers: 0, 1, 2, ... all the way to 10. It cannot be 3.5. **Discrete Distributions** model scenarios where the outcomes are countable, distinct, and separate values (like whole numbers).

Two of the most common discrete distributions in statistics and machine learning are the **Binomial Distribution** and the **Poisson Distribution**.

## 2. Definition

**Binomial Distribution:** Models the number of "successes" in a fixed number of independent 'yes/no' trials, where the probability of success is the same for every trial.

- **Parameters**: $n$ (number of trials), $p$ (probability of success in one trial).

**Poisson Distribution:** Models the number of times an event occurs within a fixed interval of time or space.

- **Parameters**: $\lambda$ (lambda), the average (expected) number of events in that interval.

## 3. Formula

**Binomial PMF:** Probability of getting exactly $k$ successes in $n$ trials:
$$P(X = k) = \binom{n}{k} \cdot p^k \cdot (1-p)^{n-k}$$
_(where $\binom{n}{k} = \frac{n!}{k!(n-k)!}$ is "n choose k")_

**Poisson PMF:** Probability of observing exactly $k$ events in an interval:
$$P(X = k) = \frac{\lambda^k \cdot e^{-\lambda}}{k!}$$
_(where $e \approx 2.71828$ is Euler's number)_

## 4. Examples & Code

### Theory Example: Biased Coin (Binomial)

You have a coin that lands on heads 60% of the time ($p=0.6$). You flip it 3 times ($n=3$). What is the probability of getting exactly 2 heads ($k=2$)?
$P(X=2) = \binom{3}{2} \cdot 0.6^2 \cdot 0.4^1 = 3 \cdot 0.36 \cdot 0.4 = 0.432$ ($43.2\%$)

### Code Example: Scipy Stats

Python's `scipy.stats` module handles complex distribution math instantly.

```python
from scipy.stats import binom, poisson

# 1. Binomial: 10 flips of a fair coin (n=10, p=0.5).
# Probability of exactly 5 heads (k=5)?
prob_5_heads = binom.pmf(k=5, n=10, p=0.5)
print(f"Binomial P(X=5): {prob_5_heads:.4f}")

# 2. Poisson: A call center gets exactly 4 calls per hour on average (lambda = 4).
# Probability of getting exactly 6 calls in the next hour (k=6)?
prob_6_calls = poisson.pmf(k=6, mu=4) # 'mu' stands for lambda in scipy
print(f"Poisson P(X=6): {prob_6_calls:.4f}")
```

## 5. Case Study: Server Infrastructure Planning (Poisson)

**Scenario**: A tech startup runs a web application that occasionally crashes due to sudden spikes in database queries. On average, the database crashes 2 times per year ($\lambda = 2$). The infrastructure team is creating their service level agreement (SLA) contracts which promise 99.9% uptime.

They need to know the probability of the database crashing _4 or more times_ in a single year to understand the risk of violating their SLA.

**Application**: Because the crashes are independent, rare events happening over a fixed interval (1 year), the team models the crashes using a **Poisson Distribution**.
They calculate $P(X \ge 4) = 1 - P(X < 4) = 1 - (P(X=0) + P(X=1) + P(X=2) + P(X=3))$.
Using `scipy.stats.poisson.sf(3, mu=2)`, they find the probability is roughly $14.2\%$. Realizing this $14.2\%$ risk is unacceptably high, the team decides to invest heavily in adding redundancy and a load balancer to their architecture before signing any SLA contracts.
