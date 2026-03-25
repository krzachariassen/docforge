# Strategy Document Template

For long-form strategic documents: technology bets, platform investments, multi-team initiatives, org restructuring proposals, AI adoption strategies.

**Audience**: Senior engineers and leadership. They want specificity, evidence, and clear asks. They push back on vague claims and missing failure modes.

**Typical depth**: 3,000–10,000+ words depending on scope. Strategy documents are the deepest document type. If the brief says "Blueprint" depth, go long and be exhaustive.

**Human contribution required**: Strategy documents require the most human input. The brief alone is not enough — the human should provide grounding files (existing docs, system inventories, metrics) and inject specific content (architecture details, code examples, definitions) through the brief's Author-Specified Content or via `/df-supplement` during the process.

---

## Core Sections

These sections appear in every strategy document.

### Executive Summary
2–3 paragraphs. The document compressed: the problem, the proposed approach, and the ask. Write it last, place it first. A reader who stops here should understand what's being proposed and what they need to decide.

For complex strategies, follow the summary with a bullet list of key deliverables or success criteria — gives the reader a concrete anchor.

### Problem Statement / Why
What problem, and why now? Structure this as a narrative, not a list:
- **The context**: What system/team/product are we talking about? Give the reader enough to understand even if they don't know the area.
- **Current state**: What exists today? Be concrete — name systems, show numbers, describe the actual setup. Tables work well for inventories ("here's what we have today").
- **The challenges**: What's wrong with the current state? Number them. Each challenge should be specific and falsifiable, not vague ("scaling issues"). Good: "Context dilution: every AI interaction receives 381 lines regardless of task type, diluting focus." Bad: "Our AI tooling has problems."
- **Why now**: What changed that makes this the right time?

### Proposed Approach / What
The high-level direction. Clear enough that a skeptic can disagree with it. Structure:
- **Vision statement**: One paragraph — the conceptual shift. What does the world look like after this succeeds?
- **Design principles**: The rules that guide every decision. 4–7 principles, each with a brief explanation. These are what you'd invoke in a debate about implementation choices.
- **Non-goals**: What this strategy explicitly does NOT do. These are as important as goals — they bound expectations and prevent scope creep. List 4–8 non-goals with brief explanations.

### Architecture / How
The technical or organizational design. This is often the longest section. Use sub-sections liberally:
- **System overview**: How the pieces fit together. ASCII diagrams work well for layer architectures, data flows, and pipeline stages.
- **Component deep-dives**: One sub-section per major component. For each: what it is, what it does, why it's designed this way, and what it connects to.
- **Key design decisions**: Call out the important choices and their rationale. Why this approach over alternatives?

For complex architectures, consider a table showing all components with their purpose, phase, and priority rationale.

If the architecture involves specific definitions (agent profiles, API schemas, config formats), include them as code blocks.

### Roadmap / Phases
Work broken into phases with clear milestones. For each phase:
- **Goal**: One sentence — what this phase proves or delivers
- **Deliverables**: Numbered list of specific things to build
- **Exit criteria**: What must be true before moving to the next phase. Measurable, not subjective.
- **What's NOT in this phase**: Explicitly state what's deferred to prevent scope creep

### Measurement / Success Criteria
How will we know this worked? Structure:
- **Baseline**: What to measure before starting, and how. You can't show improvement without a baseline.
- **Key metrics table**: Each metric with its definition, target, and measurement method. Use a table — metrics are inherently tabular.
- **Before/after comparison**: A table showing each dimension and how it changes. This is the "so what" that makes the strategy tangible.

### Risks & Mitigations
For each major risk: what it is, impact, and specific mitigation strategy. Use a table — risks are inherently tabular. Don't list risks without mitigations; that's just worry without action.

### Resource Requirements
Be explicit: headcount (roles, FTE percentages, duration), infrastructure costs, external dependencies. Break down by phase if the investment changes over time.

### Decision Points
What decisions does leadership need to make, and when? Be explicit — a document that leaves readers unsure what they're approving has failed. Include go/no-go criteria for each decision point.

## Optional Sections

Include these when the brief's Structure Notes call for them or when the subject matter demands it.

### Governance & Security
For strategies that change access patterns, introduce automation, or modify review processes:
- **Autonomy/authority policy**: Who can do what? What requires approval?
- **Security considerations**: What new risks does this create? How are they mitigated?
- **Audit and compliance**: How is the system monitored and audited?
- **Kill switch / rollback**: How do you turn it off if something goes wrong?

### Getting Started / Implementation Guide
For strategies where the "what to build first" needs to be unambiguous:
- **What to build**: Specific deliverables for the first phase
- **What NOT to build**: Explicit anti-instructions to prevent over-building
- **Who does what**: Role assignments

### Appendix: Glossary
For documents that introduce domain-specific terminology. Table format: term + definition. Only include terms that a reader outside the team wouldn't know.

### Appendix: Reference Tables
For supporting detail that would interrupt the main flow: file structures, API inventories, detailed comparison tables, configuration references.

---

## Recommended Drafting Order

For Blueprint-depth strategy documents, use sectional drafting. This lets the human review and add context between rounds.

**Round 1** — The argument: `sections:problem-statement,proposed-approach`
Draft the problem and the proposed direction. The human reviews to make sure the framing is right before the detail sections are written.

**Round 2** — The design: `sections:architecture`
This is usually the longest section. Draft it after the human confirms the framing. The human reviews for completeness and adds any missing component details, tables, or diagrams via `/df-edit`.

**Round 3** — The plan: `sections:roadmap,measurement,risks`
The execution details. By now the argument and architecture are solid, so the roadmap and metrics follow naturally.

**Round 4** — The bookends and extras: `sections:executive-summary,resources,decision-points` + any optional sections (governance, getting started, appendices)
Write the executive summary last — it compresses the full document. Add optional sections as the brief's Structure Notes direct.

After all sections are drafted, run `/df-review` on the complete document.

---

## Format Guidance

- **Use tables** when comparing items across consistent dimensions. If you're writing "X has A, B, C. Y has D, E, F." — that's a table.
- **Use ASCII diagrams** for system architectures, layer models, and pipeline flows. Keep them under 60 characters wide.
- **Use code blocks** for definitions, commands, configuration, and file formats that the reader needs to see exactly.
- **Use numbered sub-sections** (3.1, 3.2, etc.) for long sections with many components. It helps readers reference specific parts.
- **Front-load each section** with the key point. Busy readers skim the first sentence of every section.
