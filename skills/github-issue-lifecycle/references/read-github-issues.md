# Read GitHub Issues

Use this workflow at the start of issue-tracked work or when repository context is needed.

1. Use the canonical `<repo>` resolved by the skill entrypoint.
2. Review the 10 most recent closed issues:

   ```sh
   gh issue list --repo <repo> --state closed --limit 10
   ```

3. Review the 10 most recent open issues:

   ```sh
   gh issue list --repo <repo> --state open --limit 10
   ```

4. Open only the issues relevant to the request:

   ```sh
   gh issue view <number> --repo <repo> --json title,body,state,comments,url
   ```

5. Briefly state how the relevant history affects the current work. Do not turn unrelated issues into scope.
