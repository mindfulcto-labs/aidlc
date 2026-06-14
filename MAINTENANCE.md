# Maintenance

## Cadence

Quarterly review. Every path's `README.md` carries a `last_reviewed` date in its front-matter. When the date is more than four months old, the file is up for review at the next quarter boundary.

Substantive revisions to `AIDLC.md` update the `Last revised` date at the top of the document. The `CHANGELOG.md` records the change with a one-line summary.

## Budget

10 hours per week sustained across the whole portfolio, of which roughly:

- 4 hours: path curation (new entries, refreshes, removals).
- 3 hours: playbooks (new ones, updates to shipped ones).
- 2 hours: reading-list maintenance, link-rot checks.
- 1 hour: issues, PR review, replies.

The budget shrinks to about 5 hours per week once all five paths and the planned playbooks have shipped v0.1.

## Removal policy

A resource leaves a path under any of the following conditions:

- The link is broken and no archive is available.
- The author retracted or amended the work in a way that breaks the original framing.
- A clearly better resource on the same subtopic earns the slot.
- The subtopic itself loses operator relevance (rare, but the substrate runtimes change).

Removals get recorded in `notes.md` for the affected path, with the date and a one-line reason. The `CHANGELOG.md` mirrors the removal. Silent disappearance is the abandonment signal we are explicitly avoiding.

A whole path leaves the repo if the operator brief drifts away from it. Archived paths move to `paths/archive/` with a one-paragraph eulogy noting what replaced them. Five paths is the hard ceiling; the sixth never arrives without the weakest leaving first.

## Stale-signal triggers

- A path's `last_reviewed` is older than six months. Immediate review.
- A tool named in a path goes EOL, pivots, or has its company acquired in a way that changes the substrate. Same-day note in `notes.md`, full review at next quarter.
- A regulation cited gets amended (e.g. EU AI Act secondary legislation, ISO 42001 amendment). Update the `paths/02-ai-governance` references and the `AIDLC.md` §4 mappings within two weeks.
- A reader-filed issue flags a broken link, a factual drift, or a missing alternative resource. Triage weekly.

## What "in good order" looks like

- Every path file's `last_reviewed` is within four months.
- The `CHANGELOG.md` shows entries every two weeks at least.
- Open issues are under five at any quarter boundary.
- Median PR-to-decision time is under ten days.

If two of these slip simultaneously, the right move is to archive a path or a playbook, not to add more.
