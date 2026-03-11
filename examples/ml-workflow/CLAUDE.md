# [Module Name] - [Your Project Name]

## Breadcrumbs
- **Project setup** → [Root CLAUDE.md](../../CLAUDE.md)
- **Strategic context** → [ROADMAP.md](../../ROADMAP.md)
- **Current sprint** → [PROJECT_PLAN.md](../../PROJECT_PLAN.md)
- **Cross-module flows** → [SYNCHRONIZATIONS.md](../SYNCHRONIZATIONS.md)

> **Isolation rule**: This file describes only what this concept owns. Any coordination with other concepts belongs in SYNCHRONIZATIONS.md — not here.

---

## Concept Specification

**Purpose**: [Single sentence — what user-facing need does this concept serve?]

### State

| Field | Type | Description |
|-------|------|-------------|
| `[field_name]` | `[type]` | [What it holds, who owns it] |
| `[field_name]` | `[type]` | [What it holds, who owns it] |

### Actions

| Action | Signature | Description |
|--------|-----------|-------------|
| `[action]` | `([args]) → [return]` | [What it does] |
| `[action]` | `([args]) → [return]` | [What it does] |

### Invariants

- [Property that must always hold, e.g. "every record must have a non-null id"]
- [Data quality or correctness guarantee, e.g. "output shape must match input shape"]
- [Boundary condition, e.g. "probability outputs must sum to 1.0"]

---

<!--
  EXAMPLE BELOW: Delete this section and replace with your module's content.
  The ML Workflow concept is shown as a concrete illustration of the format above.
-->

## Example: ML Workflow Concept Specification

**Purpose**: Transform raw data into trained, evaluated models ready for deployment.

### State

| Field | Type | Description |
|-------|------|-------------|
| `raw_data` | `DataFrame` | Immutable source data, never modified after ingestion |
| `processed_data` | `DataFrame` | Cleaned and split data owned by this concept |
| `feature_set` | `List[str]` | Active feature names for current experiment |
| `model` | `BaseEstimator` | Trained model artifact |
| `experiment_id` | `str` | MLflow/tracker run ID for current experiment |
| `metrics` | `Dict[str, float]` | Evaluation results keyed by metric name |

### Actions

| Action | Signature | Description |
|--------|-----------|-------------|
| `ingest` | `(source: Path, schema: Schema) → DataFrame` | Load and validate raw data against schema |
| `preprocess` | `(df: DataFrame, config: PrepConfig) → DataFrame` | Clean, split, normalize |
| `engineer_features` | `(df: DataFrame, feature_list: List[str]) → DataFrame` | Apply transformations, produce feature matrix |
| `train` | `(X: DataFrame, y: Series, config: TrainConfig) → Model` | Fit model, log to experiment tracker |
| `evaluate` | `(model: Model, X_test: DataFrame, y_test: Series) → Metrics` | Score on held-out data, return metrics dict |

### Invariants

- `raw_data` is never mutated after `ingest` completes
- `processed_data` train/test split is determined once and reused across all actions
- All actions within an experiment share the same `experiment_id`
- `metrics` keys are consistent across runs for the same model type
- Feature names in `feature_set` must all exist as columns in the processed DataFrame

---

## Architecture

```
Raw Data
    ↓
┌─────────────────────────────────────┐
│ ingest(source, schema)              │
│   • Load from source                │
│   • Validate schema & types         │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ preprocess(df, config)              │
│   • Handle missing values           │
│   • Normalize / standardize         │
│   • Train/test split                │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ engineer_features(df, feature_list) │
│   • Create derived features         │
│   • Encode categoricals             │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ train(X, y, config)                 │
│   • Fit model                       │
│   • Log params + artifacts          │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ evaluate(model, X_test, y_test)     │
│   • Score on held-out data          │
│   • Log metrics                     │
└─────────────────────────────────────┘
    ↓
Trained Model + Metrics
```

---

## Common Tasks

### Running a new experiment

1. Create config in `config/experiments/[name].yaml`
2. Run: `python train.py --config config/experiments/[name].yaml`
3. Review results in MLflow UI: `mlflow ui`

### Adding a new feature

1. Implement transformation in `features/transformers.py`
2. Add feature name to experiment config under `features:`
3. Validate on sample data before running full experiment

### Adding a new data source

1. Create loader in `data/loaders/[source].py`
2. Ensure it returns a DataFrame matching the expected schema
3. Register in `config/data_sources.yaml`

---

## Implementation Notes

### [Pattern/Decision Name]

**Issue**: [What problem does this solve?]

**Solution**: [Approach chosen and why]

**Location**: `[file:line]`

```python
# example
```

---

## Known Issues & Solutions

**[✅ RESOLVED | 🔄 IN PROGRESS | ⚠️ KNOWN LIMITATION]: [Title]**
- **Issue**: [Description]
- **Solution/Workaround**: [How it's handled]
- **Location**: `[file:line]`

---

**Last Updated**: [YYYY-MM-DD] | **Status**: [Active / Production] | **Maintainer**: [Name]
