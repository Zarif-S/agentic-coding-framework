# Strategic Agentic Coding: A Documentation Framework for AI Agents

A template you copy into a new project at the start, so the coding agent knows the goals, the conventions and the reasons behind past decisions before the work is scoped.

This framework encourages building with a product and project focused mindset from the outset, ensuring technical decisions align with strategic goals.

---

## Why This Framework Exists

**The Problem**: Current agents read code quickly, but code doesn't say why it exists or what "done" means. Without that, agents:
- Make reasonable-looking guesses that contradict earlier decisions
- Miss project conventions nobody wrote down (plots without legends, parameters hardcoded in notebooks)
- Lose the reasoning behind choices once plans are rewritten
- Can't align their work with the long-term vision

**The Solution**: Document what code can't say, each kind of thing in one place:

1. **Intent at two levels**:
   - **Strategic**: "Why are we building this? What's the vision?" → ROADMAP.md and PROJECT_PLAN.md
   - **Implementation**: "How does this module work? What conventions apply?" → CLAUDE.md

2. **Conventions and a Definition of Done**: Specific, checkable rules in CLAUDE.md, checked with `/check-done` before a task is reported finished

3. **One home for decisions**: Reasons and rejected options go in DECISIONS.md, so they survive when plans change

4. **Lessons that become rules**: Mistakes go in LESSONS_LEARNED.md and are promoted to Conventions, so the agent doesn't repeat them

---

## Success Criteria

This framework is working when:
- ✅ The agent follows project conventions without being reminded
- ✅ The agent says what it did **not** verify, instead of reporting everything done
- ✅ Documentation updates have **minimal workflow disruption**
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
├── DECISIONS.md                 # Why we chose X over Y (ADRs)
├── LESSONS_LEARNED.md           # What went wrong and what we do now
├── SYNCHRONIZATIONS.md          # Cross-concept event flows
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
| Why decisions made | Link to ADR in DECISIONS.md | Link to ADR in DECISIONS.md | Edge cases |
| Conventions & Definition of Done | ✓ Primary | Module-specific additions | |
| How to extend | General guidance | Specific steps | Implementation details |

### Document Purposes

| Document | Timeframe | Purpose | Example Content |
|----------|-----------|---------|-----------------|
| **ROADMAP.md** | Quarters/Years | Strategic vision - the "destination" | "Q2 2024: Multi-tenancy support" |
| **PROJECT_PLAN.md** | Weeks/Months | Tactical execution - the "route" | "Sprint 3: Implement OAuth middleware" |
| **CLAUDE.md** (root) | Always current | Navigation hub + setup | Task routing, env setup, common commands |
| **CLAUDE.md** (subfolder) | Always current | Architecture + patterns | Component design, integration guides |
| **SYNCHRONIZATIONS.md** | Always current | Cross-concept event flows | "When user.delete fires → post.deleteAll follows" |
| **CHANGELOG.md** | Historical | *What* changed | "v2.1.0: Added rate limiting" |
| **DECISIONS.md** | Historical, append-only | *Why* we chose X over Y | "ADR-004: Batch predictions before real-time serving" |
| **LESSONS_LEARNED.md** | Historical, append-only | What experience taught us, and the rule it led to | "LL-002: Agent skipped legends → `save_figure()` helper" |

**Roadmap, plan, changelog, and decisions answer different questions.** The roadmap and plan look forward and get rewritten, so any "why" written there disappears as they change. The changelog records what happened but not the reasoning. DECISIONS.md is the one place the reasoning, including the options you rejected, is kept.

---

## Quick Start

> **New here?** See [GETTING_STARTED.md](GETTING_STARTED.md) for a step-by-step walkthrough including the skills workflow and a DS/ML project example.

### 1. Copy Template Files to Your Project

```bash
# Clone this template
git clone https://github.com/Zarif-S/agentic-coding-framework.git

# Copy core files to your project
cp agentic-coding-framework/CLAUDE.md your-project/
cp agentic-coding-framework/ROADMAP.md your-project/
cp agentic-coding-framework/PROJECT_PLAN.md your-project/
cp agentic-coding-framework/CHANGELOG.md your-project/
cp agentic-coding-framework/SYNCHRONIZATIONS.md your-project/
cp agentic-coding-framework/DECISIONS.md your-project/
cp agentic-coding-framework/LESSONS_LEARNED.md your-project/

# Copy example subfolder CLAUDE.md
cp agentic-coding-framework/examples/ml-workflow/CLAUDE.md your-project/src/your-module/
```

### 2. Customize for Your Project

1. **Edit `CLAUDE.md`**: Replace placeholders with your project's stack, commands, and Conventions. The Conventions and Definition of Done sections are what stop the agent missing details, so make them specific to your project
2. **Edit `ROADMAP.md`**: Add your strategic goals and milestones
3. **Edit `PROJECT_PLAN.md`**: Add current sprint/iteration plans
4. **Edit `CHANGELOG.md`**: Document your first version

### 3. Copy the Claude Skills (optional)

If you use Claude Code, copy the included skills into your project:

```bash
cp -r agentic-coding-framework/.claude your-project/
```

This gives you seven `/commands` that automate the most common framework tasks, plus `/teach`:

| Command | What it does |
|-------|-------------|
| `/concept-spec` | Guided wizard to generate a new concept `CLAUDE.md` |
| `/plan-feature` | Plans a feature, triages which docs need updating, and asks whether a decision needs recording |
| `/decision` | Appends an ADR to `DECISIONS.md` (options considered, decision, consequences) |
| `/check-done` | Checks the current diff against CLAUDE.md's Conventions and Definition of Done, including opening any changed figures |
| `/sync-flow` | Adds a new SYNC-NNN entry to `SYNCHRONIZATIONS.md` |
| `/changelog-gen` | Parses recent commits and drafts `CHANGELOG.md` entries |
| `/doc-health` | Scans all docs for broken links, stale dates, missing sections, leftover placeholders |
| `/teach` | Not a framework command: teaches you a topic over several sessions, keeping `MISSION.md`, `GLOSSARY.md` and learning records in the current directory. Run it in a separate folder, not your project root |

See [`.claude/commands/`](.claude/commands/) for the full command definitions.

### 4. Start Using with AI Agents

When working with Claude Code or other AI assistants:
- Point them to `CLAUDE.md` as the main entry point
- Reference specific sections for focused context
- Update docs as you make changes (see `PROJECT_PLAN.md` for documentation debt tracking)

---

## Working with AI Agents

The framework changes the *order of operations* for building with an agent, not just how things are documented. The key shift: **design your concepts before writing any code**. This gives the agent tight boundaries to work within and surfaces coordination decisions early — when they're cheap to change.

### The four-step workflow

**1. Define your concepts first**

Before touching code, ask the agent to draft the concepts your project needs:

> "I'm building a project that [brief description]. Using the concept spec format in `examples/ml-workflow/CLAUDE.md`, draft the concepts we need and their state/actions/invariants. Don't write any code yet."

Review what it proposes. Maybe two concepts collapse into one, or a concept is too thin to justify its own module. This conversation is fast — getting it wrong in a spec is a 5-minute fix; getting it wrong in code is a refactor.

**2. Write the specs and SYNCHRONIZATIONS.md**

Once you've agreed on concepts, ask the agent to create the subfolder CLAUDE.md files and populate SYNCHRONIZATIONS.md:

> "Create a CLAUDE.md for each concept using the format in `examples/ml-workflow/CLAUDE.md`. Then populate `SYNCHRONIZATIONS.md` with the cross-concept flows."

Review the sync entries. If a coordination feels wrong, fix the spec now. This is your coordination map before any implementation exists.

**3. Implement one concept at a time**

Scope each coding task strictly to one concept:

> "Implement the `[Concept]` concept. Follow the spec in `[path]/CLAUDE.md` exactly. Do not import from any other concept. Write unit tests that verify the invariants."

Repeat for each concept. Each task is self-contained — the agent has a tight spec and a clear rule about what it must not touch.

**4. Implement the coordinator last**

Once all concepts are implemented and tested in isolation:

> "Read `SYNCHRONIZATIONS.md`. Create `coordinator.py` with one function per SYNC entry. This is the only file allowed to import from multiple concepts."

The agent translates each SYNC entry directly into a function. If an entry is ambiguous, it surfaces now — not mid-implementation.

### The discipline that makes it work

Keep prompts scoped to one concept or one sync at a time. The instinct is to say "build the whole pipeline" — resist it. The framework only pays off if the agent operates within concept boundaries, and it will as long as your prompts respect them too.

### Keeping the agent careful

Agents tend to rush and miss small details: a plot without a legend, a parameter hardcoded in a notebook instead of config. This is mostly a missing-convention problem, not a speed problem. Without a stated rule, the agent does whatever is most common. In order of payoff:

1. **Write the convention down**, specifically, in CLAUDE.md's Conventions section. "No literals in notebook cells" works; "write clean code" doesn't.
2. **Plan before editing.** Use plan mode (Shift+Tab in Claude Code) for anything non-trivial, or start with: *"Before writing code, tell me your assumptions and where any new parameters will live."*
3. **Keep tasks small.** Details get dropped when one prompt asks for five things.
4. **Make it check its own output.** Run `/check-done` before calling a task finished. For plots, the agent must open the saved image; it can't see a missing legend otherwise.
5. **Review with fresh context.** Ask a subagent (or a new session) to review the diff against Conventions. Fresh eyes catch what the author missed.
6. **Escalate repeat misses**: first a LESSONS_LEARNED entry, then code that enforces the rule, then a hook. See [Advanced Features 7–8](docs/ADVANCED_FEATURES.md#7-enforcing-conventions-in-code).

### Recording decisions as you go

When you and the agent choose between alternatives (a library, a data format, where something lives), run `/decision` right then, while the context is in the conversation. Writing ADRs after the fact is how they end up never written.

### What this buys you

- **Smaller agent tasks**: Each prompt has a clear boundary. The agent isn't holding the whole system in context at once.
- **Invariants as a safety net**: The agent knows from the spec what must hold after each action. You don't have to restate constraints in every prompt.
- **Easier debugging**: If something breaks, the concept boundaries tell you exactly where to look.
- **Safe iteration**: Changing a threshold or adding a downstream effect means updating one SYNC entry and the coordinator — neither concept doc changes.

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

### 7. Enforcing Conventions in Code
**When to use**: The agent keeps missing the same detail despite a CLAUDE.md rule
- Example config and figure helpers that fail loudly
- See: [docs/ADVANCED_FEATURES.md#7-enforcing-conventions-in-code](docs/ADVANCED_FEATURES.md#7-enforcing-conventions-in-code)

### 8. Hooks
**When to use**: A rule needs to run every time, not when remembered
- Opt-in Stop and PostToolUse hook examples for Claude Code
- See: [docs/ADVANCED_FEATURES.md#8-hooks](docs/ADVANCED_FEATURES.md#8-hooks)

---

## Real-World Example

See the `examples/` folder for a two-concept worked example showing the full framework in action:

| File | What it demonstrates |
|------|----------------------|
| `examples/ml-workflow/CLAUDE.md` | Concept spec (state, actions, invariants) for a self-contained MLWorkflow concept |
| `examples/deployment/CLAUDE.md` | Concept spec for a self-contained Deployment concept |
| `examples/SYNCHRONIZATIONS.md` | How the two concepts coordinate — without either knowing about the other |

The SYNCHRONIZATIONS.md is the key file to read: it shows what a real sync entry looks like and explains *why* the coordination lives here instead of in either concept's doc.

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

### 3. Document What Code Can't Say
Agents read code quickly; they can't read your intent. Spend documentation on:
- **Why**: decisions and rejected alternatives (DECISIONS.md)
- **Rules**: conventions and the Definition of Done (CLAUDE.md)
- **Direction**: what we're doing now and next (PROJECT_PLAN.md)

Don't spend it on restating file structure or code the agent can read directly; that drifts out of date and a stale doc misleads more than a missing one. Root CLAUDE.md is loaded into every session, so every line in it should earn its place.

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

### 5. Claude Skills Integration ✅

**Shipped**: Seven Claude Code commands are included in `.claude/commands/` and ready to copy into any project. See the table in [Quick Start step 3](#3-copy-the-claude-skills-optional).

**Value**: Each command enforces framework conventions automatically: concepts stay isolated, decisions land in DECISIONS.md, sync entries stay in SYNCHRONIZATIONS.md, and work gets checked against the Definition of Done before it's called finished.

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

**Last Updated**: 2026-10-01
**Status**: Template v1.2 - Ready for use
**Feedback**: [GitHub Issues](https://github.com/Zarif-S/agentic-coding-framework/issues)
