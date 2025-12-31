# Claude Code Configuration - [Your Project Name]

## Project Overview

**[Your Project Name]** is [brief 1-2 sentence description of what your project does].

### Key Technologies
- [Language/Framework]: [e.g., Python 3.11, React 18, etc.]
- [Database]: [e.g., PostgreSQL, MongoDB, etc.]
- [Key Dependencies]: [e.g., FastAPI, Express, etc.]

### Current Status
✅ [Feature/milestone completed]
🔄 [Feature/milestone in progress]
⏳ [Feature/milestone planned]

---

## 📚 Documentation Navigation

This is your main entry point for AI-assisted development. Use this guide to find exactly what you need.

**What are you trying to do?**

```
┌────────────────────────────────────────────────────────────────┐
│ TASK                              → READ THIS FIRST            │
├────────────────────────────────────────────────────────────────┤
│ Setup project & install deps     → This file (below)          │
│ Understand strategic vision      → ROADMAP.md                 │
│ See current sprint/iteration     → PROJECT_PLAN.md            │
│ Review recent changes            → CHANGELOG.md               │
├────────────────────────────────────────────────────────────────┤
│ [Your module/component]          → [path/to/module/CLAUDE.md] │
│ [Another module/component]       → [path/to/module/CLAUDE.md] │
│ [Another module/component]       → [path/to/module/CLAUDE.md] │
└────────────────────────────────────────────────────────────────┘
```

### Advanced Navigation

For larger projects (10+ documented modules), consider creating a **DOCS.md** index file. See [docs/ADVANCED_FEATURES.md#docs-index](docs/ADVANCED_FEATURES.md#docs-index) for the pattern.

---

## For AI Agents

This file is your **entry point** for understanding the project:
- **Read this FIRST** before making code changes
- Use the navigation table above to find module-specific CLAUDE.md files
- Check [PROJECT_PLAN.md](PROJECT_PLAN.md) for current priorities before implementing features
- When you modify project structure, setup, or common workflows, **update this file**
- For data science projects: Pay attention to data paths, model artifacts, and compute requirements

---

## Documentation Hierarchy

**Where should information live?**

| Content Type | Root CLAUDE.md | Subfolder CLAUDE.md | Code Comments |
|--------------|----------------|---------------------|---------------|
| **Setup & Installation** | ✓ Primary | Module-specific setup | — |
| **Environment Variables** | ✓ All variables | Module-specific vars | — |
| **Architecture** | Overview + diagram | Detailed design | Implementation notes |
| **Design Patterns** | Mention + link | Explain + examples | Reference in code |
| **Why Decisions Made** | Strategic context | Technical rationale | Edge cases |
| **Common Tasks** | ✓ Frequent workflows | Module-specific workflows | — |

**Principle**: Optimize for **findability** and **context efficiency**. Repeat information if it aids clarity.

**Note**: Design patterns and decision rationale belong in "Important Implementation Notes" section below. See [docs/ADVANCED_FEATURES.md#hierarchical-docs](docs/ADVANCED_FEATURES.md) for extended guidance.

---

## Environment Setup

### Prerequisites

```bash
# [Language/Runtime]
[e.g., Python 3.11+, Node.js 18+, etc.]

# [Package Manager]
[e.g., pip, poetry, uv, npm, yarn, etc.]

# [Other Requirements]
[e.g., Docker, PostgreSQL, Redis, etc.]
```

### Installation

```bash
# Clone the repository
git clone [repository-url]
cd [project-name]

# Install dependencies
[e.g., pip install -r requirements.txt]
[e.g., npm install]

# Set up environment variables
cp .env.example .env
# Edit .env and add required variables (see below)

# [Database setup if needed]
[e.g., createdb myapp_dev]
[e.g., npm run migrate]

# [Run initial setup scripts if needed]
[e.g., python scripts/setup.py]
```

### Required Environment Variables

**Location**: `.env` file in project root

**Required Variables**:
```bash
# [Category 1 - e.g., API Keys]
API_KEY=your-key-here
SECRET_KEY=your-secret-here

# [Category 2 - e.g., Database]
DATABASE_URL=postgresql://user:pass@localhost/dbname

# [Category 3 - e.g., External Services]
REDIS_URL=redis://localhost:6379
```

**Optional Variables**:
```bash
# [Optional settings]
DEBUG=true
LOG_LEVEL=info
```

---

## Data Setup

### Data Storage Locations

**Local Development**:
```bash
data/
├── raw/              # Original, immutable data
├── interim/          # Intermediate processed data
├── processed/        # Final feature sets ready for modeling
└── external/         # External reference data
```

**Remote Storage**:
- **Training Data**: `[s3://bucket/path or gs://bucket/path]`
- **Model Artifacts**: `[s3://bucket/models or MLflow/W&B]`
- **Data Versioning**: [DVC, LakeFS, or version control method]

### Downloading Datasets

```bash
# [Method 1 - e.g., DVC]
dvc pull

# [Method 2 - e.g., Custom script]
python scripts/download_data.py --dataset [dataset_name]

# [Method 3 - e.g., Cloud storage]
aws s3 sync s3://bucket/path data/raw/
```

### Pre-trained Models

**Location**: `models/pretrained/` or `[remote path]`

**Download**:
```bash
# [Example command]
python scripts/download_models.py --model [model_name]
```

**Available Models**:
- **[Model 1]**: [Description, use case, size]
- **[Model 2]**: [Description, use case, size]

---

## Compute Environment

### Hardware Requirements

**Minimum**:
- CPU: [e.g., 4 cores]
- RAM: [e.g., 16GB]
- Storage: [e.g., 50GB]

**Recommended (for training)**:
- GPU: [e.g., NVIDIA GPU with 16GB+ VRAM (T4, V100, A100)]
- CUDA: [e.g., 11.8+]
- RAM: [e.g., 32GB+]
- Storage: [e.g., 100GB+ SSD]

### Cloud Setup

**Recommended Instances**:
- **Development**: [e.g., AWS p3.2xlarge, GCP n1-standard-4 with T4 GPU]
- **Training**: [e.g., AWS p3.8xlarge, GCP a2-highgpu-1g with A100]
- **Inference**: [e.g., AWS g4dn.xlarge, GCP n1-standard-2 with T4]

**Docker Image** (if applicable):
```bash
# Build
docker build -t [project-name]:[tag] .

# Run with GPU
docker run --gpus all -v $(pwd):/workspace [project-name]:[tag]
```

### Jupyter Notebooks

**Starting Jupyter**:
```bash
# Local
jupyter lab

# Remote with port forwarding
ssh -L 8888:localhost:8888 [remote-server]
jupyter lab --no-browser --port=8888
```

**Notebook Organization**:
- `notebooks/eda/`: Exploratory data analysis
- `notebooks/experiments/`: Model experiments and prototyping
- `notebooks/reports/`: Final reports and visualizations

**Execution Order**: See `notebooks/README.md` for recommended execution sequence

---

## Project Structure

```
your-project/
├── [folder]/                 # [Purpose - e.g., "Core application logic"]
│   ├── [subfolder]/          # [Purpose - e.g., "User authentication"]
│   │   └── CLAUDE.md         # 📄 Architecture guide for this module
│   └── [subfolder]/          # [Purpose]
│
├── [folder]/                 # [Purpose - e.g., "API endpoints"]
├── [folder]/                 # [Purpose - e.g., "Database models"]
├── [folder]/                 # [Purpose - e.g., "Utility functions"]
│
├── tests/                    # Test suite
│   ├── unit/                 # Unit tests
│   └── integration/          # Integration tests
│
├── scripts/                  # Automation scripts
├── docs/                     # Additional documentation
│
├── .env                      # Environment variables (not in git)
├── .env.example              # Environment variable template
├── README.md                 # Public-facing overview
├── CLAUDE.md                 # This file - AI agent entry point
├── ROADMAP.md                # Strategic vision (quarters/years)
├── PROJECT_PLAN.md           # Tactical execution (weeks/months)
├── CHANGELOG.md              # Feature and change history
├── CONTRIBUTING.md           # Contributor guidelines
└── [config files]            # [e.g., package.json, requirements.txt, etc.]
```

---

## Running the Project

### Development Mode

```bash
# Start the application in development mode
[e.g., python app.py]
[e.g., npm run dev]

# Application will be available at:
[e.g., http://localhost:3000]
```

### Running Tests

```bash
# Run all tests
[e.g., pytest]
[e.g., npm test]

# Run specific test suite
[e.g., pytest tests/unit/]
[e.g., npm run test:unit]

# Run with verbose output
[e.g., pytest -v]
[e.g., npm test -- --verbose]

# Run with coverage
[e.g., pytest --cov]
[e.g., npm run test:coverage]
```

### Building for Production

```bash
# Build production assets
[e.g., npm run build]

# Run production server
[e.g., gunicorn app:app]
[e.g., npm start]
```

---

## Common Tasks

### Training a Model

**Example: Running a new training experiment**

1. **Prepare dataset**: Ensure data is available (see [Data Setup](#data-setup))
2. **Configure experiment**: Update `configs/[model_config].yaml` with hyperparameters
3. **Run training**: `python train.py --config configs/[model_config].yaml`
4. **Track metrics**: Experiment automatically logs to [MLflow/W&B/Neptune]
5. **Save checkpoint**: Model artifacts saved to `models/[experiment_id]/`
6. **Update documentation**:
   - Add experiment results to `CHANGELOG.md` if significant
   - Update `ROADMAP.md` if this changes strategic direction

### Running Data Pipelines

**Example: Processing new data or updating features**

1. **Configure pipeline**: Update `pipelines/[pipeline_name].py` or config file
2. **Run locally**: `python pipelines/[pipeline_name].py --env dev`
3. **Verify output**: Check output in `data/processed/` or data warehouse
4. **Run tests**: `pytest tests/pipelines/test_[pipeline_name].py`
5. **Deploy to production**: [Deployment command or Airflow DAG]

### Adding New Features (to datasets)

**Example: Engineering a new feature for model input**

1. **Implement feature**: Add to `features/[feature_name].py`
2. **Add to pipeline**: Register in feature engineering pipeline
3. **Validate**: Check feature distributions in `notebooks/eda/[feature_name]_validation.ipynb`
4. **Backfill**: Run backfill for historical data if needed
5. **Update schema**: Document in `docs/data_dictionary.md` or feature store

### Updating Documentation

**When to update each document**:

- **ROADMAP.md**: When strategic goals change (quarterly review)
- **PROJECT_PLAN.md**: When completing major initiatives, or when current focus/blockers change (weekly/biweekly)
- **CLAUDE.md** (root): When project structure, setup, or common tasks change
- **CLAUDE.md** (subfolder): When module architecture or patterns change
- **CHANGELOG.md**: When releasing a new version or completing significant features

**Documentation Debt Tracking**: See [CONTRIBUTING.md#documentation-practices](CONTRIBUTING.md#documentation-practices) for how to track and manage documentation debt.

---

## Important Implementation Notes

### [Category 1 - e.g., API Rate Limiting]

**Issue**: [Describe the constraint or consideration]

**Solution**: [Describe the approach implemented]

**Location**: `[file path:line number]`

**Example**:
```[language]
[code example showing the pattern]
```

### [Category 2 - e.g., Caching Strategy]

**Issue**: [Describe the problem this solves]

**Solution**: [Describe the caching approach]

**Location**: `[file path:line number]`

**Usage**:
```[language]
[code example]
```

### [Category 3 - e.g., Authentication Flow]

**Overview**: [High-level description]

**Key Components**:
1. **[Component 1]**: [Purpose and location]
2. **[Component 2]**: [Purpose and location]
3. **[Component 3]**: [Purpose and location]

**See**: `[module/CLAUDE.md]` for detailed authentication architecture

---

## Known Issues & Solutions

Document issues as they arise using this format:

**[✅ RESOLVED | 🔄 IN PROGRESS | ⚠️ KNOWN LIMITATION]: [Issue Title]**
- **Issue**: [Description]
- **Solution/Workaround**: [How it's fixed or worked around]
- **Location**: `[file:line]` or [GitHub issue link]

---

## Best Practices

Document project-specific patterns and conventions as they emerge. Add entries when you establish a pattern worth following consistently.

### Example: Experiment Naming

**Pattern**: `[model-type]_[feature-set]_[YYYYMMDD]_[initials]`

**Rationale**: Enables sorting by date, filtering by model type, and identifying owner

```bash
# Good
bert_baseline_20250115_jd
xgboost_full_features_20250116_sm

# Avoid
experiment_1
final_model_v2
```

### Example: Data Validation

**Pattern**: Always validate data schema at pipeline boundaries

**Rationale**: Catches data drift early, prevents silent failures in training

```python
# Validate before training
schema.validate(df)  # Raises if schema mismatch
```

---

**Add your own practices here as the project evolves. Common categories**: Model versioning, code organization, error handling, testing patterns.

---

## Quick Reference Commands

```bash
# Development
[command]                              # [Description]

# Training & Experiments
[command]                              # [Description]

# Data Pipelines
[command]                              # [Description]

# Testing
[command]                              # [Description]
```

---

## Contributing

**For team members**: See [CONTRIBUTING.md](CONTRIBUTING.md) for development workflow and PR guidelines.

**For external contributors**: We welcome contributions! Please open an issue first to discuss proposed changes.

---

**Last Updated**: [YYYY-MM-DD]
**Status**: [e.g., "Active development", "Production ready", "Beta"]
**Maintainers**: [Names or links]

---

**Related Documentation**:
- [ROADMAP.md](ROADMAP.md) - Strategic vision
- [PROJECT_PLAN.md](PROJECT_PLAN.md) - Tactical execution
- [docs/ADVANCED_FEATURES.md](docs/ADVANCED_FEATURES.md) - Advanced patterns
