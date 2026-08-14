#process #architecture #documentation #adr

A lightweight template for recording a non-trivial architectural decision so future readers understand why the system looks the way it does, not just what it does.

## Template

``` markdown
# <Short Decision Title>

## Context

What situation forced this decision? What was breaking down, what constraint or requirement made the status quo untenable. Describe the problem, not the solution.

## Decision

What was decided, and the reasoning for choosing this option over the alternatives considered.

## Status

Proposed / Accepted / Superseded (link to the superseding ADR if so).

## Consequences

What gets better, what gets worse or harder as a direct result of this decision. Be honest about the trade-offs, not just the upside.

## Next Steps

Follow-up work this decision unblocks or requires, so it doesn't get lost once the immediate change ships.
```

## Guidance

- Write the Context section assuming the reader has none of the tribal knowledge that led to the meeting where this was decided.
- One ADR per decision, don't bundle unrelated decisions to save a file.
- Keep old ADRs immutable once accepted, a changed decision gets a new ADR that supersedes the old one, don't edit history.
- Store ADRs in one place in the repo (e.g. an `adr/` folder) numbered sequentially, so the decision history reads chronologically.
