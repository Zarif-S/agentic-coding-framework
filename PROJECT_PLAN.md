# Project Plan - Tactical Execution

## 📍 Breadcrumbs

- **New to the project?** → [CLAUDE.md](CLAUDE.md) for setup and overview
- **Looking for strategic vision?** → [ROADMAP.md](ROADMAP.md)
- **Looking for implementation details?** → [CLAUDE.md - Task Navigation](CLAUDE.md#-documentation-navigation)
- **Looking for completed features?** → [CHANGELOG.md](CHANGELOG.md)

---

## Purpose of This Document

**PROJECT_PLAN.md** answers tactical questions:
- **What are we building right now?** (current sprint/iteration)
- **What's the execution plan?** (the "route")
- **Who's working on what?** (assignments)
- **What's blocking us?** (blockers and dependencies)

**This is NOT**:
- Strategic vision (see [ROADMAP.md](ROADMAP.md))
- Long-term goals (see [ROADMAP.md](ROADMAP.md))
- Implementation architecture (see [CLAUDE.md](CLAUDE.md))

**Timeframe**: Weeks to months, updated weekly or at sprint boundaries

---

## Current Sprint/Iteration

### Sprint [X]: [Sprint Name/Theme] ([Date Range])

**Sprint Goal**: [1-2 sentence description of what this sprint aims to achieve]

**Alignment**: This sprint supports [ROADMAP milestone - e.g., "Q1 2025: Multi-tenancy foundation"]

---

## In Progress

### High Priority

| Task | Assignee | Status | Target Date | Notes |
|------|----------|--------|-------------|-------|
| [Task 1 - e.g., "Implement tenant isolation in database layer"] | [Name] | 🔄 In Progress | [Date] | [Blockers/updates] |
| [Task 2] | [Name] | 🔄 In Progress | [Date] | [Notes] |

### Medium Priority

| Task | Assignee | Status | Target Date | Notes |
|------|----------|--------|-------------|-------|
| [Task 3] | [Name] | 🔄 In Progress | [Date] | [Notes] |
| [Task 4] | [Name] | ⏸️ Blocked | [Date] | Waiting on [dependency] |

---

## Upcoming (Next Sprint)

| Task | Priority | Estimated Effort | Dependencies | Notes |
|------|----------|------------------|--------------|-------|
| [Task 1] | High | [e.g., "3 days"] | [Prerequisites] | [Context] |
| [Task 2] | Medium | [e.g., "1 week"] | [Prerequisites] | [Context] |
| [Task 3] | Low | [e.g., "2 days"] | None | [Context] |

---

## Recently Completed

| Task | Completed Date | Outcome | Documentation Updated |
|------|----------------|---------|----------------------|
| [Task 1] | [Date] | [Brief description of what was delivered] | ✅ [Link to CHANGELOG or CLAUDE.md section] |
| [Task 2] | [Date] | [Outcome] | ✅ [Link] |
| [Task 3] | [Date] | [Outcome] | ⚠️ Pending (see Documentation Debt below) |

---

## Blockers & Dependencies

### Active Blockers

**Blocker 1: [e.g., "Waiting for third-party API credentials"]**
- **Impact**: Blocks [task name]
- **Owner**: [Who's responsible for unblocking]
- **ETA**: [When we expect this to be resolved]
- **Mitigation**: [What we're doing in the meantime]

**Blocker 2: [Description]**
- **Impact**: [What's affected]
- **Owner**: [Responsible party]
- **ETA**: [Expected resolution]
- **Mitigation**: [Workaround or parallel work]

### Dependencies

| Dependency | Status | Impact | Mitigation |
|------------|--------|--------|------------|
| [e.g., "External API integration"] | 🟡 At Risk | Delays Q1 milestone | Parallel development with mocks |
| [Dependency 2] | 🟢 On Track | None | N/A |

---

## Documentation Debt

**What is documentation debt?** Technical debt in documentation - areas where docs are outdated, incomplete, or missing.

### High Priority (Address This Sprint)

| Item | Type | Last Updated | Reason | Assignee |
|------|------|--------------|--------|----------|
| `[module/CLAUDE.md]` - [Section] | Outdated | [Date] | [Why it's urgent - e.g., "New architecture not reflected"] | [Name] |
| `ROADMAP.md` - Q2 milestones | Missing | N/A | Strategic goals shifted, needs update | [Name] |

### Medium Priority (Address Next Sprint)

| Item | Type | Last Updated | Reason | Assignee |
|------|------|--------------|--------|----------|
| `[file path]` - [Section] | Incomplete | [Date] | [Why it matters] | [Name] |
| `CHANGELOG.md` | Missing entries | [Date] | Last 3 features not documented | [Name] |

### Low Priority (Backlog)

| Item | Type | Last Updated | Reason |
|------|------|--------------|--------|
| `[file path]` | Minor inconsistency | [Date] | [Description] |
| `[file path]` | Missing examples | [Date] | [Description] |

### Completed Documentation Updates (This Sprint)

| Item | Completed Date | PR/Commit | Notes |
|------|----------------|-----------|-------|
| `api-service/CLAUDE.md` | [Date] | [Link] | Updated authentication flow diagram |
| `ROADMAP.md` | [Date] | [Link] | Added Q2 strategic goals |

---

## Sprint Retrospective (Previous Sprint)

### Sprint [X-1]: [Previous Sprint Name] ([Date Range])

**What Went Well** ✅
- [Achievement 1]
- [Achievement 2]
- [Achievement 3]

**What Could Be Improved** 🔄
- [Issue 1]
- [Issue 2]

**Action Items**
- [ ] [Action 1 - e.g., "Schedule architecture review before starting complex features"]
- [ ] [Action 2]

**Documentation Health**
- **Updates made**: [Number] docs updated
- **Debt created**: [Number] new debt items
- **Debt resolved**: [Number] debt items closed
- **Net change**: [Positive/negative trend]

---

## Capacity & Allocation

### Team Capacity (Current Sprint)

| Team Member | Available Days | Allocation | Focus Areas |
|-------------|----------------|------------|-------------|
| [Name 1] | [e.g., "8 days"] | 100% | [Tasks/areas] |
| [Name 2] | [e.g., "6 days"] | 75% (25% support) | [Tasks/areas] |
| [Name 3] | [e.g., "5 days"] | 50% (part-time) | [Tasks/areas] |

### Time Allocation by Category

| Category | Estimated % | Actual % (Updated Weekly) |
|----------|-------------|---------------------------|
| Feature development | 60% | [Track actuals] |
| Bug fixes | 15% | [Track actuals] |
| Technical debt | 10% | [Track actuals] |
| Documentation | 10% | [Track actuals] |
| Meetings & planning | 5% | [Track actuals] |

---

## Definition of Done

A task is considered "done" when:
- [ ] Code is written and reviewed
- [ ] Tests are passing (unit + integration)
- [ ] Documentation is updated (see checklist below)
- [ ] Changes are deployed to [environment]
- [ ] Stakeholders are notified

### Documentation Update Checklist

When completing a task, check if these docs need updating:

- [ ] **ROADMAP.md** - Does this change strategic direction or milestones?
- [ ] **PROJECT_PLAN.md** - Mark task as complete, update blockers
- [ ] **CLAUDE.md** (root) - Does this change setup, structure, or common tasks?
- [ ] **CLAUDE.md** (subfolder) - Does this change module architecture or patterns?
- [ ] **CHANGELOG.md** - Is this a user-facing feature or breaking change?
- [ ] **Code comments** - Are there complex implementations needing inline docs?

**If unsure**, add to [Documentation Debt](#documentation-debt) for review.

---

## Metrics & Progress Tracking

### Sprint Burndown

| Day | Planned Remaining | Actual Remaining | Notes |
|-----|-------------------|------------------|-------|
| Day 1 | [Points/tasks] | [Actual] | |
| Day 2 | [Points/tasks] | [Actual] | |
| ... | | | |

### Velocity Trend

| Sprint | Planned | Completed | Velocity | Notes |
|--------|---------|-----------|----------|-------|
| Sprint [X-2] | [Points] | [Points] | [%] | [Context] |
| Sprint [X-1] | [Points] | [Points] | [%] | [Context] |
| Sprint [X] | [Points] | [TBD] | [TBD] | Current sprint |

---

## Risk Register

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| [e.g., "Key engineer taking leave mid-sprint"] | Medium | High | Cross-train team members | [Name] |
| [Risk 2] | [Level] | [Level] | [Strategy] | [Name] |

---

## Communication Plan

### Weekly Updates

**When**: Every [day] at [time]
**Format**: [Stand-up, email, Slack, etc.]
**Attendees**: [Who should participate]

### Sprint Review

**When**: End of sprint ([date])
**Format**: Demo + retrospective
**Attendees**: Full team + stakeholders

### Ad-hoc Updates

**Trigger**: Significant blocker or milestone achieved
**Channel**: [Slack channel, email, etc.]

---

## Links & Resources

### Internal Resources
- **[ROADMAP.md](ROADMAP.md)**: Strategic context for current sprint
- **[CLAUDE.md](CLAUDE.md)**: Implementation guidance
- **[CHANGELOG.md](CHANGELOG.md)**: Record completed work here
- **Project Board**: [Link to Jira, GitHub Projects, etc.]

### External Resources
- **Design Docs**: [Link to design documents folder]
- **Figma/Design**: [Link to design files]
- **API Documentation**: [Link to API docs]

---

## Revision History

### 2025-01-31: Sprint [X] Planning
- Initialized Sprint [X] with [number] tasks
- Added [number] documentation debt items
- Updated team capacity

---

**Last Updated**: 2025-01-31
**Current Sprint**: Sprint [X] ([dates])
**Next Review**: [Date - typically weekly or at sprint end]

---

**Related Documentation**:
- [ROADMAP.md](ROADMAP.md) - Strategic vision and quarterly goals
- [CLAUDE.md](CLAUDE.md) - Implementation guidance and architecture
- [CHANGELOG.md](CHANGELOG.md) - Completed feature history
