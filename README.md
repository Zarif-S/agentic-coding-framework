# Strategic Agentic Coding: Planning and Context Efficiency Framework

This repo outlines an approach to coding in the era of AI agents. It maximizes the value of strategic decisions and maintains clear documentation for optimal context efficiency when working with AI coding assistants.

This framework encourages building with a product and project focused mindset from the outset, ensuring technical decisions align with strategic goals.

---

## Why This Framework Exists

**The Problem**: AI coding agents require context to work effectively. Traditional documentation approaches either:
- Provide too much context (overwhelming, slow to parse)
- Provide too little context (agents make wrong assumptions)
- Lack strategic clarity (agents can't align with long-term vision)
- Force agents to rebuild context from scratch on every interaction

**The Solution**: A hierarchical documentation system that enables rapid context rebuilding at any altitude:

1. **Multi-level context access**: Agents can quickly rebuild context from either:
   - **Higher level** (strategic): "Why are we building this? What's the vision?" → ROADMAP.md
   - **Lower level** (implementation): "How does this module work? What patterns do we use?" → CLAUDE.md

2. **Right-sized context**: Agents find exactly what they need in <30 seconds, at the right level of detail

3. **Strategic alignment**: Clear separation between vision (ROADMAP) and execution (PROJECT_PLAN) ensures agents understand both what to build and why

4. **Zero workflow interruption**: Documentation helps rather than hinders development, supporting seamless context switching

---

## Success Criteria

This framework is working when:
- ✅ Developers find the correct documentation in **under 30 seconds** from any entry point
- ✅ AI agents receive **exactly the context they need** without excess
- ✅ Documentation updates cause **zero workflow interruption**
- ✅ Strategic decisions are **preserved and discoverable** months later

---

## Framework Overview

### Core Documentation Hierarchy (Tier 1)

```
your-project/
├── README.md                    # Public-facing overview
├── CLAUDE.md                    # 🎯 Main entry point for AI agents
├── ROADMAP.md                   # Strategic vision (quarters/years)
├── PROJECT_PLAN.md              # Tactical execution (weeks/months)
├── CHANGELOG.md                 # Feature and change history
├── CONTRIBUTING.md              # Contributor guidelines
│
└── src/
    └── your-module/
        └── CLAUDE.md            # Module-specific architecture & patterns
```

### What Goes Where?

| Content Type | Root CLAUDE.md | Subfolder CLAUDE.md | Code Comments |
|--------------|----------------|---------------------|---------------|
| Setup & installation | ✓ Primary | | |
| High-level architecture | ✓ Overview | Detailed design | |
| Design patterns | Mention | Explain + examples | Reference |
| API contracts | Link | Full specification | Implementation notes |
| Why decisions made | Strategic context | Technical rationale | Edge cases |
| How to extend | General guidance | Specific steps | Implementation details |

### Document Purposes

| Document | Timeframe | Purpose | Example Content |
|----------|-----------|---------|-----------------|
| **ROADMAP.md** | Quarters/Years | Strategic vision - the "destination" | "Q2 2024: Multi-tenancy support" |
| **PROJECT_PLAN.md** | Weeks/Months | Tactical execution - the "route" | "Sprint 3: Implement OAuth middleware" |
| **CLAUDE.md** (root) | Always current | Navigation hub + setup | Task routing, env setup, common commands |
| **CLAUDE.md** (subfolder) | Always current | Architecture + patterns | Component design, integration guides |
| **CHANGELOG.md** | Historical | Feature history | "v2.1.0: Added rate limiting" |

---

## Quick Start

### 1. Copy Template Files to Your Project

```bash
# Clone this template
git clone https://github.com/your-username/agentic-coding-framework.git

# Copy core files to your project
cp agentic-coding-framework/CLAUDE.md your-project/
cp agentic-coding-framework/ROADMAP.md your-project/
cp agentic-coding-framework/PROJECT_PLAN.md your-project/
cp agentic-coding-framework/CHANGELOG.md your-project/

# Copy example subfolder CLAUDE.md
cp agentic-coding-framework/examples/ml-workflow/CLAUDE.md your-project/src/your-module/
```

### 2. Customize for Your Project

1. **Edit `CLAUDE.md`**: Replace placeholder content with your project structure, setup steps, and task navigation
2. **Edit `ROADMAP.md`**: Add your strategic goals and milestones
3. **Edit `PROJECT_PLAN.md`**: Add current sprint/iteration plans
4. **Edit `CHANGELOG.md`**: Document your first version

### 3. Start Using with AI Agents

When working with Claude Code or other AI assistants:
- Point them to `CLAUDE.md` as the main entry point
- Reference specific sections for focused context
- Update docs as you make changes (see `PROJECT_PLAN.md` for documentation debt tracking)

---

## Advanced Features (Tier 2)

Once you're comfortable with the core framework, explore these optional patterns:

### 1. DOCS.md Index Pattern
**When to use**: Projects with 10+ documented folders
- Creates an ASCII navigation tree
- Quick reference for complex codebases
- See: [docs/ADVANCED_FEATURES.md#docs-index](docs/ADVANCED_FEATURES.md#docs-index)

### 2. PR Documentation Checklist
**When to use**: Team collaboration starts
- Automated reminders to update docs in PRs
- Reduces documentation drift
- See: [.github/PULL_REQUEST_TEMPLATE/documentation.md](.github/PULL_REQUEST_TEMPLATE/documentation.md)

### 3. Documentation Debt Tracking
**When to use**: Fast iteration creates doc gaps
- Track TODOs in `PROJECT_PLAN.md`
- Prioritize doc updates alongside features
- See: [docs/ADVANCED_FEATURES.md#doc-debt-tracking](docs/ADVANCED_FEATURES.md#doc-debt-tracking)

### 4. Conflict Detection Patterns
**When to use**: Multiple people editing docs
- Severity levels (🔴 Critical, 🟡 Moderate, 🟢 Minor)
- Manual checklist for spotting contradictions
- See: [docs/ADVANCED_FEATURES.md#conflict-detection](docs/ADVANCED_FEATURES.md#conflict-detection)

### 5. Multi-Folder Strategy Guide
**When to use**: Project structure evolves
- Heuristics for when to split CLAUDE.md into subfolders
- Examples of folder size thresholds
- See: [docs/ADVANCED_FEATURES.md#multi-folder-strategy](docs/ADVANCED_FEATURES.md#multi-folder-strategy)

### 6. Scheduled Retrospectives
**When to use**: Continuous improvement culture
- Every 2-3 months review template
- Questions about doc effectiveness
- See: [docs/ADVANCED_FEATURES.md#retrospectives](docs/ADVANCED_FEATURES.md#retrospectives)

---

## Real-World Example

See the `examples/ml-workflow/` folder for a minimal working example showing:
- Task-based navigation in root `CLAUDE.md`
- Subfolder `CLAUDE.md` for a data science/ML module
- Breadcrumb navigation between docs
- Strategic vs tactical separation (ROADMAP vs PROJECT_PLAN)

---

## Philosophy & Principles

### 1. Hierarchical Separation of Concerns
Documentation exists at different altitudes:
- **Strategic (ROADMAP)**: Where are we going and why?
- **Tactical (PROJECT_PLAN)**: What are we doing right now?
- **Architectural (CLAUDE.md)**: How does the system work?
- **Implementation (Code)**: What does this specific function do?

### 2. Flexible Guidelines, Not Rigid Rules
The "What Goes Where" table is a guide, not a law. Use your judgment:
- If repetition aids clarity, repeat
- If a detail feels important at multiple levels, include it at both
- Optimize for **findability**, not purity

### 3. Context Efficiency Over Completeness
AI agents work best with:
- **Focused context**: 2-5KB of targeted docs beats 50KB of comprehensive docs
- **Task-oriented navigation**: "What are you trying to do?" not "Here's everything"
- **Breadcrumbs**: Clear paths between related documents

### 4. No Workflow Interruption
Documentation should:
- ✅ Be updated **after** completing a task (batch at task end)
- ✅ Use severity levels for conflicts (only critical ones interrupt)
- ❌ **Never** pause development mid-task for doc updates
- ❌ **Never** enforce strict rules that slow down iteration

---

## Contributing

This framework is designed to evolve based on real-world usage. Contributions welcome:
- Share your adaptations and improvements
- Report what works (and what doesn't) in your projects
- Suggest new advanced patterns based on your experience

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## License

MIT License - see [LICENSE](LICENSE) file for details.

Use this framework freely in your projects, commercial or personal.

---

## Future Improvements

This framework is designed to evolve. Potential enhancements being considered:

### 1. Specialized Sub-Agents Support

**Concept**: Documentation patterns for teams using different LLMs for different purposes

**Examples**:
- Gemini for code reviews
- Claude Code for coding and implementation
- OpenAI for brainstorming and ideation
- Specialized models for data science workflows

**Value**: Guide teams on how to document when different AI agents handle different aspects of development

### 2. Compound Engineering Integration

**Resource**: [Compound Engineering Plugin](https://github.com/EveryInc/compound-engineering-plugin)

**Concept**: Integrate compound engineering principles into the documentation framework

**Value**: Enhanced patterns for building complex systems with clear documentation boundaries

### 3. Automation Tooling

**Validation Script** (`scripts/check_docs.sh`):
- Detect broken internal links
- Find inconsistent terminology
- Verify hierarchical structure
- Check documentation debt items

**GitHub Actions Workflow**:
- Automated doc checks on pull requests
- Link validation in CI/CD
- Documentation coverage reporting

**Pre-commit Hooks**:
- Remind developers to update relevant docs
- Validate markdown formatting
- Check for placeholder text

**Status**: Focus is on establishing manual patterns first, then automate when pain points are clear.

### 4. Model Context Protocol (MCP) Integration

**Concept**: Integrate Model Context Protocol to enable AI agents to access contextual information more efficiently

**Potential Features**:
- MCP servers for documentation navigation
- Context-aware documentation retrieval
- Standardized interfaces for AI agents to query project structure
- Dynamic context loading based on agent tasks

**Value**: Reduces token usage and improves AI agent performance by providing only relevant context when needed

### 5. Claude Skills Integration

**Concept**: Develop custom Claude skills that understand and leverage this documentation framework

**Potential Skills**:
- `/docs-search` - Intelligent search across hierarchical documentation
- `/update-roadmap` - Guided roadmap updates with validation
- `/plan-feature` - Feature planning that auto-generates PROJECT_PLAN entries
- `/sync-docs` - Detect and fix documentation inconsistencies

**Value**: Seamless workflow for maintaining and using the documentation framework within Claude Code

### 6. Framework Plugin/Extension

**Concept**: Create a standalone plugin that scaffolds and maintains this documentation structure

**Features**:
- One-command project initialization with templates
- Automatic detection of documentation drift
- Interactive documentation update wizard
- Integration with popular IDEs and editors
- Documentation health metrics and dashboards

**Value**: Lower barrier to entry and easier maintenance for teams adopting the framework

---

## Acknowledgments

This framework emerged from practical experience using AI coding assistants for coding and optimising documentation during onboarding, particularly when using [Claude Code](https://claude.com/claude-code).

Inspired by the need to maintain clarity and strategic alignment in fast-moving AI-assisted development environments.

**Research**: The philosophy of this framework is supported by research from MIT, notably:
Meng, E. and Jackson, D. (2025). *What You See Is What It Does: A Structural Pattern for Legible Software*. Available at: https://arxiv.org/abs/2508.14511.

**Contributors**: Thanks to James Algers for contributing.

---

**Last Updated**: 2025-01-31
**Status**: Template v1.0 - Ready for use
**Feedback**: [GitHub Issues](https://github.com/your-username/agentic-coding-framework/issues)
