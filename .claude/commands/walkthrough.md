# Walkthrough

Write the interview walkthrough for a milestone's code, so the user can understand and explain it without reading the code first. Run after `/polish` and its commit, on the final code.

Argument: the milestone (e.g. `M2`). Default: the most recent milestone marked done in PROJECT_PLAN.md.

## Steps

1. **Read** the milestone's modules in full (see the Repo layout in CLAUDE.md for which modules belong to which milestone), their tests, and the ADRs they rely on. Skim earlier `docs/code_walkthrough_m*.md` files so you don't repeat them; link to them instead.

2. **Write `docs/code_walkthrough_m[N].md`** (one file per milestone; overwrite if it exists). Plain English, short sentences, no code beyond one-line examples. Use the format below.

3. **Check it** against the code: every function named exists with that name, every claim about behaviour is true (run a one-liner if unsure), every ADR number is right.

4. **Offer explain-it-back**: ask the user to explain the module in 3–5 sentences as they would to an interviewer. Then point out what was wrong, missing or vague, briefly. Don't lecture.

---

## Section Format

```markdown
## M[N]: [module(s)]

**In one sentence**: [what this code does for the pipeline]

**How it flows**: [3–6 numbered steps, top to bottom, naming the functions]

**Functions** (one line each: what it does, not how)
- `name(args)`: ...

**Design choices** (the "why X not Y" an interviewer will ask)
- [choice]: [why, alternative rejected] (ADR-NNN)

**Data quirks it handles**: [only if any]

**What's tested and what isn't**: [one or two lines]

**Likely interview questions**
- *Q*: ...
  *A*: [two or three sentences the user could say]
```

## Rules

- Write for someone who hasn't read the code. If a sentence needs the code open to make sense, rewrite it.
- 3–6 interview questions per milestone; favour the "why" and "what if" ones over "what does line N do".
- Don't restate ADRs at length; one line and the ADR number.
