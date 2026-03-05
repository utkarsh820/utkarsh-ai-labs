# Evaluation Metrics
## From a Professor & Industry Practitioner Perspective

---

# 📚 LEVEL 1: INTUITION

## Why Do We Need Metrics?

**Think of it like a Report Card:**
Imagine you're a teacher grading students. You could say "Student A did well" but that's vague. Instead, you give:
- **Score:** 85/100
- **Rank:** Top 10%
- **Improvement:** +15% from last test

**Metrics do the same for ML models:**
- They tell you **how good** your model is (not just "it works")
- They help you **compare** different models objectively
- They tell you **where** your model fails (not just that it fails)

## The Golden Rule of Metrics

> **"Choose the metric that matches your BUSINESS GOAL, not just the mathematical convenience."**

**Example:**
- **Spam Detection:** You care more about NOT marking important emails as spam → **Precision**
- **Cancer Detection:** You care more about NOT missing any cancer cases → **Recall**
- **House Price Prediction:** You care about average error in dollars → **MAE/RMSE**

## Regression vs Classification Metrics - Quick View

```
┌─────────────────────────────────────────────────────────────────┐
│                    EVALUATION METRICS MAP                        │
├─────────────────────────────────────────────────────────────────┤
│  REGRESSION (Predicting Numbers)                                │
│  ├── MAE → Average error magnitude                              │
│  ├── MSE → Penalizes large errors                               │
│  ├── RMSE → Error in original units                             │
│  ├── R² → How much better than baseline                         │
│  └── MAPE → Percentage error                                    │
├─────────────────────────────────────────────────────────────────┤
│  CLASSIFICATION (Predicting Categories)                         │
│  ├── Accuracy → Overall correctness                             │
│  ├── Precision → Quality of positive predictions                │
│  ├── Recall → Coverage of actual positives                      │
│  ├── F1-Score → Balance of Precision & Recall                   │
│  ├── ROC-AUC → Ranking ability across thresholds                │
│  └── Confusion Matrix → Detailed error breakdown                │
└─────────────────────────────────────────────────────────────────┘
```

---

# 📚 LEVEL 2: DEFINITION (Interview/Academic Ready)

## Regression Metrics - Formal Definitions

| **Metric** | **Definition** | **When to Use** |
|:---|:---|:---|
| **MAE** | Mean Absolute Error - Average magnitude of errors without direction | When outliers exist, interpretable error needed |
| **MSE** | Mean Squared Error - Average of squared differences | When large errors are particularly undesirable |
| **RMSE** | Root Mean Squared Error - Square root of MSE | When error needs to be in original units |
| **R²** | Coefficient of Determination - Proportion of variance explained | When comparing model to baseline (mean) |
| **Adjusted R²** | R² adjusted for number of predictors | When comparing models with different features |
| **MAPE** | Mean Absolute Percentage Error - Average percentage error | When relative error matters more than absolute |

## Classification Metrics - Formal Definitions

| **Metric** | **Definition** | **When to Use** |
|:---|:---|:---|
| **Accuracy** | Ratio of correct predictions to total predictions | Balanced classes, all errors equally costly |
| **Precision** | Ratio of true positives to all positive predictions | False positives are costly (spam detection) |
| **Recall** | Ratio of true positives to all actual positives | False negatives are costly (cancer detection) |
| **F1-Score** | Harmonic mean of Precision and Recall | Need balance, imbalanced classes |
| **ROC-AUC** | Area under Receiver Operating Characteristic curve | Comparing models across all thresholds |
| **PR-AUC** | Area under Precision-Recall curve | Highly imbalanced datasets |

## The Confusion Matrix Foundation

```
┌─────────────────────────────────────────────────────────────┐
│                    CONFUSION MATRIX                          │
├─────────────────────────────────────────────────────────────┤
│                      │  Predicted: NO  │  Predicted: YES   │
├──────────────────────┼─────────────────┼───────────────────┤
│  Actual: NO          │  TN (True Neg)  │  FP (False Pos)   │
├──────────────────────┼─────────────────┼───────────────────┤
│  Actual: YES         │  FN (False Neg) │  TP (True Pos)    │
└──────────────────────┴─────────────────┴───────────────────┘

TP = Correctly predicted positive
TN = Correctly predicted negative
FP = Type I Error (False Alarm)
FN = Type II Error (Missed Detection)
```

---

# 📚 LEVEL 3: FORMULAS & WORKING

## 3.1 Regression Metrics - Formulas

### Mean Absolute Error (MAE)
```math
MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|
```
- **Range:** [0, ∞)
- **Lower is better**
- **Interpretation:** Average error in original units

### Mean Squared Error (MSE)
```math
MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
```
- **Range:** [0, ∞)
- **Lower is better**
- **Interpretation:** Penalizes large errors quadratically

### Root Mean Squared Error (RMSE)
```math
RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
```
- **Range:** [0, ∞)
- **Lower is better**
- **Interpretation:** Error in original units, sensitive to outliers

### R-Squared (Coefficient of Determination)
```math
R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2} = 1 - \frac{SS_{res}}{SS_{tot}}
```
- **Range:** (-∞, 1]
- **Higher is better**
- **Interpretation:** % of variance explained by model
- **Baseline:** R² = 0 means model is as good as predicting mean

### Adjusted R-Squared
```math
R^2_{adj} = 1 - (1 - R^2) \frac{n - 1}{n - p - 1}
```
- **Range:** (-∞, 1]
- **Higher is better**
- **Interpretation:** Penalizes adding useless features
- **Where:** n = samples, p = predictors

### Mean Absolute Percentage Error (MAPE)
```math
MAPE = \frac{100\%}{n} \sum_{i=1}^{n} \left| \frac{y_i - \hat{y}_i}{y_i} \right|
```
- **Range:** [0%, ∞)
- **Lower is better**
- **Interpretation:** Average percentage error
- **Warning:** Undefined when y_i = 0

## 3.2 Classification Metrics - Formulas

### Accuracy
```math
Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
```
- **Range:** [0, 1]
- **Higher is better**
- **Problem:** Misleading with imbalanced classes

### Precision
```math
Precision = \frac{TP}{TP + FP}
```
- **Range:** [0, 1]
- **Higher is better**
- **Question answered:** "Of all predicted positives, how many are actually positive?"

### Recall (Sensitivity, True Positive Rate)
```math
Recall = \frac{TP}{TP + FN}
```
- **Range:** [0, 1]
- **Higher is better**
- **Question answered:** "Of all actual positives, how many did we find?"

### F1-Score
```math
F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall} = \frac{2TP}{2TP + FP + FN}
```
- **Range:** [0, 1]
- **Higher is better**
- **Interpretation:** Harmonic mean (punishes extreme values)

### Fβ-Score (Generalized F1)
```math
F_\beta = (1 + \beta^2) \times \frac{Precision \times Recall}{(\beta^2 \times Precision) + Recall}
```
- **β > 1:** Recall more important (e.g., β=2)
- **β < 1:** Precision more important (e.g., β=0.5)

### Specificity (True Negative Rate)
```math
Specificity = \frac{TN}{TN + FP}
```
- **Range:** [0, 1]
- **Higher is better**
- **Use:** When false positives are critical

### ROC Curve & AUC
```math
TPR (Recall) = \frac{TP}{TP + FN}
FPR = \frac{FP}{FP + TN}
```
- **ROC Curve:** Plot TPR vs FPR at various thresholds
- **AUC:** Area under ROC curve
- **Range:** [0, 1]
- **Interpretation:** Probability that model ranks random positive higher than random negative
- **Baseline:** AUC = 0.5 (random guessing)

### Precision-Recall Curve & AUC
```math
Plot Precision vs Recall at various thresholds
```
- **Better than ROC for imbalanced data**
- **Baseline:** AUC = proportion of positives in dataset

## 3.3 Metric Selection Decision Tree

```
                    ┌─────────────────────────┐
                    │   What are you predicting? │
                    └───────────┬─────────────┘
                                │
            ┌───────────────────┼───────────────────┐
            │                   │                   │
            ▼                   ▼                   ▼
      ┌──────────┐        ┌──────────┐        ┌──────────┐
      │ Numbers  │        │ Binary   │        │ Multi-   │
      │ (Regression)│    │ (2 Classes)│      │ class    │
      └────┬─────┘        └────┬─────┘        └────┬─────┘
           │                   │                   │
           ▼                   ▼                   ▼
    ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
    │ Outliers?   │     │ Class Balance?│   │ Macro/Micro │
    └──────┬──────┘     └──────┬──────┘     └──────┬──────┘
           │                   │                   │
    ┌──────┴──────┐     ┌──────┴──────┐     ┌──────┴──────┐
    │             │     │             │     │             │
    ▼             ▼     ▼             ▼     ▼             ▼
  Yes           No   Balanced     Imbalanced  All classes  Focus on
    │             │     │             │     │  equally    specific
    ▼             ▼     ▼             ▼     │  class
  MAE/         RMSE/  Accuracy    Precision/  │
  Huber        R²               Recall/F1     ▼
                                    │     Macro/Micro/
                                    ▼     Weighted Avg
                              ROC-AUC/
                              PR-AUC
```

---

# 📚 LEVEL 4: EXAMPLES WITH CODE & THEORY

## 4.1 Regression Metrics - Complete Implementation

```python
import numpy as np
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
from sklearn.linear_model import LinearRegression, Ridge
from sklearn.model_selection import cross_val_score
import matplotlib.pyplot as plt

# Sample data
y_true = np.array([100, 200, 300, 400, 500, 600, 700, 800, 900, 10000])  # 10000 is outlier
y_pred = np.array([110, 190, 310, 390, 510, 590, 710, 790, 910, 5000])

# Calculate all regression metrics
mae = mean_absolute_error(y_true, y_pred)
mse = mean_squared_error(y_true, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_true, y_pred)

# MAPE (custom - sklearn doesn't have it)
def mape(y_true, y_pred):
    mask = y_true != 0
    return np.mean(np.abs((y_true[mask] - y_pred[mask]) / y_true[mask])) * 100

mape_score = mape(y_true, y_pred)

print("=" * 50)
print("REGRESSION METRICS COMPARISON")
print("=" * 50)
print(f"MAE:    {mae:>10.2f}  (Average error in original units)")
print(f"MSE:    {mse:>10.2f}  (Penalizes large errors)")
print(f"RMSE:   {rmse:>10.2f}  (Error in original units)")
print(f"R²:     {r2:>10.4f}  (Variance explained)")
print(f"MAPE:   {mape_score:>10.2f}% (Percentage error)")
print("=" * 50)

# Compare with/without outlier
y_true_no_outlier = y_true[:-1]
y_pred_no_outlier = y_pred[:-1]

print("\nWITHOUT OUTLIER:")
print(f"MAE:  {mean_absolute_error(y_true_no_outlier, y_pred_no_outlier):.2f}")
print(f"RMSE: {np.sqrt(mean_squared_error(y_true_no_outlier, y_pred_no_outlier)):.2f}")
print(f"R²:   {r2_score(y_true_no_outlier, y_pred_no_outlier):.4f}")

# Visualization
fig, axes = plt.subplots(1, 3, figsize=(15, 4))

# 1. Actual vs Predicted
axes[0].scatter(y_true, y_pred, alpha=0.7)
axes[0].plot([y_true.min(), y_true.max()], [y_true.min(), y_true.max()], 'r--')
axes[0].set_xlabel('Actual')
axes[0].set_ylabel('Predicted')
axes[0].set_title('Actual vs Predicted')

# 2. Residuals
axes[1].scatter(y_pred, y_true - y_pred, alpha=0.7)
axes[1].axhline(0, color='red', linestyle='--')
axes[1].set_xlabel('Predicted')
axes[1].set_ylabel('Residuals')
axes[1].set_title('Residual Plot')

# 3. Error Distribution
axes[2].hist(y_true - y_pred, bins=20, edgecolor='black', alpha=0.7)
axes[2].set_xlabel('Error')
axes[2].set_ylabel('Frequency')
axes[2].set_title('Error Distribution')

plt.tight_layout()
plt.show()
```

## 4.2 Classification Metrics - Complete Implementation

```python
from sklearn.metrics import (confusion_matrix, classification_report, 
                             accuracy_score, precision_score, recall_score, 
                             f1_score, roc_curve, auc, precision_recall_curve,
                             roc_auc_score, average_precision_score)
from sklearn.datasets import make_classification
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
import seaborn as sns

# Generate imbalanced dataset
X, y = make_classification(n_samples=1000, n_features=20, n_classes=2,
                           n_informative=15, n_redundant=5,
                           weights=[0.9, 0.1], random_state=42)  # 90-10 split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Train model
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

# Get predictions and probabilities
y_pred = model.predict(X_test)
y_pred_proba = model.predict_proba(X_test)[:, 1]

# Basic Metrics
print("=" * 50)
print("CLASSIFICATION METRICS")
print("=" * 50)
print(f"Accuracy:  {accuracy_score(y_test, y_pred):.4f}")
print(f"Precision: {precision_score(y_test, y_pred):.4f}")
print(f"Recall:    {recall_score(y_test, y_pred):.4f}")
print(f"F1-Score:  {f1_score(y_test, y_pred):.4f}")
print("=" * 50)

# Confusion Matrix
cm = confusion_matrix(y_test, y_pred)
plt.figure(figsize=(8, 6))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
            xticklabels=['Negative', 'Positive'],
            yticklabels=['Negative', 'Positive'])
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Confusion Matrix')
plt.show()

# Classification Report (All metrics per class)
print("\nCLASSIFICATION REPORT:")
print(classification_report(y_test, y_pred, target_names=['Class 0', 'Class 1']))

# ROC Curve
fpr, tpr, thresholds = roc_curve(y_test, y_pred_proba)
roc_auc = auc(fpr, tpr)

plt.figure(figsize=(8, 6))
plt.plot(fpr, tpr, color='darkorange', lw=2, label=f'ROC Curve (AUC = {roc_auc:.2f})')
plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--', label='Random Classifier')
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('Receiver Operating Characteristic (ROC) Curve')
plt.legend(loc='lower right')
plt.show()

# Precision-Recall Curve (Better for imbalanced data)
precision_curve, recall_curve, thresholds_pr = precision_recall_curve(y_test, y_pred_proba)
pr_auc = average_precision_score(y_test, y_pred_proba)

plt.figure(figsize=(8, 6))
plt.plot(recall_curve, precision_curve, color='blue', lw=2, 
         label=f'PR Curve (AUC = {pr_auc:.2f})')
plt.xlabel('Recall')
plt.ylabel('Precision')
plt.title('Precision-Recall Curve')
plt.legend(loc='lower left')
plt.show()

# Threshold Analysis
print("\nTHRESHOLD ANALYSIS:")
thresholds_to_check = [0.3, 0.4, 0.5, 0.6, 0.7]
for thresh in thresholds_to_check:
    y_pred_thresh = (y_pred_proba >= thresh).astype(int)
    print(f"Threshold {thresh}: Precision={precision_score(y_test, y_pred_thresh):.3f}, "
          f"Recall={recall_score(y_test, y_pred_thresh):.3f}, "
          f"F1={f1_score(y_test, y_pred_thresh):.3f}")
```

## 4.3 Cross-Validation for Robust Metrics

```python
from sklearn.model_selection import cross_validate, StratifiedKFold

# Multiple scoring metrics
scoring = {
    'accuracy': 'accuracy',
    'precision': 'precision',
    'recall': 'recall',
    'f1': 'f1',
    'roc_auc': 'roc_auc'
}

# Stratified K-Fold (maintains class distribution)
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)

# Cross-validate
cv_results = cross_validate(model, X, y, cv=cv, scoring=scoring, return_train_score=False)

# Display results
print("=" * 70)
print("CROSS-VALIDATION RESULTS (5-Fold)")
print("=" * 70)
for metric in scoring.keys():
    mean_score = cv_results[f'test_{metric}'].mean()
    std_score = cv_results[f'test_{metric}'].std()
    print(f"{metric:12s}: {mean_score:.4f} (+/- {std_score:.4f})")
print("=" * 70)

# Compare models
from sklearn.linear_model import LogisticRegression
from sklearn.svm import SVC

models = {
    'Logistic Regression': LogisticRegression(max_iter=1000),
    'Random Forest': RandomForestClassifier(n_estimators=100),
    'SVM': SVC(probability=True)
}

print("\nMODEL COMPARISON (ROC-AUC):")
for name, mdl in models.items():
    scores = cross_validate(mdl, X, y, cv=cv, scoring='roc_auc')
    print(f"{name:20s}: {scores['test_score'].mean():.4f} (+/- {scores['test_score'].std():.4f})")
```

## 4.4 Custom Metric Implementation

```python
from sklearn.metrics import make_scorer

# Business-specific metric example
# E.g., Fraud detection where false negatives cost 10x more than false positives
def business_cost_metric(y_true, y_pred, fp_cost=1, fn_cost=10):
    """
    Calculate total business cost of predictions
    Lower is better
    """
    cm = confusion_matrix(y_true, y_pred)
    tn, fp, fn, tp = cm.ravel()
    
    total_cost = (fp * fp_cost) + (fn * fn_cost)
    return total_cost

# Make it a scorer for sklearn
business_scorer = make_scorer(business_cost_metric, greater_is_better=False)

# Use in cross-validation
cost_results = cross_validate(model, X, y, cv=cv, scoring=business_scorer)
print(f"Average Business Cost: {-cost_results['test_score'].mean():.2f}")

# Weighted F1-Score (for multi-class imbalance)
def weighted_f1(y_true, y_pred, class_weights=None):
    """Calculate weighted F1 score"""
    from sklearn.metrics import f1_score
    return f1_score(y_true, y_pred, average='weighted', sample_weight=class_weights)
```

---

# 📚 LEVEL 5: CASE STUDIES

## Case Study 1: House Price Prediction (Regression)

### Problem
Predict house prices for a real estate platform. Business needs accurate price estimates for listings.

### Dataset
- **Source:** Kaggle House Prices
- **Size:** 1,460 houses, 79 features
- **Target:** SalePrice (USD)

### Metric Selection Process

```
Business Question → "How wrong are our predictions in dollars?"
        ↓
Primary Metric → RMSE (error in original units)
        ↓
Secondary Metric → R² (how much better than baseline)
        ↓
Validation → Cross-Validation RMSE
```

### Model Comparison

| **Model** | **Train RMSE** | **CV RMSE** | **R²** | **Overfitting?** |
|:---|:---|:---|:---|:---|
| Linear Regression | $35,000 | $38,000 | 0.82 | No |
| Ridge Regression | $34,500 | $37,200 | 0.83 | No |
| Random Forest | $28,000 | $35,500 | 0.86 | Slight |
| XGBoost | $25,000 | $34,800 | 0.88 | Slight |
| **Ensemble** | **$23,000** | **$34,200** | **0.89** | **No** |

### Key Learnings

1. **CV RMSE > Train RMSE** indicates some overfitting
2. **R² of 0.89** means model explains 89% of price variance
3. **RMSE of $34,200** on average house price of $180,000 = ~19% error
4. **Business Decision:** Good enough for estimates, but human review needed for high-value properties

### Production Monitoring

```python
# Track metric drift over time
class MetricTracker:
    def __init__(self):
        self.history = []
    
    def log(self, date, rmse, r2, n_samples):
        self.history.append({
            'date': date,
            'rmse': rmse,
            'r2': r2,
            'n_samples': n_samples
        })
    
    def check_drift(self, baseline_rmse, threshold=0.15):
        """Alert if RMSE drifts more than 15% from baseline"""
        latest = self.history[-1]['rmse']
        drift = abs(latest - baseline_rmse) / baseline_rmse
        if drift > threshold:
            return f"ALERT: RMSE drifted {drift:.1%} from baseline!"
        return "OK"
```

---

## Case Study 2: Credit Card Fraud Detection (Classification - Imbalanced)

### Problem
Detect fraudulent transactions in real-time. Dataset is 99.8% legitimate, 0.2% fraud.

### Dataset
- **Source:** Kaggle Credit Card Fraud
- **Size:** 284,807 transactions
- **Fraud Cases:** 492 (0.172%)
- **Features:** 28 (PCA-transformed) + Time + Amount

### The Accuracy Trap

| **Model** | **Accuracy** | **Precision** | **Recall** | **F1-Score** | **ROC-AUC** | **PR-AUC** |
|:---|:---|:---|:---|:---|:---|:---|
| **Predict All Legitimate** | **99.8%** | **0%** | **0%** | **0%** | **0.5** | **0.0017** |
| Logistic Regression | 99.8% | 86.5% | 62.4% | 72.5% | 0.96 | 0.72 |
| Random Forest | 99.8% | 91.2% | 78.6% | 84.4% | 0.98 | 0.81 |
| **XGBoost (Tuned)** | **99.8%** | **93.8%** | **84.2%** | **88.7%** | **0.99** | **0.87** |

### Key Insight
**Accuracy is meaningless here!** All models show 99.8% accuracy, but performance varies drastically.

### Metric Selection for Production

```
Business Cost Analysis:
- False Negative (missed fraud): $1,000 average loss
- False Positive (blocked legitimate): $10 customer service cost
- Ratio: 100:1

Optimal Threshold Selection:
→ Minimize: (FN × $1000) + (FP × $10)
→ Not maximize accuracy or F1!
```

### Threshold Optimization Code

```python
def find_optimal_threshold(y_true, y_proba, fn_cost=1000, fp_cost=10):
    """Find threshold that minimizes business cost"""
    thresholds = np.arange(0.01, 0.99, 0.01)
    best_threshold = 0.5
    min_cost = float('inf')
    
    for thresh in thresholds:
        y_pred = (y_proba >= thresh).astype(int)
        cm = confusion_matrix(y_true, y_pred)
        tn, fp, fn, tp = cm.ravel()
        
        total_cost = (fn * fn_cost) + (fp * fp_cost)
        
        if total_cost < min_cost:
            min_cost = total_cost
            best_threshold = thresh
    
    return best_threshold, min_cost

optimal_thresh, min_cost = find_optimal_threshold(y_test, y_pred_proba)
print(f"Optimal Threshold: {optimal_thresh:.2f}")
print(f"Minimum Expected Cost: ${min_cost:,.2f}")
```

### Results

| **Threshold** | **Precision** | **Recall** | **Expected Cost** |
|:---|:---|:---|:---|
| 0.5 (Default) | 93.8% | 84.2% | $45,600 |
| **0.23 (Optimized)** | **78.5%** | **94.6%** | **$28,400** |
| 0.1 | 45.2% | 98.9% | $67,800 |

### Business Impact
- **37% reduction** in expected fraud losses
- **Higher recall** prioritized (catch more fraud)
- **Accept lower precision** (more false alarms acceptable)

---

## Case Study 3: Medical Diagnosis - Multi-Class Classification

### Problem
Classify skin lesions into 7 categories (benign vs malignant types). Imbalanced classes with critical misclassification costs.

### Dataset
- **Source:** ISIC Skin Image Classification
- **Classes:** 7 types (Melanoma, Nevus, Basal Cell, etc.)
- **Size:** 25,000 images
- **Imbalance:** Some classes have 100x more samples than others

### Multi-Class Metric Strategies

| **Averaging Method** | **Formula** | **When to Use** |
|:---|:---|:---|
| **Macro** | Unweighted mean per class | All classes equally important |
| **Micro** | Global TP, FP, FN | Overall performance, class size matters |
| **Weighted** | Mean weighted by support | Imbalanced datasets, reflect real distribution |

### Results Comparison

| **Model** | **Accuracy** | **Macro F1** | **Weighted F1** | **Per-Class Recall (Melanoma)** |
|:---|:---|:---|:---|:---|
| ResNet50 | 82.3% | 0.71 | 0.81 | 78.5% |
| EfficientNet | 84.1% | 0.74 | 0.83 | 82.3% |
| **Ensemble** | **85.6%** | **0.78** | **0.85** | **87.9%** |

### Critical Finding
**Macro F1 is the true metric here** - Melanoma detection matters more than common benign lesions, even though it's rare.

### Confusion Matrix Analysis

```
┌─────────────────────────────────────────────────────────────────┐
│              NORMALIZED CONFUSION MATRIX                         │
├─────────────────────────────────────────────────────────────────┤
│  Key Insight: Model confuses Melanoma with Nevus (both dark)    │
│  Action: Collect more training data for these confusing pairs   │
│  Metric: Per-class recall more important than overall accuracy  │
└─────────────────────────────────────────────────────────────────┘
```

### Production Deployment Metrics

```python
class MedicalModelMonitor:
    def __init__(self, critical_classes=['Melanoma', 'Basal Cell']):
        self.critical_classes = critical_classes
        self.alerts = []
    
    def evaluate(self, y_true, y_pred, class_names):
        """Evaluate with focus on critical classes"""
        report = classification_report(y_true, y_pred, 
                                       target_names=class_names,
                                       output_dict=True)
        
        # Check critical class recall
        for cls in self.critical_classes:
            recall = report[cls]['recall']
            if recall < 0.85:  # 85% minimum threshold
                self.alerts.append(f"ALERT: {cls} recall ({recall:.2%}) below threshold!")
        
        # Check macro F1
        macro_f1 = report['macro avg']['f1-score']
        if macro_f1 < 0.75:
            self.alerts.append(f"ALERT: Macro F1 ({macro_f1:.2%}) below threshold!")
        
        return report, self.alerts
```

---

# 🎯 INDUSTRY INSIGHTS & INTERVIEW PREPARATION

## Top 10 Interview Questions on Metrics

1.  **Q:** When would you choose MAE over RMSE?
    *   **A:** MAE when outliers exist and you want interpretable error. RMSE when large errors are particularly costly.

2.  **Q:** Why is accuracy misleading for imbalanced datasets?
    *   **A:** A model predicting only majority class can have high accuracy but zero utility. Use Precision/Recall/F1 or ROC-AUC instead.

3.  **Q:** What does R² = 0.5 mean?
    *   **A:** Model explains 50% of variance in target. 50% better than predicting the mean.

4.  **Q:** When is PR-AUC better than ROC-AUC?
    *   **A:** Highly imbalanced datasets (<10% positive class). ROC-AUC can be optimistic with many true negatives.

5.  **Q:** How do you choose the classification threshold?
    *   **A:** Based on business cost function, not default 0.5. Optimize for precision/recall trade-off that matches use case.

6.  **Q:** What's the difference between Macro and Micro averaging?
    *   **A:** Macro treats all classes equally. Micro weights by class size. Use Macro for balanced importance, Micro for overall performance.

7.  **Q:** Can R² be negative?
    *   **A:** Yes! When model performs worse than predicting the mean. Indicates serious model problems.

8.  **Q:** Why use cross-validation for metrics?
    *   **A:** Single train/test split can be lucky/unlucky. CV gives robust estimate of generalization performance.

9.  **Q:** What metric would you use for ranking problems?
    *   **A:** NDCG (Normalized Discounted Cumulative Gain), MAP (Mean Average Precision), not accuracy.

10. **Q:** How do you monitor metrics in production?
    *   **A:** Track metric drift, data drift, set up alerts for threshold violations, retrain triggers.

## Metric Selection Cheat Sheet

| **Business Problem** | **Primary Metric** | **Secondary Metric** | **Watch Out For** |
|:---|:---|:---|:---|
| House Price Prediction | RMSE | R² | Outliers, Log-transform target |
| Stock Price Forecast | MAPE | MAE | Non-stationarity, Look-ahead bias |
| Spam Detection | Precision | F1-Score | False positives annoy users |
| Cancer Detection | Recall | F2-Score | False negatives are deadly |
| Fraud Detection | PR-AUC | Business Cost | Extreme imbalance (0.1% fraud) |
| Customer Churn | ROC-AUC | Precision@K | Class imbalance, Time-based validation |
| Recommendation | NDCG@K | Hit Rate | Cold start, Diversity |
| Multi-class Image | Macro F1 | Per-class Recall | Class imbalance, Confusing pairs |
| Sentiment Analysis | Weighted F1 | Accuracy | Neutral class dominance |
| Anomaly Detection | Precision@K | Recall@K | Extreme imbalance, Unsupervised |

## Current Trends (2025-2026)

| **Trend** | **Impact on Metrics** | **New Considerations** |
|:---|:---|:---|
| **LLM Evaluation** | Traditional metrics insufficient | BLEU, ROUGE, BERTScore, Human eval |
| **Fairness Metrics** | Beyond accuracy | Demographic parity, Equalized odds |
| **Uncertainty Quantification** | Point estimates inadequate | Calibration error, Confidence intervals |
| **Multi-Objective Optimization** | Single metric insufficient | Pareto fronts, Weighted combinations |
| **Production Monitoring** | Offline metrics ≠ online performance | A/B testing, Business KPIs |
| **Explainability** | Black-box metrics questioned | SHAP, LIME, Counterfactual explanations |

---

# 🎓 FINAL MENTOR ADVICE

> **"Metrics are the compass of your ML journey. Choose the wrong one, and you'll optimize for the wrong destination. Choose wisely, and every improvement moves you toward real business value."**

## My Top 5 Recommendations:

1.  **Always Start with Business Goals:** What does success look like in dollars, lives saved, or user satisfaction? Translate that to a metric.

2.  **Never Trust a Single Metric:** Use 2-3 complementary metrics. Accuracy + F1 + ROC-AUC. RMSE + R² + MAE.

3.  **Validate with Cross-Validation:** Single train/test split is luck. 5-fold CV is standard. Time-series needs time-based splits.

4.  **Monitor in Production:** Training metrics ≠ Production metrics. Set up dashboards, alerts, and retrain triggers.

5.  **Understand the Limitations:** Every metric has blind spots. Know yours. Document them.

## Common Pitfalls to Avoid:

❌ **Using accuracy for imbalanced data** (The 99% trap)
❌ **Optimizing training metrics only** (Overfitting)
❌ **Ignoring business costs** (Mathematically optimal ≠ Business optimal)
❌ **Not checking metric assumptions** (R² assumes linearity)
❌ **Comparing models on different test sets** (Must be same data)
❌ **Forgetting confidence intervals** (Point estimates hide uncertainty)

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────────┐
│                    METRIC QUICK REFERENCE                        │
├─────────────────────────────────────────────────────────────────┤
│  REGRESSION:                                                    │
│  • Want interpretable error? → MAE                              │
│  • Large errors costly? → RMSE                                  │
│  • Compare to baseline? → R²                                    │
│  • Percentage matters? → MAPE                                   │
├─────────────────────────────────────────────────────────────────┤
│  CLASSIFICATION (Balanced):                                     │
│  • All errors equal? → Accuracy                                 │
│  • Need threshold-independent? → ROC-AUC                        │
│  • Want single number? → F1-Score                               │
├─────────────────────────────────────────────────────────────────┤
│  CLASSIFICATION (Imbalanced):                                   │
│  • Care about positives? → Precision/Recall                     │
│  • Need balance? → F1 or Fβ                                     │
│  • Compare models? → PR-AUC (not ROC-AUC)                       │
│  • Business costs known? → Optimize threshold for cost          │
└─────────────────────────────────────────────────────────────────┘
```

---