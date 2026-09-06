# Contributing

This repo only houses the organization profile README (`profile/README.md`), but it
follows the same conventions as the other AI Crafting repositories.

## Signed commits are required

Every commit must carry a valid signature. Enforced in two places:

- **Locally**, by the pre-push hook. Enable it once per clone:

  ```bash
  git config core.hooksPath .githooks
  ```

  The hook runs `scripts/runChecks.sh`, which runs every executable check in
  `scripts/checks/`: `lint.sh` (yamllint + shellcheck) and `verifyGitLogs.sh`, which
  rejects any unpushed commit whose signature is not good (`%G?` of `G` or `U`).
  `U` is accepted because a good signature from a key you have not personally
  trusted is still a valid signature; GitHub's own merge commits show as `U` until
  you trust its web-flow key.

- **In CI**, by the `ci-global-commits-signed` workflow, which fails a pull request if
  GitHub reports any of its commits as unverified. That check is required on `main`.

Run the checks on demand with:

```bash
scripts/runChecks.sh
```

Code style: tabs (width 4), trailing whitespace trimmed on save except in `.md`
files, one final newline. See `AGENTS.md`.
