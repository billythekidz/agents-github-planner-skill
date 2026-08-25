# GitHub Access and REST Fallback

## Default transport

Use `gh` issue commands first. They provide consistent authentication and output across supported agent CLIs.

Before the first mutation:

```sh
gh auth status
gh repo view <repo>
```

Keep `--repo <repo>` on every issue command.

## When REST fallback is allowed

Use REST only when `gh` is not installed, the installed version lacks the required command or flag, or the operation has no equivalent `gh` command.

Do not switch transports after authentication, authorization, validation, rate-limit, or ambiguous-target errors. If a write timed out or returned an unknown result, read GitHub state before deciding whether anything remains to do.

When `gh` exists but its high-level command lacks a capability, prefer `gh api`. Otherwise use the platform's native HTTP client with an existing `GH_TOKEN` or `GITHUB_TOKEN`. Never print, persist, or embed the token in issue content.

## REST contract

Use these headers for direct HTTP requests:

```text
Accept: application/vnd.github+json
Authorization: Bearer <token-from-environment>
X-GitHub-Api-Version: 2026-03-10
```

Private reads require appropriate repository access. Writes require `Issues: write`. Do not create credentials or broaden token permissions without explicit authorization.

For canonical `<repo>` value `OWNER/REPO`, use these endpoints:

| Operation | Method and endpoint | Body or note |
|:--|:--|:--|
| Verify repository | `GET /repos/OWNER/REPO` | Confirm `full_name` before mutation. |
| List issues | `GET /repos/OWNER/REPO/issues` | Filter out entries containing `pull_request`. |
| Search issues | `GET /search/issues?q=repo:OWNER/REPO+<query>` | URL-encode the query. |
| Read issue | `GET /repos/OWNER/REPO/issues/<number>` | Capture `id`, `number`, and `html_url`. |
| Create issue | `POST /repos/OWNER/REPO/issues` | `{ "title": "...", "body": "..." }` |
| Update or close issue | `PATCH /repos/OWNER/REPO/issues/<number>` | Close with `{ "state": "closed", "state_reason": "completed" }`. |
| List comments | `GET /repos/OWNER/REPO/issues/<number>/comments` | Check for an equivalent comment before posting. |
| Create comment | `POST /repos/OWNER/REPO/issues/<number>/comments` | `{ "body": "..." }` |
| Update comment | `PATCH /repos/OWNER/REPO/issues/comments/<comment-id>` | `{ "body": "..." }` |
| List sub-issues | `GET /repos/OWNER/REPO/issues/<parent>/sub_issues` | Use native parent state. |
| Attach sub-issue | `POST /repos/OWNER/REPO/issues/<parent>/sub_issues` | `{ "sub_issue_id": <issue-id> }` |
| Add blocked-by dependency | `POST /repos/OWNER/REPO/issues/<number>/dependencies/blocked_by` | `{ "issue_id": <blocking-issue-id> }` |

REST sub-issue creation is two mutations: create the child issue, then attach its numeric `id` to the parent. If attachment fails, keep and reuse the created child on resume; do not create another issue.

Accept only successful `2xx` responses. Stop on `401`, `403`, `404`, `422`, or `429`. After timeouts or `5xx` responses, re-read the target state before any retry.
