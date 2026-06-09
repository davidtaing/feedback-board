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
- **Vote** — a demand signal on a request; one per identity per request. The vote count is the
  ranked demand signal.
- **Comment** — a flat, public note on a request carrying a user's words and intent. Thin by
  design (no threading, no internal/pinned) — present only because merge relocates these words.
- **Status** — lifecycle state of a request: Under Review → Planned → In Progress → Complete,
  plus the graveyard state **Won't do**.
- **Graveyard / resolution note** — closing a request into a "Won't do" state, which requires a
  public **resolution note**: the structured, honest "no." The honesty lives in the status
  taxonomy + this public copy, not in a notification.
- **Merge** — declaring two requests the same and collapsing the duplicate into a surviving
  request: votes sum, comments roll up, the duplicate redirects. The irreducibly subjective
  call at the heart of the product.
- **Unmerge** — reverses a merge; the safety net for a wrong "same" call. **Merge is reversible.**
- **Roadmap** — the single public view organizing requests by status; the commitment surface.
  A request's place on it follows its status.

## Open modeling questions

_Deferred to the technical grill (`grill-with-prd`) — these are data-shape, not why-level:_

- On **unmerge**, what happens to votes/comments added *after* the merge — to which request do
  they belong? (David flagged the unmerge data shape as a point of technical interest.)
- How are **simulated identities** represented (enough to enforce one-vote-per-identity without
  real auth)?
- Is the **resolution note** a field on the request, on the status transition, or its own record?
