# ML Workflow Module - Data Science Documentation Example

## 📍 Breadcrumbs

- **New to the project?** → [Root CLAUDE.md](../../CLAUDE.md) for setup and overview
- **Looking for strategic context?** → [ROADMAP.md](../../ROADMAP.md)
- **Looking for current sprint work?** → [PROJECT_PLAN.md](../../PROJECT_PLAN.md)
- **Looking for other modules?** → [Root CLAUDE.md - Documentation Navigation](../../CLAUDE.md#-documentation-navigation)

---

## When to Read This Doc

**Read this document when**:
- Building or modifying ML pipelines or experiments
- Understanding data processing workflows
- Adding new features or models
- Tracking experiments and model performance

**Skip this document if**:
- You just need to set up the project → See [root CLAUDE.md](../../CLAUDE.md)
- You're working on infrastructure/deployment → See `[deployment/CLAUDE.md]`

---

## Module Overview

**Purpose**: The ML workflow module handles the end-to-end machine learning pipeline from raw data to trained models.

**Key Responsibilities**:
- Data ingestion and preprocessing
- Feature engineering and transformation
- Model training and evaluation
- Experiment tracking and reproducibility

**Not Responsible For**:
- Data storage infrastructure (see `[storage/CLAUDE.md]`)
- Model serving/deployment (see `[deployment/CLAUDE.md]`)
- Data visualization dashboards (see `[dashboards/CLAUDE.md]`)

---

## Architecture

### Workflow Overview

```
Raw Data
    ↓
┌────────────────────────────────────────────────┐
│ 1. Data Ingestion & Validation                 │
│    • Load from sources (CSV, database, API)    │
│    • Schema & data quality validation          │
│    • See: Testing Strategy > Data Validation   │
└────────────────────────────────────────────────┘
    ↓
┌────────────────────────────────────────────────┐
│ 2. Preprocessing                               │
│    • Handle missing values                     │
│    • Normalize/standardize                     │
│    • Train/test split                          │
└────────────────────────────────────────────────┘
    ↓
┌────────────────────────────────────────────────┐
│ 3. Feature Engineering                         │
│    • Create derived features                   │
│    • Feature selection                         │
│    • Encoding categorical variables            │
└────────────────────────────────────────────────┘
    ↓
┌────────────────────────────────────────────────┐
│ 4. Model Training                              │
│    • Initialize model                          │
│    • Train with hyperparameters                │
│    • Log metrics and artifacts                 │
└────────────────────────────────────────────────┘
    ↓
┌────────────────────────────────────────────────┐
│ 5. Evaluation                                  │
│    • Test set performance                      │
│    • Generate evaluation reports               │
│    • Compare with baseline                     │
└────────────────────────────────────────────────┘
    ↓
Trained Model + Metrics
```

---

## Design Patterns

### 1. Configuration-Driven Pipelines

**Why**: Separate code from configuration for reproducibility and easy experimentation.

**Example**:
```yaml
# config/experiment.yaml
data:
  source: "data/raw/dataset.csv"
  test_split: 0.2

preprocessing:
  handle_missing: "mean"
  normalize: true

features:
  - feature_1
  - feature_2
  - derived_ratio

model:
  type: "random_forest"
  hyperparameters:
    n_estimators: 100
    max_depth: 10
```

**Benefits**: Version control experiments, easy parameter sweeps, reproducible results.

### 2. Experiment Tracking

**Why**: Track experiments, compare results, and ensure reproducibility.

**Tools**: MLflow, ZenML, or custom logging

**Example workflow**:
```python
# Using MLflow for experiment tracking
import mlflow

with mlflow.start_run(run_name="rf_experiment_1"):
    # Log parameters
    mlflow.log_param("n_estimators", 100)
    mlflow.log_param("max_depth", 10)

    # Train model
    model = train_model(X_train, y_train)

    # Log metrics
    mlflow.log_metric("accuracy", accuracy)
    mlflow.log_metric("f1_score", f1)

    # Log model
    mlflow.sklearn.log_model(model, "model")
```

### 3. Data Versioning

**Why**: Track data changes alongside code for full reproducibility.

**Pattern**: Store data hashes or version identifiers with each experiment

**Example**:
```python
import pandas as pd
import hashlib

# Load and version data
df = pd.read_csv("data/dataset.csv")
data_hash = hashlib.md5(pd.util.hash_pandas_object(df).values).hexdigest()

# Log with experiment
mlflow.log_param("data_version", data_hash[:8])
```

---

## Common Tasks

### Adding a New Data Source

1. **Create data loader** in `data/loaders/[source_name].py`
2. **Add to configuration** in `config/data_sources.yaml`
3. **Write data validation** to check schema and types
4. **Update documentation** if pipeline architecture changes

### Adding a New Feature

1. **Define transformation** in `features/transformers.py`
2. **Add to feature list** in experiment configuration
3. **Validate feature** on sample data
4. **Run experiment** to evaluate impact on model performance

### Running a New Experiment

1. **Create experiment config** in `config/experiments/`
2. **Run training**: `python train.py --config experiments/my_experiment.yaml`
3. **Check results**: Review MLflow/ZenML UI for metrics
4. **Compare with baseline**: Analyze metric improvements

### Tracking and Comparing Experiments

**Using MLflow**:
```bash
# View all experiments
mlflow ui

# Compare specific runs
mlflow ui --backend-store-uri ./mlruns
```

**Key metrics to track**:
- Model performance (accuracy, F1, AUC, etc.)
- Training time
- Hyperparameters used
- Data version

---

## Testing Strategy

### Data Validation

**Purpose**: Ensure data quality before training

**Tools**: pandas, great_expectations

**Example**:
```python
def validate_data(df):
    # Check for required columns
    assert all(col in df.columns for col in required_cols)

    # Check data types
    assert df['numeric_col'].dtype in [int, float]

    # Check value ranges
    assert df['age'].between(0, 120).all()
```

### Model Evaluation

**Purpose**: Validate model performance on test set

**Metrics**:
- Classification: accuracy, precision, recall, F1, AUC-ROC
- Regression: MSE, RMSE, MAE, R²

**Example**:
```python
from sklearn.metrics import accuracy_score, f1_score

y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred, average='weighted')

print(f"Test Accuracy: {accuracy:.3f}")
print(f"Test F1 Score: {f1:.3f}")
```

---

## Additional Resources

### Internal Documentation
- **[Root CLAUDE.md](../../CLAUDE.md)**: Project setup and overview
- **[ROADMAP.md](../../ROADMAP.md)**: Strategic vision for ML development
- **[PROJECT_PLAN.md](../../PROJECT_PLAN.md)**: Current sprint and experiments

### External Resources
- **pandas**: https://pandas.pydata.org/docs/
- **scikit-learn**: https://scikit-learn.org/
- **PyTorch**: https://pytorch.org/docs/
- **MLflow**: https://mlflow.org/docs/
- **ZenML**: https://docs.zenml.io/

---

**Last Updated**: [YYYY-MM-DD]
**Status**: [e.g., "Active development", "Production ready"]
**Maintainer**: [Name or team]

---

**Related Documentation**:
- [Root CLAUDE.md](../../CLAUDE.md) - Project overview and setup
- [ROADMAP.md](../../ROADMAP.md) - Strategic vision
- [PROJECT_PLAN.md](../../PROJECT_PLAN.md) - Current sprint work
