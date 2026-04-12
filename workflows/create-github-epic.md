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
3. **Create Subtask Issues and Document Changes**
   - For each extracted component, run:
     `gh issue create --title "Task: [Component/Action]" --body "**Part of Epic #[Main ID]** \n\n [Actionable bullet points]"`
   - **MANDATORY DOCUMENTATION**: Once code is implemented or if documenting existing changes, you MUST post a SEPARATE follow-up comment for EACH file affected:
     - **Format**: Each comment must focus on exactly ONE file.
     - **Content for MODIFIED files**: Include a fenced code block showing the meaningful changes (diff format or key snippets).
     - **Content for NEW files**: Include the **COMPLETE script/source code** in a fenced code block.
     - **Explanation**: Provide a detailed description of **what** was changed/created and **why** (the technical reasoning and architectural intent).
   - Capture the `#ID`s of each created subtask.

4. **Link Subtasks Built to Epic**
   - Accumulate all Subtask IDs.
   - Run `gh issue edit [Main ID] --body "[Previous Epic Body] \n\n **Subtasks:** \n - [ ] #[Sub ID 1] \n - [ ] #[Sub ID 2]"`

5. **Acknowledge User**
   - Provide the user with the direct GitHub URL points to the unified Epic and notify them that progress tracking will be maintained on these issues moving forward.
