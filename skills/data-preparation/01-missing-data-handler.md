# Missing Data Handler

## Skill ID
`data-preparation-01-missing-data-handler`

## Category
Data Preparation & Feature Engineering

## Priority
Phase 2 (Data Preparation) - High Priority

## Purpose
Provide intelligent strategies for handling missing data, from analysis of missingness patterns to implementation of appropriate imputation methods.

## User Problem Solved
Choosing the right missing data strategy is complex and impacts model performance. This skill analyzes missingness patterns and recommends/implements appropriate handling strategies.

## Capabilities

### Core Functions
1. **Missingness Pattern Analysis**
   - Classify as MCAR, MAR, or MNAR
   - Visualize missing data patterns
   - Identify correlations in missingness
   - Test statistical assumptions about missingness

2. **Strategy Recommendation**
   - Suggest appropriate methods based on pattern
   - Compare pros/cons of different approaches
   - Estimate impact on dataset size and bias
   - Recommend deletion vs imputation

3. **Deletion Methods**
   - Listwise deletion (complete case analysis)
   - Pairwise deletion
   - Column deletion (high missingness)
   - Impact analysis of deletion

4. **Simple Imputation**
   - Mean/median/mode imputation
   - Forward/backward fill (time series)
   - Constant value imputation
   - Random sampling from observed values

5. **Advanced Imputation**
   - K-Nearest Neighbors imputation
   - Iterative imputation (MICE)
   - Matrix factorization methods
   - Multiple imputation for uncertainty quantification

6. **Missing Value Indicators**
   - Create binary indicators for missingness
   - Useful when missingness is informative (NMAR)
   - Include in feature set for modeling

7. **Impact Assessment**
   - Compare distributions before/after imputation
   - Evaluate bias introduced
   - Assess statistical properties
   - Cross-validate imputation quality

## Usage Examples

### Example 1: Comprehensive Missing Data Analysis
```python
# User requests:
missing_analysis = analyze_missing_data(data)

# Agent provides:
# 
# ===== MISSING DATA ANALYSIS =====
# 
# Overall: 3.2% of values missing (32,000 / 1,000,000 values)
# Affected rows: 4,523 / 10,000 (45.2%)
# 
# --- COLUMNS WITH MISSING VALUES ---
# 
# income (45.2% missing):
#   Pattern: MAR (Missing At Random)
#   Correlated with: age < 25 (p < 0.001)
#   Recommendation: KNN or Iterative Imputation
#   Alternative: Create missing indicator + median imputation
# 
# phone (12.3% missing):
#   Pattern: MCAR (Missing Completely At Random)
#   No significant correlations detected
#   Recommendation: Simple imputation (mode) is safe
# 
# purchase_amount (2.1% missing):
#   Pattern: NMAR (Not Missing At Random)
#   Missingness likely indicates no purchase
#   Recommendation: Fill with 0 + add missing indicator
# 
# --- RECOMMENDED STRATEGY ---
# 
# 1. income: KNN imputation (k=5) using age, education, occupation
# 2. phone: Mode imputation
# 3. purchase_amount: Fill with 0 + create 'had_purchase' indicator
# 
# Expected outcome:
#   - Retain all 10,000 rows
#   - Minimal bias introduced
#   - Missingness information preserved where informative
```

### Example 2: Apply Imputation Strategy
```python
# User approves strategy:
imputed_data = handle_missing_data(
    data,
    strategies={
        'income': {'method': 'knn', 'n_neighbors': 5},
        'phone': {'method': 'mode'},
        'purchase_amount': {'method': 'constant', 'value': 0, 'add_indicator': True}
    }
)

# Agent executes:
# 
# ✓ Applying missing data strategies...
# 
# Processing 'income':
#   Method: KNN Imputation (k=5)
#   Features used: age, education, occupation
#   Imputed: 4,523 values
#   [Before/After distribution comparison plot]
#   ✓ Distribution preserved (KS test: p=0.23)
# 
# Processing 'phone':
#   Method: Mode imputation
#   Imputed: 1,230 values with most common value
#   ✓ Completed
# 
# Processing 'purchase_amount':
#   Method: Constant (0) + indicator
#   Imputed: 210 values
#   Created: 'purchase_amount_was_missing' column
#   ✓ Completed
# 
# ===== SUMMARY =====
# Original shape: (10,000, 15)
# Final shape: (10,000, 16)  # Added 1 missing indicator
# Missing values: 0
# 
# ✓ All missing values handled
```

### Example 3: Compare Imputation Methods
```python
# User wants to compare:
comparison = compare_imputation_methods(
    data,
    column='income',
    methods=['mean', 'median', 'knn', 'iterative']
)

# Output:
# 
# ===== IMPUTATION METHOD COMPARISON: 'income' =====
# 
# Method         Distribution  Bias    Variance  Computation  Score
#                Preservation  (MSE)   Introduced Time(s)     
# Mean           Fair          125.3   Low       0.01         68/100
# Median         Good          89.7    Low       0.01         75/100
# KNN (k=5)      Excellent     45.2    Medium    2.3          88/100
# Iterative      Excellent     42.1    Medium    8.7          90/100
# 
# [Visualizations comparing distributions]
# 
# Recommendation: Iterative imputation
#   Best statistical properties, acceptable computation time
#   Use KNN if speed is critical (only 3 points difference)
```

### Example 4: Multiple Imputation
```python
# User requests uncertainty quantification:
imputed_datasets = multiple_imputation(
    data,
    n_imputations=5,
    columns=['income', 'age']
)

# Output:
# 
# ✓ Generated 5 imputed datasets
# 
# Each dataset has different plausible values for missing data
# Use for:
#   - Uncertainty quantification in estimates
#   - Robust model training
#   - Sensitivity analysis
# 
# [Returns list of 5 complete datasets]
```

## Input Requirements
- **Required**: DataFrame with missing values
- **Optional**:
  - Specific columns to handle
  - Preferred imputation methods
  - Predictor columns for advanced methods
  - Validation dataset for method comparison

## Output Format
- Imputed dataset(s)
- Imputation report with statistics
- Before/after visualizations
- Missing value indicators (if created)
- Quality metrics for imputation

## Configuration Options
```yaml
analysis:
  detect_patterns: true
  visualize: true
  recommend: true

imputation:
  default_method: "auto"  # auto, mean, median, mode, knn, iterative
  knn:
    n_neighbors: 5
    weights: "distance"
  iterative:
    max_iter: 10
    random_state: 42
  multiple:
    n_imputations: 5

validation:
  compare_methods: false
  show_distributions: true
  statistical_tests: true

indicators:
  add_for_nmar: true  # Add missing indicators for NMAR variables
  threshold: 0.05  # Only if >5% missing
```

## Integration Points
- Receives analysis from Data Quality Assessor
- Uses profiling data from Data Profiler
- Feeds cleaned data to Feature Engineering
- Connects to Model Trainer pipeline

## Success Metrics
- Accuracy of missingness pattern detection
- Quality of imputed values (when ground truth available)
- Distribution preservation
- Model performance improvement
- User satisfaction with recommendations

## Implementation Notes
- Use scikit-learn's SimpleImputer and IterativeImputer
- Implement custom KNN with appropriate distance metrics
- For large datasets, consider sampling for method comparison
- Preserve original data (create copy for imputation)
- Track which values were imputed for transparency

## Edge Cases & Limitations
- **High missingness (>50%)**: Warn about reliability, suggest deletion
- **All missing**: Cannot impute, must delete column or use domain knowledge
- **Categorical with high cardinality**: Mode may not be appropriate
- **Time series**: Require forward/backward fill or interpolation
- **Spatial data**: May need geographic-aware imputation

## Future Enhancements
- Deep learning-based imputation (autoencoders, GANs)
- Time series-specific methods (interpolation, seasonal decomposition)
- Spatial imputation for geographic data
- Domain-specific imputation templates
- Active learning to request critical missing values
- Uncertainty-aware imputation with confidence intervals
- Integration with data collection to prevent future missingness
