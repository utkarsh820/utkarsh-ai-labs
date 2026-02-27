---
title: "Module 0 — Statistics & Probability for Production AI"
tags:
  - statistics
  - foundations
  - month-01
---

# Module 0 — Statistics & Probability for Production AI

> **Prerequisite for:** P9 (A/B Testing Statistical Framework), all model evaluation modules.

## Why This Module Exists

Every model comparison is a statistical claim. Every A/B test is a hypothesis test. Every confidence interval you report to stakeholders is a probability statement. If you cannot rigorously validate these claims, you are shipping **noise dressed as signal**.

This module builds the statistical toolkit required to:

1. Determine whether Model B is *actually* better than Model A, or if you got lucky.
2. Design experiments (A/B tests) with proper power analysis.
3. Communicate uncertainty to non-technical stakeholders without hand-waving.

## Lessons

| # | Topic | Type |
|---|-------|------|
| 01 | [Statistical Significance & Hypothesis Testing in ML Pipelines](01_hypothesis_testing.md) | Theory + Lab |

## Labs & Challenges

| Resource | Description |
|----------|-------------|
| [Implementation Lab: Statistical Validator](lab_statistical_validator.md) | Build a reusable `StatisticalValidator` class |
| [Proof of Work](proof_of_work.md) | The commit-or-fail challenge |

## Key References

- Wasserman, L. (2004). *All of Statistics*. Springer.
- Downey, A. (2014). *Think Stats*. O'Reilly.
- Google's [Rules of ML](https://developers.google.com/machine-learning/guides/rules-of-ml) — Rule #14: "Starting with an interpretable model makes debugging easier."
