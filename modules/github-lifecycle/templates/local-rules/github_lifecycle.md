---
name: GitHub Issue Lifecycle
description: Enforces that all features, tasks, and handoffs are tracked via GitHub Issues throughout their full lifecycle.
---

# GitHub Issue Lifecycle — cliproxyapi

## Core Principle
GitHub Issues are the **single source of truth** for this repository.
Local artifacts (`implementation_plan.md`, `task.md`) are temporary scratchpads; their final permanent home is GitHub.

## Lifecycle Phases

### A. Discovery (MANDATORY first step)
- Review 10 latest closed + 10 latest open issues at session start.
- Search by keyword if needed: `gh issue list --search "keyword"`.

### B. Planning (Epics and Subtasks)
- Major plans → Epic via `/create-github-epic`.
- Subtasks link to parent: `**Part of Epic #ID**`.
- Epic links to children: `- [ ] #ID`.
- Dependencies: `**Depends on #ID**` / `**Blocks #ID**`.

### C. Development (Progress Logging)
- Log progress via `/update-github-issue` — don't hoard updates.
- Log milestones, blockers, and design decision divergences immediately.

### D. Completion (Verification + Close)
- Verify → summarize → close via `/complete-github-task`.
- If verification fails, reopen the issue — don't create duplicates.
- Session handoffs → `/update-github-issue` with precise context.

## Available Workflows
- `/read-github-issue` — Context gathering
- `/search-github-issue` — Historical search
- `/create-github-epic` — Plan → Epic + Subtasks + Code Docs
- `/update-github-issue` — Progress / blocker logging
- `/complete-github-task` — Verification + Close
