---
description: Implements tasks from a GitHub Epic, updates the checklist, and documents code changes per file.
---

# Workflow: Implement GitHub Epic

This workflow should be executed after tasks have been fully detailed as comments within a GitHub Epic. It manages the implementation process while ensuring rigorous, structured documentation in the GitHub issue thread.

1. **Initialize the Master Task Checklist**
   - Read the GitHub Epic thread to extract the complete list of tasks.
   - Post a **new comment** on the Epic containing a Markdown Checklist (`- [ ] Task Name...`) encompassing all tasks. This serves as the master checklist to be updated as work progresses.
   - Note the Comment ID of this checklist for future updates.

// turbo-all
2. **Implement Tasks Sequentially**
   - Review the detailed instructions for the target task (requirements, expected outcome).
   - Perform the code implementation (creating, modifying, or deleting files).
   - Once the task is implemented and passes verification, perform the following actions immediately:

   **Action A: Update the Checklist**
   - Edit the master checklist comment to mark the completed task as done (`- [x] Task Name`).

   **Action B: Document the Code Changes**
   - Post a **detailed comment** to the Epic thread detailing the specific code changes.
   - Since the `gh` CLI does not support direct file uploads to issues, documentation should follow this format:
      - **New or Deleted Files**: Provide the entire source code to simulate an attachment.
      - **Modified Files**: Include the diff block or key snippets showing the changes.
   - Use a collapsible HTML `<details>` tag for better readability.
     *Example format (write to a temp file, then run `gh issue comment <id> --body-file`):*
     ```markdown
     <details><summary>Click to view code changes: filename.ext</summary>

     ```language
     (Source code, diff block, or key snippets)
     ```
     </details>
     ```

   - Your comment **MUST** include these four sections:
     - **What**: Clearly define what this function, class, module, or feature does (e.g., *"This function validates the user's email input format."*).
     - **Why**: Provide the technical reasoning and the problem it resolves (e.g., *"Validation ensures data integrity before persistence, preventing system errors."*).
     - **Who**: Identify the consumers of this feature or the modules affected by the change.
     - **How**: Describe the implementation approach, algorithms, or logic used (e.g., *"Utilized Regex to check email structure, returning true if valid."*).

3. **Repeat & Finalize**
   - Proceed to the next task in the checklist and repeat Step 2.
   - Once all tasks are completed and checked off, formally conclude the implementation flow.
