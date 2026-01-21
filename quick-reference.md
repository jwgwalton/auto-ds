# Quick Reference: Agent Skills

A concise reference guide for all 28 agent skills in the auto-ds framework.

## Phase 1: Core EDA (Start Here)

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Data Loader & Inspector** | Load data from various sources | File path, DB connection | Loaded data + overview |
| **Data Profiler** | Statistical profiling of dataset | DataFrame | Comprehensive profile report |
| **Data Quality Assessor** | Identify data quality issues | DataFrame | Quality report with issues |
| **Auto-Visualizer** | Generate appropriate visualizations | Data + variables | Publication-ready plots |

**When to use**: Beginning of every project, when exploring new datasets

---

## Phase 2: Data Preparation

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Missing Data Handler** | Analyze and handle missing values | DataFrame with missing values | Imputation strategy + imputed data |
| **Feature Encoder** | Encode categorical variables | DataFrame + categorical columns | Encoded features |
| **Feature Scaler & Transformer** | Scale and transform features | DataFrame + numerical columns | Scaled/transformed data |

**When to use**: After EDA, before modeling

---

## Phase 3: Basic ML

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Problem Formulator** | Define ML problem and approach | Data + business goal | Problem setup + recommendations |
| **Baseline Model Builder** | Create baseline models | Data + target | Baseline results |
| **Model Trainer** | Train models with best practices | Model + data | Trained model + metrics |
| **Model Evaluator** | Comprehensive model evaluation | Model + test data | Evaluation report |

**When to use**: Model development phase

---

## Phase 4: Advanced ML

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Algorithm Recommender** | Suggest appropriate algorithms | Data characteristics + constraints | Algorithm recommendations |
| **Hyperparameter Tuner** | Optimize model parameters | Model + parameter space | Best parameters + performance |
| **Feature Engineer** | Create new features | DataFrame + domain knowledge | Engineered features |
| **Feature Selector** | Select most relevant features | DataFrame + target | Selected feature subset |

**When to use**: Model optimization phase

---

## Phase 5: Interpretation & Validation

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Model Interpreter** | Explain model predictions | Model + data | Feature importance + explanations |
| **Error Analyzer** | Analyze model errors | Model + predictions + actuals | Error patterns + insights |
| **Model Validator** | Validate model robustness | Model + validation data | Validation results |

**When to use**: After model training, before deployment

---

## Phase 6: Analysis & Patterns

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Correlation & Relationship Analyzer** | Find variable relationships | DataFrame | Correlation matrix + relationships |
| **Pattern & Trend Detector** | Identify patterns in data | Time series or general data | Detected patterns + trends |

**When to use**: During EDA, feature engineering

---

## Phase 7: Communication

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Insight Extractor** | Identify key findings | Analysis results | Ranked insights + summaries |
| **Report Generator** | Create analysis reports | All analysis components | Structured report |
| **Visualization Enhancer** | Polish visualizations | Raw plots | Publication-ready visuals |

**When to use**: Final reporting, presentations

---

## Phase 8: Quality & Governance

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Bias & Fairness Checker** | Detect model biases | Model + sensitive attributes | Fairness metrics + issues |
| **Best Practice Advisor** | Provide methodology guidance | Context + planned approach | Recommendations + warnings |
| **Code Quality Checker** | Verify analysis code quality | Analysis code | Issues + improvement suggestions |

**When to use**: Throughout project, especially before deployment

---

## Phase 9: Advanced Features

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Code Documenter** | Generate code documentation | Analysis code | Documented code + README |
| **Experiment Tracker** | Track ML experiments | Experiments + results | Experiment comparison + insights |

**When to use**: Complex projects, team collaboration

---

## Skill Combinations (Workflows)

### Quick EDA Workflow
1. **Data Loader & Inspector** → Load and preview
2. **Data Quality Assessor** → Identify issues
3. **Data Profiler** → Comprehensive analysis
4. **Auto-Visualizer** → Create visualizations
5. **Insight Extractor** → Summarize findings

**Time**: 15 minutes (vs 2 hours manual)

---

### Complete ML Pipeline
1. **Data Loader & Inspector** → Load data
2. **Data Quality Assessor** → Check quality
3. **Problem Formulator** → Define problem
4. **Missing Data Handler** → Handle missing values
5. **Feature Encoder** → Encode categoricals
6. **Feature Scaler & Transformer** → Scale features
7. **Baseline Model Builder** → Create baselines
8. **Model Trainer** → Train models
9. **Model Evaluator** → Evaluate performance
10. **Model Interpreter** → Explain predictions
11. **Report Generator** → Create report

**Time**: 3 hours (vs 13 hours manual)

---

### Model Optimization Workflow
1. **Algorithm Recommender** → Suggest algorithms
2. **Feature Engineer** → Create features
3. **Feature Selector** → Select best features
4. **Hyperparameter Tuner** → Optimize parameters
5. **Error Analyzer** → Analyze mistakes
6. **Model Validator** → Validate robustness

**Time**: 2 hours (vs 6 hours manual)

---

## Skill Selection Guide

**Use this table to choose which skills to apply:**

| Your Goal | Recommended Skills |
|-----------|-------------------|
| Understand new dataset | Data Loader, Data Profiler, Data Quality Assessor, Auto-Visualizer |
| Prepare data for modeling | Missing Data Handler, Feature Encoder, Feature Scaler |
| Start ML project | Problem Formulator, Baseline Model Builder |
| Train initial models | Model Trainer, Model Evaluator |
| Improve model performance | Feature Engineer, Feature Selector, Hyperparameter Tuner |
| Understand model | Model Interpreter, Error Analyzer |
| Ensure quality | Data Quality Assessor, Model Validator, Bias & Fairness Checker |
| Create deliverables | Insight Extractor, Report Generator, Visualization Enhancer |
| Team collaboration | Code Documenter, Experiment Tracker, Best Practice Advisor |

---

## Key Principles

1. **Start Simple**: Begin with Phase 1 skills (EDA)
2. **Build Up**: Progress through phases as needed
3. **Combine Skills**: Most tasks benefit from multiple skills
4. **Stay in Control**: Skills suggest, you decide
5. **Learn as You Go**: Skills explain their recommendations

---

## Next Steps

1. **Familiarize**: Read skill specifications in `skills/` directory
2. **Practice**: Try example workflow in `example-workflow.md`
3. **Customize**: Configure skills for your needs
4. **Implement**: Build skills according to specifications
5. **Iterate**: Improve based on usage and feedback

---

## Resources

- **Full Documentation**: See `data-scientist-role.md` and `agent-skills-breakdown.md`
- **Skill Details**: Browse `skills/` directory
- **Example Usage**: See `example-workflow.md`
- **Skills Catalog**: See `skills/README.md`
