# Problem Formulator

## Skill ID
`ml-development-01-problem-formulator`

## Category
Machine Learning Model Development

## Priority
Phase 3 (Basic ML) - High Priority

## Purpose
Help data scientists properly formulate ML problems by identifying problem type, suggesting appropriate metrics, and recommending initial approaches.

## User Problem Solved
Correctly framing the ML problem is critical but often overlooked. Wrong problem formulation leads to inappropriate algorithms, metrics, and ultimately poor results. This skill ensures proper problem setup.

## Capabilities

### Core Functions
1. **Problem Type Classification**
   - Identify: Regression, Binary Classification, Multi-class Classification, Multi-label, Ranking, Clustering, Anomaly Detection, Time Series Forecasting, etc.
   - Analyze target variable characteristics
   - Consider business objectives
   - Suggest alternative formulations if applicable

2. **Metric Recommendation**
   - Suggest appropriate evaluation metrics
   - Explain metric choice rationale
   - Consider business context (cost of errors, class importance)
   - Recommend primary and secondary metrics
   - Warning about inappropriate metrics

3. **Baseline Strategy**
   - Recommend simple baseline approaches
   - Define minimum acceptable performance
   - Suggest naive predictors for comparison
   - Set performance expectations

4. **Data Split Strategy**
   - Recommend train/validation/test splits
   - Suggest split ratios
   - Identify need for stratification
   - Handle temporal data (time-based splits)
   - Consider data leakage prevention

5. **Class Imbalance Assessment**
   - Detect imbalanced classes
   - Suggest handling strategies
   - Recommend appropriate metrics for imbalanced data
   - Advise on sampling techniques

6. **Problem Constraints Identification**
   - Identify: interpretability needs, latency requirements, fairness constraints, resource limitations
   - Document assumptions
   - Flag potential challenges
   - Suggest mitigation strategies

7. **Success Criteria Definition**
   - Help define what "good enough" means
   - Translate business goals to ML metrics
   - Set realistic expectations
   - Define stopping criteria

## Usage Examples

### Example 1: Binary Classification Problem
```python
# User provides:
formulate_problem(
    data=customer_data,
    target='will_churn',
    business_goal='Predict customer churn to enable retention campaigns'
)

# Agent analyzes:
# 
# ===== ML PROBLEM FORMULATION =====
# 
# --- PROBLEM TYPE ---
# Binary Classification
#   Target variable: 'will_churn' (binary: 0/1)
#   Positive class: 1 (churned) - 15.2% of data
#   Negative class: 0 (retained) - 84.8% of data
# 
# --- IMBALANCE DETECTED ---
# ⚠️ Moderate class imbalance (1:5.6 ratio)
# 
# Recommendations:
#   - Use stratified sampling in train/test split
#   - Consider: SMOTE, class weights, or threshold adjustment
#   - Avoid accuracy as primary metric
# 
# --- RECOMMENDED METRICS ---
# 
# Primary Metric: F1-Score
#   Rationale: Balances precision and recall for imbalanced data
#   Business context: Equal cost for false positives and false negatives
# 
# Secondary Metrics:
#   - Precision: Avoid wasting resources on non-churners
#   - Recall: Capture as many actual churners as possible
#   - AUC-ROC: Overall model discrimination ability
#   - Precision-Recall AUC: Better for imbalanced data
# 
# Metrics to AVOID:
#   ❌ Accuracy: Misleading with imbalance (can get 84.8% by always predicting "no churn")
# 
# --- BASELINE STRATEGY ---
# 
# Baseline 1: Majority Class Predictor
#   Always predict "no churn"
#   Expected Accuracy: 84.8%
#   Expected F1: 0.0 (useless for positive class)
# 
# Baseline 2: Stratified Random Predictor
#   Predict based on class distribution
#   Expected F1: ~0.26
# 
# Baseline 3: Simple Logistic Regression
#   Use top 5 most correlated features
#   Expected F1: ~0.40-0.50
# 
# Target: Beat Baseline 3 by >10% (F1 > 0.55)
# 
# --- DATA SPLIT STRATEGY ---
# 
# Recommended split: 70% train / 15% validation / 15% test
#   Train: 7,000 samples (stratified)
#   Validation: 1,500 samples (for hyperparameter tuning)
#   Test: 1,500 samples (final evaluation)
# 
# ✓ Use stratified sampling to maintain class balance
# ✓ Set random seed for reproducibility
# 
# --- HANDLING IMBALANCE ---
# 
# Options (in order of recommendation):
#   1. Use class weights in model training
#   2. Apply SMOTE to training data only
#   3. Adjust decision threshold (optimize on validation set)
#   4. Ensemble of over/under-sampled models
# 
# --- PROBLEM CONSTRAINTS ---
# 
# Identified considerations:
#   - Interpretability: Moderate need (explain to retention team)
#   - Latency: Batch predictions acceptable (monthly)
#   - Fairness: Review predictions across customer segments
#   - Resource: Standard ML infrastructure sufficient
# 
# --- SUCCESS CRITERIA ---
# 
# Minimum Viable Performance:
#   F1-Score > 0.55 (10% improvement over baseline)
#   Precision > 0.60 (limit false alarms)
#   Recall > 0.50 (catch at least half of churners)
# 
# Target Performance:
#   F1-Score > 0.70
#   Precision > 0.75
#   Recall > 0.65
# 
# Business Success:
#   Enable retention team to reduce churn by 20%
#   ROI positive after 3 months
# 
# --- RECOMMENDED NEXT STEPS ---
# 
# 1. ✓ Create stratified train/validation/test splits
# 2. ✓ Build and evaluate baseline models
# 3. → Perform exploratory data analysis on features
# 4. → Try multiple algorithms (Logistic Reg, Random Forest, Gradient Boosting)
# 5. → Optimize on validation set using F1-score
# 6. → Evaluate final model on test set
# 7. → Analyze errors and iterate
```

### Example 2: Regression Problem
```python
# User provides:
formulate_problem(
    data=housing_data,
    target='sale_price',
    business_goal='Predict house prices for real estate platform'
)

# Output:
# 
# ===== ML PROBLEM FORMULATION =====
# 
# --- PROBLEM TYPE ---
# Regression
#   Target variable: 'sale_price' (continuous, positive)
#   Range: $50,000 - $800,000
#   Distribution: Right-skewed (consider log transformation)
# 
# --- RECOMMENDED METRICS ---
# 
# Primary Metric: Root Mean Squared Error (RMSE)
#   Rationale: Penalizes large errors, interpretable in $ units
#   Business context: Large prediction errors are costly
# 
# Secondary Metrics:
#   - MAE: More robust to outliers
#   - MAPE: Percentage error (for relative comparison)
#   - R²: Proportion of variance explained
# 
# --- BASELINE STRATEGY ---
# 
# Baseline 1: Mean Predictor
#   Predict median price: $180,000
#   Expected RMSE: ~$95,000
# 
# Baseline 2: Linear Regression on sqft
#   Use square footage only
#   Expected RMSE: ~$65,000
# 
# Target: RMSE < $45,000 (R² > 0.75)
# 
# --- DATA CONSIDERATIONS ---
# 
# ⚠️ Target is right-skewed
# Recommendation: Consider log transformation
#   - Train on log(price)
#   - Transform predictions back
#   - May improve model performance
# 
# --- SUCCESS CRITERIA ---
# 
# Minimum: RMSE < $50,000 (within 28% of median price)
# Target: RMSE < $40,000 (within 22% of median price)
# Stretch: RMSE < $30,000 (within 17% of median price)
```

### Example 3: Multi-class Classification
```python
# User provides:
formulate_problem(
    data=product_data,
    target='product_category',
    business_goal='Auto-categorize products for e-commerce platform'
)

# Output:
# 
# ===== ML PROBLEM FORMULATION =====
# 
# --- PROBLEM TYPE ---
# Multi-class Classification
#   Target variable: 'product_category' (15 classes)
#   Balanced: No (imbalance ratio: 1:8.3)
#   
# Class distribution:
#   Electronics: 2,345 (23.5%)
#   Clothing: 1,823 (18.2%)
#   ...
#   Books: 156 (1.6%)  ⚠️ Rare class
# 
# --- RECOMMENDED METRICS ---
# 
# Primary: Macro F1-Score
#   Treats all classes equally (important for rare categories)
# 
# Also consider:
#   - Weighted F1: Accounts for class frequency
#   - Per-class metrics: Identify weak spots
#   - Confusion matrix: Understand common misclassifications
# 
# --- CHALLENGES ---
# 
# ⚠️ Rare classes (3 classes with <200 samples)
#   May need: More data, SMOTE, or hierarchical approach
# 
# ⚠️ Potential class confusion
#   Some categories may overlap
#   Review confusion matrix to identify
```

## Input Requirements
- **Required**:
  - Dataset or target variable
  - Business goal/context
- **Optional**:
  - Constraints (interpretability, latency, etc.)
  - Cost matrix (if different errors have different costs)
  - Feature information

## Output Format
- Structured problem formulation report
- Problem type classification
- Recommended metrics with rationale
- Baseline strategy
- Success criteria
- Next steps recommendations

## Configuration Options
```yaml
analysis_depth: "standard"  # quick, standard, comprehensive
include_baselines: true
suggest_metrics: true
detect_imbalance: true
recommend_splits: true
identify_constraints: true
```

## Integration Points
- Feeds directly into Baseline Model Builder
- Informs Model Trainer about appropriate setup
- Guides Model Evaluator on metrics to use
- Connects to Best Practice Advisor

## Success Metrics
- Accuracy of problem type identification
- Appropriateness of metric recommendations
- User adoption of suggestions
- Prevention of common mistakes

## Implementation Notes
- Analyze target variable distribution and type
- Consider business context in recommendations
- Provide clear rationale for all suggestions
- Warn about common pitfalls
- Remain flexible - allow user override

## Edge Cases & Limitations
- **Ambiguous problems**: Offer multiple formulations
- **Multi-objective**: Help prioritize or create composite metrics
- **Novel problem types**: Provide general guidance
- **Conflicting constraints**: Highlight trade-offs

## Future Enhancements
- Interactive problem formulation wizard
- Industry-specific templates
- Cost-sensitive learning setup
- Multi-task learning formulation
- Online/continual learning setup
- Causal inference problem formulation
