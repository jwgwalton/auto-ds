# Model Trainer

## Skill ID
`ml-development-04-model-trainer`

## Category
Machine Learning Model Development

## Priority
Phase 3 (Basic ML) - High Priority

## Purpose
Handle the infrastructure and best practices for training ML models, allowing data scientists to focus on model selection and interpretation rather than implementation details.

## User Problem Solved
Setting up proper training pipelines with cross-validation, handling data splits, managing random seeds, and tracking experiments involves significant boilerplate code. This skill automates the infrastructure.

## Capabilities

### Core Functions
1. **Training Pipeline Setup**
   - Automatic train/validation/test splits
   - Stratified sampling for classification
   - Time-based splits for temporal data
   - Cross-validation fold creation

2. **Model Training Execution**
   - Fit models with specified parameters
   - Handle scikit-learn, XGBoost, LightGBM, CatBoost, PyTorch, TensorFlow
   - Implement early stopping for iterative models
   - Monitor training progress

3. **Reproducibility Management**
   - Set and track random seeds
   - Version data and model configurations
   - Log all hyperparameters
   - Save trained models

4. **Special Data Handling**
   - Class imbalance: Apply SMOTE, class weights, or sampling
   - Large datasets: Batch training, incremental learning
   - Feature scaling: Apply transformations in pipeline
   - Categorical encoding: One-hot, label, target encoding

5. **Training Monitoring**
   - Track training time
   - Monitor memory usage
   - Display progress bars
   - Alert on errors or warnings

6. **Model Persistence**
   - Save trained models (pickle, joblib, native format)
   - Save preprocessing pipelines
   - Version control for models
   - Easy model loading for inference

## Usage Examples

### Example 1: Simple Classification
```python
# User provides:
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=100, random_state=42)

# Agent executes:
results = train_model(
    model=model,
    X=X_data,
    y=y_target,
    test_size=0.2,
    validation_size=0.1,
    stratify=True
)

# Output:
# ✓ Data split: 70% train (7,000), 10% validation (1,000), 20% test (2,000)
# ✓ Stratification applied (class balance maintained)
# ✓ Training RandomForestClassifier...
#   [Progress bar] 100% complete
# ✓ Training completed in 12.3 seconds
# 
# Training Performance:
#   Accuracy: 0.89
#   Precision: 0.87
#   Recall: 0.91
# 
# Validation Performance:
#   Accuracy: 0.86
#   Precision: 0.84
#   Recall: 0.88
# 
# ✓ Model saved to: models/random_forest_20240115_103045.pkl
```

### Example 2: Cross-Validation Training
```python
# User requests:
results = train_with_cv(
    model=model,
    X=X_data,
    y=y_target,
    cv=5,
    scoring='f1'
)

# Output:
# ✓ 5-fold cross-validation
# 
# Fold 1: F1 = 0.87 (completed in 2.3s)
# Fold 2: F1 = 0.89 (completed in 2.1s)
# Fold 3: F1 = 0.85 (completed in 2.4s)
# Fold 4: F1 = 0.88 (completed in 2.2s)
# Fold 5: F1 = 0.86 (completed in 2.3s)
# 
# Mean F1: 0.87 ± 0.02
# 
# ✓ Final model trained on full training set
# ✓ Model saved
```

### Example 3: Imbalanced Data Handling
```python
# Agent detects imbalance and suggests:
results = train_model(
    model=model,
    X=X_data,
    y=y_target,
    handle_imbalance='smote'  # or 'class_weight', 'undersample', 'oversample'
)

# Output:
# ⚠️ Class imbalance detected: 
#   Class 0: 9,000 samples (90%)
#   Class 1: 1,000 samples (10%)
# 
# ✓ Applying SMOTE to balance classes...
#   Synthetic samples created for minority class
#   New distribution: 9,000 vs 9,000
# 
# ✓ Training with balanced data...
# [Continues with training]
```

## Input Requirements
- **Required**: 
  - Model instance (sklearn-compatible or specific framework)
  - Features (X)
  - Target (y)
- **Optional**:
  - Train/validation/test split ratios
  - Cross-validation strategy
  - Imbalance handling method
  - Random seed

## Output Format
- Training results summary
- Validation metrics
- Trained model object
- Training history (for iterative models)
- Model file path

## Configuration Options
```yaml
test_size: 0.2
validation_size: 0.1
stratify: true  # For classification
shuffle: true
random_state: 42
cross_validation:
  enabled: false
  folds: 5
  strategy: "stratified"  # kfold, stratified, timeseries
imbalance_handling:
  auto_detect: true
  method: "class_weight"  # smote, undersample, oversample, class_weight
early_stopping:
  enabled: true  # For gradient boosting models
  rounds: 50
save_model: true
save_path: "models/"
verbose: 1
```

## Integration Points
- Receives model from Algorithm Recommender or user selection
- Uses data from Feature Engineering pipeline
- Feeds results to Model Evaluator
- Connects to Experiment Tracker for logging

## Success Metrics
- Successful training completion rate
- Proper handling of edge cases
- Time to train vs manual setup
- Reproducibility of results

## Implementation Notes
- Wrap scikit-learn's train_test_split with smart defaults
- Implement proper pipeline to prevent data leakage
- Use joblib for efficient model saving
- Support GPU acceleration when available
- Implement checkpoint saving for long training runs

## Edge Cases & Limitations
- **Very small datasets**: Warn about split sizes, suggest Leave-One-Out CV
- **Large models**: Implement batch training, show progress
- **Memory constraints**: Suggest data sampling or incremental learning
- **Categorical features**: Ensure proper encoding before training
- **Time series**: Use time-based splits, not random

## Future Enhancements
- Distributed training for large datasets
- Auto-retry with different random seeds
- Learning curve generation
- Automated feature scaling detection and application
- Integration with MLflow, Weights & Biases
- Hyperparameter tracking across training runs
- Model checkpointing and resume capability
