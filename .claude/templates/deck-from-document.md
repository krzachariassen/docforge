# Document-to-Deck Template

For converting a finished DocForge document (ERD, strategy doc, abstract, RFC, vision doc) into a presentation for review meetings, stakeholder alignment, or team communication.

The source document has all the content. Your job is NOT to summarize it — it's to restructure the strongest 20% for spoken delivery and put the remaining 80% in the appendix (or leave it in the document with a "see the full [doc type]" reference).

**Audience**: Same as the source document, but they're in a room (or video call), not reading at their desk. They have less patience, more distractions, and will ask questions out loud.

**Typical slide count**: Source document length ÷ 100 lines ≈ target content slides. A 600-line abstract → ~6 content slides + appendix. A 1,600-line ERD → ~16 content slides + appendix. Cap at 20 content slides for any document — beyond that, you're reading the document aloud.

---

## Slide Structure by Source Document Type

### From Strategy Documents

| Section | Slides | What to include | What to cut |
|---------|--------|----------------|-------------|
| Executive Summary | 1 | The thesis and the ask — one slide | All detail |
| Problem Statement | 2-3 | The "why now" narrative + key data points | Sub-section depth, lengthy evidence chains |
| Proposed Approach | 2-3 | Vision, design principles (as a table), non-goals | Detailed explanations per principle |
| Architecture | 2-3 | System diagram + one component deep-dive | Full component details — appendix |
| Roadmap | 1-2 | Phase timeline with milestones | Per-phase deliverable lists — appendix |
| Measurement | 1 | Before/after comparison table | Metric methodology |
| Risks | 1 | Top 3-5 risks as a table | Full mitigation details |
| Decision Points | 1 | The ask — what needs approval | Go/no-go criteria detail |
| **Appendix** | 3-5 | Full architecture, detailed roadmap, metrics definitions, resource breakdown | |

### From ERDs

| Section | Slides | What to include | What to cut |
|---------|--------|----------------|-------------|
| Motivation | 1-2 | Why now + quantified impact (big number slide) | Full narrative |
| Current Architecture | 1 | Architecture diagram only | Component descriptions |
| Challenges | 1 | Top 3-4 challenges as a table | Root cause analysis |
| Options Analysis | 3-4 | One slide per option (title + pros/cons), one comparison table slide | Full option descriptions |
| Recommended Design | 2-3 | Architecture diagram + key design decisions | Proto definitions, full API specs — appendix |
| Capacity & Testing | 1 | Key numbers: latency impact, storage, throughput | Full calculations — appendix |
| Rollout | 1-2 | Phase table + timeline | Detailed migration steps |
| Ask | 1 | Decision needed + resources requested | |
| **Appendix** | 4-6 | Proto definitions, full options comparison, capacity math, testing plan, cross-team dependencies | |

### From Abstracts

| Section | Slides | What to include | What to cut |
|---------|--------|----------------|-------------|
| Summary + Problem | 1-2 | Problem statement with evidence | Background detail |
| Proposal | 2-3 | What changes + key code/proto (one slide), diagram (one slide) | Full implementation detail |
| Alternatives | 1 | Comparison table: chosen vs. rejected | Full alternative descriptions |
| Risks + Rollout | 1 | Combined: top risks + rollout phases | Detailed migration steps |
| Ask | 1 | Approval needed + timeline | |
| **Appendix** | 2-3 | Full proto definitions, data analysis, migration detail | |

### From RFCs

| Section | Slides | What to include | What to cut |
|---------|--------|----------------|-------------|
| Summary + Motivation | 1-2 | The proposal in one sentence + why | Background |
| Proposed Solution | 2-3 | Key design + diagram | Implementation detail |
| Alternatives | 1 | Comparison table | Full alternative descriptions |
| Trade-offs | 1 | Key trade-offs accepted | |
| Rollout + Ask | 1 | Plan + what you need | |
| **Appendix** | 2-3 | Design details, migration plan | |

---

## Conversion Rules

1. **Read the source document's Executive Summary / Summary first.** This tells you the thesis and the ask. The presentation's first and last slides come from here.

2. **Identify the 3-5 strongest data points.** These become big-number slides or table highlights. A presentation lives and dies by its data — pick the numbers that are hardest to argue with.

3. **Every diagram from the source document gets its own slide.** Diagrams are the most visual-friendly content. Don't skip them.

4. **Every comparison table from the source gets its own slide.** Tables (options comparison, before/after, risk matrix) are slide-ready content.

5. **Cut prose ruthlessly.** If the source document has a 3-paragraph explanation of a design decision, the slide gets the decision as a title and the rationale as 2-3 bullets. The full explanation goes in speaker notes.

6. **The appendix is your safety net.** Anything cut from the main slides that a reviewer might ask about goes in the appendix. The presenter can pull it up during Q&A. "Great question — let me show appendix slide 3."

7. **Slide titles tell the story.** Read only the slide titles in sequence — they should form a coherent argument. If they read like a table of contents ("Problem Statement", "Architecture", "Roadmap"), rewrite them as claims ("Polling Causes 60% of Our API Load", "The Outbox Pattern Solves All 6 POC Failures", "Phase 1 Cuts Traffic by 83%").

---

## Format Guidance

- **Big numbers**: Use when a single metric is surprising or decisive. "127 tickets resolved" on a slide by itself is more impactful than buried in a bullet list.
- **Tables**: Use for comparisons, scorecards, and structured data. Keep to 3-5 columns and 4-8 rows — more than that, split or move to appendix.
- **Diagrams**: Reproduce ASCII diagrams from the source document. If the source has a complex diagram, simplify it for the slide (fewer labels, fewer arrows) and put the full version in the appendix.
- **Bullets**: Maximum 5 per slide. Each bullet is one line — no sub-bullets on slides.
- **Speaker notes**: Include for every slide. Cover: what to say, data sources, likely questions, transitions to the next slide.
