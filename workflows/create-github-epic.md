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
   - Because the body usually contains huge texts and markdown syntax, write the entire markdown contents to a temporary file (e.g., `/tmp/epic_body.md`), appending a `- [ ] Pending Subtasks...` section at the bottom.
   - Run `gh issue create --title "Epic: [Plan Title]" --body-file /tmp/epic_body.md`
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

4. **Create Subtask Issues and Document Code Changes**
   - For each task, create a linked issue:
     `gh issue create --title "Task: [Component/Action]" --body "**Part of Epic #[Main ID]** \n\n See Epic thread for detailed requirements, expected output, and test cases."`
   - Accumulate all `#ID`s and link them in the Epic's body: `gh issue edit [Main ID] --body "[Previous Epic Body] \n\n **Subtasks:** \n - [ ] #[Sub ID 1] \n - [ ] #[Sub ID 2]"`
   - **MANDATORY CODE DOCUMENTATION**: Once code is implemented, post a SEPARATE follow-up comment for EACH file affected on the appropriate **Subtask Issue**:
     - **Format**: Each comment must focus on exactly ONE file.
     - **Content for MODIFIED files**: Include a fenced code block showing meaningful changes (diff format or key snippets).
     - **Content for NEW files**: Include the **COMPLETE script/source code** in a fenced code block.
     - **Explanation**: Provide a detailed description of **what** was changed/created and **why** (the technical reasoning and architectural intent).

5. **Acknowledge User**
   - Provide the user with the direct GitHub URL points to the unified Epic and notify them that progress tracking will be maintained on these issues moving forward.
