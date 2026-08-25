# Update a GitHub Issue

Use this workflow for meaningful progress, blockers, decisions, or session handoffs.

1. Read recent comments and do not post an equivalent update twice.
2. Draft a concise update containing the current state, completed work, verification, blockers, and next action. Include exact errors or commands only when useful.
3. Write it to a temporary Markdown file and post it:

   ```sh
   gh issue comment <number> --repo <repo> --body-file <update-path>
   ```

4. If relationships changed, use native parent/sub-issue or blocking relationships instead of prose-only links.
5. Return the issue URL and summarize what was recorded.
