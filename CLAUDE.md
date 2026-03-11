# Claude Code Configuration - [Your Project Name]

## Project Overview

**[Your Project Name]** is [brief 1-2 sentence description of what your project does].

### Key Technologies
- [Language/Runtime]: [e.g., Python 3.11, Node.js 18]
- [Database/Storage]: [e.g., PostgreSQL, S3]
- [Key Dependencies]: [e.g., FastAPI, React, PyTorch]

### Current Status
✅ [Completed milestone]
🔄 [In-progress milestone]
⏳ [Planned milestone]

---

## Documentation Navigation

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
│ [Module/component name]          → [path/to/module/CLAUDE.md] │
│ [Module/component name]          → [path/to/module/CLAUDE.md] │
└────────────────────────────────────────────────────────────────┘
```

**For AI agents**: Read this file first, then follow the navigation table above to find module-specific context. Check [PROJECT_PLAN.md](PROJECT_PLAN.md) for current priorities before implementing features.

---

## Environment Setup

```bash
# Clone and install
git clone [repository-url]
cd [project-name]
[pip install -r requirements.txt | npm install | ...]

# Environment variables
cp .env.example .env
# Fill in required variables (see below)

# [Any one-time setup steps]
[e.g., createdb myapp_dev && python manage.py migrate]
```

### Environment Variables

```bash
# Required
API_KEY=
DATABASE_URL=
[OTHER_REQUIRED_VAR]=

# Optional
DEBUG=false
LOG_LEVEL=info
```

---

## Project Structure

```
[project-name]/
├── [src/app/lib]/            # [Core logic]
│   ├── [module]/
│   │   └── CLAUDE.md         # Module-specific architecture guide
│   └── [module]/
├── tests/
├── scripts/                  # Automation and utilities
├── docs/
├── .env.example
├── CLAUDE.md                 # This file
├── ROADMAP.md
├── PROJECT_PLAN.md
└── CHANGELOG.md
```

---

## Common Tasks

### [Primary workflow - e.g., "Running the app"]

```bash
[dev command]     # Development mode → http://localhost:[port]
[test command]    # Run test suite
[build command]   # Production build
```

### [Secondary workflow - e.g., "Adding a new feature"]

1. [Step 1]
2. [Step 2]
3. [Step 3]

---

## Important Implementation Notes

Use this section to document non-obvious decisions and patterns as they emerge.

### [Pattern/Decision Name]

**Issue**: [What problem does this solve?]

**Solution**: [What approach was chosen and why?]

**Location**: `[file:line_number]`

**Example**:
```[language]
// example code snippet
```

---

## Known Issues & Solutions

**[✅ RESOLVED | 🔄 IN PROGRESS | ⚠️ KNOWN LIMITATION]: [Title]**
- **Issue**: [Description]
- **Solution/Workaround**: [How it's handled]
- **Location**: `[file:line]`

---

**Last Updated**: [YYYY-MM-DD] | **Status**: [Active development / Production] | **Maintainers**: [Names]

**Docs**: [ROADMAP.md](ROADMAP.md) · [PROJECT_PLAN.md](PROJECT_PLAN.md) · [CONTRIBUTING.md](CONTRIBUTING.md)
