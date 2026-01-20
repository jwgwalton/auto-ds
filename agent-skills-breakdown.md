# Agent Skills Breakdown for Data Science Augmentation

This document breaks down the data scientist role into discrete, implementable agent skills that can augment human data scientists in their EDA and ML workflows.

## Skill Categories

### Category 1: Data Understanding & Profiling

#### Skill 1.1: Data Loader & Inspector
**Purpose**: Automate the initial data loading and basic inspection process.

**Capabilities**:
- Load data from various formats (CSV, Excel, JSON, Parquet, SQL databases)
- Automatically infer data types
- Display basic information (shape, columns, memory usage)
- Preview first/last rows
- Generate quick summary report

**User Interaction**:
- User provides data source
- Agent loads and presents basic overview
- User can focus on interpretation rather than boilerplate code

#### Skill 1.2: Data Profiler
**Purpose**: Generate comprehensive statistical profiles of datasets.

**Capabilities**:
- Compute descriptive statistics (mean, median, std, min, max, quartiles)
- Analyze distributions of numerical variables
- Profile categorical variables (unique values, frequencies, cardinality)
- Identify data types and suggest corrections if needed
- Generate automated profiling reports (similar to pandas-profiling)

**User Interaction**:
- User requests profile of entire dataset or specific columns
- Agent generates comprehensive statistical summary
- User reviews insights and identifies areas for deeper investigation

#### Skill 1.3: Data Quality Assessor
**Purpose**: Automatically identify and report data quality issues.

**Capabilities**:
- Detect missing values (counts, percentages, patterns)
- Identify duplicate records
- Find outliers using statistical methods (IQR, Z-score)
- Detect anomalies and inconsistencies
- Flag potential data entry errors
- Check for data type mismatches
- Identify columns with zero variance
- Report on data quality metrics

**User Interaction**:
- User requests data quality assessment
- Agent provides detailed quality report with severity levels
- User decides which issues to address and how

### Category 2: Exploratory Visualization

#### Skill 2.1: Auto-Visualizer
**Purpose**: Generate appropriate visualizations based on data types and analysis goals.

**Capabilities**:
- Create univariate plots (histograms, box plots, violin plots for numerical; bar charts for categorical)
- Generate bivariate plots (scatter plots, line plots, grouped bar charts)
- Produce correlation heatmaps
- Create distribution plots with statistical overlays
- Generate automated EDA visualization dashboards
- Adapt plot types based on data characteristics (e.g., log scale for skewed data)

**User Interaction**:
- User specifies variables or requests automated visualization suite
- Agent generates publication-ready plots
- User interprets patterns and refines visualizations as needed

#### Skill 2.2: Correlation & Relationship Analyzer
**Purpose**: Identify and visualize relationships between variables.

**Capabilities**:
- Compute correlation matrices (Pearson, Spearman, Kendall)
- Identify highly correlated variable pairs
- Perform chi-square tests for categorical relationships
- Create pair plots for multivariate analysis
- Detect non-linear relationships
- Generate relationship summary reports

**User Interaction**:
- User requests relationship analysis
- Agent identifies significant relationships and visualizes them
- User explores interesting relationships for feature engineering

#### Skill 2.3: Pattern & Trend Detector
**Purpose**: Automatically identify patterns, trends, and anomalies in data.

**Capabilities**:
- Detect temporal trends and seasonality
- Identify cyclical patterns
- Flag unusual observations or outlier clusters
- Recognize common data patterns (linear, exponential, logarithmic trends)
- Detect change points in time series
- Identify segments or clusters in data

**User Interaction**:
- User requests pattern detection on specific variables or dataset
- Agent highlights discovered patterns with visualizations
- User validates findings and incorporates into analysis

### Category 3: Data Preparation & Feature Engineering

#### Skill 3.1: Missing Data Handler
**Purpose**: Suggest and implement strategies for handling missing data.

**Capabilities**:
- Analyze missing data patterns (MCAR, MAR, MNAR)
- Suggest appropriate imputation strategies
- Implement various imputation methods (mean, median, mode, forward/backward fill, KNN, iterative)
- Create missing value indicators
- Recommend when to drop vs impute
- Compare impact of different strategies

**User Interaction**:
- User reviews missing data analysis
- Agent suggests strategies with pros/cons
- User selects approach; agent implements it

#### Skill 3.2: Feature Encoder
**Purpose**: Transform categorical and other features into model-ready formats.

**Capabilities**:
- Apply one-hot encoding for nominal categories
- Implement label encoding for ordinal features
- Create target encoding for high-cardinality categories
- Handle rare categories (grouping, dropping)
- Encode datetime features (extract year, month, day, day_of_week, etc.)
- Implement binary encoding, hash encoding
- Suggest appropriate encoding based on cardinality and model type

**User Interaction**:
- User identifies categorical features
- Agent recommends encoding strategies
- User approves; agent implements encoding

#### Skill 3.3: Feature Scaler & Transformer
**Purpose**: Apply appropriate scaling and transformations to features.

**Capabilities**:
- Standardize features (Z-score normalization)
- Normalize to range (Min-Max scaling)
- Apply robust scaling for data with outliers
- Implement log, square root, box-cox transformations
- Handle skewed distributions
- Create polynomial features
- Suggest appropriate scaling based on algorithm requirements

**User Interaction**:
- User specifies or agent recommends transformation needs
- Agent applies transformations and shows before/after distributions
- User validates appropriateness

#### Skill 3.4: Feature Engineer
**Purpose**: Generate new features from existing ones based on domain patterns.

**Capabilities**:
- Create interaction features (products, ratios)
- Generate polynomial features
- Extract datetime components
- Create aggregation features (groupby operations)
- Generate rolling window statistics for time series
- Create domain-specific features based on templates
- Suggest feature engineering ideas based on data characteristics

**User Interaction**:
- User reviews feature engineering suggestions
- User provides domain knowledge to guide creation
- Agent generates features; user selects which to keep

#### Skill 3.5: Feature Selector
**Purpose**: Identify and select the most relevant features for modeling.

**Capabilities**:
- Remove zero/low variance features
- Identify and handle multicollinear features
- Apply filter methods (correlation, mutual information, chi-square)
- Implement wrapper methods (RFE, forward/backward selection)
- Use embedded methods (L1 regularization, tree-based importance)
- Generate feature importance rankings
- Suggest optimal feature subsets

**User Interaction**:
- User specifies selection criteria or constraints
- Agent performs selection analysis
- User reviews recommendations and makes final decision

### Category 4: Machine Learning Model Development

#### Skill 4.1: Problem Formulator
**Purpose**: Help define the ML problem and suggest appropriate approaches.

**Capabilities**:
- Classify problem type (regression, binary/multi-class classification, clustering, etc.)
- Suggest appropriate evaluation metrics
- Recommend baseline models
- Identify problem-specific constraints
- Suggest train/validation/test split strategies
- Recommend handling of imbalanced classes (if applicable)

**User Interaction**:
- User describes business problem
- Agent suggests ML formulation and approach
- User confirms or refines the approach

#### Skill 4.2: Baseline Model Builder
**Purpose**: Quickly create baseline models for comparison.

**Capabilities**:
- Implement simple baseline models (mean, median, mode predictions)
- Create statistical baselines (linear regression, logistic regression)
- Build simple rule-based models
- Generate baseline performance metrics
- Establish minimum performance thresholds

**User Interaction**:
- User specifies problem
- Agent creates and evaluates baselines
- User uses baselines as comparison points for advanced models

#### Skill 4.3: Algorithm Recommender
**Purpose**: Suggest appropriate ML algorithms based on data and problem characteristics.

**Capabilities**:
- Analyze data characteristics (size, dimensionality, linearity)
- Consider problem constraints (interpretability, speed, accuracy)
- Recommend algorithms with rationale
- Suggest ensemble approaches when appropriate
- Provide algorithm comparison matrix
- Reference best practices for the problem type

**User Interaction**:
- User provides problem context and constraints
- Agent recommends algorithms with explanations
- User selects algorithms to try

#### Skill 4.4: Model Trainer
**Purpose**: Train models with appropriate configurations and best practices.

**Capabilities**:
- Set up model training pipelines
- Implement proper train/validation/test splits
- Apply cross-validation strategies
- Handle class imbalance with appropriate techniques
- Set random seeds for reproducibility
- Monitor training progress
- Generate training reports

**User Interaction**:
- User selects model and parameters
- Agent handles training infrastructure
- User monitors progress and reviews results

#### Skill 4.5: Hyperparameter Tuner
**Purpose**: Optimize model hyperparameters efficiently.

**Capabilities**:
- Define appropriate hyperparameter search spaces
- Implement grid search, random search, Bayesian optimization
- Use cross-validation for robust evaluation
- Handle computational budget constraints
- Parallelize search when possible
- Track and compare different configurations
- Generate tuning reports with best parameters

**User Interaction**:
- User specifies model and rough parameter ranges
- Agent executes systematic hyperparameter search
- User reviews results and selects best configuration

#### Skill 4.6: Model Evaluator
**Purpose**: Comprehensively evaluate model performance.

**Capabilities**:
- Compute relevant metrics (accuracy, precision, recall, F1, AUC, RMSE, MAE, R², etc.)
- Generate confusion matrices for classification
- Create ROC and Precision-Recall curves
- Produce residual plots for regression
- Analyze performance across different data segments
- Compare multiple models systematically
- Generate evaluation reports with visualizations

**User Interaction**:
- User specifies models to evaluate
- Agent produces comprehensive evaluation
- User interprets results to select best model

#### Skill 4.7: Model Interpreter
**Purpose**: Explain model predictions and behavior.

**Capabilities**:
- Calculate feature importance scores
- Generate SHAP values and plots
- Create partial dependence plots
- Produce individual prediction explanations
- Identify key drivers of predictions
- Visualize decision boundaries (for simple models)
- Generate model interpretation reports

**User Interaction**:
- User requests explanation of model behavior
- Agent provides interpretability analysis
- User gains insights into what the model learned

### Category 5: Model Validation & Analysis

#### Skill 5.1: Error Analyzer
**Purpose**: Analyze model errors to identify improvement opportunities.

**Capabilities**:
- Identify patterns in misclassifications or prediction errors
- Segment errors by feature values
- Find data regions where model struggles
- Compare errors across different models
- Generate error analysis reports
- Suggest potential improvements based on error patterns

**User Interaction**:
- User requests error analysis
- Agent identifies systematic error patterns
- User uses insights to improve model or features

#### Skill 5.2: Model Validator
**Purpose**: Validate models meet requirements and generalize well.

**Capabilities**:
- Perform cross-validation with multiple splits
- Test on holdout/test sets
- Check for overfitting/underfitting
- Validate statistical assumptions
- Test model stability across different samples
- Verify performance meets requirements

**User Interaction**:
- User specifies validation requirements
- Agent executes validation protocol
- User reviews validation results for approval

#### Skill 5.3: Bias & Fairness Checker
**Purpose**: Identify and measure potential biases in models.

**Capabilities**:
- Analyze performance across different demographic groups
- Compute fairness metrics (demographic parity, equal opportunity, etc.)
- Identify disparate impact
- Check for proxy discrimination
- Generate fairness reports
- Suggest mitigation strategies

**User Interaction**:
- User identifies sensitive attributes
- Agent assesses fairness across groups
- User addresses identified biases

### Category 6: Communication & Documentation

#### Skill 6.1: Insight Extractor
**Purpose**: Automatically identify and summarize key insights from analysis.

**Capabilities**:
- Identify statistically significant findings
- Summarize key patterns and relationships
- Highlight unexpected or counterintuitive results
- Rank insights by potential impact
- Generate natural language insight descriptions
- Create executive summaries

**User Interaction**:
- User completes analysis
- Agent extracts and summarizes key insights
- User refines and incorporates into reports

#### Skill 6.2: Visualization Enhancer
**Purpose**: Create publication-ready, polished visualizations.

**Capabilities**:
- Apply consistent styling and color schemes
- Add appropriate titles, labels, legends
- Optimize for readability (font sizes, aspect ratios)
- Create multi-panel figures
- Export in various formats (PNG, PDF, SVG)
- Generate interactive visualizations

**User Interaction**:
- User provides rough visualization or specifications
- Agent creates polished, presentation-ready version
- User incorporates into reports/presentations

#### Skill 6.3: Code Documenter
**Purpose**: Generate documentation for analysis code.

**Capabilities**:
- Add docstrings to functions
- Create inline comments explaining complex logic
- Generate README files for projects
- Create analysis workflows documentation
- Document data transformations and their rationale
- Generate reproducibility instructions

**User Interaction**:
- User writes analysis code
- Agent adds comprehensive documentation
- User reviews and refines documentation

#### Skill 6.4: Report Generator
**Purpose**: Create structured analysis reports.

**Capabilities**:
- Generate Jupyter notebooks with analysis flow
- Create markdown reports
- Produce HTML dashboards
- Structure reports with standard sections (intro, methods, results, conclusions)
- Include visualizations and tables
- Export to various formats

**User Interaction**:
- User specifies report requirements
- Agent assembles report from analysis components
- User reviews and customizes

### Category 7: Best Practices & Guidance

#### Skill 7.1: Best Practice Advisor
**Purpose**: Provide guidance on data science best practices.

**Capabilities**:
- Suggest appropriate validation strategies
- Recommend sample size requirements
- Warn about common pitfalls (data leakage, p-hacking, etc.)
- Advise on reproducibility practices
- Suggest when more data is needed
- Recommend appropriate statistical tests

**User Interaction**:
- Agent proactively warns about potential issues
- User requests guidance on specific decisions
- User follows recommendations or consciously chooses alternative

#### Skill 7.2: Code Quality Checker
**Purpose**: Ensure analysis code follows best practices.

**Capabilities**:
- Check for proper train/test separation
- Identify potential data leakage
- Verify random seed setting
- Check for proper scaling (applied to train, then transform test)
- Identify inefficient code patterns
- Suggest code improvements

**User Interaction**:
- User writes analysis code
- Agent reviews and provides feedback
- User addresses identified issues

#### Skill 7.3: Experiment Tracker
**Purpose**: Help organize and track multiple experiments.

**Capabilities**:
- Log model configurations and parameters
- Track performance metrics across experiments
- Version datasets and models
- Compare experiments systematically
- Generate experiment comparison reports
- Recommend next experiments based on results

**User Interaction**:
- User runs various experiments
- Agent tracks all details automatically
- User reviews experiment history to make decisions

## Implementation Priority

Suggested order for implementing these skills based on impact and frequency of use:

**Phase 1 (Core EDA)**:
1. Data Loader & Inspector (1.1)
2. Data Profiler (1.2)
3. Data Quality Assessor (1.3)
4. Auto-Visualizer (2.1)

**Phase 2 (Data Preparation)**:
5. Missing Data Handler (3.1)
6. Feature Encoder (3.2)
7. Feature Scaler & Transformer (3.3)

**Phase 3 (Basic ML)**:
8. Problem Formulator (4.1)
9. Baseline Model Builder (4.2)
10. Model Trainer (4.4)
11. Model Evaluator (4.6)

**Phase 4 (Advanced ML)**:
12. Algorithm Recommender (4.3)
13. Hyperparameter Tuner (4.5)
14. Feature Engineer (3.4)
15. Feature Selector (3.5)

**Phase 5 (Interpretation & Validation)**:
16. Model Interpreter (4.7)
17. Error Analyzer (5.1)
18. Model Validator (5.2)

**Phase 6 (Analysis & Patterns)**:
19. Correlation & Relationship Analyzer (2.2)
20. Pattern & Trend Detector (2.3)

**Phase 7 (Communication)**:
21. Insight Extractor (6.1)
22. Report Generator (6.4)
23. Visualization Enhancer (6.2)

**Phase 8 (Quality & Governance)**:
24. Bias & Fairness Checker (5.3)
25. Best Practice Advisor (7.1)
26. Code Quality Checker (7.2)

**Phase 9 (Advanced Features)**:
27. Code Documenter (6.3)
28. Experiment Tracker (7.3)

## Notes on Agent Implementation

Each skill should be implemented as:
- **Modular**: Can be used independently or combined with other skills
- **Configurable**: Allows user control over behavior and parameters
- **Transparent**: Explains what it's doing and why
- **Interactive**: Presents options and recommendations, not just automated actions
- **Educational**: Helps users learn while working
- **Context-aware**: Understands the broader analysis context when needed
