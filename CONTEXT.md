# Context

Domain language and the working model for feedback-board. Kept current as decisions
land (via grilling sessions / ADRs). This is the shared vocabulary — when a term here
and a term in the code disagree, one of them is wrong.

## Domain glossary

> _Why-level terms settled in the product grill (see [docs/prd/feedback-board-mvp.md](docs/prd/feedback-board-mvp.md)).
> Data-shape questions are deferred to the technical grill (`grill-with-prd`)._

- **Board** — the single public board that holds all requests. No multiple/private boards in
  the MVP (out of scope). The board *is* the public surface.
- **Request** — a tracked feedback item on the board. There is **no separate `Submission`**: a
  post lands directly on the board as a request (no triage inbox). "Post" and "request" are the
  same thing.
- **Identity** — a seeded, simulated actor on the board (no real auth). Carries a `role` of
  **customer** (posts, votes, comments) or **admin** (status moves, graveyard, merge/unmerge).
  The current identity is chosen via a switcher and held in a cookie — "choosing a hat," not
  logging in. The instrument that gives the judgment calls stakes (believable people filing
  near-duplicates).
- **Vote** — a demand signal on a request; one per identity per request (enforced by a unique
  constraint). The vote count is the ranked demand signal.
- **Comment** — a flat, public note on a request carrying a user's words and intent. Thin by
  design (no threading, no internal/pinned) — present only because merge relocates these words.
- **Status** — lifecycle state of a request: Under Review → Planned → In Progress → Complete,
  plus the graveyard state **Won't do**.
- **Graveyard / resolution note** — closing a request into a "Won't do" state, which requires a
  public **resolution note**: the structured, honest "no." The honesty lives in the status
  taxonomy + this public copy, not in a notification.
- **Merge** — declaring two requests the same and redirecting the **duplicate** into a
  **survivor**. Non-destructive: the duplicate keeps its own votes and comments untouched; the
  survivor's vote count and comment list are *aggregated across itself and its merged
  duplicates* (votes deduped by identity). The duplicate's page redirects to the survivor, so
  new votes/comments land on the survivor. The irreducibly subjective call at the heart of the
  product.
- **Survivor / duplicate** — the two roles in a merge: the surviving request that stays on the
  board, and the merged-away duplicate that redirects to it. Merges are **at most one level
  deep** — a duplicate cannot itself be a survivor, and a survivor cannot be merged away — so
  every duplicate points directly at a live survivor (no chains).
- **Unmerge** — reverses a single merge by detaching one duplicate from its survivor; the
  duplicate returns to the board carrying exactly the votes and comments it had at merge time.
  The safety net for a wrong "same" call. **Merge is reversible.** Votes and comments added
  *after* a merge belong to whichever request they were posted to — the survivor, since the
  duplicate redirected — and **stay on the survivor** when the merge is reversed.
- **Roadmap** — the single public view organizing requests by status; the commitment surface.
  A request's place on it follows its status.

## Open modeling questions

_Deferred to the technical grill (`grill-with-prd`) — these are data-shape, not why-level:_

- ~~On **unmerge**, what happens to votes/comments added *after* the merge?~~ **Resolved:** they
  belong to the request they were posted to (the survivor, via redirect) and stay there on
  unmerge; the duplicate returns with only what it had at merge time. Merge is a non-destructive,
  depth-1 redirect — see Merge/Survivor/Unmerge above and [docs/adr/0002-merge-by-redirect-pointer.md](docs/adr/0002-merge-by-redirect-pointer.md).
- ~~How are **simulated identities** represented?~~ **Resolved:** a seeded `identity` table with
  a `customer`/`admin` role; current selection held in a cookie via a switcher; votes enforce
  one-per-identity with a `(request_id, identity_id)` unique constraint. See **Identity** above.
- _(open)_ Is the **resolution note** a field on the request, on the status transition, or its
  own record?
