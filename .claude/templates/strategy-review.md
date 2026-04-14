# Strategy Review Deck Template

For recurring leadership presentations: monthly strategy reviews with senior directors, quarterly portfolio reviews, org-level status updates.

**Meeting format**: 1 hour. ~25 content slides + 5-10 appendix slides. One slide per 2 minutes of speaking, with room for questions and 1-2 deep dives.

**Audience**: Senior Director or equivalent. They want: (1) Are we on track? (2) What moved? (3) What's at risk? (4) What do you need from me? They will interrupt with questions.

**Core challenge this template solves**: Large teams (20-40+ people) that present like small teams. If leadership can't see the volume and breadth of work, they'll undervalue the org regardless of what shipped. This template forces visibility.

---

## Deck Structure

The strategy review follows a strict narrative order. **Do not reorder these sections.** The sequence is: context → scorecard → headlines → programs → depth → forward look → ask.

### SECTION 1: OPENING (2 slides)

#### Slide 1: Title
- Team/org name, review period (month or quarter), presenter name
- Keep it clean. One image or logo if appropriate. No clutter.

#### Slide 2: Agenda with Time Allocations
- List each section with allocated time
- Name the deep dive topics explicitly so the audience knows what's coming
- Example: "Scoreboard (10 min) · Highlights & Flags (10 min) · Programs (15 min) · Deep Dive: [Topic] (15 min) · Forward Look + Ask (10 min)"

Time allocations serve two purposes: they manage audience expectations, and they force the presenter to budget their own airtime. Without them, scoreboard discussion bleeds into everything.

---

### SECTION 2: SCOREBOARD (3-4 slides)

The scoreboard answers "are we on track?" before the audience has to ask. All data, no narrative. The story comes later.

#### Slide 3: OKR / Priority Tracker

The single most important slide in the deck. A table showing every committed priority and its status:

| Objective | Key Result | Baseline | Target | Current | MoM Δ | Realized Impact | Owner |
|-----------|-----------|----------|--------|---------|-------|----------------|-------|
| [Objective 1] | [KR] | [start] | [goal] | [now] | [trend] | [what's banked] | [name] |

**Critical columns:**
- **MoM Δ** (month-over-month change): Shows trajectory, not just position. A metric at 5% that was 3% last month tells a different story than one that was 7%.
- **Realized Impact**: Separates what's *shipped and measured* from what's *projected*. This is accountability — "we banked +14 bps from these two launches" vs. "we project +50 bps from the full roadmap."
- **Owner**: Names make the org real. A 30-person team should show 6+ different owners. If you're showing 2-3 owners, you're presenting themes, not workstreams.

**Format guidance**: One row per KR, grouped by objective. Use color or status indicators (🟢🟡🔴 or On Track / At Risk / Off Track). If a metric hasn't moved yet (0% → 0%), add a comment explaining when movement is expected — unexplained zeros erode confidence.

#### Slide 4: Engineering Health (optional but recommended)

One slide that makes team output and health visible:

| Metric | Last Review | Current | Trend | Benchmark |
|--------|------------|---------|-------|-----------|
| PRs merged | [N] | [N] | ↑/↓ | [org benchmark if available] |
| Tickets resolved (KTLO) | [N] | [N] | ↑/↓ | |
| Support questions handled | [N] | [N] | ↑/↓ | |
| On-call incidents | [N] | [N] | ↑/↓ | |
| MTTD / MTTR | [time] | [time] | ↑/↓ | |

This slide exists to combat the "feels like a small team" problem. 30 people produce volume — PRs, tickets, support responses, on-call coverage. Show it. An org-wide benchmark (e.g., "top 10% in diffs/engineer") gives external context that leadership values.

**When to include**: Always include if team size > 15 or if leadership has questioned productivity. Skip if the team is small enough that volume is self-evident.

**When to skip a metric**: Only show metrics that either (a) demonstrate strength or (b) show a clear improvement plan. A flat or declining metric without a story is worse than no metric.

#### Slide 5: Cost Health

One slide covering platform/infrastructure cost:

| Metric | Last Review | Current | Trend | Target |
|--------|------------|---------|-------|--------|
| [Primary cost metric, e.g., CPI] | [value] | [value] | ↑/↓ | [guardrail] |
| [Secondary cost metric] | [value] | [value] | ↑/↓ | |
| Total platform spend | [$] | [$] | ↑/↓ | |

Include major cost movements: "Redis migration saved $X/month" or "New workload added $Y — within budget." If cost reporting is obscured by methodology issues (e.g., RI vs. RI-EXP), say so — leadership respects transparency about measurement challenges.

**When to include**: Always include for infrastructure/platform teams. Cost is a first-class leadership concern — having it upfront prevents the surprise question that derails your narrative. For product teams with less direct infra ownership, this can be skipped or folded into a single line in the OKR table.

---

### SECTION 3: SUMMARY — Ts / Bs / FLAGS (2-3 slides)

The T/B/Flag format is a proven structure for communicating headlines. Each item gets its own row — not crammed into dense table cells.

#### Slide 6: Tops & Bottoms

| | Tops (wins) | | Bottoms (gaps) |
|---|---|---|---|
| T1 | [Specific achievement with impact] | B1 | [Specific gap with context] |
| T2 | [Specific achievement with impact] | B2 | [Specific gap with context] |
| T3 | [Specific achievement with impact] | | |

**Rules for Ts**: Be specific. Not "made progress on X" but "shipped X, measured Y impact." Name the project and the person. Include metrics where available.

**Rules for Bs**: Be honest. Not "slightly behind on X" but "X delayed 2 weeks because [reason]." Bottoms that are vague make leadership nervous — they assume you're hiding something.

Aim for 3-5 Tops and 2-3 Bottoms per review. All Tops with no Bottoms is not credible.

#### Slide 7: Flags

Separate from Bs. Flags are forward-looking risks and blockers, not past performance.

| Flag | Impact | What We Need |
|------|--------|-------------|
| [Risk/blocker] | [What happens if unresolved] | [Specific ask — decision, resources, escalation] |

The "What We Need" column is what makes this actionable. Without it, you're listing worries. With it, you're giving leadership something to do. If a flag has no ask, it's informational — consider whether it belongs in the main deck or the appendix.

---

### SECTION 4: PROGRAM OVERVIEWS (8-12 slides)

One section per program area / workstream / pod. For a 30-person org, expect 4-6 programs. Each program gets 2-3 slides.

#### Per-Program Structure (repeat for each program)

**Slide A: Program Summary**

Combines T/B with priorities in a single slide:

| Last Month Priorities | This Month Priorities | Flags |
|----------------------|----------------------|-------|
| ✅ [Completed] | [Priority 1] | [Flag if any] |
| ✅ [Completed] | [Priority 2] | |
| 🔄 [In progress] | [Priority 3] | |

Plus a compact T/B for the program (2-3 Tops, 1-2 Bottoms).

Checking off last month's priorities creates accountability. If something from last month isn't checked off and isn't called out, the audience will notice.

**Slide B: Program OKR Table**

Same format as the hero OKR table but scoped to this program:

| KR | Baseline | Target | Current | MoM Δ | Realized Impact | Commentary |
|----|----------|--------|---------|-------|----------------|------------|

Include commentary for every KR — especially ones showing no movement. "No launches in Feb, impact expected in March" is better than a silent zero.

**Slide C: Roadmap Sequencing (if needed)**

Gantt-like table showing project timelines:

| Project | Status | [Month 1] | [Month 2] | [Month 3] | [Month 4] | [Month 5] | [Month 6] | Comments |
|---------|--------|-----------|-----------|-----------|-----------|-----------|-----------|---------|
| [Project 1] | 🟢 | Dev | XP | Rollout | | | | |
| [Project 2] | 🟡 | | Plan | Dev | Dev | XP | Rollout | Delayed from original Q1 target |
| [Project 3] | ⚪ | | | Plan | Dev | Dev | Rollout | Not started |

Use status indicators: 🟢 On Track, 🟡 At Risk, 🔴 Off Track, ⚪ Not Started. This format shows breadth (many projects = many people working) and timeline (realistic vs. aspirational).

Include this slide for programs with 4+ active projects. For smaller programs, fold the timeline into the summary slide.

---

### SECTION 5: DEEP DIVES (5-8 slides)

1-2 selected topics that deserve detailed attention. Not every program gets a deep dive — pick the 1-2 that are most impactful, most contentious, or most in need of a leadership decision.

#### Deep Dive Structure

Each deep dive follows one of these arcs:

**For XP / experiment results:**
1. Design (1 slide): What we tested, how, coverage
2. Results (1-2 slides): Data tables, charts, key metrics
3. Recommendation (1 slide): What we recommend and why

**For technical decisions / architecture:**
1. Problem (1 slide): What's broken, why it matters
2. Options (1 slide): Comparison table with evaluation criteria
3. Recommendation (1 slide): What we recommend, what we need to proceed

**For project updates requiring attention:**
1. Context (1 slide): Where we are, what changed
2. Data (1-2 slides): Evidence supporting the story
3. Ask (1 slide): What we need from leadership

The deep dive ends with a clear **recommendation or ask**. If it doesn't end with one of those, it's informational — and informational content belongs in the appendix, not the main narrative.

---

### SECTION 6: FORWARD LOOK + ASK (2 slides)

#### Slide: Commitments for Next Review

| Commitment | Target Date | Owner | Success Metric |
|------------|------------|-------|---------------|
| [Commitment 1] | [date] | [name] | [how we'll know] |

This creates a forward contract. At the next review, reference this slide to show you delivered. The audience sees accountability in both directions.

#### Slide: The Ask

The single most important thing you need from leadership. Be specific:
- Good: "We need the remaining 2 approved headcount filled by April to staff the event migration — can you escalate with recruiting?"
- Good: "We need a decision on whether to proceed with Option B by March 15 — the team is blocked until then."
- Bad: "We need more resources."
- Bad: "We need support."

If you have no ask, this slide becomes **Key Takeaways** — 3 bullets reinforcing the headline story of this review. But try to have an ask. Leadership that isn't asked for anything assumes they aren't needed.

---

### SECTION 7: APPENDIX (5-10 slides)

The appendix is your depth. It proves you have command of the details. Include:

- **Detailed per-program roadmaps**: Full Gantt tables that were too dense for the main deck
- **Full OKR tables**: Every KR with history, not just the hero metrics
- **Eng investment / work plan**: How engineering weeks are allocated across projects (by platform: iOS/Android/BE/Web) with % of team per project. This table makes team size VISIBLE.
- **Incident summaries**: If relevant, a table of incidents with impact and resolution
- **Metric deep-dives**: Full dashboards, trend charts, methodology notes
- **Per-person or per-sub-team output**: What each sub-team or individual contributed

The appendix should be rich enough that any leadership question can be answered by pulling up an appendix slide. "Great question — let me show you appendix slide 4."

---

## Adapting by Team Type

### Infrastructure / Platform Teams
- **Value metrics**: Adoption %, teams unblocked, developer time saved, migration progress, SLA improvements, incidents prevented. These replace $ revenue metrics.
- **Cost slide**: Always include. Infrastructure cost is a first-class leadership concern.
- **Engineering Health slide**: Strongly recommended — platform teams do invisible work (KTLO, on-call, support). Make it visible.
- **Deep dives**: Tend toward technical decisions, migration progress, or reliability improvements rather than XP results.

### Product Teams
- **Value metrics**: GB impact, conversion rates, defect rates, user metrics with $ attribution where natural.
- **Cost slide**: Optional — include if the team owns significant infra or if cost is a leadership concern.
- **Deep dives**: Tend toward XP results with data analysis and recommendations.
- **Competitive comparisons**: Include when available — "Instacart does X, we now do X+Y."

---

## Common Mistakes This Template Prevents

1. **"Feels like a team of 10"**: The OKR table shows 6+ owners. The Engineering Health slide shows volume. The per-program sections show breadth. The appendix work plan shows eng weeks per project.

2. **No data**: Every program has an OKR table. Every claim has a metric. MoM deltas show trajectory. Realized Impact separates shipped from projected.

3. **All good news**: The T/B format forces Bottoms. The Flags section forces forward-looking risks with asks. All-green reviews are not credible.

4. **No accountability**: Last month's priorities are checked off (or not). Commitments are made for next review. Realized Impact shows what actually shipped vs. projected.

5. **No depth for Q&A**: The appendix has detailed roadmaps, work plans, and metric deep-dives ready for any question.

6. **Topic titles instead of claim titles**: Slide titles should be claims ("KTLO Resolution Up 40%") not topics ("KTLO Update"). The audience should understand the story by reading only the titles.

7. **Dense table cells with embedded paragraphs**: T/B items get their own rows. One point per row. If a cell needs line breaks, the content is too dense for a slide.

8. **No ask**: The Ask slide forces a specific request. Leadership that isn't asked for anything assumes they aren't needed.

9. **Overrunning time**: The agenda slide with time allocations forces budgeting. The template limits deep dives to 1-2 topics. Everything else goes in appendix.

---

## Grounding Files for Strategy Reviews

The human should provide these in the project's `grounding/` folder:

- **OKR / priority tracker**: Current status of each committed OKR with actuals
- **Per-program updates**: Raw status updates from each program lead or pod lead
- **Metric snapshots**: Dashboard exports, trend data, key numbers
- **Eng metrics**: PR counts, ticket resolution data, on-call stats, diffs/SWE percentile
- **Cost data**: Infrastructure spend, CPI, cost changes from migrations or new workloads
- **Previous review deck**: So the presenter can show progress vs. last review's commitments
- **Feedback from last review**: What leadership said — this shapes the narrative
- **Deep dive material**: Data, XP results, architecture options for the 1-2 deep dive topics

---

## Format Guidance

- **Slide titles are claims, not topics.** "Shift Left Cut Structural Issues by 22%" not "Shift Left Update." If you read only the titles in sequence, you should understand the story.
- **Use tables aggressively.** OKRs, priorities, roadmaps, T/B, flags, eng investment — all naturally tabular. Tables show structure and volume simultaneously.
- **Big numbers for wins.** "127 tickets resolved" as a full-slide number is more impactful than a bullet in a list. Use when the number is surprising.
- **Before/after for progress.** Side-by-side or MoM columns are the most convincing visual format.
- **Name people.** Owner columns in OKR tables, commitment tables, and roadmaps make the org feel real.
- **Speaker notes on every slide.** Talking points, data sources, likely questions, transitions. The presenter needs preparation, not just slides.
- **Status indicators are visual shorthand.** 🟢🟡🔴 or On Track / At Risk / Off Track. The audience scans color before reading text.
- **One message per slide.** If a slide makes two points, split it.
- **Max 5 bullets per slide.** More than that, you need a table or another slide.
