# AGENTS.md

Shared guidance for every coding agent working in this repository — Codex discovers this
file directly; Claude Code reads it through the `@AGENTS.md` import in `CLAUDE.md`. Put
repo-wide rules here; put harness-specific notes (Claude-only hooks, Codex-only settings) in
that harness's own file.

## Project

AI Crafting's .github repo, mainly containing just a README for the GitHub org to point people
to the relavent product repos inside the organization.

## Code Style

- **Code:** Prefer tabs (width 4) over spaces.
- **Trailing whitespace:** Trimmed on save (except for .md files)
- **Final newlines:** Trimmed (but leave one final newline)

## Issue tracking — flight

This repo manages issues/PRs/CI with the **flight** plugin. The backend is
**GitHub** at `github.com` (`AICrafting/.github`). Issue, PR, and label actions
still go through the dispatcher/skills, not raw `gh`. Coordinates, stage
pipeline, and label names live in `.flightdirector/config.json` (token in
`.flightdirector/secrets.json`, git-ignored). Act through the flight skills
(working-an-issue, promoting-a-branch, filing-issues, …) or the dispatcher:
`flight <group> <verb>`.

Workflow red lines — these hold for every model and survive context
compaction; re-read them before any git write, especially if the session's
earlier instructions were summarized away or the model changed mid-session:

- Each issue is worked on its own `feature/<N>-<slug>` branch in its own
  `.worktrees/<N>-<slug>` worktree — NEVER commit directly to the integration
  branch (`main`), which is also the only stage; changes land via PR.
- Merging is gated on the user's explicit go-ahead ("promote"); it happens
  through the promoting-a-branch skill, never by hand.
- Keep the issue's status label honest at every transition
  (in-progress → to-test → …) via `flight issues set-status`.
