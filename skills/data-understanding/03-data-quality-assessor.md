# Data Quality Assessor

## Skill ID
`data-understanding-03-data-quality-assessor`

## Category
Data Understanding & Profiling

## Priority
Phase 1 (Core EDA) - High Priority

## Purpose
Automatically identify and report data quality issues, enabling data scientists to quickly understand data problems and prioritize cleaning efforts.

## User Problem Solved
Manual data quality assessment is tedious and error-prone. Issues often go unnoticed until they cause problems in modeling. This skill provides comprehensive, automated quality assessment.

## Capabilities

### Core Functions
1. **Missing Value Analysis**
   - Count and percentage of missing values per column
   - Identify missing value patterns (MCAR, MAR, MNAR)
   - Detect columns with excessive missingness
   - Visualize missing value patterns
   - Correlations between missingness

2. **Duplicate Detection**
   - Identify exact duplicate rows
   - Find near-duplicates with fuzzy matching
   - Detect duplicate keys/IDs
   - Report duplicate statistics

3. **Outlier Detection**
   - Statistical methods (IQR, Z-score)
   - Distribution-based detection
   - Multivariate outlier detection
   - Flag extreme values
   - Context-aware outlier assessment

4. **Data Consistency Checks**
   - Type mismatches (numeric stored as string)
   - Format inconsistencies (dates, phone numbers)
   - Range violations (negative ages, future dates)
   - Referential integrity (foreign key violations)
   - Business rule violations

5. **Data Type Assessment**
   - Verify appropriate data types
   - Identify type conversion opportunities
   - Flag mixed-type columns
   - Suggest type corrections

6. **Cardinality Analysis**
   - Identify zero-variance columns
   - Detect high-cardinality categoricals
   - Find single-value columns
   - Assess uniqueness constraints

7. **Data Quality Scoring**
   - Overall quality score per column
   - Dataset-wide quality metrics
   - Severity classification (critical, warning, info)
   - Prioritized issue list

## Usage Examples

### Example 1: Comprehensive Quality Assessment
```python
# User requests:
quality_report = assess_data_quality(data)

# Agent generates:
# 
# ===== DATA QUALITY ASSESSMENT =====
# Dataset: customer_data.csv
# Assessment Date: 2024-01-15 10:30:00
# 
# OVERALL QUALITY SCORE: 72/100 (Fair)
# 
# --- CRITICAL ISSUES (4) ---
# 
# 1. ❌ EXCESSIVE MISSING VALUES: 'income' column
#    - 4,523 missing (45.2% of records)
#    - Action: Review data collection process
#    - Impact: High - May bias analysis
# 
# 2. ❌ DUPLICATE RECORDS: 234 exact duplicates found
#    - Affects 2.3% of dataset
#    - Action: Investigate and remove duplicates
#    - Impact: High - Inflates statistics
# 
# 3. ❌ TYPE MISMATCH: 'order_date' column
#    - Stored as: object (should be datetime)
#    - Contains: 98% valid dates, 2% 'N/A' strings
#    - Action: Convert to datetime, handle invalid values
#    - Impact: High - Prevents temporal analysis
# 
# 4. ❌ REFERENTIAL INTEGRITY: 'product_id' column
#    - 156 IDs don't exist in product table
#    - Action: Validate with source system
#    - Impact: High - Invalid foreign keys
# 
# --- WARNINGS (7) ---
# 
# 5. ⚠️ OUTLIERS DETECTED: 'age' column
#    - 23 values below 0 (invalid)
#    - 12 values above 120 (suspicious)
#    - Action: Review and correct
#    - Impact: Medium - May distort analysis
# 
# 6. ⚠️ HIGH CARDINALITY: 'customer_id' column
#    - 9,856 unique values in 10,000 records
#    - May not be suitable as categorical feature
#    - Impact: Medium - Feature engineering needed
# 
# 7. ⚠️ ZERO VARIANCE: 'country' column
#    - Single value: 'USA' (100%)
#    - Action: Consider removing (no information)
#    - Impact: Low - Wastes memory
# 
# [Additional warnings...]
# 
# --- SUMMARY BY COLUMN ---
# 
# Column         Missing  Duplicates  Outliers  Type Issues  Quality Score
# customer_id    0.0%     0          0         None         95/100
# age            0.3%     0          35        None         88/100
# income         45.2%    0          78        None         45/100 ❌
# order_date     0.0%     0          0         Type mismatch 60/100 ⚠️
# product_id     0.5%     0          0         Ref. integrity 65/100 ⚠️
# 
# [Detailed visualizations of issues]
```

### Example 2: Missing Value Pattern Analysis
```python
# User requests:
missing_analysis = assess_missing_values(data)

# Output:
# 
# ===== MISSING VALUE ANALYSIS =====
# 
# Overall: 3.2% of all values are missing
# 
# Columns with Missing Values:
# 
# income: 45.2% missing (4,523 / 10,000)
#   Pattern: Missing At Random (MAR)
#   Correlation: Higher missingness in age < 25 group
#   [Visualization: Missing value heatmap]
# 
# phone: 12.3% missing (1,230 / 10,000)
#   Pattern: Missing Completely At Random (MCAR)
#   No significant correlation with other variables
# 
# email: 5.6% missing (560 / 10,000)
#   Pattern: Not Missing At Random (NMAR)
#   Missingness correlates with income and age
#   Likely: Older, lower-income customers less likely to provide
# 
# Recommendations:
# - income: Consider imputation or collect more data
# - phone: Safe to use simple imputation methods
# - email: Be cautious - missingness is informative
```

### Example 3: Quick Quality Check
```python
# User requests quick check:
quick_check = assess_data_quality(data, mode='quick')

# Output:
# ✓ No critical issues found
# ⚠️ 2 warnings detected
# ℹ️ 5 informational notes
# 
# Quality Score: 85/100 (Good)
# Safe to proceed with analysis.
```

## Input Requirements
- **Required**: DataFrame or data structure
- **Optional**:
  - Assessment mode (quick/standard/comprehensive)
  - Custom quality rules
  - Severity thresholds
  - Reference datasets for validation

## Output Format
- Structured quality report (text/markdown/HTML)
- Quality score (0-100)
- Prioritized issue list
- Visualizations of quality issues
- Actionable recommendations

## Configuration Options
```yaml
assessment_mode: "standard"  # quick, standard, comprehensive
missing_threshold: 0.05  # Flag if >5% missing
outlier_method: "iqr"  # iqr, zscore, isolation_forest
outlier_threshold: 3  # Standard deviations or IQR multiplier
duplicate_check: true
type_inference: true
referential_checks: false  # Requires reference datasets
generate_visualizations: true
severity_levels:
  critical: true  # Show critical issues
  warning: true   # Show warnings
  info: false     # Hide informational notes
```

## Integration Points
- Receives data from Data Loader & Inspector
- Complements Data Profiler with quality focus
- Informs Missing Data Handler about patterns
- Provides input for data cleaning decisions

## Success Metrics
- Completeness of issue detection
- False positive rate (flagging non-issues)
- Usefulness of recommendations
- Time saved vs manual inspection

## Implementation Notes
- Efficient computation for large datasets
- Use statistical methods for outlier detection
- Pattern recognition for common issues
- Context-aware severity classification
- Interactive HTML reports with drill-down capability

## Edge Cases & Limitations
- **Large datasets**: Sample for expensive checks
- **Complex business rules**: May need custom configuration
- **Domain-specific issues**: Can't detect all domain problems
- **Temporal data**: May need special handling for time series
- **Nested/hierarchical data**: Flatten or handle recursively

## Future Enhancements
- Machine learning-based anomaly detection
- Custom quality rule engine
- Integration with data catalogs
- Automated data profiling comparisons (drift detection)
- Data quality monitoring over time
- Suggested fix automation
- Quality SLA tracking
