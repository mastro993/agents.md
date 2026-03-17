# AGENTS.md

Version: 0.01 (2026-03-17)

Work style: Be radically precise. No fluff. Pure information only (drop grammar; min tokens).

## Agent Protocol

- “Make a note” => edit AGENTS.md (Ignore `CLAUDE.md`, symlink for AGENTS.md).
- "Remember" (or similar) -> edit AGENTS.md under "User Notes"
- Editor: `code <path>`.
- New deps: quick health check (recent releases/commits, adoption).
- When asked to update the `AGENTS.md` to the latest version:
  1. Fetch `https://raw.githubusercontent.com/robinebers/agents.md/main/AGENTS.md`.
  2. Check if newer version version and merge without losing local changes.

## Guardrails

- Use `trash` for deletes.
- Use `mv` / `cp` to move and copy files.
- Bugs: add regression test when it fits.
- Keep files <~400 LOC; split/refactor as needed.
- Simplicity first: handle only important cases; no enterprise over-engineering/fallbacks.
- New functionality: small OR absolutely necessary.
- NEVER delete files, folders or other data unless explicilty approved or part of a plan.
- Before writing code, stricly follow the below research rules

## Plan Mode

- Make the plan extremely concise. Sacrifice grammar for the sake of concision.
- At the end of each plan, give me a list of unresolved questions to answer, if any.
- Ask me questions until you have at least a 90% understanding of the plan.

## Research

- Prefer skills if available over research.
- Prefer researched knowledge over existing knowledge when skills are unavailable.
- Research: Exa to websearch early, and Ref to seek specific documention or web fetch.
- Best results: Quote exact errors; prefer 2025-2026+ sources.

## Git

- Always use `gh` to communicate with GitHub.
- GitHub CLI for PRs/CI/releases. Given issue/PR URL (or `/pull/5`): use `gh`, not web search.
- Examples: `gh issue view <url> --comments -R owner/repo`, `gh pr view <url> --comments --files -R owner/repo`.
- Conventional branches (`feat|fix|refactor|build|ci|chore|docs|style|perf|test`).
- Safe by default: `git status/diff/log`. Push only when user asks.
- `git checkout` ok for PR review / explicit request.
- Branch changes require user consent.
- Destructive ops forbidden unless explicit (`reset --hard`, `clean`, `restore`, `rm`, …).
- No repo-wide S/R scripts; keep edits small/reviewable.
- Avoid manual `git stash`; if Git auto-stashes during pull/rebase, that’s fine (hint, not hard guardrail).
- If user types a command (“pull and push”), that’s consent for that command.
- Big review: `git --no-pager diff --color=never`.

## Error Handling

- Expected issues: explicit result types (not throw/try/catch).
  - Exception: external systems (git, gh) → try/catch ok.
  - Exception: React Query mutations → throw ok.
- Unexpected issues: fail LOUD (throw/console.error + toast.error); NEVER add fallbacks.

## Backwards Compat

- Always minimum only, you typically overthink this. Keep things simple.
- When in doubt, ask the user before you overengineer solutions.

## Critical Thinking

- Fix root cause (not band-aid).
- Unsure: read more code; if still stuck, ask w/ short options (A/B/C).
- Conflicts: stop. call out; pick safer path.
- Unrecognized changes: assume other agent; keep going; focus your changes. If it causes issues, stop + ask user.

## Completion and Autonomy Gate

- Assume "continue" unless the user explicitly says "stop" or "pause".
- Do not ask "should I continue?" or similar questions.
- If more progress is possible without user input, continue.
- BEFORE you end a turn or ask the user a question, run this checklist
  -- Answer these privately, then act:
  1.  Was the initial task fully completed?
  2.  If a definition-of-done was provided, did you run and verify every item?
  3.  Are you about to stop to ask a question?
      - If yes: is the question actually blocking forward progress?
  4.  Can the question be answered by choosing an opinionated default?
      - If yes: choose a default, document it in , and continue.
- When you choose opinionated defaults, document them in `/docs/choices.md` as you work.
- Leave breadcrumb notes in thread and `/docs/breadcrumbs.md`.
- When writing to `/docs/choices.md` or `/docs/breadcrumbs.md` categorize by date (tail)
- If you must ask the user:
  -- Ask exclusively blocking question only.
  -- Explain why it is blocking and what you will do once answered.
  -- Provide your best default/assumption as an alternative if the user does not care.

## Useful Tidbits

- When using Convex, run `pnpm convex dev --once` to verify, not `pnpm convex codegen`.
- When tasked to use the computer, prefer simple screenshot/mouse pointer events over accessibility.

## UI

Avoid “AI slop” UI. Be opinionated + distinctive.

Do:

- Typography: pick a real font; avoid Inter/Roboto/Arial/system defaults.
- Theme: commit to a palette; use CSS vars; bold accents > timid gradients.
- Motion: 1–2 high-impact moments (staggered reveal beats random micro-anim).
- Background: add depth (gradients/patterns), not flat default.

Avoid: purple-on-white clichés, generic component grids, predictable layouts.

## User Notes

Use below list to store and recall user notes when asked to do so.

- (Replace this one when asked for first note)
