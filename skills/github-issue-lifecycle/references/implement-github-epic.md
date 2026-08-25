# Implement a GitHub Epic

Use this workflow after an Epic contains native sub-issues and implementation is authorized.

1. Read the Epic and its existing sub-issues. Their native open/closed states are the progress tracker; do not create a duplicate checklist comment.
2. For each open sub-issue, in dependency order:

   - Read its requirements and expected output.
   - Implement the smallest complete change.
   - Run risk-appropriate verification that proves the task works.
   - If verification fails, keep the sub-issue open, follow [update-github-issue.md](update-github-issue.md), and stop that task.
   - If verification passes, follow [complete-github-task.md](complete-github-task.md) to post one completion summary and close the sub-issue.

3. The completion summary should contain one compact changed-files table:

   | File | What and why | Affected consumers | Approach |
   |:--|:--|:--|:--|
   | `<path>` | `<change and reason>` | `<consumer>` | `<implementation>` |

4. Link the commit or PR when available. Add only focused snippets needed to explain non-obvious behavior; omit generated, vendored, binary, sensitive, and oversized content.
5. After all sub-issues close, verify the Epic-level acceptance criteria and complete the Epic. Native sub-issue progress replaces manual checklist editing.
