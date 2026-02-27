---
title: "Implementation Lab — Statistical Validator"
tags:
  - lab
  - statistics
  - month-01
---

# Implementation Lab: Statistical Validator

<span class="pow-badge">Lab · Module 0</span>

---

## Objective

Package the hypothesis testing workflow from the lesson into a **reusable, production-grade Python class** called `StatisticalValidator`. This is the utility you will use in every future model comparison — and the foundation for **P9: A/B Testing Statistical Framework**.

---

## The `StatisticalValidator` Class

```python title="statistical_validator.py" linenums="1"
"""
statistical_validator.py
========================
Reusable statistical comparison utility for ML model evaluation.

Usage:
    validator = StatisticalValidator(alpha=0.05)
    result = validator.compare(scores_a, scores_b)
    print(result)

Part of: Utkarsh AI Labs — Month 1, Module 0
"""

from dataclasses import dataclass
from typing import Optional

import numpy as np
from scipy import stats


@dataclass
class ComparisonResult:
    """Structured result of a two-sample statistical comparison."""

    model_a_mean: float
    model_b_mean: float
    model_a_std: float
    model_b_std: float
    t_statistic: float
    p_value: float
    cohens_d: float
    ci_lower: float
    ci_upper: float
    alpha: float
    is_significant: bool
    effect_magnitude: str  # "negligible", "small", "medium", "large"
    recommendation: str

    def __str__(self) -> str:
        return (
            "\n╔══════════════════════════════════════════════╗\n"
            "║       STATISTICAL COMPARISON REPORT          ║\n"
            "╠══════════════════════════════════════════════╣\n"
            f"║ Model A — Mean: {self.model_a_mean:.4f} ± {self.model_a_std:.4f}       ║\n"
            f"║ Model B — Mean: {self.model_b_mean:.4f} ± {self.model_b_std:.4f}       ║\n"
            "╠══════════════════════════════════════════════╣\n"
            f"║ T-statistic:   {self.t_statistic:>8.4f}                  ║\n"
            f"║ P-value:       {self.p_value:>8.4f}                  ║\n"
            f"║ Cohen's d:     {self.cohens_d:>8.4f} ({self.effect_magnitude})     ║\n"
            f"║ 95% CI:        [{self.ci_lower:.4f}, {self.ci_upper:.4f}]      ║\n"
            "╠══════════════════════════════════════════════╣\n"
            f"║ Significant (α={self.alpha}): {'YES ✓' if self.is_significant else 'NO ✗':>6}              ║\n"
            f"║ Recommendation: {self.recommendation:<28} ║\n"
            "╚══════════════════════════════════════════════╝"
        )


class StatisticalValidator:
    """
    Compare two sets of model evaluation scores using
    Welch's t-test, Cohen's d, and confidence intervals.

    Parameters
    ----------
    alpha : float
        Significance level (default: 0.05).
    """

    def __init__(self, alpha: float = 0.05) -> None:
        if not 0 < alpha < 1:
            raise ValueError(f"alpha must be in (0, 1), got {alpha}")
        self.alpha = alpha

    # ------------------------------------------------------------------ #
    #  Public API                                                         #
    # ------------------------------------------------------------------ #

    def compare(
        self,
        scores_a: np.ndarray,
        scores_b: np.ndarray,
        model_a_name: Optional[str] = None,
        model_b_name: Optional[str] = None,
    ) -> ComparisonResult:
        """
        Run a full statistical comparison between two score arrays.

        Parameters
        ----------
        scores_a : array-like
            Evaluation scores for Model A (e.g., k-fold accuracies).
        scores_b : array-like
            Evaluation scores for Model B.

        Returns
        -------
        ComparisonResult
        """
        a = np.asarray(scores_a, dtype=float)
        b = np.asarray(scores_b, dtype=float)

        if len(a) < 2 or len(b) < 2:
            raise ValueError("Each sample must have at least 2 observations.")

        # Welch's t-test
        t_stat, p_val = stats.ttest_ind(a, b, equal_var=False)

        # Effect size
        d = self._cohens_d(a, b)
        magnitude = self._effect_magnitude(d)

        # Confidence interval for difference in means
        ci_lo, ci_hi = self._confidence_interval(a, b)

        # Decision
        is_sig = p_val < self.alpha
        recommendation = self._recommend(is_sig, d, a.mean(), b.mean())

        return ComparisonResult(
            model_a_mean=a.mean(),
            model_b_mean=b.mean(),
            model_a_std=a.std(ddof=1),
            model_b_std=b.std(ddof=1),
            t_statistic=t_stat,
            p_value=p_val,
            cohens_d=d,
            ci_lower=ci_lo,
            ci_upper=ci_hi,
            alpha=self.alpha,
            is_significant=is_sig,
            effect_magnitude=magnitude,
            recommendation=recommendation,
        )

    # ------------------------------------------------------------------ #
    #  Internal methods                                                   #
    # ------------------------------------------------------------------ #

    @staticmethod
    def _cohens_d(a: np.ndarray, b: np.ndarray) -> float:
        n1, n2 = len(a), len(b)
        pooled_std = np.sqrt(
            ((n1 - 1) * a.std(ddof=1) ** 2 + (n2 - 1) * b.std(ddof=1) ** 2)
            / (n1 + n2 - 2)
        )
        if pooled_std == 0:
            return 0.0
        return float((a.mean() - b.mean()) / pooled_std)

    @staticmethod
    def _effect_magnitude(d: float) -> str:
        d_abs = abs(d)
        if d_abs < 0.2:
            return "negligible"
        elif d_abs < 0.5:
            return "small"
        elif d_abs < 0.8:
            return "medium"
        return "large"

    def _confidence_interval(
        self, a: np.ndarray, b: np.ndarray
    ) -> tuple[float, float]:
        diff = a.mean() - b.mean()
        se = np.sqrt(a.var(ddof=1) / len(a) + b.var(ddof=1) / len(b))
        df = len(a) + len(b) - 2
        t_crit = stats.t.ppf(1 - self.alpha / 2, df)
        return float(diff - t_crit * se), float(diff + t_crit * se)

    @staticmethod
    def _recommend(is_sig: bool, d: float, mean_a: float, mean_b: float) -> str:
        if not is_sig:
            return "Keep current model (A)"
        if abs(d) < 0.2:
            return "Significant but negligible Δ"
        better = "B" if mean_b > mean_a else "A"
        return f"Deploy Model {better}"


# ================================================================== #
#  Quick demo (runs when executed directly)                           #
# ================================================================== #
if __name__ == "__main__":
    from sklearn.datasets import load_breast_cancer
    from sklearn.ensemble import RandomForestClassifier
    from sklearn.linear_model import LogisticRegression
    from sklearn.model_selection import cross_val_score

    X, y = load_breast_cancer(return_X_y=True)

    scores_lr = cross_val_score(
        LogisticRegression(max_iter=10_000, random_state=42),
        X, y, cv=10, scoring="accuracy",
    )
    scores_rf = cross_val_score(
        RandomForestClassifier(n_estimators=100, random_state=42),
        X, y, cv=10, scoring="accuracy",
    )

    validator = StatisticalValidator(alpha=0.05)
    result = validator.compare(scores_lr, scores_rf)
    print(result)
```

---

## How to Use It

=== "Basic"

    ```python
    from statistical_validator import StatisticalValidator
    import numpy as np

    scores_a = np.array([0.91, 0.89, 0.90, 0.92, 0.88, 0.91, 0.90, 0.89, 0.91, 0.90])
    scores_b = np.array([0.93, 0.92, 0.91, 0.94, 0.90, 0.93, 0.92, 0.91, 0.93, 0.92])

    validator = StatisticalValidator(alpha=0.05)
    result = validator.compare(scores_a, scores_b)
    print(result)
    ```

=== "Stricter α (Medical/Finance)"

    ```python
    validator = StatisticalValidator(alpha=0.01)
    result = validator.compare(scores_a, scores_b)
    print(f"Significant at α=0.01? {result.is_significant}")
    ```

=== "With Custom Metric"

    ```python
    from sklearn.model_selection import cross_val_score

    # Use F1 instead of accuracy
    scores_a = cross_val_score(model_a, X, y, cv=10, scoring="f1")
    scores_b = cross_val_score(model_b, X, y, cv=10, scoring="f1")

    result = validator.compare(scores_a, scores_b)
    ```

---

## Acceptance Criteria

- [x] Class is importable and passes `mypy --strict`
- [x] `ComparisonResult` is a dataclass with a human-readable `__str__`
- [x] Welch's t-test used (not Student's — never assume equal variance)
- [x] Cohen's d computed and classified
- [x] 95% CI for the mean difference reported
- [x] Recommendation logic is deterministic and testable
