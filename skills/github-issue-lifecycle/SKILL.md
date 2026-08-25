---
name: github-issue-lifecycle
description: Manage GitHub Issues from context discovery through Epic planning, implementation tracking, handoffs, verification, and closure. Use when work is tracked in GitHub Issues or when asked to create, implement, search, update, or complete a GitHub Epic or Issue.
---

# GitHub Issue Lifecycle

Use GitHub Issues as the durable record for tracked work. Treat local plans and temporary Markdown files as scratch space.

## Repository and authorization

- Use the `gh` CLI by default. Use GitHub REST API only under the fallback conditions in [references/github-access.md](references/github-access.md).
- Resolve one canonical `<repo>` in `OWNER/REPO` form before any operation: use the explicitly requested repository, otherwise `gh repo view --json nameWithOwner --jq .nameWithOwner`, or parse the Git remote when `gh` is unavailable.
- If fork/upstream selection is ambiguous, stop before mutation and ask which repository is authoritative.
- After resolution, pass `--repo <repo>` to every issue command; do not rely on the current directory.
- Before the first CLI mutation, verify authentication and access with `gh auth status` and `gh repo view <repo>`.
- Read issue context when it is relevant. Create, comment on, edit, or close issues only when the request authorizes that external change.
- Pass long bodies with files instead of shell-escaped inline strings.
- Never expose tokens or credentials in commands, logs, or issue content.

## Mutation protocol

For every external write:

1. Read the relevant current state first: duplicate candidates, target issue, sub-issues, and comments as applicable.
2. Perform one mutation at a time and capture every returned identifier and URL.
3. If a mutation fails, stop the sequence. Re-read GitHub state before resuming and execute only missing actions.
4. Never retry issue or comment creation blindly; reuse an equivalent existing item.

## Route the task

Read only the reference needed for the current operation:

- Use the REST fallback: [references/github-access.md](references/github-access.md)
- Gather recent context: [references/read-github-issues.md](references/read-github-issues.md)
- Search history: [references/search-github-issues.md](references/search-github-issues.md)
- Convert a plan into an Epic: [references/create-github-epic.md](references/create-github-epic.md)
- Implement an Epic: [references/implement-github-epic.md](references/implement-github-epic.md)
- Log progress, blockers, or handoffs: [references/update-github-issue.md](references/update-github-issue.md)
- Verify and close work: [references/complete-github-task.md](references/complete-github-task.md)

## Invariants

- Reuse an existing relevant issue instead of creating a duplicate.
- Represent independently trackable Epic tasks as native GitHub sub-issues. Use native blocking relationships when dependencies are known.
- Document implementation once per task or sub-issue. Summarize changed files in a compact table covering what changed, why, affected consumers, and approach; link the commit or PR when available.
- Never paste secrets, generated files, vendored code, binaries, or oversized source into issue comments. Include focused snippets only when they materially aid review.
- Verify the requested outcome before closing an issue. If verification fails, leave it open and record the blocker when authorized.
- Return direct issue URLs after mutations.
