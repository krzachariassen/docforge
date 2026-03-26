# Strategy Review Deck Template

For recurring leadership presentations: monthly/quarterly strategy reviews, org-level status updates, portfolio reviews with senior directors or VPs.

This template is designed for **large teams (20-40+ people)** where the primary challenge is making the volume and breadth of work visible. A 30-person org that presents like a 10-person team has a communication problem, not a delivery problem.

**Audience**: Senior Director, VP, or equivalent. They want: (1) Are we on track? (2) What moved? (3) What's at risk? (4) What do you need from me? They have 30-60 minutes and will interrupt with questions.

**Typical slide count**: 15-25 content slides + 5-10 appendix slides for a 30-minute review. One slide per 2 minutes of speaking time.

**Human contribution required**: This template requires the MOST human input of any DocForge output. The human must provide: team-level updates from each workstream, metric snapshots (dashboards, scorecards), specific wins and deliverables, risk assessments, and the narrative they want to tell. Without this grounding, the deck will be generic and unconvincing.

> **NOTE**: This is an initial template. It will be refined with real strategy review examples and feedback. Treat it as a strong starting point, not a final format.

---

## Deck Structure

The strategy review follows a strict narrative order. **Do not reorder these sections.**

### OPENING (1-2 slides)

#### Slide 1: Title + Agenda
- Team/org name, review period, presenter name
- Agenda as 4-5 bullets (one per section of the deck)
- Set expectations: "30 minutes, questions throughout"

#### Slide 2: TL;DR — The Headline
The single most important message for this review. A claim, not a topic.
- Good: "INCA Platform shipped 4 major initiatives and reduced KTLO by 40% in Q1"
- Bad: "Q1 Update"

This slide sets the tone. If the Senior Director remembers one thing, it's this.

### SCOREBOARD (2-3 slides)

The scoreboard answers "are we on track?" before the audience has to ask.

#### Slide 3: Priority Tracker
A table showing every committed priority and its status:

| Priority | Status | Key Metric | Target | Actual | Owner |
|----------|--------|-----------|--------|--------|-------|
| [Priority 1] | 🟢 On Track | [metric] | [target] | [actual] | [name] |
| [Priority 2] | 🟡 At Risk | [metric] | [target] | [actual] | [name] |
| ... | | | | | |

**This slide makes team size visible.** A 30-person org should show 6-10 priorities with different owners. If you're showing 2-3 priorities, you're presenting themes, not workstreams — and the audience will think you have a team of 8.

**Speaker notes**: Walk through each row. Dwell on yellow/red items — the audience will ask about them anyway.

#### Slide 4: Key Metrics Dashboard
3-6 metrics that the Senior Director cares about, with trend indicators:

| Metric | Last Review | Now | Trend | Target |
|--------|------------|-----|-------|--------|
| [metric 1] | [value] | [value] | ↑/↓/→ | [target] |
| ... | | | | |

Only include metrics you can explain. If a metric moved unexpectedly, have the explanation ready in speaker notes.

#### Slide 5 (optional): Velocity / Volume Summary
For large teams, a slide that shows the raw output volume:
- PRs merged: X
- Tickets resolved: Y (Z% automated)
- Design docs written: N
- On-call incidents handled: M
- Teams unblocked: K

This slide exists specifically to combat the "feels like a team of 10" problem. 30 people produce volume — show it.

### SUBSTANCE (5-10 slides)

The meat of the review. One section per top priority, 1-3 slides each.

#### Per-Priority Deep-Dive (repeat for each major priority)

**Slide: [Priority Name] — [Claim about progress]**
- What we committed to (from last review or the planning cycle)
- What we delivered (specific deliverables, not vague progress)
- Key metric (with before/after if available)
- What's next (what this priority looks like by next review)

**For large or cross-functional initiatives**, add a second slide showing:
- Team members involved (names or count)
- Deliverables list (specific PRs, docs, launches — show volume)
- Dependencies shipped or unblocked

**For technical initiatives**, include:
- Architecture diagram or data flow (if applicable)
- Performance numbers (before/after latency, error rates, etc.)

#### Cross-Cutting Work (1-2 slides)

Work that doesn't fit in a single priority but demonstrates org-level investment:
- **Process improvements**: On-call rotation improvements, incident response changes, planning process upgrades
- **Tooling investments**: Internal tools built, developer experience improvements
- **People investments**: Hiring, mentoring, knowledge sharing, team structure changes
- **Tech debt reduction**: Systems decommissioned, migrations completed, code health improvements

This section makes invisible work visible. Most of a platform team's value is invisible to leadership unless you show it.

### RISKS & BLOCKERS (1-2 slides)

#### Slide: What's At Risk
A table — not a paragraph. For each risk:

| Risk | Impact | Likelihood | Mitigation | Need from leadership |
|------|--------|-----------|------------|---------------------|
| [risk 1] | [what happens] | H/M/L | [what we're doing] | [specific ask] |

The "need from leadership" column is what makes this actionable. Without it, you're just listing worries.

#### Slide: Blockers (if any)
Things that are actually blocking progress today — not risks, but current impediments:
- What's blocked
- Who is blocking it (diplomatically)
- What resolution looks like
- What you need from the Senior Director

### NEXT MONTH / NEXT QUARTER (1-2 slides)

#### Slide: Commitments for Next Review
A table of what you're committing to deliver by the next review:

| Commitment | Target Date | Owner | Success Metric |
|------------|------------|-------|---------------|
| [commitment 1] | [date] | [name] | [how we'll know] |

This creates accountability in both directions. The Senior Director sees what you're promising; you can reference this slide at the next review to show you delivered.

### ASK (1 slide)

#### Slide: What We Need
The single most important ask — headcount, budget, executive sponsorship, a decision, or just continued support. Be specific:
- Good: "We need 2 additional senior engineers for Q2 to staff the event system migration (approved headcount, not filled)"
- Bad: "We need more resources"

If you have no ask, this slide becomes "Key Takeaways" — 3 bullets that reinforce the headline from Slide 2.

### APPENDIX (5-10 slides)

The appendix is NOT filler. It's your depth. It proves you have command of the details when questioned. Include:

- **Team-by-team breakdown**: What each sub-team delivered. One row per person or per sub-team.
- **Detailed metric deep-dives**: Full dashboards, trend charts, methodology notes
- **Project plans**: Gantt charts, milestone trackers, dependency maps
- **Technical details**: Architecture diagrams, performance analysis, capacity planning
- **Incident summaries**: If relevant, a table of incidents with impact and resolution

The appendix should be rich enough that any question from the Senior Director can be answered by pulling up an appendix slide.

---

## Common Mistakes This Template Prevents

1. **"Feels like a team of 10"**: The Priority Tracker (slide 3) forces you to show 6-10 workstreams with different owners. The Velocity Summary (slide 5) shows raw output volume. The per-priority deep-dives show deliverables, not themes.

2. **No data**: The Metrics Dashboard (slide 4) forces quantification. Every priority has a key metric. Trends are shown, not claimed.

3. **All good news**: The Risks section forces honesty. The "need from leadership" column forces actionable asks. Senior Directors distrust reviews that are 100% green.

4. **No accountability**: The Commitments slide (next review) creates a forward contract. The Priority Tracker references last review's commitments.

5. **No depth**: The appendix proves you have detail without drowning the narrative in it.

---

## Grounding Files for Strategy Reviews

The human should provide these in `workspace/grounding/`:

- **Priority tracker / OKR status**: Current status of each committed priority
- **Metric snapshots**: Screenshots or exports from dashboards showing key metrics
- **Deliverable lists**: Per-team or per-person lists of what was shipped
- **Incident reports**: If relevant to the review period
- **Previous review deck**: So the presenter can show progress since last review
- **Feedback from last review**: What the Senior Director said — this shapes the narrative
- **Team roster**: Who is on the team, by sub-team, so the deck can show breadth

---

## Format Guidance

- **Use tables aggressively.** Strategy reviews are inherently tabular — priorities, metrics, risks, commitments all have consistent dimensions. Tables show structure and volume simultaneously.
- **Big numbers for wins.** "127 KTLO tickets resolved" as a full-slide number is more impactful than a bullet in a list.
- **Before/after comparisons** for anything that changed. Side-by-side is the most convincing visual format for progress.
- **Name people.** Putting owner names in the priority tracker and commitment table makes the org feel real — not a faceless team of 30.
- **Speaker notes are critical.** The presenter needs talking points, data sources, and prepared answers for likely questions. Every slide should have speaker notes.
