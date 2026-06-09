# 2. Merge by non-destructive redirect pointer, depth-1

Date: 2026-06-09

## Status

Accepted

## Context

Merge/unmerge is the product's central judgment call, and unmerge is a first-class safety
net for a wrong "these are the same" decision (see the PRD and CONTEXT.md). The data shape
has to make reversal cheap and lossless. Two families were on the table:

- **Destructive / relocate-and-soft-delete** — on merge, rewrite the duplicate's votes and
  comments to point at the survivor, then tombstone the duplicate. (This is what a colleague's
  real-world implementation does.) Reversal requires remembering which rows originally came
  from the duplicate, and merging can create double-votes (an identity that voted on both)
  that must be detected and dropped.
- **Non-destructive redirect pointer** — on merge, change nothing about the votes/comments;
  set one field on the request.

## Decision

A request carries a nullable `merged_into` pointer to its survivor. **Merge** sets that
pointer and nothing else — the duplicate's votes and comments are left untouched, still
referencing the duplicate. The survivor's demand signal is **aggregated at read time**:
its vote count is `COUNT(DISTINCT identity)` across the survivor and every request pointing
at it; its comment list is the union of the same set. The duplicate's page redirects to the
survivor, so any vote/comment posted after the merge lands natively on the survivor.
**Unmerge** clears the pointer — the duplicate returns to the board with exactly the votes
and comments it had at merge time, because they were never moved. Activity added during the
merged window stays on the survivor (that is where it was actually posted).

Merges are constrained to **at most one level deep**. Enforced at merge time by two guards:
the survivor must be a root (`merged_into IS NULL`), and the duplicate must be a leaf (it has
no incoming pointers — a survivor cannot itself be merged away). The graph is therefore always
a flat star, never a chain.

## Consequences

- Unmerge is a single-field write; no origin-tracking columns, no reconstruction, no
  double-vote cleanup. The dedup is inherent in `COUNT(DISTINCT identity)`.
- Vote counts and comment lists are **derived, not stored** — every read walks the merged set
  (`WHERE id = :s OR merged_into = :s`, one hop). Trivial at learning scale; denormalizable
  later if it ever matters.
- Depth-1 keeps every read one hop and every unmerge one edge, avoiding recursive CTEs and
  depth management. The cost: you cannot merge a request that already has duplicates into a
  third request in one move — you must unmerge its duplicates first. Rare; surfaced as a clear
  error. Chains and bulk merge are deliberately out, consistent with the PRD cut-line.
