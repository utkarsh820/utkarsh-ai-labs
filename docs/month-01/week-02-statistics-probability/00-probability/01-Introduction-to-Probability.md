# Introduction to Probability

## 1. Intuition

Imagine you are blindfolded and picking a marble from a bag containing 3 red marbles and 7 blue marbles. Intuitively, you know you are more likely to pick a blue marble because there are more of them. Probability is simply a mathematical way to quantify this "likelihood" or chance of an event happening. It gives us a language to deal with uncertainty and make informed guesses about the future.

## 2. Definition

**Probability** is a measure of the likelihood that a specific event will occur, expressed as a number between 0 and 1, inclusive.

- A probability of 0 indicates an impossible event.
- A probability of 1 indicates a certain event.
- An event is a set of outcomes of an experiment to which a probability is assigned.

## 3. Formula

For an event $A$ in a finite sample space where all outcomes are equally likely, the theoretical probability of event $A$, denoted as $P(A)$, is given by:

$$P(A) = \frac{\text{Number of favorable outcomes for } A}{\text{Total number of possible outcomes}}$$

## 4. Examples & Code

### Theory Example: Coin Toss

When tossing a fair coin, the sample space is $\{Heads, Tails\}$.

- Favorable outcomes for "Heads" = 1
- Total possible outcomes = 2
- $P(Heads) = 1/2 = 0.5$

### Code Example: Simulating Coin Tosses in Python

We can use Python to simulate coin tosses and calculate the _empirical_ probability.

```python
import numpy as np

# Set random seed for reproducibility
np.random.seed(42)

# Simulate 10,000 coin tosses (0 for Tails, 1 for Heads)
tosses = np.random.randint(0, 2, 10000)

# Calculate empirical probability of getting Heads (1)
num_heads = np.sum(tosses)
prob_heads = num_heads / 10000

print(f"Empirical Probability of Heads: {prob_heads}")
```

## 5. Case Study: Customer Conversion Rate

**Scenario**: In purely practical terms, businesses use probability to forecast revenues via "Conversion Rates."

If an e-commerce website has 10,000 daily visitors and, on average, 250 of them make a purchase:

- The "experiment" is a visitor landing on the page.
- The "event" ($A$) is the visitor making a purchase.
- The probability of conversion is $P(A) = \frac{250}{10000} = 0.025$ or $2.5\%$.

**Application**: The business uses this baseline probability to allocate server resources, forecast quarterly profits, and evaluate the effectiveness of new marketing campaigns (A/B testing aims to see if changing the website _increases_ this conversion probability).
