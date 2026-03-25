# Postmortem Template

For incident postmortems: service outages, data issues, security incidents, deployment failures, process breakdowns.

**Audience**: Engineers and leadership who want to understand what happened, why, and what prevents recurrence. Blame-free, specific, action-oriented. Vague root causes and fuzzy action items are the failure mode of this document type.

---

## Sections

### Summary
3–5 sentences. What happened, when, what was the impact, what resolved it. Written for someone who wasn't involved.

### Impact
Specific, quantified: duration (start and end with timezone), user/customer impact (how many, what they experienced), business impact (if quantifiable), data impact (if any).

### Timeline
Chronological log with precise timestamps. Include: when the incident started, when detected and how, key investigation steps, when mitigation began and what was done, when fully resolved, all significant actions in order.

### Root Cause
The technical or process cause. Be specific. "A configuration change caused X to do Y" is better than "a configuration issue caused the outage." Describe the chain of failures if applicable.

### Contributing Factors
Conditions that allowed the root cause to have this impact. Not excuses — systemic issues that, if addressed, reduce future risk. Missing alerts, missing safeguards, process gaps, knowledge gaps.

### What Went Well
Specific, honest. What worked during the incident? Important to preserve and reinforce.

### What Went Wrong
Not just root cause — what made this worse than it needed to be?

### Action Items
Each item requires: **What** (specific, concrete), **Owner** (person's name), **Due date** (specific date), **Priority** (P0/P1/P2). Unowned or undated action items do not get done.
