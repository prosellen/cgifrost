# Issue tracker: GitHub

Issues and specs for this repo live as GitHub issues in `prosellen/cgifrost`. Use the `gh` CLI for all operations.

## Conventions

- **Create an issue**: `gh issue create --repo prosellen/cgifrost --title "..." --body "..."`. Use a heredoc for multi-line bodies.
- **Read an issue**: `gh issue view <number> --repo prosellen/cgifrost --comments`, filtering comments by `jq` and also fetching labels.
- **List issues**: `gh issue list --repo prosellen/cgifrost --state open --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'` with appropriate `--label` and `--state` filters.
- **Comment on an issue**: `gh issue comment <number> --repo prosellen/cgifrost --body "..."`
- **Apply / remove labels**: `gh issue edit <number> --repo prosellen/cgifrost --add-label "..."` / `--remove-label "..."`
- **Close**: `gh issue close <number> --repo prosellen/cgifrost --comment "..."`

## Pull requests as a triage surface

**PRs as a request surface: no.** _(Set to `yes` if this repo treats external PRs as feature requests; `/triage` reads this flag.)_

When set to `yes`, PRs run through the same labels and states as issues, using the `gh pr` equivalents.

## When a skill says “publish to the issue tracker”

Create a GitHub issue in `prosellen/cgifrost`.

## When a skill says “fetch the relevant ticket”

Run `gh issue view <number> --repo prosellen/cgifrost --comments`.

## Wayfinding operations

Used by `/wayfinder`. The map is a single issue with child issues as tickets.

- **Map**: a single issue labelled `wayfinder:map`, holding the Notes / Decisions-so-far / Fog body.
- **Child ticket**: a GitHub sub-issue linked to the map, labelled `wayfinder:<type>` (`research`/`prototype`/`grilling`/`task`). Where sub-issues are unavailable, add `Part of #<map>` at the top of the child body.
- **Blocking**: use GitHub’s native issue dependencies where available; otherwise use a `Blocked by: #<n>, #<n>` line at the top of the child body.
- **Frontier query**: list the map’s open children, drop any with an open blocker or assignee, and take the first in map order.
- **Claim**: `gh issue edit <n> --repo prosellen/cgifrost --add-assignee @me`.
- **Resolve**: comment with the answer, close the issue, then append a context pointer to the map’s Decisions-so-far.
