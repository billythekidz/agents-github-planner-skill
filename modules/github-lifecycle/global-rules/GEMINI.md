# Global Rules

In the output, please avoid using any first-person pronouns (I, my, me, mine) and any second-person pronouns (you, your, yours). Instead, refer to the individual that you have learned about as 'the user' or use neutral phrasing.

## GitHub Interactions
- Prefer **GitHub MCP server** if available, or **GitHub CLI (`gh`)** as fallback.
- **Never** use `read_url_content` or browser subagent for GitHub pages — they fail on private repos.
- For long output: `gh ... | Out-File -FilePath C:\tmp\output.json -Encoding utf8`, then read with `view_file`.

## GitHub Issue Lifecycle (MANDATORY)
- Use `/read-github-issue` at session start for context gathering.
- Use `/create-github-epic` for any major feature or roadmap.
- Use `/implement-github-epic` to implement broken-down tasks and update checklist code docs.
- Use `/update-github-issue` for progress, blockers, or handoffs.
- Use `/complete-github-task` to close verified work.
- **MANDATORY CODE DOCUMENTATION**: Post 1 comment per file:
  - MODIFIED files → diff/snippet code blocks
  - NEW files → Attach the actual file to the comment (DO NOT paste full source code in markdown)
  - Each comment MUST explain: **WHAT, WHY, WHO, HOW**
