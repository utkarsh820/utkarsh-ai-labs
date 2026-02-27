---
title: "P9 — A/B Testing Statistical Framework"
tags:
  - project
  - a-b-testing
  - statistics
---

# P9 — A/B Testing Statistical Framework

<span class="pow-badge">Portfolio Project</span>

---

## Overview

A production-grade A/B testing framework that provides:

- **Statistical validation** of experiment results (Welch's t-test, Bayesian methods).
- **Power analysis** for experiment design (required sample size calculations).
- **REST API** endpoint for CI/CD integration.
- **Dashboard** for real-time experiment monitoring.

## Prerequisite: Module 0 — Statistics & Probability

!!! warning "This project CANNOT begin until M0 is complete"

    The `StatisticalValidator` class from [Module 0](../month-01/module-00-statistics/index.md) is the **core engine** of this project. Complete the [Proof of Work](../month-01/module-00-statistics/proof_of_work.md) first.

## Roadmap

| Phase | Deliverable | Timeline |
|-------|-------------|----------|
| **Foundation** | `StatisticalValidator` class (M0) | Month 1, Week 1 |
| **Extension** | Bayesian A/B testing + sequential testing | Month 2–3 |
| **API** | FastAPI endpoint wrapping the validator | Month 4, Week 1 |
| **Dashboard** | Streamlit dashboard for experiment monitoring | Month 4, Week 2 |
| **CI/CD Gate** | GitHub Actions integration — block deploy on insignificant results | Month 4, Week 3 |
| **Documentation** | Full README, architecture diagram, usage guide | Month 4, Week 4 |

## Tech Stack

- **Core:** Python, scipy, numpy, scikit-learn
- **API:** FastAPI, Pydantic
- **Dashboard:** Streamlit or Grafana
- **CI/CD:** GitHub Actions
- **Testing:** pytest, hypothesis (property-based testing)

## Status

- [x] Foundation: `StatisticalValidator` class designed
- [ ] Foundation: Proof of Work committed
- [ ] Extension: Bayesian methods
- [ ] API layer
- [ ] Dashboard
- [ ] CI/CD integration
