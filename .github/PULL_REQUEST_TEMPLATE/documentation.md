# Documentation Update Checklist

Thank you for contributing! Please review this checklist to ensure documentation stays up-to-date with code changes.

**Not all items apply to every PR** - check N/A for items that don't apply to your changes.

---

## Documentation Review

### Strategic Documentation

- [ ] **ROADMAP.md** - Does this PR change strategic direction, quarterly goals, or major milestones?
- [ ] N/A - No strategic changes

**If yes, what changed?**
<!-- Describe what sections of ROADMAP.md need updating -->

---

### Tactical Documentation

- [ ] **PROJECT_PLAN.md** - Have you marked completed tasks? Added new blockers or dependencies?
- [ ] N/A - No project plan changes needed

**If yes, what changed?**
<!-- e.g., "Marked task XYZ as completed, removed blocker ABC" -->

---

### Architecture Documentation

- [ ] **Root CLAUDE.md** - Does this PR change setup steps, project structure, or common commands?
- [ ] N/A - No root-level changes

**If yes, what changed?**
<!-- e.g., "Added new environment variable", "Changed installation steps" -->

---

- [ ] **Subfolder CLAUDE.md** - Does this PR change module architecture, design patterns, or integration points?
- [ ] N/A - No module-level architecture changes

**If yes, which file(s)?**
<!-- e.g., "Updated api-service/CLAUDE.md - new authentication flow" -->

---

### Change History

- [ ] **CHANGELOG.md** - Is this a user-facing feature, breaking change, or significant bug fix?
- [ ] N/A - Internal refactoring only

**If yes, what category?**
<!-- e.g., "Added: New user profile API endpoint" -->
<!-- Categories: Added, Changed, Deprecated, Removed, Fixed, Security -->

---

### Decisions & Lessons

- [ ] **DECISIONS.md** - Did this PR involve choosing between alternatives? Add an ADR (`/decision`)
- [ ] **LESSONS_LEARNED.md** - Did something go wrong that shouldn't happen again?
- [ ] N/A - No decisions or lessons

**If yes, which entries?**
<!-- e.g., "ADR-007: Switch to Parquet", "LL-003: Agent hardcoded thresholds in notebook" -->

---

### Code Documentation

- [ ] **Code Comments** - Are there complex implementations that need inline documentation?
- [ ] N/A - Code is self-explanatory

**If yes, where?**
<!-- e.g., "Added docstrings to auth middleware explaining JWT validation" -->

---

## Documentation Debt

If you didn't have time to update documentation fully:

- [ ] I've added an inline `TODO` or a GitHub issue labelled `documentation` (see [CONTRIBUTING.md](../../CONTRIBUTING.md#documentation-practices))

**Debt item priority**: [ ] High [ ] Medium [ ] Low

**Reason for deferral**:
<!-- e.g., "Need to finalize API design before documenting fully" -->

---

## Conflict Check

- [ ] I've verified this PR doesn't contradict existing documentation (especially ROADMAP.md and root CLAUDE.md)
- [ ] If conflicts exist, I've documented them below or resolved them

**Conflicts identified**:
<!-- If any, describe contradictions and how they're being resolved -->

---

## Additional Notes

<!-- Any other context about documentation changes or decisions -->

---

## Quick Reference

**What goes where?**
- **ROADMAP.md**: Strategic vision, quarterly goals
- **PROJECT_PLAN.md**: Current focus, blockers
- **DECISIONS.md**: Why we chose X over Y (ADRs)
- **LESSONS_LEARNED.md**: What went wrong and what we do now
- **Root CLAUDE.md**: Setup, commands, conventions, Definition of Done
- **Subfolder CLAUDE.md**: Module architecture, design patterns, integration guides
- **CHANGELOG.md**: User-facing features, breaking changes, bug fixes
- **Code comments**: Complex implementation details, edge cases

**See**: [docs/ADVANCED_FEATURES.md](../../docs/ADVANCED_FEATURES.md#2-pr-documentation-checklist) for full guidance.
