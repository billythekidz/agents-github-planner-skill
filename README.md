# Agent-Agnostic GitHub Issues Architecture

> A centralized repository for managing AI agent workflows (like Antigravity, Claude Code, Gemini CLI, etc.) through structured GitHub Issues.

## Why this Repo?
This repository is the **Single Source of Truth** for global behavioral rules and workflows. 
Instead of copying and pasting rules whenever you reinstall or run multiple agents, use **Symlinks** to bind your local agent configuration directories directly back to this repository.

Whenever you update a workflow here, all your agents get the update instantly.

## Repository Structure

```text
.
├── ARCHITECTURE.md              ← Concept diagrams + Mermaid flows
└── modules/                     ← Modularized workflows, rules, and skills
    ├── github-lifecycle/        ← Management commands for GitHub Epic & Issue lifecycles
    │   ├── global-rules/
    │   │   └── GEMINI.md
    │   ├── workflows/
    │   │   ├── create-github-epic.md
    │   │   ├── read-github-issue.md
    │   │   ├── search-github-issue.md
    │   │   ├── update-github-issue.md
    │   │   ├── implement-github-epic.md
    │   │   └── complete-github-task.md
    │   └── templates/
    │       └── local-rules/
    │           └── github_lifecycle.md
    └── resilient-sdlc/          ← Deep knowledge mapping of SOLID to Ops limitations
        ├── global-rules/
        │   └── resilient-sdlc.md
        ├── workflows/
        │   └── apply-resilient-sdlc.md
        └── skills/
            └── resilient-sdlc/
                └── SKILL.md
```

## How to Install (Symlink Method)

Clone the repo to a permanent location (e.g. `C:\Users\theaux\github-workflows`).
Then, bind your agent directories to the repo via PowerShell (`Admin` normally required for SymbolicLink, but `Junction/HardLink` bypasses it).

### For Antigravity / Gemini CLI:
```powershell
cd C:\Users\theaux

# 1. Backup old if needed
Remove-Item -Path ".\.gemini\GEMINI.md" -Force
Remove-Item -Path ".\.gemini\antigravity\global_workflows" -Recurse -Force

# 2. Create Hardlink for GEMINI.md (Applies the global rules)
New-Item -ItemType HardLink -Path ".\.gemini\GEMINI.md" -Target ".\github-workflows\global-rules\GEMINI.md" -Force

# 3. Create Junction for global_workflows (Applies the workflows)
New-Item -ItemType Junction -Path ".\.gemini\antigravity\global_workflows" -Target ".\github-workflows\workflows" -Force
```

## How to Maintain

1. **Edit any file**: Open this repo in your IDE and edit files under `/global-rules` or `/workflows`.
2. **Auto-applied**: Because of the Symlinks/Hardlinks, your local agent instantaneously uses the updated version.
3. **Save to Cloud**: Run `git commit -am "update"` and `git push` to back up your changes.
