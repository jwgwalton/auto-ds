# Data Profiler

## Skill ID
`data-understanding-02-data-profiler`

## Category
Data Understanding & Profiling

## Priority
Phase 1 (Core EDA) - High Priority

## Purpose
Generate comprehensive statistical profiles of datasets automatically, providing data scientists with deep insights into distributions, patterns, and characteristics without manual analysis.

## User Problem Solved
Creating comprehensive data profiles manually is time-consuming and error-prone. Data scientists often miss important characteristics or patterns when profiling large datasets with many variables.

## Capabilities

### Core Functions
1. **Numerical Variable Profiling**
   - Descriptive statistics (count, mean, std, min, quartiles, max)
   - Distribution shape (skewness, kurtosis)
   - Percentile distributions
   - Identify potential outliers
   - Detect zero-inflation or other unusual patterns

2. **Categorical Variable Profiling**
   - Unique value counts
   - Frequency distributions
   - Cardinality analysis
   - Most/least common values
   - Entropy and concentration metrics

3. **Date/Time Variable Profiling**
   - Range (earliest to latest)
   - Frequency/gaps analysis
   - Granularity detection (daily, monthly, etc.)
   - Seasonality indicators

4. **Text Variable Analysis**
   - Length statistics
   - Common patterns
   - Character distribution
   - Potential for further processing

5. **Correlation Analysis**
   - Numerical correlations (Pearson)
   - Categorical associations (Cramér's V)
   - Mixed-type relationships

6. **Distribution Visualization**
   - Histograms with statistical overlays
   - Box plots
   - QQ plots for normality assessment
   - KDE plots

## Usage Examples

### Example 1: Full Dataset Profile
```python
# User requests:
profile = create_data_profile(data)

# Agent generates comprehensive report including:
# 
# ===== DATASET PROFILE =====
# Generated: 2024-01-15 10:30:00
# Dataset: sales_data.csv
# 
# Overview:
# - 10,000 rows × 15 columns
# - 8 numerical, 5 categorical, 2 datetime
# 
# --- NUMERICAL VARIABLES ---
# 
# quantity:
#   count:      10,000
#   mean:       5.23
#   std:        2.41
#   min:        1.00
#   25%:        3.00
#   50%:        5.00
#   75%:        7.00
#   max:        15.00
#   skewness:   0.12 (approximately symmetric)
#   outliers:   45 values beyond 3 std
#   [Histogram visualization]
# 
# price:
#   count:      9,998 (2 missing)
#   mean:       49.99
#   std:        35.21
#   ...
#   distribution: Log-normal (consider log transformation)
#   [Histogram + KDE visualization]
# 
# --- CATEGORICAL VARIABLES ---
# 
# product_category:
#   unique:     12
#   most_freq:  Electronics (2,345 occurrences, 23.5%)
#   least_freq: Books (156 occurrences, 1.6%)
#   entropy:    2.31 (well distributed)
#   [Bar chart of frequencies]
```

### Example 2: Targeted Column Profile
```python
# User requests specific columns:
profile = create_data_profile(data, columns=['price', 'quantity', 'category'])

# Agent provides detailed analysis of only those columns
```

## Input Requirements
- **Required**: DataFrame or data structure
- **Optional**:
  - Specific columns to profile
  - Level of detail (quick/standard/comprehensive)
  - Include visualizations (yes/no)

## Output Format
- Structured report (markdown, HTML, or JSON)
- Statistical summary tables
- Distribution visualizations
- Actionable insights and recommendations

## Configuration Options
```yaml
detail_level: "standard"  # quick, standard, comprehensive
include_visualizations: true
compute_correlations: true
max_categorical_unique: 50  # For detailed frequency tables
outlier_method: "iqr"  # iqr, zscore, isolation_forest
generate_html_report: true
```

## Integration Points
- Receives data from Data Loader & Inspector
- Feeds insights to Auto-Visualizer
- Provides context for Data Quality Assessor
- Informs Feature Engineering decisions

## Success Metrics
- Coverage of statistical properties
- Accuracy of distribution characterization
- Usefulness of insights generated
- Time saved vs manual profiling

## Implementation Notes
- Use efficient computation for large datasets (sampling if needed)
- Generate interactive HTML reports when requested
- Similar to ydata-profiling (formerly pandas-profiling) but more focused
- Cache expensive computations

## Edge Cases & Limitations
- High-cardinality categoricals: Summarize top/bottom values only
- Very skewed distributions: Use robust statistics
- Large datasets: Use sampling for visualizations
- Memory constraints: Process in chunks

## Future Enhancements
- Automatic anomaly detection in distributions
- Time series specific profiling
- Multi-variate distribution analysis
- Custom profiling templates by domain
- Comparison profiles (compare two datasets)
