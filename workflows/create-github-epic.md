---
description: Converts a local Implementation Plan into a GitHub Epic with linked Subtasks.
---

# Workflow: Create GitHub Epic from Plan

This workflow automatically takes the current `implementation_plan.md` artifact and ports it directly to GitHub Issues for long-term tracking.

1. **Understand Epic Scope**
   - Read the local `implementation_plan.md` artifact.
   - The body of the GitHub Epic MUST contain the ENTIRE detail of the implementation plan (architecture decisions, proposed changes, open questions). Do NOT summarize it to a single sentence.
   - If there are relevant scripts, configuration blocks, or terminal screenshots necessary for the plan, embed them directly or attach them to the issue via the GitHub CLI.
   - Extract the individual components from `Proposed Changes` to form actionable Subtask Issues.
   
2. **Create the Epic (Main Issue)**
   - Skip creating an intermediate temporary file (like `/tmp/epic_body.md`). Instead, directly use the source markdown file (e.g., `implementation_plan.md` or `architecture.md`) as the body of the Epic.
   - Run `gh issue create --title "Epic: [Plan Title]" --body-file path/to/the_plan.md`
   - Capture the `#ID` returned from the CLI.

// turbo-all
3. **Comment Task Breakdown on the Epic**
   - Post a **dedicated comment** on the newly created Epic for EACH extracted task.
   - Write the task details to a temporary file, then run `gh issue comment [Main ID] --body-file /tmp/task_comment.md`.
   - **MANDATORY FORMAT PER TASK COMMENT**:
     - **Full Requirements**: Exactly what needs to be built.
     - **Expected Output**: Clear criteria for what success looks like.
     - **Test Cases (Optional)**: Specific scenarios to verify the implementation.
   - You MUST post EXACTLY ONE comment per task.

4. **Transition to Implementation**
   - After fully commenting all the task breakdowns on the Epic, DO NOT implement the code immediately.
   - Proceed to invoke the `/implement-github-epic` workflow to handle the actual coding, issue updating, and PR/commit linkage.
   - Provide the user with the direct GitHub URL pointing to the unified Epic and notify them that progress tracking will be maintained on these issues moving forward.
