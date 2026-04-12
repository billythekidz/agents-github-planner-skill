---
description: Formally comments on and closes a GitHub Issue upon successful verification.
---

# Workflow: Complete GitHub Task

Use this workflow when you have fully implemented and verified the requirements of a GitHub Issue.

1. **Summarize the Work**
   - Gather what was changed, including the modified files, key logic shifts, and verification results.
   - Write this summary to a temporary file, e.g., `/tmp/completion_comment.md`.

2. **Add Verification Proof**
   - If tests were run, append the success output.
   - If UI/terminal changes were made, attach screenshots or terminal dumps to `/tmp/completion_comment.md`.

// turbo
3. **Comment & Close the Issue**
   - Run: `gh issue comment [Issue ID] --body-file /tmp/completion_comment.md`
   - Run: `gh issue close [Issue ID] -r completed`

4. **Update the Epic (If Applicable)**
   - If this was a subtask, you may want to ensure the Epic's checklist reflects the completion (though GitHub usually auto-checks `[x]` when the linked issue is closed, verify it using `gh issue view [Epic ID]`).

5. **Acknowledge User**
   - Inform the user the task is closed and state what the next active subtask is.
