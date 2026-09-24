# Agent rules

## Playbook

- Understand the real constraint, then choose the smallest realistic model that makes correct behavior unsurprising. Apply "measure twice, cut once" and YAGNI; resist scope creep and unnecessary machinery.
- Simplify when possible; prefer small (<~500 LOC), specialized modules grouped by feature and purpose over large files or swiss-army classes.
- Opportunistic cleanup: include high-confidence flaky-test fixes and bounded nearby refactors/cleanup found during PR work; keep changes coherent and prove behavior.
- Before writing code, strictly follow the below research rules

## Documentation

- Logic changes must update any docs in `docs/` that describe the affected behavior.

## Research

- Check for and prefer available skills over web research.
- Prefer researched knowledge over your own knowledge when skills are unavailable.
- Always use Context7 MCP when I need library/API documentation, code generation, setup or configuration steps without me having to explicitly ask.
- Always use Exa MCP for general search.
- Always use GitHits MCP for open source examples
- Best results: Quote exact errors; prefer late-2025/2026+ sources.

## UI

- When the repository uses a component library (eg. shadcn, BoardUI, custom library), reuse its components instead of reimplementing them. If the appropriate component is unclear, stop and ask before implementing.
- When no UI/UX direction is provided, use Mobbin MCP for inspiration. If multiple designs fit, stop and ask to choose before implementing.
- Strictly use `@hugeicons/core-free-icons`. Nothing else. If you come across lucide-react or similar, replace it.

## Bugs

- Add regression test when it fits

## PR and CI

- Before starting a task, rebase the working branch onto `main` to avoid working on stale code.
- Merge a PR only when explicitly requested; otherwise leave it unmerged.
- GitHub work: use matching workflow. Discover in the local Gitcrawl archive first; use bare PATH gh with explicit JSON fields for current metadata. PR refs use gh pr view/diff, not web search.
- Pasted GitHub issue/PR: first git status -sb. Dirty: report before mutation. URL alone grants no push/pull permission.
- PR: prefer fix/rewrite PR then merge, not close + duplicate direct commit.
- PR quality: assume generated code may come from weaker AI. Review/improve before land; full rewrite okay when cleaner.
- UI change PR: include before/after pictures. Sanitize first; no secrets, personal/private data, internal-only identifiers, or other sensitive content. Unsafe capture: state blocker; never upload.
- PR/issue media: pass repeatable `--attach '<file>#<alt text>'` to `gh issue create|edit|comment` or `gh pr create|edit|comment`; images and video only. Use a prerelease asset or repository-approved artifact store for other files.
- CI logs: fetch once per failed run; reuse printed output. One `gh search`/`list --json` over per-item view loops; narrow fields, exact refs.
- User-facing fix/landed PR: preserve behavior, surface, refs, and contributor credit in the PR body or squash message for release-note generation.
- Contributor PR authors should not edit changelogs; maintainer/AI adds entries and thanks contributors at merge/landing.
- Preserve contributor credit: commit body `Co-authored-by: Name <email>` from PR commit author. Changelog entries thank `@login` for user-visible work when added: at landing by default, at release generation only for `openclaw/openclaw`.
