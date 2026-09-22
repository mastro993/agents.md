# Agents rules

## Non negotiable

- Do not preserve complexity just because it already exists. Do not introduce machinery because it looks architecturally impressive. Understand the real constraint, then fight for the smallest model that makes the correct behavior unsurprising.
- Channel both "measure twice, cut once" and "yagni". Fight scope creep. Try to honor the dev's intent in both a minimal and realistic fashion.
- Avoid writing big files. Prefer modularization. Group code by feature, then group code within each feature by purpose. Use separation of concerns. Prefer small, specialized modules over big swissknife classes.
- When a refactoring opportunity can simplify code, take it. Remove unnecessary complexity while keeping behavior clear and correct.
- Always use Context7 MCP when I need library/API documentation, code generation, setup or configuration steps without me having to explicitly ask.

## PR / CI

- GitHub work: use matching workflow. Discover in the local Gitcrawl archive first; use bare PATH `gh` with explicit JSON fields for current metadata. PR refs use `gh pr view/diff`, not web search.
- Pasted GitHub issue/PR: first `git status -sb`. Dirty: report before mutation. URL alone grants no push/pull permission.
- PR: prefer fix/rewrite PR then merge, not close + duplicate direct commit.
- PR quality: assume generated code may come from weaker AI. Review/improve before land; full rewrite okay when cleaner.
- UI change PR: include before/after pictures. Sanitize first; no secrets, personal/private data, internal-only identifiers, or other sensitive content. Unsafe capture: state blocker; never upload.
- PR/issue image upload: never computer use/browser. `curl -s "https://uploads.github.com/user-attachments/assets?name=<file>&content_type=<mime>&repository_id=$(gh api repos/<owner>/<repo> --jq .id)" -X POST -H "Authorization: Bearer $(gh auth token)" -H "Accept: application/json" --data-binary @<file>` → response `.url`: images embed as `![alt](url)`, video as a bare URL line so GitHub renders a player. Same CDN as drag-drop, inherits repo visibility, uploads are permanent. Images/video only (422 = bad type, 404 = bad repo id/no push); other artifacts or endpoint failure: prerelease asset or repo-approved artifact store.
- `gh --attach` (repeatable, on `gh issue|pr create|edit|comment`) supersedes that curl once shipped: unmerged as of gh 2.98.0 (`cli/cli#14186`), so feature-detect, never assume. `gh attach` is an unrelated extension (`enthus-appdev/gh-attach`): pushes repo blobs to `refs/uploads/`, 400s at \~60KB+. Never use it for proof media.
- Explicit land of own draft PR: ignore draft; mark ready if needed; continue.
- `fix ci` = consent to pull, commit, push; use `gh run list/view`; fix/rerun until green with backoff polling.
- GitHub quota: bare `gh` only (Octopool cache). Watch commands (`gh run watch`, `gh pr checks --watch`) shim-native since octopool 0.4.7; still poll one exact id, not loops.
- gh reads: ALWAYS `--json <fields>`. Human-format `gh pr view/list/checks`, `run list`, bare `gh api graphql` delegate silently to real gh (GraphQL+core on personal token). Machine shapes ride the shared cache.
- `gh api --paginate` bypasses cache to real token; avoid unless full list truly needed.
- CI logs: fetch once per failed run; reuse printed output. One `gh search`/`list --json` over per-item view loops; narrow fields, exact refs.
- `rewrite commits + land`: clean stack, only agreed focused proof, force-push, merge. No PR-body proof polish or CI babysit unless asked.
- Issue fixed on `main` with proof: comment proof + commit/PR; close.
- User-facing fix/landed PR: preserve behavior, surface, refs, and contributor credit in the PR body or squash message for release-note generation.
- Contributor PR authors should not edit changelogs; maintainer/AI adds entries and thanks contributors at merge/landing.
- Explicit land/ship authorizes needed branch changes and push. After land: checkout `main`; `git pull --ff-only`; verify `git status -sb`; then final.
- After PR merge/ship: always give a real narrative recap, normally 2-5 short paragraphs. Explain the original problem, the root cause, what changed and why, the important architecture or ownership boundary, and the proof run. Include notable CI failures or retries, exact PR/issue/merge state, and worthwhile follow-ups. Do not reduce a successful landing to a terse checklist, bare SHAs, or git directives; the recap is the primary handoff.
- Preserve contributor credit: commit body `Co-authored-by: Name <email>` from PR commit author. Changelog entries thank `@login` for user-visible work when added: at landing by default.

