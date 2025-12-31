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

## 📍 Breadcrumbs

- **Looking for strategic goals?** → [ROADMAP.md](ROADMAP.md)
- **Looking for current work?** → [PROJECT_PLAN.md](PROJECT_PLAN.md)
- **Looking for feature history?** → [CHANGELOG.md](CHANGELOG.md)
- **Looking for advanced patterns?** → [docs/ADVANCED_FEATURES.md](docs/ADVANCED_FEATURES.md)

---

## Hierarchical Documentation Guide

**Where should information live?** Use this table as a flexible guideline:

| Content Type | Root CLAUDE.md | Subfolder CLAUDE.md | Code Comments |
|--------------|----------------|---------------------|---------------|
| **Setup & Installation** | ✓ Primary | Additional module setup | |
| **Environment Variables** | ✓ All variables | Module-specific vars | |
| **High-level Architecture** | ✓ Overview + diagram | Detailed component design | |
| **Design Patterns** | Mention + link | Explain + examples | Reference in code |
| **API Contracts** | Link to subfolder | Full specification | Implementation notes |
| **Why Decisions Made** | Strategic context | Technical rationale | Edge case explanations |
| **How to Extend** | General guidance | Step-by-step instructions | Implementation details |
| **Common Commands** | ✓ Frequent commands | Module-specific commands | |
| **Testing Strategy** | Overview + structure | Component test patterns | Test case explanations |

**Guiding Principle**: Optimize for **findability** and **context efficiency**, not rigid rules. If repetition aids clarity, repeat it.

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

### [Task Category 1 - e.g., Adding a New Feature]

**Example: Adding a new API endpoint**

1. **Create the endpoint** in `[folder]/[file]`
2. **Add validation** using `[validation library/pattern]`
3. **Write tests** in `tests/[category]/test_[feature].py`
4. **Update documentation**:
   - If it affects architecture, update relevant `CLAUDE.md`
   - If it's a new feature, add to `CHANGELOG.md`
   - If it changes the roadmap, update `ROADMAP.md`
5. **Run tests** to ensure nothing breaks

### [Task Category 2 - e.g., Database Operations]

**Example: Adding a new database model**

1. **Create model** in `[models folder]/[model_name].py`
2. **Create migration**: `[migration command]`
3. **Run migration**: `[migration run command]`
4. **Update tests** if schema changes affect existing tests

### [Task Category 3 - e.g., Working with External APIs]

**Example: Integrating a new external service**

1. **Add API client** to `[services folder]/[service_name].py`
2. **Add environment variables** to `.env` and `.env.example`
3. **Implement rate limiting** (see `[example file]` for pattern)
4. **Add error handling** for API failures
5. **Write integration tests** in `tests/integration/`

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

### ✅ RESOLVED: [Issue Title]
**Issue**: [Description of the problem]
**Solution**: [How it was fixed]
**Location**: `[file:line]` or `[configuration]`

### 🔄 IN PROGRESS: [Issue Title]
**Issue**: [Description of the problem]
**Current Status**: [What's being done about it]
**Tracking**: [Link to GitHub issue or PROJECT_PLAN.md section]

### ⚠️ KNOWN LIMITATION: [Issue Title]
**Issue**: [Description of the limitation]
**Workaround**: [How to work around it]
**Future**: [Plans to address it, link to ROADMAP.md if applicable]

---

## Best Practices

### [Category 1 - e.g., Code Organization]

1. **[Practice 1]**: [Description and rationale]
2. **[Practice 2]**: [Description and rationale]
3. **[Practice 3]**: [Description and rationale]

### [Category 2 - e.g., Error Handling]

1. **[Practice 1]**: [Description]
   ```[language]
   [code example]
   ```
2. **[Practice 2]**: [Description]

### [Category 3 - e.g., Performance]

1. **[Practice 1]**: [Description and when to use]
2. **[Practice 2]**: [Description and when to use]

---

## Quick Reference Commands

```bash
# Development
[command]                    # [Description]
[command]                    # [Description]

# Testing
[command]                    # [Description]
[command]                    # [Description]

# Database
[command]                    # [Description]
[command]                    # [Description]

# Deployment
[command]                    # [Description]
[command]                    # [Description]

# Utilities
[command]                    # [Description]
[command]                    # [Description]
```

---

## Additional Resources

### Internal Documentation
- **[ROADMAP.md](ROADMAP.md)**: Strategic vision and quarterly goals
- **[PROJECT_PLAN.md](PROJECT_PLAN.md)**: Current sprint/iteration plans
- **[CHANGELOG.md](CHANGELOG.md)**: Detailed feature and change history
- **[docs/ADVANCED_FEATURES.md](docs/ADVANCED_FEATURES.md)**: Optional documentation patterns

### Module-Specific Documentation
- **[Module 1]**: `[path/to/module/CLAUDE.md]` - [Brief description]
- **[Module 2]**: `[path/to/module/CLAUDE.md]` - [Brief description]

### External Resources
- **[Resource 1]**: [Link and description]
- **[Resource 2]**: [Link and description]

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
