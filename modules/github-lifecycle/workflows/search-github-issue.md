---
description: Searches GitHub Issues by keywords to find specific context, previous decisions, or related bugs.
---

# Workflow: Search GitHub Issues

Use this workflow to find historical context or detailed discussions regarding a specific keyword, error, or feature within the repository's issues.

1. **Define the Search Keyword**
   - Identify the most relevant keyword, component name, or error code based on the user's request.

2. **Search Issues via GitHub CLI**
   - Run the search command targeting both open and closed issues: `gh issue list --search "[keyword]"` Note: Replace `[keyword]` with your exact search term.

3. **Grep Search as Fallback (Optional)**
   - If `gh` search does not yield enough context, or if you suspect documentation is stored locally, use the `grep_search` tool to search for the keyword in the local workspace.

4. **Deep Dive into Relevant Results**
   - For the most relevant issues found in step 2, view their details using: `gh issue view [Issue ID] --json title,body,state,comments`.

5. **Apply Findings**
   - Incorporate the insights, code snippets, or architectural decisions discovered from the issues into your implementation plan and then proceed.
