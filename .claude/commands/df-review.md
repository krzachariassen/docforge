---
description: "DocForge Stage 4: Adversarial review of the latest draft (cold read — no prior context)"
argument-hint: "Optional: review mode — 'structural', 'substance', or 'audience' for focused review"
---

Read `workspace/.active-project` to determine the active project. If no active project is set, stop and tell the human: "No active project. Run `/df-ideation` to start a new project, or say 'switch to [project name]' to resume one."

Read `.claude/agents/reviewer/AGENT.md` and follow the process defined there exactly.

**CRITICAL**: Find the latest `draft-vN.md` in `workspace/{project}/` (highest version number). Read ONLY that file. Do NOT read `workspace/{project}/brief.md`, `workspace/{project}/research.md`, or any files in `workspace/{project}/grounding/`. See `.claude/rules/adversarial-review.md` for why this constraint exists.

If the argument ($ARGUMENTS) specifies a review mode (structural, substance, audience), focus the review on that dimension. Otherwise, do a full review.

For long documents (5,000+ words), suggest focused follow-up reviews after the human addresses findings.

Save the review to `workspace/{project}/review-vN.md` where N matches the draft version you reviewed.
