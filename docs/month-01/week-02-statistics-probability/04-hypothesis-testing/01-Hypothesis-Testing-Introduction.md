# HYPOTHESIS TESTING - Introduction

##  Module: Inferential Logic

### Topic: Introduction to Hypothesis Testing

> **Professional Context:** In Machine Learning, we don't just "hope" a new model is better. We use Hypothesis Testing (A/B testing) to determine if the increase in accuracy is **statistically significant** or just a random fluke in the test data.

---

### 1. The Conceptual Framework

Hypothesis testing is a formal procedure for investigating our ideas about the world using statistics. It always involves two competing statements:

* **The Null Hypothesis ($H_0$):** The "Status Quo" or "No Effect" statement. It assumes nothing has changed.
* **The Alternative Hypothesis ($H_a$ or $H_1$):** The claim we are trying to prove. It assumes there is a significant effect or change.

---

### 2. Case Study: The "Extinct" Tree Lobster (1920–2001)

In 1920, after a shipwreck introduced black rats to Lord Howe Island, the Tree Lobster disappeared.

#### **The Initial Phase (1920–2000):**

* **$H_0$:** The Tree Lobster is extinct (Population = 0).
* **$H_a$:** The Tree Lobster still exists (Population > 0).
* **The Evidence:** For 80 years, zero sightings were recorded. We **failed to reject** the Null.

#### **The Turning Point (2001):**

Scientists climbed Ball’s Pyramid, a jagged rock 20km away. They found 24 insects living under a single bush.

* **The Data:** $n = 24$.
* **The Decision:** Since $24 > 0$, the probability of seeing 24 insects if the species were truly extinct is **zero**.
* **Conclusion:** We **Reject the Null Hypothesis**. The species is extant.

---

### 3. The 4-Step Professional Workflow

When you document an experiment on your website, follow this standardized structure:

1. **State the Hypotheses:** Define $H_0$ (No change) and $H_a$ (The improvement).
2. **Choose Significance Level ($\alpha$):** Usually $0.05$. This is your "Threshold for Surprise."
3. **Collect Data & Calculate Test Statistic:** Use a $t\text{-test}$ or $Z\text{-test}$ to find the **$p\text{-value}$**.
4. **Make a Decision:** * If $p < \alpha$: **Reject $H_0$** (The result is significant).
* If $p \geq \alpha$: **Fail to Reject $H_0$** (Not enough evidence).



---

### 4. Implementation (Python/Statsmodels)

In AI, we often test if a new model's mean error is significantly lower than the baseline.

```python
from scipy import stats

# Accuracy scores of Baseline Model vs. New Model
baseline = [0.82, 0.81, 0.83, 0.82, 0.84]
new_model = [0.85, 0.87, 0.86, 0.88, 0.85]

# Perform a T-Test
t_stat, p_value = stats.ttest_ind(baseline, new_model)

print(f"P-Value: {p_value:.4f}")

if p_value < 0.05:
    print("Reject Null: The New Model is significantly better.")
else:
    print("Fail to Reject Null: Improvements may be due to noise.")

```

---

### 🎯 The "Interview Pass" Definition

> "Hypothesis testing is a statistical framework used to decide whether the data at hand sufficiently supports a particular breakthrough claim. We start by assuming a **Null Hypothesis**—that there is no effect—and we only reject it if our sample evidence is so extreme that it's highly unlikely to have occurred by chance (typically a probability less than 5%)."

---

### 🧪 Assessment: Mastery Check

1. **Conceptual:** Why do we say "Fail to Reject the Null" instead of "Accept the Null"? (Answer: Because science doesn't prove things true; it only finds enough evidence to prove the current assumption is likely false).
2. **Case Study:** In the Tree Lobster case, what would a **Type I Error** (False Positive) look like? (Answer: Claiming the insect exists when it's actually a different, similar-looking species).
3. **Decision:** If your $p\text{-value}$ is $0.03$ and your $\alpha$ is $0.05$, do you reject the Null? (Answer: Yes).

---
