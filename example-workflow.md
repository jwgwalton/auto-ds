# Example Workflow: Using Agent Skills in a Real Data Science Project

This document demonstrates how the agent skills work together in a real-world data science scenario.

## Scenario: Customer Churn Prediction

**Business Problem**: A telecom company wants to predict which customers are likely to churn so they can run targeted retention campaigns.

**Dataset**: Customer data with 10,000 records and 20 features including demographics, usage patterns, and service information.

## Workflow with Agent Skills

### Phase 1: Initial Data Understanding (30 minutes → 5 minutes)

#### Step 1: Load and Inspect Data
**Without Agent**:
```python
import pandas as pd
import numpy as np

# 15 lines of boilerplate code to load and inspect
df = pd.read_csv('customer_data.csv')
print(f"Shape: {df.shape}")
print(f"\nData types:\n{df.dtypes}")
print(f"\nMemory usage: {df.memory_usage().sum() / 1024**2:.2f} MB")
print(f"\nFirst few rows:\n{df.head()}")
print(f"\nBasic info:\n{df.info()}")
# ... more manual exploration
```

**With Data Loader & Inspector Agent**:
```python
data = load_and_inspect('customer_data.csv')
```
**Output**: Comprehensive overview in seconds, including automatic type inference and issue flagging.

---

#### Step 2: Profile the Data
**Without Agent**:
```python
# 50+ lines of code for comprehensive profiling
print(df.describe())
for col in df.select_dtypes(include='object'):
    print(f"\n{col}:")
    print(df[col].value_counts())
    
# Correlation analysis
numeric_cols = df.select_dtypes(include=np.number)
corr_matrix = numeric_cols.corr()
# ... manual visualization creation
```

**With Data Profiler Agent**:
```python
profile = create_data_profile(data)
```
**Output**: 
- Complete statistical summary
- Distribution analysis for all variables
- Correlation matrices
- Automated insights

**Time Saved**: 25 minutes

---

#### Step 3: Assess Data Quality
**Without Agent**:
```python
# 30+ lines to check quality issues
missing = df.isnull().sum()
missing_pct = (missing / len(df)) * 100
duplicates = df.duplicated().sum()

# Check outliers manually for each column
# Check data types
# Check for consistency issues
# ... tedious manual checks
```

**With Data Quality Assessor Agent**:
```python
quality_report = assess_data_quality(data)
```
**Output**:
```
===== DATA QUALITY ASSESSMENT =====
OVERALL QUALITY SCORE: 78/100 (Good)

--- CRITICAL ISSUES (2) ---
1. ❌ EXCESSIVE MISSING VALUES: 'monthly_charges'
   - 1,234 missing (12.3% of records)

2. ❌ TYPE MISMATCH: 'customer_since'
   - Stored as object, should be datetime

--- WARNINGS (4) ---
3. ⚠️ OUTLIERS: 'total_charges' (45 extreme values)
4. ⚠️ DUPLICATES: 23 exact duplicate records
...
```

**Time Saved**: 20 minutes

---

### Phase 2: Problem Formulation (45 minutes → 10 minutes)

**Without Agent**:
Data scientist must manually:
- Decide if it's classification or regression
- Choose appropriate metrics
- Think about class imbalance
- Design train/test split strategy
- Consider all edge cases

**With Problem Formulator Agent**:
```python
problem_setup = formulate_problem(
    data=data,
    target='churn',
    business_goal='Predict customer churn for retention campaigns'
)
```

**Output**:
```
===== ML PROBLEM FORMULATION =====

Problem Type: Binary Classification
Imbalance: Moderate (15% churn, 85% retained)

Recommended Metrics:
  Primary: F1-Score (balances precision/recall)
  Secondary: Precision, Recall, AUC-ROC

Baseline Strategy:
  1. Majority class: F1 = 0.0
  2. Simple logistic regression: F1 ≈ 0.45
  Target: F1 > 0.55

Data Split: 70/15/15 (train/val/test) with stratification

Handling Imbalance:
  - Use class weights in models
  - Consider SMOTE on training data
  - Optimize threshold on validation set

Success Criteria:
  Minimum: F1 > 0.55
  Target: F1 > 0.70, Precision > 0.75
```

**Time Saved**: 35 minutes (and prevents common mistakes)

---

### Phase 3: Data Preparation (2 hours → 30 minutes)

#### Step 3.1: Handle Missing Values
**With Missing Data Handler Agent**:
```python
missing_analysis = analyze_missing_data(data)
# Agent identifies patterns and recommends strategies

imputed_data = handle_missing_data(
    data,
    strategies={
        'monthly_charges': {'method': 'knn', 'n_neighbors': 5},
        'email': {'method': 'constant', 'value': 'unknown'},
    }
)
```

**Time Saved**: 45 minutes

---

#### Step 3.2: Encode Categorical Features
**With Feature Encoder Agent**:
```python
encoded_data = encode_features(
    imputed_data,
    # Agent automatically suggests appropriate encoding
    auto_encode=True
)
```

**Output**:
```
✓ Encoding 'contract_type' (3 categories): One-hot encoding
✓ Encoding 'payment_method' (4 categories): One-hot encoding  
✓ Encoding 'customer_segment' (high cardinality): Target encoding
```

**Time Saved**: 30 minutes

---

#### Step 3.3: Scale Features
**With Feature Scaler Agent**:
```python
scaled_data = scale_features(
    encoded_data,
    # Agent knows which algorithms need scaling
    target_algorithm='logistic_regression'
)
```

**Time Saved**: 15 minutes

---

### Phase 4: Model Development (4 hours → 1 hour)

#### Step 4.1: Create Baseline
**With Baseline Model Builder Agent**:
```python
baseline_results = build_baselines(scaled_data, target='churn')
```

**Output**:
```
Baseline 1 (Majority Class): F1 = 0.00
Baseline 2 (Random): F1 = 0.26
Baseline 3 (Logistic Regression): F1 = 0.47

Your model must beat: F1 = 0.52 (10% improvement)
```

**Time Saved**: 30 minutes

---

#### Step 4.2: Train Models
**Without Agent**:
```python
# 50+ lines for proper train/test split, cross-validation,
# handling imbalance, tracking experiments, etc.

from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from imblearn.over_sampling import SMOTE

# Manual train/test split with stratification
X = data.drop('churn', axis=1)
y = data['churn']
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

# Manual SMOTE application
smote = SMOTE(random_state=42)
X_train_balanced, y_train_balanced = smote.fit_resample(X_train, y_train)

# Train model
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train_balanced, y_train_balanced)

# ... more manual tracking
```

**With Model Trainer Agent**:
```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=100)

results = train_model(
    model=model,
    X=X_data,
    y=y_target,
    handle_imbalance='smote',
    cv=5
)
```

**Output**:
```
✓ Data split: 70% train, 15% val, 20% test (stratified)
✓ Applying SMOTE to balance classes
✓ 5-fold cross-validation

Fold 1: F1 = 0.72
Fold 2: F1 = 0.69
Fold 3: F1 = 0.71
Fold 4: F1 = 0.73
Fold 5: F1 = 0.70

Mean F1: 0.71 ± 0.02
✓ Model saved to: models/random_forest_20240115.pkl
```

**Time Saved**: 1.5 hours

---

#### Step 4.3: Evaluate Models
**With Model Evaluator Agent**:
```python
evaluation = evaluate_model(model, X_test, y_test)
```

**Output**:
```
===== MODEL EVALUATION =====
Model: RandomForestClassifier

Overall Metrics:
  Accuracy: 0.87
  Precision: 0.78
  Recall: 0.75
  F1-Score: 0.76
  AUC-ROC: 0.92

✓ EXCEEDS target (F1: 0.76 > 0.70)

[Confusion Matrix visualization]
[ROC Curve]
[Feature Importance plot]

Key Insights:
  ✓ Strong performance on both classes
  ✓ Good precision (few false alarms)
  ⚠️ Could improve recall (missing some churners)
  
Recommendation: Model ready for deployment
  Consider threshold adjustment to improve recall if needed
```

**Time Saved**: 1 hour

---

### Phase 5: Model Interpretation (2 hours → 20 minutes)

**With Model Interpreter Agent**:
```python
interpretation = interpret_model(model, X_test)
```

**Output**:
```
===== MODEL INTERPRETATION =====

Top 5 Most Important Features:
  1. contract_type_month_to_month (0.23)
  2. total_charges (0.18)
  3. monthly_charges (0.15)
  4. tenure (0.12)
  5. tech_support_no (0.09)

[SHAP summary plot]
[Partial dependence plots for top features]

Key Insights:
  - Month-to-month contracts have highest churn risk
  - Lower tenure strongly predicts churn
  - Customers without tech support more likely to churn

Business Recommendations:
  1. Offer incentives for annual contracts
  2. Focus retention on customers in first 6 months
  3. Proactively offer tech support to at-risk customers
```

**Time Saved**: 1.5 hours

---

### Phase 6: Reporting (3 hours → 30 minutes)

**With Report Generator & Insight Extractor Agents**:
```python
# Extract key insights
insights = extract_insights(
    data_profile=profile,
    quality_report=quality_report,
    model_results=results,
    interpretation=interpretation
)

# Generate report
report = generate_report(
    project_name="Customer Churn Prediction",
    insights=insights,
    format='html'
)
```

**Output**: Professional HTML report with:
- Executive summary
- Data quality assessment
- Model performance metrics
- Key insights and recommendations
- Visualizations
- Technical appendix

**Time Saved**: 2.5 hours

---

## Total Time Comparison

| Phase | Without Agents | With Agents | Time Saved |
|-------|----------------|-------------|------------|
| Data Understanding | 1.5 hours | 15 minutes | 1h 15m |
| Problem Formulation | 45 minutes | 10 minutes | 35 minutes |
| Data Preparation | 2 hours | 30 minutes | 1h 30m |
| Model Development | 4 hours | 1 hour | 3 hours |
| Model Interpretation | 2 hours | 20 minutes | 1h 40m |
| Reporting | 3 hours | 30 minutes | 2h 30m |
| **TOTAL** | **13.25 hours** | **2.75 hours** | **10.5 hours (79%)** |

## Quality Improvements

Beyond time savings, agent skills provide:

1. **Consistency**: Best practices applied automatically
2. **Completeness**: No forgotten steps or checks
3. **Education**: Learn from agent recommendations
4. **Documentation**: Automatic tracking and reporting
5. **Error Prevention**: Catch common mistakes (data leakage, wrong metrics, etc.)

## Key Takeaway

Agent skills don't just save time—they improve quality by:
- Implementing best practices automatically
- Preventing common mistakes
- Ensuring comprehensive analysis
- Generating professional documentation

The data scientist can focus on:
- Strategic decisions
- Domain expertise application
- Creative problem solving
- Interpreting and acting on results
