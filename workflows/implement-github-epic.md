---
description: Implements tasks from a GitHub Epic, updates checklist, and documents code changes per file.
---

# Workflow: Implement GitHub Epic

This workflow is to be executed after all tasks have been fully detailed as comments in a GitHub Epic. It handles the actual coding process alongside rigorous, structured GitHub issue documentation.

1. **Initialize the Master Task Checklist**
   - Read the GitHub Epic thread to get the full list of broken-down tasks.
   - Post a **new comment** on the Epic containing a Markdown Checklist (`- [ ] Task Name...`) encompassing all tasks. This will be the master checklist you actively update as work progresses.
   - Retrieve the Comment ID of this checklist for future edits.

// turbo-all
2. **Implement Tasks One by One**
   - Read the specific detailed comment for the target task (requirements, expected output).
   - Perform the code implementation (create, edit, or delete files).
   - Once the task is fully implemented and passes any necessary verification or checks, immediately perform the following two actions:

   **Action A: Update the Checklist**
   - Edit your master checklist comment to mark the completed task as done (`- [x] Task Name`).

   **Action B: Document the Code Changes**
   - Post a **detailed comment** back into the Epic thread covering the exact code changes made for this task.
   - If it is a **New or Deleted file**: Since `gh` CLI does not natively support direct file uploads to issues, you MUST simulate a file attachment by embedding the entire source code inside a collapsible HTML `<details>` tag. 
     *Example format to write to a temp markdown file, then run `gh issue comment <id> --body-file`*:
     ```markdown
     <details><summary>Click to view newly created file: filename.ext</summary>

     \`\`\`language
     (Full source code goes here)
     \`\`\`
     </details>
     ```
   - If it is a **Modified file**: Include exactly the diff block or key snippets showing what changed.
   - Your comment MUST explicitly include these 4 sections:
     - **What**: Define clearly what this function, class, module or feature does. *(e.g., "This function validates the user email input format.")*
     - **Why**: The technical reasoning and the problem it resolves. *(e.g., "A validator is needed to ensure valid data before database persistence, preventing system errors.")*
     - **Who**: Identify who consumes this feature, or which existing modules/scripts might be affected by this change.
     - **How**: The implementation approach, algorithms, or workflow logic utilized. *(e.g., "Utilized Regex for checking email structure, returning true if valid and false otherwise.")*

3. **Repeat & Finalize**
   - Move on to the next task in the checklist and repeat Step 2.
   - Once all tasks are implemented and checked off, formally conclude the implementation flow.
