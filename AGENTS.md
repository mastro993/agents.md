# Agent rules

## Non-negotiable

- Understand the real constraint, then choose the smallest realistic model that makes correct behavior unsurprising. Apply "measure twice, cut once" and YAGNI; resist scope creep and unnecessary machinery.
- Simplify when possible. Prefer small, specialized modules grouped by feature and purpose over large files or swiss-army classes.
- Always use Context7 MCP when I need library/API documentation, code generation, setup or configuration steps without me having to explicitly ask.

## PR and CI

- Before starting a task, rebase the working branch onto `main` to avoid working on stale code.
- For GitHub work, use the matching workflow and search the local Gitcrawl archive first. Use bare PATH `gh` with explicit JSON fields for current metadata. Read PR refs with `gh pr view/diff`, never web search.
- When given a GitHub issue or PR, first run `git status -sb`. Report a dirty tree before mutation. A URL alone grants no pull or push permission.
- Prefer fixing or rewriting an existing PR before merging it, not closing it and duplicating the change in a direct commit. Treat generated code as suspect; review and improve it, including a full rewrite when cleaner.
- UI change PRs require sanitized before/after images. Exclude secrets, personal or private data, internal-only identifiers, and other sensitive content. If safe capture is impossible, report the blocker and upload nothing.
- Upload PR/issue images without computer use or a browser: `curl -s "https://uploads.github.com/user-attachments/assets?name=<file>&content_type=<mime>&repository_id=$(gh api repos/<owner>/<repo> --jq .id)" -X POST -H "Authorization: Bearer $(gh auth token)" -H "Accept: application/json" --data-binary @<file>`. Use response `.url`: `![alt](url)` for images; a bare URL line for video. Uploads use the same CDN as drag-and-drop, inherit repository visibility, and are permanent. Only images and video are supported; `422` means bad type, `404` means bad repository ID or no push access. For other artifacts or endpoint failure, use a prerelease asset or repository-approved artifact store.
- Feature-detect repeatable `gh --attach` on `gh issue|pr create|edit|comment`; it supersedes the upload command when available. It was unmerged as of `gh` 2.98.0 (`cli/cli#14186`). Never use the unrelated `gh attach` extension (`enthus-appdev/gh-attach`) for proof media; it pushes blobs to `refs/uploads/` and fails near 60 KB.
- Explicitly landing an owned draft PR authorizes marking it ready and continuing.
- `fix ci` authorizes pulling, committing, and pushing. Use `gh run list/view`; fix or rerun until green with backoff polling.
- Conserve GitHub quota: use bare `gh` through the Octopool cache. Always request explicit JSON fields for reads. Human-formatted `gh pr view/list/checks`, `gh run list`, and bare `gh api graphql` silently use real `gh` with GraphQL and core personal-token access. `gh api --paginate` also bypasses the cache; use it only when the full list is required. `gh run watch` and `gh pr checks --watch` are shim-native since Octopool 0.4.7; poll one exact ID, not loops.
- Fetch each failed CI run's logs once and reuse the output. Prefer one narrow `gh search` or `list --json` call with exact refs over per-item views.
- `rewrite commits + land` means produce a clean stack with only agreed focused proof, force-push, and merge. Skip PR-body proof polish and CI babysitting unless requested.
- Preserve user-facing behavior, surface, references, and contributor credit in the PR body or squash message for release-note generation. Contributor PR authors do not edit changelogs; maintainers or AI add entries at landing and thank `@login` for user-visible work. Add `Co-authored-by: Name <email>` from the PR commit author to the commit body.
- Explicit `land` or `ship` authorizes required branch changes and push. After merge, check out `main`, run `git pull --ff-only`, verify `git status -sb`, then report.
- After merging or shipping, give a 2–5 paragraph narrative recap: original problem, root cause, change and rationale, important architecture or ownership boundary, proof, notable CI failures or retries, exact PR/issue/merge state, and useful follow-ups. Do not substitute a checklist, bare SHAs, or git commands.
