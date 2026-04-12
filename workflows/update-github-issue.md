---
description: Appends a progress report, blocker, or handoff note to an active GitHub Issue.
---

# Workflow: Update GitHub Issue

Use this workflow to document progress during multi-step tasks, to log blockers, or to create a handoff state before yielding the session.

1. **Draft the Update**
   - Determine the payload: Is it a progress update? A bug encountered? A handoff context for the next session?
   - Write the update to a temporary file, e.g., `/tmp/issue_update.md`. Include exact error logs, code snippets, or commands run.

// turbo
2. **Post the Comment**
   - Run: `gh issue comment [Issue ID] --body-file /tmp/issue_update.md`

3. **Modify Relationships (Optional)**
   - If this update discovered that the current task blocks another task, or depends on a new task, update the main issue body (`gh issue edit ...`) to include `**Blocks #ID**` or `**Depends on #ID**`.

4. **Acknowledge User**
   - Inform the user that the progress/handoff has been safely logged to GitHub.
