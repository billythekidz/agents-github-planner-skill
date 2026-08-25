# Search GitHub Issues

Use this workflow to find prior decisions, related bugs, or existing work before creating a duplicate issue.

1. Choose the narrowest useful component name, feature, error text, or keyword.
2. Search open and closed issues:

   ```sh
   gh issue list --repo <repo> --state all --search "<keyword>"
   ```

3. Inspect the most relevant results:

   ```sh
   gh issue view <number> --repo <repo> --json title,body,state,comments,url
   ```

4. If issue history is insufficient, search the local repository with `rg` for matching code or documentation.
5. Apply only findings relevant to the request and cite the issue numbers used.
