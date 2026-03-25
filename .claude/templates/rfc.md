# RFC Template

For technical proposals that need team or cross-team review: new systems, protocol changes, architectural decisions, process changes.

**Audience**: Engineers and tech leads. They want precise technical detail, honest trade-off analysis, and enough information to evaluate alternatives. They will challenge hand-waving and missing edge cases.

**Typical depth**: 2,000–6,000 words. Deep enough to evaluate, not so long that reviewers skip sections.

**Human contribution required**: RFCs need the human to provide technical specifics — interface definitions, schema examples, benchmark data. The AI can structure the argument and fill in analysis, but the core technical design comes from the human.

---

## Core Sections

### Summary
One paragraph. What's being proposed and why. A reader who stops here should understand the change and its motivation.

### Motivation
Why is this change needed? What's broken, missing, or suboptimal? Be specific — name the system, the failure mode, the cost. Include data if available.

### Proposed Solution
The technical design. Use sub-sections for complex proposals:
- **Overview**: How it works at a high level
- **Design details**: Data models, interfaces, protocols, algorithms
- **Key decisions**: Why this approach over alternatives (brief — detailed analysis goes in Alternatives Considered)

### Alternatives Considered
For each alternative: what it is, its advantages, and why it was rejected. Be fair — if an alternative was close, say so. This section builds trust.

### Design Details
Deep technical specifics. This is where code examples, schema definitions, interface contracts, and protocol descriptions go. Use code blocks and tables.

### Trade-offs
What does this proposal sacrifice? Performance vs. complexity? Consistency vs. availability? Flexibility vs. safety? Name the trade-offs explicitly and explain why the chosen trade-off is acceptable.

### Migration / Rollout Plan
How do we get from here to there? Phased rollout, feature flags, backward compatibility. Address: what happens to existing data, existing clients, and existing behavior.

### Rollback Plan
How do we undo this if it goes wrong? Be specific — not "we can roll back" but "revert commit X, restore config Y, run migration Z."

### Open Questions
Unresolved decisions the RFC is surfacing for discussion. Number them. Each should be a real question, not a rhetorical one.

## Optional Sections

### Performance Analysis
Benchmarks, load testing results, capacity planning. Use tables for comparisons.

### Security Considerations
New attack surfaces, access control changes, data handling implications.

### Appendix: Interface Definitions
Full protobuf/IDL definitions, API contracts, or schema definitions that would interrupt the main flow.

---

## Recommended Drafting Order

For complex RFCs, use sectional drafting:

**Round 1** — The proposal: `sections:summary,motivation,proposed-solution`
Draft the problem and the proposed design. The human reviews before the detail sections are written.

**Round 2** — The details: `sections:alternatives-considered,design-details,trade-offs`
The technical depth. The human may need to add interface definitions or benchmark data via grounding files between rounds.

**Round 3** — The plan: `sections:migration,rollback,open-questions` + any optional sections
The execution and operational details.

---

## Format Guidance

- **Use code blocks** for anything the reader needs to see exactly: APIs, schemas, configs, commands.
- **Use tables** for alternative comparisons, trade-off matrices, and migration phase summaries.
- **Use ASCII diagrams** for system interactions, data flows, and sequence diagrams.
- **Be precise about scope.** RFCs that try to solve everything get rejected. Narrow scope = faster approval.
