---
description: "DocForge Stage 4: Adversarial review of the latest draft (cold read — no prior context)"
argument-hint: "Optional: review mode — 'structural', 'substance', or 'audience' for focused review"
---

Read `.claude/agents/reviewer/AGENT.md` and follow the process defined there exactly.

**CRITICAL**: Find the latest `draft-vN.md` in `workspace/` (highest version number). Read ONLY that file. Do NOT read `workspace/brief.md`, `workspace/research.md`, or any files in `workspace/grounding/`. See `.claude/rules/adversarial-review.md` for why this constraint exists.

If the argument ($ARGUMENTS) specifies a review mode (structural, substance, audience), focus the review on that dimension. Otherwise, do a full review.

For long documents (5,000+ words), suggest focused follow-up reviews after the human addresses findings.

Save the review to `workspace/review-vN.md` where N matches the draft version you reviewed.
