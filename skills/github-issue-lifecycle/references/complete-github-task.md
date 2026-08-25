# Complete a GitHub Task

Use this workflow only after the issue requirements have been implemented and verified.

1. Read the current issue state and comments. If it is already closed, return its URL without another mutation.
2. Prepare one completion summary containing the changed-files table, important behavior changes, and verification results. Link the commit or PR when available; exclude sensitive or oversized content.
3. If an equivalent completion summary for the same commit and verification does not already exist, post it from a temporary Markdown file:

   ```sh
   gh issue comment <number> --repo <repo> --body-file <completion-path>
   ```

4. Re-read the issue, then close it as a separate mutation:

   ```sh
   gh issue close <number> --repo <repo> --reason completed
   ```

5. For an Epic, close it only after all native sub-issues and Epic-level acceptance criteria are complete. GitHub supplies parent progress; do not maintain a duplicate checklist comment.
6. Return the closed issue URL and identify the next open sub-issue when one exists.

If verification fails, do not close the issue. Record the failure as an update when authorized.
