# Architecture Decision Record (ADR) Template

For significant technical decisions: technology choices, design patterns, API contracts, anything future engineers need to understand.

**Audience**: Engineers (current and future) who need to understand why a decision was made, what alternatives were considered, and what consequences to expect. Short and direct — an ADR that takes more than 10 minutes to read is too long.

---

## Sections

### Title
`ADR-[number]: [Decision in one line]`
Example: `ADR-042: Use event sourcing for the payments ledger`

### Status
**Proposed** | **Accepted** | **Deprecated** | **Superseded by ADR-N**

### Context
What situation or problem forced this decision? Technical or organizational constraints in play. What happens if no decision is made. Why now. Keep to 2–4 paragraphs.

### Decision
State clearly: "We will..." or "We have decided to..."

Then explain the reasoning: why this option over the alternatives. Reference trade-offs honestly.

### Consequences
- **Positive**: What becomes easier, faster, or more reliable?
- **Negative**: What becomes harder or more constrained? What future options close off?
- **Neutral**: What changes but is neither better nor worse?

### Alternatives Rejected
For each seriously-considered alternative: what it was, why it was not chosen. Do not list alternatives you didn't seriously consider.
