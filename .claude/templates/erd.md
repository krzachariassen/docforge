# Engineering Review Document (ERD) Template

For detailed engineering designs that require review and approval: backend system changes, API redesigns, caching strategies, infrastructure changes, cross-team integrations, performance optimizations, new service architectures, data model changes.

ERDs are the most technically rigorous document type. They don't just propose a solution — they prove it's the best solution by evaluating alternatives against explicit criteria. The reader should be able to independently verify the engineering judgment: "given these constraints and trade-offs, this is the right choice."

**Audience**: Senior engineers, tech leads, and architecture reviewers. They will challenge your assumptions, probe your trade-off analysis, and stress-test your implementation plan. They want to see: alternatives genuinely considered, trade-offs explicit and honest, implementation detailed enough to estimate, and operational concerns addressed before shipping.

**Typical depth**: 3,000–10,000+ words. ERDs are the densest document type — architecture diagrams, proto definitions, code snippets, latency analysis, storage calculations, capacity projections, and step-by-step implementation plans. Every section earns its place through specificity.

**Human contribution required**: ERDs are deeply grounded in system internals. The human must provide: architecture context (how the system works today), current metrics (latency P50/P99, RPS, storage, error rates), proto/API definitions, code references, data analysis results, and any prior ERDs or design docs. Without this grounding, the ERD will be too generic to pass review. Save everything to `workspace/grounding/`.

---

## Core Sections

These sections appear in every ERD, in this order. **Do not reorder them.** The sequence is deliberate: summary → motivation → scope → current state → options → design → capacity → testing → operations → security → timeline → open questions.

### 1. Metadata
A structured header block:
- **Authors**: Who wrote this (names and handles)
- **Date**: When this was started
- **ERD/Project reference**: Link to parent initiative or project tracker
- **Project Summary**: One sentence — what this ERD proposes. Appears in doc indices.
- **System/Asset**: Which system, service, or platform this affects
- **Related documents**: Links to prior ERDs, abstracts, design docs, or RFCs that set context. Briefly note what each one covers (e.g., "[ERD] Rides Payment Bar — establishes the short-term architecture this ERD extends").

### 2. Motivation
Why this work matters and why now. Structure in three parts:

- **What it enables**: The capability, improvement, or unblock this ERD delivers. Be specific — not "improves performance" but "reduces payment selection P99 from 350ms to 150ms on the Rides product selector."
- **Quantified impact**: Concrete numbers. Latency reduction, conversion improvement, cost savings, error reduction, developer velocity gain. If you have data (e.g., "15% of user drop-offs traced to payment errors"), include it with the source. If you're estimating, say so and explain the basis.
- **Why now**: What makes this urgent? A dependent project blocked, a scaling cliff approaching, customer-facing degradation, a compliance deadline, or a strategic window closing. Without urgency, a reviewer will suggest deferring.

A reviewer who reads only this section should understand why the ERD was written and what's at stake if the work isn't done.

### 3. Scope & Non-Goals
Explicitly bound the design. This section prevents the review from expanding into adjacent problems.

**In scope**: What this ERD covers — the specific system behaviors, APIs, or flows that will change.

**Non-goals**: What this ERD explicitly does NOT address, even if related. For each non-goal:
- What it is
- Why it's deferred (not enough information, too much effort for this cycle, being addressed separately, not urgent enough)
- Whether it's blocked by this ERD's outcome or independent

Good non-goals pre-empt the "but what about..." questions that derail design reviews.

### 4. Current Architecture
How the system works today. This is the baseline against which all options are evaluated. A reviewer who doesn't know the system should understand the relevant parts after reading this section.

- **Architecture diagram**: ASCII diagram or reference to an external diagram (Lucidchart, Miro, etc.) showing the components, data flows, and integration points relevant to this ERD. Label every component and every arrow.
- **Key components**: Brief description of each component's role in the flow this ERD will change. Don't describe the entire system — only what's relevant.
- **Current behavior**: Step-by-step: how does the system handle the specific flow(s) this ERD will modify? "When a user opens the product selector, MOP calls PaySel, which calls UCR and WAG, which returns..."
- **Current metrics**: Latency (P50/P99), throughput (RPS), storage, error rates — whatever is relevant to evaluating the proposed change. Include the source (dashboard, monitoring tool, analysis query). These numbers are the baseline your design will be measured against.

### 5. Current Challenges
The specific technical problems or limitations this ERD addresses. Separate from Motivation (which explains why the work matters) — this section explains what's technically wrong.

Number each challenge. For each:
- **Title**: Short descriptive name
- **Description**: What's wrong, with system names, field names, specific numbers
- **Impact**: How this challenge manifests — latency spikes, cache misses, blocked features, inconsistent behavior
- **Root cause**: Why the current architecture has this problem (design decision, organic growth, changed requirements)

Understanding root causes helps reviewers evaluate whether the proposed design truly fixes the problem or just masks it.

### 6. Options Analysis
The heart of the ERD. This is where the engineering judgment lives. Present 3–5 options with explicit, honest trade-offs evaluated against consistent criteria.

**Before listing options, define your evaluation criteria.** State the 4–6 dimensions that matter most for this decision. Common dimensions:
- Latency impact (P99)
- Implementation effort (weeks/sprints)
- Cross-team dependencies
- Backward compatibility
- Future extensibility
- Operational complexity
- Data consistency guarantees

**For each option:**
- **Title**: Descriptive name that captures the approach (not "Option 1" but "Cache at gateway layer" or "Move L7 eligibility under PaySel")
- **How it works**: Enough technical detail to evaluate the approach — architecture changes, data flow, API modifications. Include a brief diagram if the architecture differs significantly from the current state.
- **Pros**: Specific, concrete advantages. Not "simpler" but "no changes to downstream APIs, all changes contained within PaySel service." Each pro should reference an evaluation criterion.
- **Cons**: Specific, honest disadvantages. Not hedged or minimized — if an option has a real weakness, state it plainly. Each con should reference an evaluation criterion.
- **Verdict**: One of:
  - **Recommended** — this is the proposed option (exactly one)
  - **Viable but not recommended** — could work, but the recommended option is better on the criteria that matter most (say which ones)
  - **Excluded** — not feasible or not acceptable (say why specifically)

**After all options, include a comparison table** showing each option scored or rated against the evaluation criteria. This makes the decision transparent and auditable.

**Mark the preferred option clearly** and write 2–3 sentences summarizing why it wins: on which criteria does it outperform, and what trade-offs are you accepting?

### 7. Proposed Design
Detailed implementation of the recommended option. This is where the ERD becomes buildable. A senior engineer reading this section should be able to create tickets from it.

Structure with numbered sub-sections for each major area:

- **7.1 API Changes**: Proto definitions, struct changes, new fields, modified endpoints. **Show the actual code** — proto messages, Go interfaces, Thrift structs. Not descriptions of what they look like, but the definitions themselves. Annotate new or changed fields with comments explaining their purpose.
- **7.2 Data Flow**: How data moves through the system after the change. Include a diagram showing the new flow — label what's new vs. unchanged. If the flow varies by case (e.g., cache hit vs. miss, restricted vs. unrestricted products), show each path.
- **7.3 Key Design Decisions**: Specific choices within the implementation and their rationale. Cache key structure, TTL strategy, serialization approach, hashing algorithm, retry policy. For each: what you chose, what you considered, why this is right. These are the decisions a reviewer will challenge — justify them proactively.
- **7.4 Integration Points**: How upstream and downstream services interact with the change. For each service: what changes (if anything) in their calls, what new data they send or receive, what happens if they don't upgrade. Include backward compatibility analysis.
- **7.5 Error Handling & Edge Cases**: What happens when things go wrong? Cache misses, downstream timeouts, malformed input, partial failures. For each: the error condition, the expected behavior, and the user-facing impact (if any).

### 8. Capacity & Performance
Quantified impact on infrastructure. Show your math — reviewers will check it.

- **Latency**: Expected impact on P50/P99. Break down by call path if relevant (cache hit vs. miss, happy path vs. fallback). Compare to current metrics from section 4.
- **Throughput**: Expected RPS changes. Current vs. projected, broken down by endpoint or operation if relevant.
- **Storage**: Additional storage needed. Include the calculation: (record size) × (number of records) × (replication factor) × (TTL-based accumulation). Compare to current allocation.
- **Cost**: Infrastructure cost impact — additional instances, storage, bandwidth. Include current cost for context.
- **Scaling plan**: How to handle traffic ramp-up during rollout. Capacity provisioning timeline, auto-scaling configuration, or manual scaling steps.

### 9. Testing Strategy
How the design will be validated before and during rollout. This section is often the most questioned in reviews — an untested design is an unshipped design.

- **Unit tests**: What new test cases are needed? What invariants does the code need to maintain?
- **Integration tests**: How will the end-to-end flow be tested? What test environments are needed?
- **Load testing**: If the change affects latency or throughput, how will it be load-tested? Target RPS, duration, success criteria.
- **Shadow traffic**: Will the new path run in shadow mode alongside the existing path? How will results be compared?
- **Canary analysis**: What metrics will the canary monitor? What thresholds trigger a rollback?

Not every ERD needs all of these — but every ERD needs to address how the design is tested. Omitting testing strategy is a red flag.

### 10. Rollout & Migration
How the change gets to production, step by step.

**Rollout plan:**
- **Phases**: What happens in each phase — percentage of traffic, geography, or user segment
- **Feature flags**: What flags control the rollout, and what each flag does
- **Advancement criteria**: What must be true before moving to the next phase
- **Rollback procedure**: Exact steps to revert. Not "we'll roll back" but the specific sequence — disable flag, drain traffic, revert config, verify metrics. Include estimated rollback time.

**Data migration** (if applicable):
- Step-by-step migration sequence
- Verification approach at each step
- Rollback procedure specific to data changes
- Timing constraints (maintenance windows, low-traffic periods)
- What happens to in-flight requests during migration

### 11. Operational Readiness
Production operation after rollout. How does the team live with this change?

- **Observability**: What new metrics, dashboards, and log signals are needed? What existing dashboards need updating?
- **Alerting**: What new alerts are needed? Define thresholds and escalation paths. What false-positive risks exist?
- **SLOs**: Service level objectives for the new behavior — latency targets, availability targets, error rate budgets
- **Runbooks**: What new runbook entries are needed? Common failure scenarios and resolution steps.
- **On-call impact**: Does this change the on-call burden? New failure modes to watch for, new debugging procedures, new escalation paths.

### 12. Security & Compliance
Address even if brief. If truly not applicable, state why in one sentence rather than omitting.

- **Data handling**: What data is stored, cached, or transmitted differently? Is any of it PII, payment data, or otherwise sensitive?
- **Access control**: Who/what can access new data or endpoints? Are there authorization changes?
- **Compliance**: Any regulatory considerations — SOX, GDPR, PCI, data retention, audit requirements.
- **Threat model**: For changes that introduce new attack surfaces (new APIs, new data stores, new integrations), briefly describe the threat model and mitigations.

### 13. Open Questions
Unresolved items that need reviewer input or further investigation. For each:
- **Question**: What needs to be decided or investigated
- **Impact**: What part of the design is affected by this question
- **Proposed answer**: Your current thinking, if any
- **Who can resolve it**: The person or team who has the answer

This section is honest about what you don't know yet. It focuses the review discussion on the decisions that actually need input, rather than letting reviewers discover gaps on their own.

## Optional Sections

Include these when the brief's Structure Notes explicitly call for them. **Do not invent optional sections that aren't listed here or in the brief's Structure Notes.**

### Cross-Team Dependencies
When the implementation requires changes in services owned by other teams:
- **Dependency table**: Team, service, what's needed, timeline, status of alignment (agreed / in discussion / not yet contacted)
- **Risk**: What happens if a dependency isn't delivered on time — is there a degraded path?
- **Coordination plan**: How will cross-team work be tracked?

### Cost-Benefit Analysis
When the investment is significant enough to justify a formal cost analysis:
- **Costs**: Engineering time, infrastructure, ongoing maintenance
- **Benefits**: Quantified returns — time saved, errors prevented, revenue impact, cost reduction
- **Payback period**: When do the benefits exceed the costs?

### Appendices
- **Only create appendices called for by the brief's Structure Notes** or clearly demanded by the content.
- **Every appendix must be referenced from the main text.**
- **Common appendix types**: Full proto definitions (when too long for section 7), data analysis queries with results, latency measurement methodology, detailed capacity calculations, architectural comparison diagrams.

---

## Recommended Drafting Order

For Blueprint-depth ERDs, use sectional drafting. ERDs are heavily reviewed — getting the problem framing and options right early prevents wasted effort on implementation details.

**Round 1** — The case: sections 1–5 (Metadata, Motivation, Scope, Current Architecture, Challenges)
Establish the problem and baseline. The human reviews to confirm the framing is accurate, the architecture description is complete, and the challenges are correctly identified. This round often surfaces missing context that the human needs to add to grounding files.

**Round 2** — The options: section 6 (Options Analysis)
The most review-intensive section. Present all options with trade-offs. The human validates that the right options were considered, the evaluation criteria are the right ones, and the trade-off analysis is fair and honest. It's common for the human to add or modify options after this round.

**Round 3** — The design: sections 7–8 (Proposed Design, Capacity & Performance)
Detail the recommended option. The human reviews for completeness and adds any missing proto definitions, latency data, capacity calculations, or edge cases. This is also where integration point details often need human input.

**Round 4** — Ship readiness: sections 9–13 (Testing, Rollout, Operations, Security, Open Questions)
Everything needed to ship and operate the change. The human reviews for operational completeness and adds monitoring, alerting, and runbook details.

After all sections are drafted, run `/df-review` on the complete document.

---

## Format Guidance

- **Use code blocks for every API definition.** Proto messages, Go interfaces, Thrift structs, configuration — these are the substance of an ERD. Describe them in prose AND show them in code. A reviewer evaluating an API change needs to see the actual definition, not a summary of it.
- **Use ASCII diagrams** for architecture (current and proposed), data flows, and system interactions. Include at least two diagrams: current state and proposed state. Label every component and arrow. Keep diagrams under 60 characters wide.
- **Use tables** for options comparison (mandatory), capacity calculations, latency analysis, dependency tracking, metric definitions, and risk matrices. Tables make trade-offs scannable.
- **Use numbered sub-sections** liberally (7.1, 7.2, etc.). ERDs are long and reviewers reference specific parts in their feedback — "I have a concern about 7.3" is much more useful than "I have a concern about the implementation."
- **Show your math.** Storage calculations, latency estimates, RPS projections, cost estimates — include the actual numbers, formulas, and assumptions, not just the conclusions. Reviewers will verify them.
- **Front-load each section** with the key conclusion. The first sentence of every section should tell the reader what this section concludes. Busy reviewers skim headers and first sentences.
- **Cross-reference between sections.** "This addresses Challenge 3 from section 5." "See section 8 for the capacity impact of this choice." Cross-references help reviewers trace the logic.
