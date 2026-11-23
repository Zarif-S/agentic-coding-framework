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

# Copy the core templates (CLAUDE.md, ROADMAP.md, PROJECT_PLAN.md, CHANGELOG.md,
# DECISIONS.md, LESSONS_LEARNED.md, .env.example)
cp -r ../agentic-coding-framework/templates/. .

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

Leave `PROJECT_PLAN.md`, `CHANGELOG.md`, `DECISIONS.md` and `LESSONS_LEARNED.md` as-is for now. They fill in as you work.

### Conventions examples by project type

The template's Conventions are written for a data-science project. Pick the block closest to yours as a starting point, then rewrite it in your project's terms: real paths, real commands, the mistakes you've actually seen.

**RAG / LLM application**

```markdown
**Prompts & model settings**
- Prompts live in `prompts/*.md` and are loaded by name. No prompt text inline in code.
- Model name, temperature, max tokens, chunk size, chunk overlap and top-k live in `config/*.yaml`. No literals at call sites.
- All model calls go through `[src/app]/llm.py`, which logs the prompt name, model, token counts and latency.

**Evaluation**
- Any change to a prompt, the retriever, chunking or the model runs `[make eval]` and reports the score next to the last baseline in `evals/results.md`.
- Eval sets in `evals/` are versioned data. Never edit a case to make it pass; add a new case and say why.
- A retrieval answer cites the source chunk IDs it used.

**Secrets**
- API keys come from environment variables (`.env`, never committed). Never print or log them.
```

**Web app / API**

```markdown
**API**
- Request and response bodies are validated by schemas in `[src/app]/schemas/`. Handlers never read raw JSON.
- Errors return `{"error": {"code", "message"}}` with the right HTTP status. No stack traces in responses.
- Every new endpoint has a test that calls it over HTTP, including one failure case.

**Data**
- Database access goes through `[src/app]/repositories/`. No queries in handlers or templates.
- Schema changes are new migrations. Never edit a migration that has been applied anywhere.

**Frontend**
- Colours, spacing and type sizes come from design tokens in `[src/ui]/tokens`. No hex values or pixel sizes in components.
- Every interactive element is reachable by keyboard and has an accessible name.
```

---

## 3. Sketch the system (before writing code)

Ask Claude:

> "I'm building [brief description]. Draft 'The system' section of CLAUDE.md: a short sketch of how data flows through the project, and the rules a wrong change would break silently. Don't write any code yet."

Keep it to what the agent needs every session: the flow, plus rules such as "test labels are never changed". Getting it wrong here is a five-minute fix; getting it wrong in code is a refactor. For a small project, a few lines or nothing at all is fine.

**Later, as the project grows**: when one module has rules the agent keeps breaking, or the root CLAUDE.md fills up with one module's detail, run `/module-doc`. Claude Code loads a folder's CLAUDE.md only when working in that folder, so module rules cost nothing elsewhere.

---

## 4. Event-driven projects only: synchronizations

If modules react to each other's events (an app where deleting a user deletes their posts, or a deployment service that stages a model when evaluation passes), copy [examples/SYNCHRONIZATIONS.md](examples/SYNCHRONIZATIONS.md) to your project root, delete its example entries, and add one entry per reaction with `/sync-flow`.

A pipeline that runs its steps in order doesn't need this; the sketch from step 3 covers it. Skip this step unless your modules react to each other.

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

For anything non-trivial, start in plan mode (Shift+Tab) or ask Claude to state its assumptions first. Work one milestone at a time: plan, approve, build, then `/check-done` and `/polish`. Keep each prompt to one milestone:

> "Implement M2 from PROJECT_PLAN.md. Follow 'The system' in CLAUDE.md and any module CLAUDE.md you touch. Write tests for the rules that must not break."

When you and Claude choose between alternatives along the way, Claude records it with `/decision`.

---

## 7. Ongoing maintenance

| When | Run |
|------|-----|
| Chose between alternatives | `/decision` |
| Before calling a task done | `/check-done` |
| Agent made the same mistake twice | Add to `LESSONS_LEARNED.md` and a rule to CLAUDE.md Conventions |
| Before a release or at end of sprint | `/changelog-gen` |
| Before sharing or submitting the project | Clone it into a fresh folder, install from scratch, and run the tests and main command end to end. Timing bugs and missing files show up here, not in your working copy. |
| Something feels out of sync across docs | `/doc-health` |
| A module needs rules of its own | `/module-doc` |
| Planning the next feature | `/plan-feature` |
| Event-driven project: modules start reacting to each other | `/sync-flow` |

---

## Example: Data Science / ML project

**The system** in the root CLAUDE.md:

```
raw data → clean → split (by time) → features → train → evaluate
```

**Must not break**:
- Split before fitting anything; scalers, encoders and imputers are fitted on training folds only.
- The test period is used once, for the final model.

**Module docs, once the project grows**: for example `src/noise/CLAUDE.md` with "noise is added to training labels only; test labels are never changed". See [examples/ml-workflow/CLAUDE.md](examples/ml-workflow/CLAUDE.md).

**Synchronizations**: usually none, because the steps run in order. They become useful when, say, a deployment service reacts to evaluation results; see [examples/SYNCHRONIZATIONS.md](examples/SYNCHRONIZATIONS.md).

---

## What good looks like

After the first session you should have:
- [ ] Root `CLAUDE.md` with your project name, stack, commands, and Conventions filled in, and no placeholders left
- [ ] `ROADMAP.md` with at least one quarterly goal
- [ ] "The system" sketched in CLAUDE.md (or deleted, if the project is small)
- [ ] `PROJECT_PLAN.md` with your first feature in the Now section

That's enough context for Claude to rebuild a useful mental model of your project from scratch on any future session.

---

**Next**: [README.md](README.md) for the full framework philosophy · [docs/ADVANCED_FEATURES.md](docs/ADVANCED_FEATURES.md) for scaling patterns
