---
description: Fetches and displays the latest closed and open GitHub Issues to gather context before starting a task.
---

# Workflow: Read GitHub Issues

Use this workflow at the beginning of a conversation or specifically when context gathering is required. It retrieves the latest open and closed issues to help you understand the current state of the repository.

1. **Review Recent Closed Issues**
   - Run the command to list the last 10 closed issues: `gh issue list --state closed --limit 10`
   - Read the output to understand recently completed work, bugs fixed, or features merged.

2. **Review Recent Open Issues**
   - Run the command to list the last 10 open issues: `gh issue list --state open --limit 10`
   - Read the output to figure out current priorities, pending bugs, and active tasks.

3. **Read Specific Issue Details (Optional)**
   - If a specific issue title is highly relevant to your current task, run: `gh issue view [Issue ID] --json title,body,state,comments` to read its full context.

4. **Summarize Context**
   - Briefly explain how the retrieved issues relate to the user's current request before proceeding with task planning or execution.
