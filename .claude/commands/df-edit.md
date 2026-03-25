---
description: "DocForge Stage 5: Edit the draft based on human feedback on the review"
argument-hint: "Your feedback: which findings to accept/reject, plus any additional changes. E.g.: accept 1,2,4 reject 3 also tighten the intro"
---

Read `.claude/agents/editor/AGENT.md` and follow the process defined there exactly.

The human's feedback is: $ARGUMENTS

If no feedback argument was provided, stop and ask: "Please tell me which findings to accept or reject, and any additional changes. Example: `accept 1,3 reject 2 also shorten the executive summary`"

Find the latest `draft-vN.md` and `review-vN.md` in `workspace/`. Read both. Apply the human's feedback.

Save the revised document as `workspace/draft-vN+1.md` (increment the version number by 1).
