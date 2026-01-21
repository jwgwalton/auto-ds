# Agent Skills Catalog

This directory contains detailed specifications for discrete agent skills designed to augment data scientists in their EDA and ML workflows.

## Directory Structure

```
skills/
├── data-understanding/          # Skills for initial data exploration
├── exploratory-visualization/   # Skills for data visualization
├── data-preparation/           # Skills for data cleaning and feature engineering
├── ml-development/             # Skills for model training and evaluation
├── validation/                 # Skills for model validation and analysis
├── communication/              # Skills for reporting and documentation
└── best-practices/             # Skills for guidance and quality assurance
```

## Complete Skills Index

### Phase 1: Core EDA (High Priority)

#### Data Understanding & Profiling
1. **Data Loader & Inspector** (`data-understanding/01-data-loader-inspector.md`)
   - Load data from various sources
   - Automatic type inference
   - Basic dataset overview
   
2. **Data Profiler** (`data-understanding/02-data-profiler.md`)
   - Comprehensive statistical profiling
   - Distribution analysis
   - Automated profiling reports

3. **Data Quality Assessor** (`data-understanding/03-data-quality-assessor.md`)
   - Missing value detection
   - Outlier identification
   - Data quality metrics

#### Exploratory Visualization
4. **Auto-Visualizer** (`exploratory-visualization/01-auto-visualizer.md`)
   - Intelligent plot type selection
   - Univariate and bivariate plots
   - Automated EDA dashboards

### Phase 2: Data Preparation

5. **Missing Data Handler** (`data-preparation/01-missing-data-handler.md`)
   - Missing data pattern analysis
   - Imputation strategies
   - Impact comparison

6. **Feature Encoder** (`data-preparation/02-feature-encoder.md`)
   - Categorical encoding (one-hot, label, target)
   - Datetime feature extraction
   - High-cardinality handling

7. **Feature Scaler & Transformer** (`data-preparation/03-feature-scaler-transformer.md`)
   - Standardization and normalization
   - Distribution transformations
   - Algorithm-specific scaling

### Phase 3: Basic ML

8. **Problem Formulator** (`ml-development/01-problem-formulator.md`)
   - ML problem classification
   - Metric recommendation
   - Baseline strategy

9. **Baseline Model Builder** (`ml-development/02-baseline-model-builder.md`)
   - Simple baseline models
   - Performance benchmarks
   - Comparison foundations

10. **Model Trainer** (`ml-development/04-model-trainer.md`)
    - Training pipeline setup
    - Cross-validation
    - Model persistence

11. **Model Evaluator** (`ml-development/06-model-evaluator.md`)
    - Comprehensive metrics
    - Visualization generation
    - Model comparison

### Phase 4: Advanced ML

12. **Algorithm Recommender** (`ml-development/03-algorithm-recommender.md`)
    - Algorithm suggestions
    - Problem-specific recommendations
    - Trade-off analysis

13. **Hyperparameter Tuner** (`ml-development/05-hyperparameter-tuner.md`)
    - Grid/random/Bayesian search
    - Cross-validated tuning
    - Optimal parameter selection

14. **Feature Engineer** (`data-preparation/04-feature-engineer.md`)
    - Interaction features
    - Polynomial features
    - Domain-specific features

15. **Feature Selector** (`data-preparation/05-feature-selector.md`)
    - Filter/wrapper/embedded methods
    - Feature importance
    - Multicollinearity handling

### Phase 5: Interpretation & Validation

16. **Model Interpreter** (`ml-development/07-model-interpreter.md`)
    - Feature importance
    - SHAP values
    - Prediction explanations

17. **Error Analyzer** (`validation/01-error-analyzer.md`)
    - Error pattern identification
    - Misclassification analysis
    - Improvement suggestions

18. **Model Validator** (`validation/02-model-validator.md`)
    - Cross-validation
    - Overfitting detection
    - Statistical validation

### Phase 6: Analysis & Patterns

19. **Correlation & Relationship Analyzer** (`exploratory-visualization/02-correlation-analyzer.md`)
    - Correlation matrices
    - Relationship detection
    - Statistical tests

20. **Pattern & Trend Detector** (`exploratory-visualization/03-pattern-detector.md`)
    - Trend identification
    - Seasonality detection
    - Anomaly flagging

### Phase 7: Communication

21. **Insight Extractor** (`communication/01-insight-extractor.md`)
    - Key finding identification
    - Insight summarization
    - Impact ranking

22. **Report Generator** (`communication/04-report-generator.md`)
    - Automated report creation
    - Structured documentation
    - Multi-format export

23. **Visualization Enhancer** (`communication/02-visualization-enhancer.md`)
    - Publication-quality polish
    - Consistent styling
    - Interactive visualizations

### Phase 8: Quality & Governance

24. **Bias & Fairness Checker** (`validation/03-bias-fairness-checker.md`)
    - Fairness metrics
    - Disparate impact detection
    - Mitigation strategies

25. **Best Practice Advisor** (`best-practices/01-best-practice-advisor.md`)
    - Methodology guidance
    - Pitfall warnings
    - Statistical advice

26. **Code Quality Checker** (`best-practices/02-code-quality-checker.md`)
    - Data leakage detection
    - Best practice verification
    - Code improvement suggestions

### Phase 9: Advanced Features

27. **Code Documenter** (`communication/03-code-documenter.md`)
    - Automated documentation
    - Docstring generation
    - Reproducibility guides

28. **Experiment Tracker** (`best-practices/03-experiment-tracker.md`)
    - Experiment logging
    - Parameter tracking
    - Result comparison

## Skill Design Principles

Each skill follows these principles:

1. **Modularity**: Can be used independently or combined
2. **Configurability**: User controls behavior through parameters
3. **Transparency**: Explains actions and reasoning
4. **Interactivity**: Presents options, not just automation
5. **Educational**: Helps users learn while working
6. **Context-Aware**: Understands the broader workflow

## Using These Skills

### As a Data Scientist
- Review skill capabilities to understand what's available
- Request specific skills as needed in your workflow
- Combine multiple skills for comprehensive analysis
- Provide feedback to improve skill effectiveness

### As a Developer
- Each skill document provides detailed specifications
- Use as blueprint for implementation
- Follow the integration points to connect skills
- Implement configuration options for flexibility

### As a Product Manager
- Use to understand user value proposition
- Prioritize implementation based on phases
- Track success metrics for each skill
- Gather user feedback on skill utility

## Implementation Status

Current status: **Planning Phase**

All skills are currently in specification/design phase. Implementation will proceed according to the phase priorities outlined above.

## Contributing

To propose a new skill or modify an existing one:
1. Follow the skill template format
2. Define clear capabilities and use cases
3. Specify integration points
4. Include configuration options
5. Document edge cases and limitations

## Related Documents

- `../data-scientist-role.md` - Full description of data scientist role
- `../agent-skills-breakdown.md` - High-level skill categorization and breakdown
