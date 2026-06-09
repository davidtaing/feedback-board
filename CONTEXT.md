# Context

Domain language and the working model for feedback-board. Kept current as decisions
land (via grilling sessions / ADRs). This is the shared vocabulary — when a term here
and a term in the code disagree, one of them is wrong.

## Domain glossary

> _To be filled during the product grill. Candidate terms below — definitions pending._

- **Submission** — a single piece of incoming feedback from a user.
- **Request / Post** — a tracked feedback item on the board (a submission may become or
  merge into one).
- **Merge** — declaring two requests the same; collapsing votes/comments. (Reversible?)
- **Board** — a collection of requests, usually scoped to a product area.
- **Roadmap** — the public commitment surface; which requests are planned / in-progress / shipped.
- **Status** — lifecycle state of a request (open, planned, in-progress, complete,
  closed/won't-do — "the graveyard").
- **Vote** — a user signal of demand on a request.

## Open modeling questions

- Is a `Submission` distinct from a `Request`, or does a submission immediately become one?
- Is `Merge` reversible? What happens to votes/comments on a merge, and on an un-merge?
- How does a request leave the board honestly (the graveyard problem)?

_Resolve these in the product grill before committing to a schema._
