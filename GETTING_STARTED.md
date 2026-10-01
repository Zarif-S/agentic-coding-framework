# Getting Started

This guide walks you from zero to a working project structure in about 20 minutes. It assumes you're using Claude Code.

---

## 1. Set up your project

```bash
# Clone the framework
git clone https://github.com/Zarif-S/agentic-coding-framework.git

# Create your project
mkdir my-project && cd my-project
git init

# Copy the core templates
cp ../agentic-coding-framework/CLAUDE.md .
cp ../agentic-coding-framework/ROADMAP.md .
cp ../agentic-coding-framework/PROJECT_PLAN.md .
cp ../agentic-coding-framework/CHANGELOG.md .
cp ../agentic-coding-framework/SYNCHRONIZATIONS.md .
cp ../agentic-coding-framework/DECISIONS.md .
cp ../agentic-coding-framework/LESSONS_LEARNED.md .

# Copy the Claude skills
cp -r ../agentic-coding-framework/.claude .
```

Open the project in Claude Code:

```bash
claude .
```

---

## 2. Fill in the root docs

Before writing any code, spend 15 minutes on these two files:

**`CLAUDE.md`** — Claude loads this into every session, so leftover placeholders are noise it reads every time. Fill in:
- Project name, one-line description, and stack
- Setup, test, and lint commands
- **Conventions**: the rules you'd otherwise find yourself repeating. Where do parameters live? What does a finished plot (or prompt, or endpoint) look like? Replace the examples with your own; specific beats general.
- Delete any section you have nothing for yet rather than leaving placeholders.

**`ROADMAP.md`** — write one paragraph describing what you're building and why. Add your first goal. This takes 5 minutes and saves significant context-rebuilding later.

Leave `PROJECT_PLAN.md`, `CHANGELOG.md`, `DECISIONS.md`, `LESSONS_LEARNED.md`, and `SYNCHRONIZATIONS.md` as-is for now. They fill in as you work.

---

## 3. Design your concepts (before writing code)

This is the key step most people skip. Run:

```
/concept-spec
```

Claude will ask you for the concept name, purpose, state, actions, and invariants. For each major module or responsibility in your project, create one concept spec. Aim for 2–4 concepts to start.

**Not sure how to split your project into concepts?** Ask Claude:

> "I'm building [brief description]. What concepts should I define? Draft the state/actions/invariants for each — don't write any code yet."

Review what it proposes. Adjust until the boundaries feel right. Getting this wrong in a spec is a 5-minute fix; getting it wrong in code is a refactor.

---

## 4. Define cross-concept coordination

Once your concepts are specced, run:

```
/sync-flow
```

For every place where one concept's action should trigger another's, add a SYNC entry. This is your coordination map — written before any implementation exists.

If nothing in your project coordinates across concepts yet, skip this step and come back when it's needed.

---

## 5. Plan your first feature

```
/plan-feature
```

Describe the first thing you want to build. The skill will:
- Classify it as Now / Next / Later
- Show a triage of which docs need updating
- Write the PROJECT_PLAN.md entry for you

---

## 6. Implement

For anything non-trivial, start in plan mode (Shift+Tab) or ask Claude to state its assumptions first. Then hand off with tight, concept-scoped prompts:

> "Implement the `[Concept]` concept. Follow the spec in `[path]/CLAUDE.md` exactly. Do not import from any other concept. Write tests that verify the invariants."

Repeat for each concept independently. Once all concepts are implemented and tested:

> "Read `SYNCHRONIZATIONS.md`. Create `coordinator.py` with one function per SYNC entry. This is the only file allowed to import from multiple concepts."

Before calling each task done, run `/check-done`. When you and Claude choose between alternatives along the way, run `/decision` straight away.

---

## 7. Ongoing maintenance

| When | Run |
|------|-----|
| Chose between alternatives | `/decision` |
| Before calling a task done | `/check-done` |
| Agent made the same mistake twice | Add to `LESSONS_LEARNED.md` and a rule to CLAUDE.md Conventions |
| Before a release or at end of sprint | `/changelog-gen` |
| Something feels out of sync across docs | `/doc-health` |
| Adding a new module | `/concept-spec` |
| Planning the next feature | `/plan-feature` |
| New cross-concept flow emerges | `/sync-flow` |

---

## Example: Data Science / ML project

Here's how the workflow maps to a typical DS/ML project:

**Concepts to define first** (run `/concept-spec` for each):
- `DataPipeline` — ingestion, validation, preprocessing
- `Experiment` — training, evaluation, metric tracking
- `Deployment` — staging, promotion, rollback

**Synchronizations to define** (run `/sync-flow` for each):
- When `Experiment.evaluate` passes threshold → `Deployment.stage`
- When `Deployment.promote` fires → `Experiment.archive`

**Implementation order**:
1. `DataPipeline` — no dependencies, implement and test in isolation
2. `Experiment` — depends on `DataPipeline` output, but not its internals
3. `Deployment` — depends on `Experiment` output, but not its internals
4. `coordinator.py` — the only file that wires them together, driven by SYNCHRONIZATIONS.md

See `examples/` for a worked version of exactly this structure.

---

## What good looks like

After the first session you should have:
- [ ] Root `CLAUDE.md` with your project name, stack, commands, and Conventions filled in, and no placeholders left
- [ ] `ROADMAP.md` with at least one quarterly goal
- [ ] At least one concept `CLAUDE.md` with state/actions/invariants
- [ ] `PROJECT_PLAN.md` with your first feature in the Now section

That's enough context for Claude to rebuild a useful mental model of your project from scratch on any future session.

---

**Next**: [README.md](README.md) for the full framework philosophy · [docs/ADVANCED_FEATURES.md](docs/ADVANCED_FEATURES.md) for scaling patterns
