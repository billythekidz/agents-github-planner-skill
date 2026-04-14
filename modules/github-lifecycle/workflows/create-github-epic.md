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
   
2. **Create the Epic (Main Issue) - RAW PUSH ONLY**
   - **CRITICAL RULE**: ALL agent-generated plans (including `.md` and `.resolved` artifact paths) MUST be passed directly as raw files. DO NOT read the file into memory to summarize it, and DO NOT create intermediate summary files.
     - *Target Path Example*: You must find and use the absolute path, for example: `C:\Users\theaux\.gemini\antigravity\brain\510581c8-9546-44a8-bd4b-e99310605606\artifacts\implementation_plan.md.resolved`
   - **Method 1: GitHub CLI (Preferred)**
     - Run: `gh issue create --title "Epic: [Plan Title]" --body-file /absolute/path/to/the_plan.md.resolved`
   - **Method 2: GitHub API via PowerShell**
     - If `gh` CLI is unavailable, use `Invoke-RestMethod` to push the raw string intact.
     - Example:
       ```powershell
       $RawBody = Get-Content -Path "/absolute/path/to/the_plan.md.resolved" -Raw -Encoding UTF8
       $JsonPayload = @{ title = "Epic: [Plan Title]"; body = $RawBody } | ConvertTo-Json -Depth 10
       Invoke-RestMethod -Uri "https://api.github.com/repos/OWNER/REPO/issues" -Method Post -Headers @{"Authorization"="Bearer $env:GITHUB_TOKEN"} -Body $JsonPayload -ContentType "application/json"
       ```
   - Capture the `#ID` returned from the chosen method.

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
