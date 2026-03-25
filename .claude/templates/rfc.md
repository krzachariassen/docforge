# RFC Template

For Request for Comment documents: technical design proposals, API changes, infrastructure decisions, process changes affecting multiple teams.

**Audience**: Engineers and technical leads who will implement, integrate with, or be affected by this change. They want technical specificity, clear trade-off analysis, and explicit consideration of alternatives. They will ask "why not X?" — answer it before they do.

---

## Sections

### Summary
One paragraph. What are you proposing and why? Enough for a reviewer to understand scope before reading details.

### Motivation
What problem are you solving? Current behavior and costs. Concrete examples (real cases, not hypotheticals). Why now vs. later.

### Proposed Solution
The full technical design: how it works (system model, data flow, interfaces), key design decisions and reasoning, examples (code snippets, API signatures, config as appropriate), what changes for existing users.

### Alternatives Considered
**Required.** For each alternative: what it is, why it was considered, why it was not chosen. At minimum: "doing nothing" and the most obvious alternative to your proposal.

### Design Details
Additional technical depth: implementation notes, edge cases, error handling, performance characteristics.

### Trade-offs
What does this proposal give up? Name costs honestly: what gets more complex, what it won't support, what you're uncertain about.

### Migration / Rollout Plan
How do we get from here to there? Phases, backward compatibility, how existing users migrate, feature flags and gradual rollout.

### Rollback Plan
If this goes wrong: rollback triggers, rollback procedure, what state changes would be permanent.

### Open Questions
Unresolved questions for reviewers. Tag with decision owner if known.
