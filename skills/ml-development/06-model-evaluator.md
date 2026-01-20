# Model Evaluator

## Skill ID
`ml-development-06-model-evaluator`

## Category
Machine Learning Model Development

## Priority
Phase 3 (Basic ML) - High Priority

## Purpose
Comprehensively evaluate ML model performance using appropriate metrics and visualizations, enabling data scientists to make informed decisions about model selection and improvement.

## User Problem Solved
Evaluating models requires computing numerous metrics, creating various plots, and comparing results across models. This skill automates comprehensive evaluation with best practices built-in.

## Capabilities

### Core Functions
1. **Classification Metrics**
   - Accuracy, Precision, Recall, F1-score
   - Confusion matrix
   - ROC curve and AUC
   - Precision-Recall curve and Average Precision
   - Class-specific metrics (for multi-class)
   - Cohen's Kappa, Matthews Correlation Coefficient

2. **Regression Metrics**
   - R² (coefficient of determination)
   - Mean Absolute Error (MAE)
   - Mean Squared Error (MSE)
   - Root Mean Squared Error (RMSE)
   - Mean Absolute Percentage Error (MAPE)
   - Median Absolute Error
   - Explained Variance Score

3. **Visualization Generation**
   - Confusion matrix heatmap
   - ROC curves (single and multi-class)
   - Precision-Recall curves
   - Predicted vs Actual plots (regression)
   - Residual plots (regression)
   - Learning curves
   - Calibration curves (classification)

4. **Segmented Analysis**
   - Performance by data segments
   - Performance by feature ranges
   - Time-based performance (if temporal)
   - Error distribution analysis

5. **Model Comparison**
   - Side-by-side metric comparison
   - Statistical significance tests
   - Relative performance rankings
   - Trade-off analysis (speed vs accuracy)

6. **Report Generation**
   - Comprehensive evaluation report
   - Executive summary with key findings
   - Detailed metric breakdowns
   - Recommendation for model selection

## Usage Examples

### Example 1: Binary Classification Evaluation
```python
# User provides:
evaluate_model(model, X_test, y_test, task='classification')

# Agent generates:
# 
# ===== MODEL EVALUATION REPORT =====
# Model: RandomForestClassifier
# Dataset: test set (2,000 samples)
# 
# --- OVERALL METRICS ---
# Accuracy:    0.86
# Precision:   0.84
# Recall:      0.88
# F1-Score:    0.86
# AUC-ROC:     0.92
# 
# --- CONFUSION MATRIX ---
#              Predicted
#              Neg    Pos
# Actual Neg   820    180
#        Pos   100    900
# 
# [Confusion matrix heatmap visualization]
# 
# --- CLASSIFICATION REPORT ---
#              precision    recall  f1-score   support
#     Class 0       0.89      0.82      0.85      1000
#     Class 1       0.83      0.90      0.87      1000
# 
# [ROC Curve visualization]
# [Precision-Recall Curve visualization]
# 
# --- KEY INSIGHTS ---
# ✓ Strong overall performance (AUC = 0.92)
# ⚠️ Higher false positives for Class 0 (18%)
# ✓ Good recall for Class 1 (90%)
# 
# Recommendation: Model performs well. Consider threshold adjustment
# to reduce false positives if needed.
```

### Example 2: Regression Evaluation
```python
# User provides:
evaluate_model(model, X_test, y_test, task='regression')

# Output:
# 
# ===== MODEL EVALUATION REPORT =====
# Model: RandomForestRegressor
# Dataset: test set (2,000 samples)
# 
# --- REGRESSION METRICS ---
# R² Score:    0.87
# RMSE:        12.45
# MAE:         8.32
# MAPE:        15.2%
# 
# [Predicted vs Actual scatter plot]
# [Residual plot]
# 
# --- ERROR ANALYSIS ---
# Mean residual: -0.03 (approximately unbiased)
# Residual std:  12.44
# 
# Residual distribution:
# [Histogram of residuals with normal overlay]
# 
# Outlier predictions (|error| > 30):
#   5 samples (0.25% of test set)
#   [Details of outliers]
# 
# --- KEY INSIGHTS ---
# ✓ Strong predictive power (R² = 0.87)
# ✓ Residuals approximately normal (good model fit)
# ⚠️ Slight heteroscedasticity observed (variance increases with prediction)
# 
# Recommendation: Model performs well. Consider log transformation
# of target to address heteroscedasticity.
```

### Example 3: Multi-Model Comparison
```python
# User provides multiple models:
compare_models([model1, model2, model3], X_test, y_test)

# Output:
# 
# ===== MODEL COMPARISON =====
# 
#                      Accuracy  Precision  Recall   F1    AUC   Time(s)
# RandomForest          0.86      0.84      0.88   0.86   0.92    2.3
# GradientBoosting      0.88      0.87      0.89   0.88   0.94    5.1
# LogisticRegression    0.82      0.80      0.84   0.82   0.88    0.1
# 
# [Bar chart comparing metrics]
# 
# Best by metric:
#   Accuracy: GradientBoosting (0.88)
#   AUC: GradientBoosting (0.94)
#   Speed: LogisticRegression (0.1s)
# 
# Recommendation: GradientBoosting offers best performance with
# acceptable inference time. Use if accuracy is priority.
# LogisticRegression suitable for real-time applications.
```

## Input Requirements
- **Required**:
  - Trained model
  - Test features (X_test)
  - Test labels (y_test)
- **Optional**:
  - Task type (auto-detected if not provided)
  - Specific metrics to compute
  - Visualization preferences

## Output Format
- Structured evaluation report (text/markdown/HTML)
- Metric dictionary/dataframe
- Visualization figures
- Recommendations and insights

## Configuration Options
```yaml
task: "auto"  # auto, classification, regression
metrics:
  classification: ["accuracy", "precision", "recall", "f1", "auc"]
  regression: ["r2", "rmse", "mae", "mape"]
visualizations:
  enabled: true
  save_figures: true
  format: "png"
threshold: 0.5  # For classification probability threshold
cross_validation_eval: false  # Evaluate using CV instead of holdout
generate_report: true
report_format: "html"  # text, markdown, html
confidence_intervals: true
statistical_tests: true  # For model comparison
```

## Integration Points
- Receives trained models from Model Trainer
- Uses predictions from models
- Feeds results to Error Analyzer for detailed investigation
- Supports Model Interpreter for understanding predictions
- Outputs to Report Generator

## Success Metrics
- Completeness of evaluation metrics
- Clarity of visualizations
- Usefulness of insights
- Time saved vs manual evaluation

## Implementation Notes
- Use scikit-learn metrics module as foundation
- Generate publication-quality plots with seaborn/matplotlib
- Support custom metrics via user-defined functions
- Handle class imbalance in metric computation
- Implement efficient computation for large test sets

## Edge Cases & Limitations
- **Multi-class classification**: Use macro/micro/weighted averaging
- **Imbalanced classes**: Report per-class metrics prominently
- **Very small test sets**: Warning about statistical significance
- **Regression with outliers**: Report robust metrics alongside standard ones
- **Missing predictions**: Handle gracefully, report separately

## Future Enhancements
- Automated threshold optimization for classification
- Fairness metrics across demographic groups
- Calibration analysis and suggestions
- Cost-sensitive evaluation
- Online evaluation for production models
- A/B test analysis integration
- Model card generation
- Interactive dashboards for exploration
