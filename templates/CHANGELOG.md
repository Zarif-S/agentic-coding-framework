# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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

<!--
  EXAMPLE of a released version. Not real project history; delete once you
  have your first release.

## [0.2.0] - YYYY-MM-DD

### Added
- Model serving API with FastAPI

### Changed
- Feature pipeline now handles missing values explicitly instead of dropping rows

### Fixed
- Corrected feature scaling in the inference pipeline

### Deprecated
- CSV-based data loading (use Parquet)
-->

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

**Last Updated**: [YYYY-MM-DD]
**Current Version**: [X.Y.Z]
