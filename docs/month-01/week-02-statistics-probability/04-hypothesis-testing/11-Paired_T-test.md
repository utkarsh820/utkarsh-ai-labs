# Paired T-Test (Dependent T-Test)

## 1. Intuition

Imagine we want to know if an SAT prep course actually works. We _could_ test 50 random students who took the course (Group A) and 50 random students who didn't (Group B) using an Independent T-Test. But what if Group A just happened to have smarter students to begin with?

To eliminate that wild card, we test the _exact same 50 students_ twice: once before the course, and once after. Because we are testing the exact same people, the two sets of data are "dependent" or "paired." By subtracting the "Before" scores from the "After" scores, we create a single column of "Differences." The **Paired T-test** simply checks if the average of those differences is statistically greater than 0.

## 2. Definition

A **Paired T-Test (Dependent Sample T-Test)** is a statistical procedure used to determine whether the mean difference between two sets of observations is zero.

It is exclusively used when the two samples are dependent (e.g., matched pairs, or the same subjects measured at two different points in time). This drastically reduces the background "noise" (natural variance between different people) and makes the signal (the actual effect of the treatment) much easier to mathematically isolate.

## 3. Formula

A Paired T-test is mathematically identical to a **One-Sample T-test** performed strictly on the _differences_ between the pairs.

**Paired T-Statistic:**
$$t = \frac{\bar{d}}{\frac{s_d}{\sqrt{n}}}$$

Where:

- $\bar{d}$ = The Mean of the Differences (After - Before)
- $s_d$ = Standard Deviation of the Differences
- $n$ = Number of pairs (e.g., Number of students)

_(Degrees of Freedom = $n - 1$)_

## 4. Examples & Code

### Theory Example: Blood Pressure Medication

You measure the resting heart rate of 10 patients _before_ giving them medication.
An hour later, you measure the heart rate of those _same_ 10 patients.
You calculate the difference for each patient: $D = HR_{After} - HR_{Before}$.
The average drop ($\bar{d}$) is -8 bpm.

If this drop of -8 is consistently seen across the 10 patients (low $s_d$), the T-score becomes highly negative, yielding a tiny P-value, which definitively proves the medication lowers heart rate.

### Code Example (Python/Scipy)

_Do people type faster on a Mechanical Keyboard vs a Membrane Keyboard?_
_(Note: Each person types on BOTH keyboards)_

```python
import numpy as np
import scipy.stats as stats

# WPM (Words Per Minute) for 15 users.
# User 1 is index 0 in both arrays, User 2 is index 1, etc.
np.random.seed(42)
wpm_membrane = np.random.normal(loc=65, scale=10, size=15)

# Simulate mechanical causing a slight 5 WPM boost on average for the same users
wpm_mechanical = wpm_membrane + np.random.normal(loc=5, scale=2, size=15)

# Paired T-Test (Related T-Test in Scipy)
# H0: Mean difference between the two keyboards is 0.
t_stat, p_value = stats.ttest_rel(wpm_mechanical, wpm_membrane)

print(f"Mean Difference: {np.mean(wpm_mechanical - wpm_membrane):.2f} WPM")
print(f"Paired T-Statistic: {t_stat:.4f}")
print(f"P-Value: {p_value:.6f}")

if p_value < 0.05:
    print("\nReject Null: The mechanical keyboard significantly increases typing speed.")
```

## 5. Case Study: Software Performance Upgrades

**Scenario**: A SaaS company rolls out a major backend refactor designed to speed up their API response times. They want to prove mathematically that the system is faster.

**Application**: Simply comparing average response times "Before Tuesday" vs "After Tuesday" using an Independent T-Test is heavily flawed. What if Wednesday traffic was just naturally lighter?

Instead, the engineering team uses a **Paired T-Test**. They select 10,000 specific API endpoints. They record the benchmark time for Endpoint A on the old code, and the bench time for Endpoint A on the _new_ code. They pair the 10,000 identical endpoints together, calculating the millisecond difference for every single one. Because this eliminates the variance between different _types_ of queries (e.g., logging in vs generating a report), the Paired T-Test guarantees with 99.9% confidence that the specific code commit actually reduced latency by 45ms across the board.
