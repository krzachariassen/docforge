# Abstract Template

For tactical proposals that solve a specific, bounded problem: unblocking a migration, introducing an enforcement mechanism, resolving a technical debt issue, proposing a system change, adding a new capability to an existing system.

Abstracts are the "just enough to decide" document. They're shorter than strategy docs, more focused than ERDs. One problem, one proposed solution, clear risks, ship plan. The reader walks away knowing exactly what's proposed, why the alternatives are worse, and what the blast radius is.

**Audience**: Engineers, tech leads, and engineering managers who need to approve or implement the change. They want to evaluate the proposal on its merits — is the problem real, is the solution sound, are the risks managed?

**Typical depth**: 1,500–5,000 words. Dense and concrete. Abstracts earn credibility through specificity: code examples, proto definitions, data analysis, migration steps. Every claim should be backed by something concrete. No hand-waving.

**Human contribution required**: Abstracts are grounded in specific system knowledge. The human should provide code snippets, proto definitions, architecture context, data analysis results, and migration constraints via grounding files or Author-Specified Content. Without these, the abstract will be too generic to be useful.

---

## Core Sections

These sections appear in every abstract, in this order. **Do not reorder them.** The sequence is deliberate: summary → context → problem → boundaries → solution → alternatives → risks → ship plan → verification → timeline.

### 1. Metadata
A structured header block at the very top. Include all fields that apply:
- **Authors**: Who wrote this (names and handles)
- **Date**: When this was started
- **Project/ERD reference**: Link to parent initiative if this abstract is part of a larger effort
- **Project Summary**: One sentence — what this abstract proposes. This is the sentence someone reads in a doc index.
- **System/Asset**: Which system, service, or platform this affects
- **Related documents**: Links to prior art, parent ERDs, related abstracts, or docs this builds on

### 2. Summary
3–5 sentences maximum. The entire abstract compressed: what problem exists, what you propose, and why it's the right approach. A reviewer who reads only this paragraph should understand what they're being asked to approve.

This is NOT the background — it's the punchline up front. Write it last.

### 3. Background
2–3 paragraphs. Set the stage without repeating the full history. Answer three things:
- What broader initiative or context does this exist within?
- What has already been decided that constrains this proposal?
- What triggered this abstract specifically? (a migration blocker, a customer incident, a scaling limit)

End with a single sentence framing what this document proposes. The reader should transition smoothly from "here's the situation" to "here's what I'm proposing."

### 4. Problem Statement
The specific problems this abstract solves. Number them. For each problem:
- **Title**: Short descriptive name (e.g., "ExternalID length is uncapped in MenuStore")
- **What's wrong**: Concrete description — field names, byte limits, system behaviors, error conditions
- **Evidence**: Why this is a real problem, not a theoretical one. Data, incidents, customer reports, or blocked work.
- **Impact if unresolved**: What happens if we don't fix this? Blocked migrations, data loss risk, customer-facing errors, scaling failures.

The "impact if unresolved" is critical — it establishes urgency and justifies the effort. Without it, a reviewer can always ask "why not later?"

### 5. Non-Goals
What this proposal explicitly does NOT solve. List each non-goal with a brief rationale for why it's deferred. These serve two purposes:
1. **Scope control**: Prevent the proposal from growing during review
2. **Honest framing**: Show the reviewer you've thought about the broader picture but are deliberately scoping down

Good non-goals are things a reasonable reviewer would ask about. Pre-empt those questions here.

### 6. Proposal
The core of the document. This section should be detailed enough that an engineer could start building from it.

**For single-part proposals**: One section with clear structure:
- What changes and why
- How it works technically (code, APIs, data flow)
- How it addresses each problem from section 4 (explicit cross-references)

**For multi-part proposals**: Numbered sub-proposals (6.1, 6.2, etc.), each structured the same way. Multi-part proposals should explain why the parts work together — the whole should be more than the sum.

**What to include:**
- **Code blocks** for every proposed interface, API, proto definition, algorithm, or configuration format. These make the proposal concrete and reviewable. Don't describe code — show it.
- **Diagrams** for data flow changes, conversion pipelines, or system interactions before and after the change.
- **Data tables** when feasibility depends on adoption analysis, coverage metrics, or compatibility assessment.
- **Backward compatibility**: If the proposal changes an API, data format, or contract, explicitly address: what happens to existing callers/consumers? Do they need to change? Is there a compatibility period?

### 7. Alternatives Considered
Other approaches that were evaluated. For each alternative:
- **What it proposes**: Brief description — enough to understand the approach
- **Why it was rejected**: Specific, honest reasons. "Too much effort" is acceptable if you explain why (e.g., "requires rewriting all 14 mappers vs. our proposal's 2 changes"). "Blocks future work" is only valid if you say what future work.
- **What it got right**: If the alternative has merits that influenced the chosen proposal, say so. This shows intellectual honesty.

Don't pad this section with straw-man alternatives. 2–3 genuinely considered alternatives, well-argued, is better than 5 superficial ones.

### 8. Risks & Mitigations
What could go wrong — both technical and business risks. For each risk:
- **Risk**: What specifically could fail or break
- **Severity**: How bad is it if this happens? (data loss, degraded experience, blocked workflow, cosmetic issue)
- **Likelihood**: How likely is this? (certain during migration, possible under edge cases, unlikely but high-impact)
- **Mitigation**: What specific action prevents or reduces this risk

Use a table for 4+ risks. Include at least:
- **Technical risks**: Data migration failures, hash collisions, backward compatibility breaks, performance regressions
- **Business risks**: Changed assumptions that affect users/partners, broken integrations, incorrect data exposure
- **Operational risks**: Rollback difficulty, monitoring gaps, on-call burden

### 9. Rollout Plan
How the change gets to production. Be specific — not "we will roll this out" but the actual sequence of steps.

- **Prerequisites**: What must be true before rollout starts (dependencies shipped, configs set, feature flags created)
- **Phases**: If the rollout is phased, what happens in each phase and what triggers advancement
- **Verification at each step**: How you confirm each phase succeeded before moving forward
- **Rollback procedure**: Exact steps to revert if something goes wrong. Include what triggers a rollback decision.

**If data migration is required**, include it here as a dedicated sub-section:
- Migration sequence (numbered steps)
- Data verification approach
- Rollback procedure specific to the migration
- Timing constraints (e.g., "during closed hours", "during low-traffic window")

### 10. Success Criteria
How you know this worked. Define 2–5 measurable outcomes:
- **What to measure**: Specific metric or condition
- **Target**: What "success" looks like in numbers
- **How to measure**: Dashboard, query, manual check
- **When to measure**: How long after rollout before you evaluate

This section closes the loop. Without it, the proposal ships and nobody verifies it actually solved the problem.

### 11. Project Plan
How the work breaks down. Include:
- **Phases or work streams** with brief descriptions
- **Effort estimates** (t-shirt sizing or days/weeks is fine)
- **Dependencies** between phases or on external teams
- **Milestones** with target dates if known

A table works well here. This can be brief for small proposals (3–5 rows) or detailed for multi-team efforts.

## Optional Sections

Include these when the brief's Structure Notes explicitly call for them. **Do not invent optional sections that aren't listed here or in the brief's Structure Notes.**

### Adoption Analysis
When the proposal's success depends on how well existing data or systems fit the new model. Include data tables showing coverage, compatibility, or migration scope across relevant dimensions (tiers, entity types, integration types, etc.). Show the analysis methodology — link to queries or scripts.

### Default Configuration
When the proposal introduces configurable behavior, document the defaults and the rationale behind each. Explain what would need to change for a different use case.

### Appendices
- **Only create appendices called for by the brief's Structure Notes** or clearly demanded by the content.
- **Every appendix must be referenced from the main text.**
- **Common appendix types**: Data analysis queries with results, detailed migration scripts, full proto definitions (when too long for the proposal section), before/after workflow diagrams.

---

## Format Guidance

- **Use code blocks liberally.** Abstracts are technical — proto definitions, Go interfaces, SQL queries, configuration examples, and algorithm pseudocode belong in the document, not described in prose. If a reviewer needs to evaluate an API, they need to see the API.
- **Use tables** for adoption analysis, risk matrices, migration scope, entity inventories, and comparison data. If you're listing items with consistent attributes, that's a table.
- **Use ASCII diagrams** for data flows, conversion pipelines, before/after architectures, and system interactions. Keep them under 60 characters wide with labeled components.
- **Number sub-sections** when the proposal has multiple parts (6.1, 6.2, etc.). Reviewers need to reference specific aspects in their feedback.
- **Front-load each section** with the key point. The first sentence of every section should tell the reader what this section concludes.
- **Cross-reference between sections.** When the proposal addresses a specific problem, say "This addresses Problem 3 from section 4." When a risk relates to a specific proposal part, reference it.
