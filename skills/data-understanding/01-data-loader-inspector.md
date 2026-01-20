# Data Loader & Inspector

## Skill ID
`data-understanding-01-loader-inspector`

## Category
Data Understanding & Profiling

## Priority
Phase 1 (Core EDA) - High Priority

## Purpose
Automate the initial data loading and basic inspection process, eliminating boilerplate code and allowing data scientists to quickly understand dataset structure.

## User Problem Solved
Data scientists spend significant time writing repetitive code to load data from various sources and perform basic inspection. This skill removes that friction and provides instant insights into data structure.

## Capabilities

### Core Functions
1. **Multi-Format Loading**
   - CSV, TSV files
   - Excel files (single or multiple sheets)
   - JSON (flat and nested)
   - Parquet files
   - SQL databases (via connection strings)
   - Feather, HDF5, Stata, SAS formats

2. **Automatic Type Inference**
   - Infer appropriate data types for each column
   - Detect dates/datetimes and parse them
   - Identify numerical vs categorical columns
   - Flag columns that might have incorrect types

3. **Basic Information Display**
   - Dataset shape (rows × columns)
   - Memory usage
   - Column names and data types
   - Non-null counts per column
   - Quick statistics (for numerical columns)

4. **Data Preview**
   - Display first/last N rows (configurable)
   - Show random sample of rows
   - Display specific columns

5. **Quick Summary Report**
   - One-page overview of the dataset
   - Highlight potential issues (missing values, duplicates)
   - Provide initial recommendations

## Usage Examples

### Example 1: Load CSV
```python
# User provides:
data_path = "sales_data.csv"

# Agent executes:
data = load_and_inspect(data_path)
# Output:
# ✓ Loaded sales_data.csv successfully
# Shape: 10,000 rows × 15 columns
# Memory: 1.2 MB
# 
# Columns (15):
#   - order_id (int64): 10,000 non-null
#   - customer_id (int64): 10,000 non-null
#   - order_date (datetime64): 10,000 non-null
#   - product_name (object): 10,000 non-null
#   - quantity (int64): 10,000 non-null
#   - price (float64): 9,998 non-null ⚠️ 2 missing
#   ...
# 
# Preview (first 5 rows):
# [DataFrame display]
```

### Example 2: Load from Database
```python
# User provides:
connection_string = "postgresql://user:pass@localhost/db"
query = "SELECT * FROM customers WHERE signup_date > '2023-01-01'"

# Agent executes:
data = load_and_inspect(connection_string, query=query)
# Similar output with additional info about source database
```

## Input Requirements
- **Required**: File path, database connection, or data URL
- **Optional**: 
  - Format-specific parameters (delimiter, sheet name, encoding)
  - Preview size (default: 5)
  - Type inference hints

## Output Format
- Loaded DataFrame/data structure
- Structured summary report (text + visualizations)
- Warnings about potential issues

## Configuration Options
```yaml
preview_rows: 5
infer_types: true
parse_dates: true
detect_encoding: true
memory_efficient: false  # Use chunking for large files
sample_for_preview: false  # Use random sample instead of head
```

## Integration Points
- Outputs to Data Profiler skill for detailed analysis
- Provides input to Data Quality Assessor
- Feeds into Auto-Visualizer for initial plots

## Success Metrics
- Time saved vs manual loading code
- Accuracy of type inference
- User satisfaction with initial insights

## Implementation Notes
- Use pandas as primary engine, with fallbacks for large files (Dask, chunking)
- Implement smart encoding detection for international data
- Cache loaded data to avoid re-loading
- Handle common file issues gracefully (wrong delimiter, encoding problems)

## Edge Cases & Limitations
- Very large files (>1GB): Use sampling or chunked loading
- Nested JSON: Flatten or preserve structure based on user preference
- Multi-sheet Excel: Load all or let user select
- Compressed files: Auto-detect and decompress

## Future Enhancements
- Auto-detection of file format without extension
- Integration with cloud storage (S3, GCS, Azure Blob)
- Streaming data sources
- API data loading with authentication
