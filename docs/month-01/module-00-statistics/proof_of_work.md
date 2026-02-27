---
title: "Proof of Work — Statistical Validator Challenge"
tags:
  - proof-of-work
  - challenge
  - statistics
  - month-01
---

# Proof of Work — Module 0: Statistics & Probability

<span class="pow-badge">COMMIT OR FAIL</span>

---

## Philosophy

!!! quote "The Utkarsh AI Labs Rule"

    **Reading is not learning. Committing code is.**
    
    If you can't build it, you don't understand it. This "Proof of Work" is your *AI Clinic Equivalent* — the artifact that proves comprehension under real constraints.

---

## The Challenge: `statistical_validator` CLI Tool

### Mission

Build a **command-line utility** called `statistical_validator` that:

1. Accepts two CSV files (or a single CSV with a group column) containing evaluation scores.
2. Runs the full statistical comparison pipeline (Welch's t-test, Cohen's d, 95% CI).
3. Outputs a structured report to `stdout` **and** saves a JSON artifact.
4. Exits with code `0` if $H_0$ is rejected (model improvement confirmed) or `1` if not.

This tool will become a building block for **P9: A/B Testing Statistical Framework**.

---

### Specification

```
statistical_validator compare \
    --scores-a results_model_a.csv \
    --scores-b results_model_b.csv \
    --alpha 0.05 \
    --output report.json
```

### Required Output (JSON)

```json
{
  "model_a": {
    "mean": 0.908,
    "std": 0.012,
    "n": 10
  },
  "model_b": {
    "mean": 0.913,
    "std": 0.014,
    "n": 10
  },
  "test": {
    "name": "welch_t_test",
    "t_statistic": -0.8721,
    "p_value": 0.2314,
    "alpha": 0.05,
    "significant": false
  },
  "effect_size": {
    "cohens_d": -0.3826,
    "magnitude": "small"
  },
  "confidence_interval": {
    "level": 0.95,
    "lower": -0.0142,
    "upper": 0.0042
  },
  "recommendation": "Keep current model (A)"
}
```

---

### Grading Rubric

| Criterion | Points | Requirement |
|-----------|--------|-------------|
| **Core Logic** | 30 | Welch's t-test, Cohen's d, and CI are correctly computed |
| **CLI Interface** | 20 | Uses `argparse` or `click`; handles missing files gracefully |
| **JSON Output** | 15 | Matches the schema above; parseable by downstream tools |
| **Exit Codes** | 10 | `0` = significant improvement, `1` = no improvement |
| **Tests** | 15 | At least 3 unit tests using `pytest` (edge cases included) |
| **Documentation** | 10 | README with usage examples and a "Why this matters" section |
| **Total** | **100** | |

!!! warning "Minimum passing score: 70/100"

    You must implement Core Logic + CLI + JSON Output at minimum.

---

### Required Unit Tests

Write at least these three test cases:

```python title="test_statistical_validator.py"
import numpy as np
import pytest
from statistical_validator import StatisticalValidator


def test_identical_distributions_not_significant():
    """Two identical score sets should NOT be significant."""
    scores = np.array([0.90, 0.91, 0.89, 0.90, 0.92, 0.91, 0.90, 0.89, 0.91, 0.90])
    validator = StatisticalValidator(alpha=0.05)
    result = validator.compare(scores, scores)
    assert result.is_significant is False
    assert result.p_value == 1.0  # identical → p = 1


def test_clearly_different_distributions_significant():
    """Widely separated distributions should be significant."""
    a = np.array([0.50, 0.51, 0.49, 0.52, 0.50, 0.48, 0.51, 0.49, 0.50, 0.52])
    b = np.array([0.95, 0.94, 0.96, 0.93, 0.95, 0.94, 0.96, 0.95, 0.94, 0.93])
    validator = StatisticalValidator(alpha=0.05)
    result = validator.compare(a, b)
    assert result.is_significant is True
    assert abs(result.cohens_d) > 0.8  # large effect


def test_invalid_alpha_raises():
    """Alpha outside (0, 1) should raise ValueError."""
    with pytest.raises(ValueError):
        StatisticalValidator(alpha=0.0)
    with pytest.raises(ValueError):
        StatisticalValidator(alpha=1.5)
```

---

### Stretch Goals (Bonus)

- [ ] **Power Analysis:** Add a `power` subcommand that computes required sample size given desired $\alpha$, power, and minimum detectable effect.
- [ ] **Paired Test:** Support `--paired` flag for paired t-tests (same dataset, different models).
- [ ] **Visualization:** Generate a box plot comparing the two distributions (save as PNG).
- [ ] **CI/CD Integration:** Write a GitHub Actions workflow that runs the validator on every PR.

---

### Submission Checklist

```
your-repo/
├── statistical_validator.py      # Core class
├── cli.py                        # CLI entry point
├── test_statistical_validator.py  # pytest tests
├── requirements.txt              # scipy, numpy, scikit-learn
├── sample_data/
│   ├── scores_model_a.csv
│   └── scores_model_b.csv
└── README.md                     # Usage + "Why this matters"
```

!!! success "Definition of Done"

    This module is **complete** when:

    1. All three unit tests pass (`pytest -v`).
    2. The CLI produces valid JSON output.
    3. The code is committed to your GitHub repo with the message:
    
    ```
    feat(m0): add statistical validator — proof of work for Module 0
    ```

    4. The commit SHA is logged in your [Dashboard](../../dashboard.md).

---

## Why This Matters for Your Career

This isn't a toy exercise. The `StatisticalValidator` pattern is used at:

- **Netflix** — for comparing recommendation model variants.
- **Google** — for evaluating search ranking changes.
- **Any ML team** — as a gate in the model promotion pipeline.

When you sit in an interview and they ask *"How do you decide whether to deploy a new model?"*, you won't recite a textbook definition. You'll say: *"I built a tool for that. Here's the commit."*

That's **Unstoppable.**
