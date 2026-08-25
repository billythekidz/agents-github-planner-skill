# GitHub SDLC Agent Skills

Two portable [Agent Skills](https://agentskills.io) installable through Vercel's `skills` CLI. The same source works with Codex, Claude Code, Gemini/Antigravity, OpenCode, Cursor, and other supported agents.

## Skills

### `github-issue-lifecycle`

Manages GitHub Issue and Epic work from context discovery through closure. It uses `gh` by default, GitHub REST API as fallback, and native sub-issues for independently tracked tasks without depending on agent-specific integrations.

### `impact-scope-reduction`

Applies SOLID, risk-based testing, and targeted operations to reduce change blast radius while protecting unrelated and stateful services.

## Install

List the skills before installing:

```sh
npx skills add billythekidz/github-sdlc-agent-skills --list
```

Install interactively to detected agents:

```sh
npx skills add billythekidz/github-sdlc-agent-skills
```

Install one skill globally:

```sh
npx skills add billythekidz/github-sdlc-agent-skills --skill github-issue-lifecycle -g
npx skills add billythekidz/github-sdlc-agent-skills --skill impact-scope-reduction -g
```

Install both skills globally to every supported agent:

```sh
npx skills add billythekidz/github-sdlc-agent-skills --all -g
```

## Structure

```text
skills/
├── github-issue-lifecycle/
│   ├── SKILL.md
│   └── references/
│       ├── github-access.md
│       ├── read-github-issues.md
│       ├── search-github-issues.md
│       ├── create-github-epic.md
│       ├── implement-github-epic.md
│       ├── update-github-issue.md
│       └── complete-github-task.md
└── impact-scope-reduction/
    └── SKILL.md
```

Each directory is self-contained so `npx skills` installs the instructions and their supporting references together.
