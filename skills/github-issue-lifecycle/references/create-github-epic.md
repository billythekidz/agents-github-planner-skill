# Create a GitHub Epic

Use this workflow when an implementation plan should become durable GitHub tracking.

1. Find the final implementation plan artifact. If none exists, use the detailed plan supplied in the request.
2. Preserve its architecture decisions, proposed changes, constraints, and open questions. Do not reduce it to a short summary.
3. Search open and closed issues for the exact Epic title. Inspect likely matches and reuse an equivalent Epic.
4. If no equivalent exists, create the Epic from the plan file and capture its number and URL:

   ```sh
   gh issue create --repo <repo> --title "Epic: <plan title>" --body-file <absolute-plan-path>
   ```

5. Extract independently trackable tasks. For each task, first inspect the Epic's existing sub-issues and reuse an equivalent one. Otherwise create a native sub-issue:

   ```sh
   gh issue create --repo <repo> --parent <epic-number> --title "<task title>" --body-file <task-body-path>
   ```

   Each task body should contain:

   - Full requirements
   - Expected output
   - Acceptance tests when they add useful coverage

   When dependencies are known, add native blocking relationships with `--blocked-by <numbers>`. If the installed CLI lacks native relation flags, follow [github-access.md](github-access.md) instead of using prose-only task comments.

6. Create one sub-issue at a time and capture its number and URL. On failure, stop and report the Epic plus successfully created children; a later run must resume from that state.
7. Return the Epic and sub-issue URLs. Begin implementation only when the request also authorizes it; then follow [implement-github-epic.md](implement-github-epic.md).
