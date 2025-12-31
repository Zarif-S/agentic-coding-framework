# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## 📍 Breadcrumbs

- **Looking for strategic vision?** → [ROADMAP.md](ROADMAP.md)
- **Looking for current sprint work?** → [PROJECT_PLAN.md](PROJECT_PLAN.md)
- **Looking for implementation details?** → [CLAUDE.md](CLAUDE.md)

---

## [Unreleased]

### Added
- [Feature/addition that has been implemented but not yet released]

### Changed
- [Change in existing functionality]

### Deprecated
- [Soon-to-be removed feature]

### Removed
- [Removed feature]

### Fixed
- [Bug fix]

### Security
- [Security improvement or fix]

---

## [1.0.0] - 2025-01-31

### Added
- Initial release with core ML pipeline
- Baseline XGBoost model achieving 0.85 F1 score on test set
- Feature engineering pipeline with 47 derived features
- MLflow experiment tracking integration
- Data validation framework using Great Expectations
- Documentation framework:
  - Root CLAUDE.md for project overview
  - ROADMAP.md for strategic planning
  - PROJECT_PLAN.md for tactical execution

### Changed
- N/A (initial release)

### Fixed
- N/A (initial release)

---

## [0.2.0] - 2025-01-15

### Added
- Model serving API with FastAPI and ONNX Runtime
- Automated data quality monitoring dashboard

### Changed
- Updated feature engineering pipeline to handle missing values more robustly
- Improved model training logging with detailed hyperparameter tracking

### Fixed
- Fixed memory leak in data preprocessing pipeline for large datasets
- Corrected feature scaling in production inference pipeline

### Deprecated
- Legacy CSV-based data loading (use Parquet format)

---

## [0.1.0] - 2025-01-01

### Added
- Initial project setup
- Basic data pipeline structure
- Exploratory data analysis notebooks
- Initial model training framework

---

## How to Use This Changelog

**Format**: Based on [Keep a Changelog](https://keepachangelog.com/) + [Semantic Versioning](https://semver.org/)

**When to update**:
- Releasing a new version: Move items from [Unreleased] to new version section
- Completing user-facing features, bug fixes, or breaking changes: Add to [Unreleased]
- Don't update for internal refactoring or minor cleanup

**Version numbering**:
- **Major (X.0.0)**: Breaking changes (e.g., removed model API, changed data format)
- **Minor (0.X.0)**: New features, backwards-compatible (e.g., new model, new pipeline)
- **Patch (0.0.X)**: Bug fixes, backwards-compatible (e.g., fixed inference bug)

---

## Template for New Entries

```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- [New feature or capability description]

### Changed
- [Change to existing functionality]
- **BREAKING**: [Note breaking changes clearly]

### Fixed
- [Bug fix description]
```

---

## Data Science Changelog Patterns

**Model Updates**: Document performance changes and version increments
```markdown
### Added
- Trained model v2.1 with transformer architecture (F1: 0.82 → 0.87)
- Deployed gradient boosting ensemble to production
```

**Dataset Changes**: Track data updates and quality fixes
```markdown
### Changed
- Updated training dataset with 10k new labeled samples (total: 100k)
- Fixed data quality issues in feature_x (affected 3% of records)
```

**Experiment Results**: Reference experiment tracking for reproducibility
```markdown
### Added
- Completed hyperparameter tuning (see MLflow run #234)
- A/B tested model v2.0 in production (5% traffic, +12% accuracy)
```

**Version Bumping for ML**:
- **Major**: Breaking changes to model API, data format, or feature schema
- **Minor**: New models, new features, pipeline improvements
- **Patch**: Bug fixes in inference, training, or data processing

---

**Last Updated**: 2025-01-31
**Current Version**: 1.0.0
