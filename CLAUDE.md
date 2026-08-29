# mech-interp-tinkering — agent instructions

Quarto site published at <https://xavierdurawa.github.io/mech-interp-tinkering/>. Source on
`main`, rendered output on `gh-pages`. Posts are pure markdown (`posts/<slug>/index.qmd`) — no
executable cells, no venv, nothing to fetch.

## Publishing: ALWAYS `git pull` before `quarto publish`

**There are two publishers, and that is deliberate.**

1. `.github/workflows/publish.yml` renders on every push to `main` and deploys to `gh-pages`.
2. Agents also run `quarto publish gh-pages` by hand.

**The hazard.** `quarto publish` renders from the **local working copy**. `gh-pages` holds
generated output, so git reports no conflict and **the last publisher silently wins**. Posts can
be edited directly from the published page (the "Edit this page" link added by `repo-actions`),
which commits straight to remote `main`. If this checkout hasn't pulled that commit, publishing
renders stale source and **silently reverts the live page** — no error, no warning. The commit
stays safe in `main`'s history; only the published site regresses, and nothing surfaces it.

**So:**

- **`git pull` immediately before any `quarto publish`.** Not optional.
- After pulling, **re-read any changed `.qmd`** — a browser edit is a real content change you
  have not seen.
- Often you don't need to publish at all: pushing to `main` triggers the workflow, which renders
  from the remote and is therefore never stale. Prefer that.
- `quarto render` and `quarto preview` are local-only and safe any time (`_site/` is gitignored).

A `PreToolUse` hook (`~/.claude/hooks/quarto-publish-guard.py`, registered in
`~/.claude/settings.json`) fetches and blocks `quarto publish` when this checkout is behind its
upstream. It is a backstop, not a substitute for pulling — and it is machine-local, so it will not
protect a clone on another machine.

## Writing posts

Voice is colloquial and first-person; negative results are shippable and often the point (see
`posts/plans-read-just-in-time/` and `posts/fv-not-legible/`). Setup framing is brief — enough
that a reader could approximately recreate the work, not a methods section.

**Every number in a post must be traceable to raw result JSON in the originating project repo,
and re-verified against it before publishing.** Report effect sizes and n; be sparing with
p-values — an over-powered continuous measure makes them uninformative, and one previously
published p-value could not be reproduced because its endpoint was never pinned. See
`~/Personal/research_kb/landmines.md` §3.
