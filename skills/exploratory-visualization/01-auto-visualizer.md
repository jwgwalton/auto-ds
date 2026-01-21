# Auto-Visualizer

## Skill ID
`exploratory-visualization-01-auto-visualizer`

## Category
Exploratory Visualization

## Priority
Phase 1 (Core EDA) - High Priority

## Purpose
Automatically generate appropriate, publication-ready visualizations based on data types and analysis goals, eliminating the need for boilerplate plotting code.

## User Problem Solved
Data scientists spend considerable time deciding on appropriate visualization types and writing matplotlib/seaborn code. This skill automates visualization selection and creation based on data characteristics.

## Capabilities

### Core Functions
1. **Intelligent Plot Type Selection**
   - Analyze variable types (numerical, categorical, datetime)
   - Consider number of variables (univariate, bivariate, multivariate)
   - Select optimal visualization for the data

2. **Univariate Visualizations**
   - **Numerical**: Histograms, KDE plots, box plots, violin plots
   - **Categorical**: Bar charts, pie charts (when appropriate)
   - **Datetime**: Timeline plots, seasonal decomposition

3. **Bivariate Visualizations**
   - **Num × Num**: Scatter plots, line plots, hex bins (for dense data)
   - **Cat × Num**: Box plots, violin plots, strip plots grouped by category
   - **Cat × Cat**: Stacked/grouped bar charts, heatmaps, mosaic plots
   - **Time × Num**: Line plots, area charts

4. **Multivariate Visualizations**
   - Correlation heatmaps
   - Pair plots (scatter plot matrices)
   - Parallel coordinates
   - Small multiples/facet grids

5. **Statistical Overlays**
   - Mean/median lines
   - Confidence intervals
   - Trend lines and regression fits
   - Distribution parameters

6. **Automatic Styling**
   - Professional color schemes
   - Appropriate axis labels and titles
   - Legends and annotations
   - Optimal figure sizes

## Usage Examples

### Example 1: Automatic Single Variable Plot
```python
# User requests:
visualize(data['price'])

# Agent analyzes and creates:
# - Detects numerical continuous variable
# - Creates combined plot: histogram + KDE + box plot
# - Adds statistical annotations (mean, median, std)
# - Uses appropriate title: "Distribution of price"
# [Shows professional-looking visualization]
```

### Example 2: Relationship Visualization
```python
# User requests:
visualize(data, x='age', y='income', hue='education_level')

# Agent creates:
# - Scatter plot with color-coded education levels
# - Adds regression line for each education level
# - Includes correlation coefficient
# - Professional styling with legend
```

### Example 3: Automated EDA Suite
```python
# User requests overview:
visualize_all(data)

# Agent generates:
# - Distribution plot for each numerical variable
# - Frequency chart for each categorical variable
# - Correlation heatmap
# - Organized in multi-panel figure or separate plots
# - Saves as HTML dashboard or PDF report
```

### Example 4: Time Series
```python
# User requests:
visualize(data, x='date', y='sales')

# Agent creates:
# - Line plot with trend
# - Highlights seasonal patterns
# - Adds moving average overlay
# - Annotates significant events (outliers, peaks)
```

## Input Requirements
- **Required**: Data (DataFrame, Series, or arrays)
- **Optional**:
  - Specific columns to visualize
  - Plot type hint (if user has preference)
  - Grouping variables
  - Statistical overlays

## Output Format
- Matplotlib/Seaborn figure objects
- Interactive Plotly visualizations (optional)
- Saved images (PNG, PDF, SVG)
- HTML dashboards for multiple plots

## Configuration Options
```yaml
style: "seaborn-v0_8"  # matplotlib style
color_palette: "deep"  # seaborn palette
figure_size: "auto"  # or specific (width, height)
dpi: 100
interactive: false  # Use Plotly instead of matplotlib
save_format: "png"  # png, pdf, svg, html
statistical_annotations: true
show_grid: true
dark_mode: false
```

## Integration Points
- Receives profiling data from Data Profiler
- Works with Pattern Detector for highlighting findings
- Outputs to Report Generator
- Supports Visualization Enhancer for final polish

## Success Metrics
- Appropriateness of visualization for data type
- Visual clarity and readability
- Time saved vs manual plotting
- User satisfaction with defaults

## Implementation Notes
- Use seaborn for statistical plots
- Matplotlib as base, with option for Plotly interactivity
- Implement smart defaults for all plot parameters
- Handle edge cases (too many categories, extreme outliers)
- Responsive to data size (sampling for very large datasets)

## Edge Cases & Limitations
- **Too many categories**: Show top N, group others as "Other"
- **Extreme outliers**: Offer to remove or use log scale
- **High data density**: Use transparency, hex bins, or sampling
- **Missing values**: Clearly indicate how they're handled
- **Very small datasets**: Adjust plot types accordingly

## Future Enhancements
- Animated visualizations for time series
- 3D plots when appropriate
- Network graphs for relationship data
- Geographic maps for spatial data
- Custom templates by industry/domain
- A/B testing of visualization effectiveness
- Accessibility features (colorblind-friendly palettes, alt text)
