# Postmortem Template

For incident analysis: production outages, data loss, security events, near-misses worth documenting.

**Audience**: Engineering team and leadership. They want to understand what happened, why, and what's being done to prevent recurrence. They will push back on incomplete timelines, missing root causes, and action items without owners.

**Typical depth**: 1,500–4,000 words. Thorough enough to prevent recurrence, concise enough to be read.

**Human contribution required**: Postmortems are inherently grounded in internal data — the human must provide incident timelines, metrics, logs, and context. The AI can structure and write, but the facts come from the human.

---

## Core Sections

### Summary
2–3 sentences. What happened, when, and the impact. A reader who stops here should understand the severity and scope.

### Impact
Quantified impact. Users affected, duration, revenue impact, SLA implications, data loss. Use numbers, not adjectives. "50,000 users unable to place orders for 47 minutes" not "significant user impact."

### Timeline
Chronological event log. Use a table or timestamped list:
- **[Time]**: [Event] — [who did what or what system did what]

Include: first signal, detection, escalation, mitigation attempts (including failed ones), resolution, all-clear. Be honest about delays.

### Root Cause
The technical root cause. Be precise — name the component, the code path, the configuration. Distinguish root cause from contributing factors. There should be one root cause (even if it's "a combination of X and Y created conditions where Z occurred").

### Contributing Factors
What made the incident worse, harder to detect, or harder to fix? These are not the root cause, but they amplified the impact. Common examples: missing monitoring, incomplete runbooks, cascading failures, on-call response gaps.

### What Went Well
What worked during the incident response? Detection speed, team coordination, mitigation effectiveness. Be specific. This section builds trust and reinforces good practices.

### What Went Wrong
What failed during the incident response? Slow detection, missing alerts, inadequate runbooks, communication gaps. Be direct — this is not the place for hedging.

### Action Items
Table format with columns: Action, Owner, Priority (P0/P1/P2), Due Date, Status.

Every action item must have an owner and a date. "Improve monitoring" is not an action item. "Add latency p99 alert for payment-service with 500ms threshold — @jane — P0 — 2026-04-01" is.

## Optional Sections

### Detection Analysis
How was the incident detected? Was it automated alerting, customer reports, or an engineer noticing? What should have detected it earlier?

### Customer Communication
What was communicated to customers and when? Was the communication timely and accurate?

### Appendix: Metrics and Logs
Supporting data that's too detailed for the main body: error rate graphs, log excerpts, configuration diffs.

---

## Format Guidance

- **Use timestamps consistently.** Pick one timezone and stick to it. Include timezone abbreviation.
- **Use tables** for timelines, action items, and impact summaries.
- **Be blame-free but specific.** Name systems and processes, not people. "The deployment pipeline lacked a canary step" not "someone deployed without checking."
- **Link action items to findings.** Every "what went wrong" should have a corresponding action item.
