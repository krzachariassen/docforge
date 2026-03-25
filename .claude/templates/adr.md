# Architecture Decision Record Template

For documenting specific technical decisions: library choices, pattern adoption, API design decisions, infrastructure selections.

**Audience**: Current and future engineers on the team. They want to understand what was decided, why, and what alternatives were considered. The most important reader is the engineer 18 months from now who asks "why did we do it this way?"

**Typical depth**: 500–2,000 words. ADRs should be short and focused — one decision per record. If you're writing more than 2,000 words, you might need an RFC instead.

**Human contribution required**: ADRs need the human to articulate the decision context and the alternatives they actually considered. The AI can structure and fill in consequences, but the decision rationale comes from the human.

---

## Core Sections

### Title
Format: `ADR-NNN: [Decision Title]`. The title should be a short declarative statement of the decision. "Use PostgreSQL for user data" not "Database decision."

### Status
One of: **Proposed** / **Accepted** / **Deprecated** / **Superseded by ADR-NNN**

### Context
What situation or problem led to this decision? Include:
- The technical context (what system, what constraint)
- The forces at play (competing requirements, trade-offs)
- Any time pressure or constraints that influenced the decision

Be specific enough that a reader unfamiliar with the project can understand the decision space.

### Decision
What was decided, stated as a clear, unambiguous declaration. "We will use X for Y" not "We are considering X."

If the decision has conditions or caveats, state them: "We will use X for Y, with the constraint that Z."

### Consequences
What follows from this decision? Both positive and negative:
- **Benefits**: What this enables or improves
- **Costs**: What this makes harder, more expensive, or impossible
- **Obligations**: What we now must do (maintain, monitor, migrate)

Be honest about costs. An ADR that only lists benefits is not trustworthy.

### Alternatives Rejected
For each alternative that was seriously considered:
- **What**: Brief description
- **Why rejected**: Specific reason — not just "it didn't fit." What trade-off made it worse than the chosen option?

## Optional Sections

### Implementation Notes
Brief guidance on how the decision should be implemented. Not a full design — just enough to prevent misinterpretation.

### Review Date
When should this decision be revisited? Some decisions are permanent; others should be re-evaluated when conditions change.

---

## Format Guidance

- **Keep it short.** The value of an ADR is that it's concise enough to actually be read.
- **Use tables** if comparing more than two alternatives across multiple dimensions.
- **One decision per ADR.** If you're documenting multiple decisions, create multiple ADRs.
- **Link to related ADRs** if this decision builds on or supersedes a previous one.
