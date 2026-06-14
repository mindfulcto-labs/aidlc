# Contributing

Pull requests are welcome. The bar is operator-tested over comprehensive.

## What gets merged

- A correction to a fact in `AIDLC.md` that I can verify against a public source. Cite the source in the PR body.
- A typo, a grammar fix, a link rot fix.
- A new resource for a `paths/*` directory, only if it meets all four conditions:
  1. The PR author has read or watched the resource themselves.
  2. The resource is publicly accessible (no paywalls behind sales funnels).
  3. The annotation is one sentence and explains *why* it earns its slot, not just *what* the resource covers.
  4. Adding the resource does not push the path past its slot count. If the path is full, the PR has to propose what comes out.

## What does not get merged

- A resource added without an annotation, or with an annotation that paraphrases the title.
- A vendor brochure, a sales-deck PDF, or a video gated behind an email capture.
- Any addition to the substrate table in `AIDLC.md` §3. The five-substrate set is intentional. New substrates are a quarterly review conversation, not a PR.
- Edits that introduce em-dashes, the words "transformative", "leverage", "robust", "world-class", or rule-of-three lists. These are pre-commit-hook flagged on the maintainer's side; PRs hit the same bar.

## What to expect on review

Most PRs get a response within a week. Substantive PRs sometimes get a counter-proposal where I argue for a slightly different shape; that is not personal, it is the editorial line.

Resource-addition PRs are easier to merge than prose-revision PRs because the prose is opinion-anchored. If a prose revision is large enough to constitute a substantive disagreement, please open an issue first.

## What to call the issue or PR

The repo follows boring conventional-commit-style prefixes: `docs:`, `fix:`, `add:`, `remove:`, `chore:`. The prefix is not enforced by CI; it is just easier to scan the log.

## What this is not

This is not a place to add your own AI tool, vendor brochure, course, or product. Vendor self-promotion gets closed without merge. If you genuinely think your tool belongs in a path, get someone else to add it; that filter usually clarifies whether it actually belongs.
