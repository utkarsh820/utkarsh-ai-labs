# Conditional Probability and Bayes' Theorem

## 1. Intuition

Imagine you are trying to guess if it will rain today. The chance of rain might be 30% overall. However, if you look outside and see dark, heavy clouds gathering (new information), your estimate of the chance of rain suddenly jumps to 80%. **Conditional Probability** is adjusting your probability estimate based on the knowledge that another related event has already occurred. **Bayes' Theorem** is the formal mathematical rule that tells us exactly _how_ to update our beliefs given this new evidence.

## 2. Definition

**Conditional Probability**, $P(A|B)$, is the probability of an event $A$ occurring given that another event $B$ has already occurred.

**Bayes' Theorem** describes the probability of an event based on prior knowledge of conditions that might be related to the event. It is a way to find a probability when we know certain other probabilities.

## 3. Formula

**Conditional Probability:**
$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$
_(Where $P(B) > 0$)_

**Bayes' Theorem:**
$$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}$$

Where:

- $P(A|B)$ is the **Posterior probability**: Probability of $A$ given $B$.
- $P(A)$ is the **Prior probability**: Initial probability of $A$.
- $P(B|A)$ is the **Likelihood**: Probability of observing evidence $B$ given $A$ is true.
- $P(B)$ is the **Marginal likelihood**: Total probability of observing evidence $B$ under all possible conditions.

## 4. Examples & Code

### Theory Example: Medical Testing

Suppose a disease affects 1% of the population ($P(D) = 0.01$). You take a test.

- If you have the disease, the test is positive 99% of the time: $P(+|D) = 0.99$ (True Positive Rate)
- If you do NOT have the disease ($D'$), the test is falsely positive 5% of the time: $P(+|D') = 0.05$ (False Positive Rate)

If you get a positive test, what is the probability you actually have the disease, $P(D|+)$?
Using Bayes' Theorem:
$P(D|+) = \frac{P(+|D) \cdot P(D)}{P(+|D) \cdot P(D) + P(+|D') \cdot P(D')}$
$P(D|+) = \frac{0.99 \cdot 0.01}{(0.99 \cdot 0.01) + (0.05 \cdot 0.99)} \approx 0.166$ (or $16.6\%$)

Counter-intuitively, even with a positive test, the chance you have the rare disease is still quite low!

### Code Example: Bayes' Theorem in Python

```python
def bayes_theorem(p_a, p_b_given_a, p_b_given_not_a):
    """
    Calculates P(A|B) using Bayes' Theorem.
    """
    p_not_a = 1 - p_a
    # Law of Total Probability for the denominator
    p_b = (p_b_given_a * p_a) + (p_b_given_not_a * p_not_a)

    # Bayes formula
    p_a_given_b = (p_b_given_a * p_a) / p_b
    return p_a_given_b

# Medical Test Example
p_disease = 0.01
p_pos_given_disease = 0.99
p_pos_given_no_disease = 0.05

prob = bayes_theorem(p_disease, p_pos_given_disease, p_pos_given_no_disease)
print(f"Probability of having disease given positive test: {prob:.4f}")
```

## 5. Case Study: Email Spam Filtering

**Scenario**: One of the most famous applications of Bayes' Theorem in tech is the **Naive Bayes Classifier** used for detecting spam emails.

- **Prior ($P(\text{Spam})$)**: The general historical probability that any incoming email is spam (e.g., 40%).
- **Evidence ($B$)**: The email contains the words "Free", "Money", and "Click".
- **Likelihood ($P(\text{Words}|\text{Spam})$)**: If we know an email is in the spam folder, what is the probability it contains these specific words? (Usually very high).

**Application**: The email provider's algorithm calculates $P(\text{Spam} | \text{Words})$. If this posterior probability crosses a certain threshold (e.g., 90%), the email is automatically routed to the user's Spam folder instead of the Inbox. The algorithm continuously updates its "Priors" and "Likelihoods" every time a user manually marks an email as "Spam" or "Not Spam," making it smarter over time.
