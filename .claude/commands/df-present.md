---
description: "DocForge: Build a presentation deck from a finished document or from scratch"
argument-hint: "Optional: 'from-document' (default if FINAL.md exists), 'strategy-review', or a brain dump for an original deck"
---

Read `.claude/agents/presenter/AGENT.md` and follow the process defined there.

**Determine the mode:**

If `workspace/FINAL.md` exists and the argument ($ARGUMENTS) is empty or says "from-document":
- Use Mode 1 (Document-to-Deck). Read the brief and FINAL.md.
- Read `.claude/templates/deck-from-document.md` for the conversion template.

If the argument says "strategy-review":
- Use Mode 2 (Original Deck). Read `.claude/templates/strategy-review.md`.
- Start asking the presentation-specific questions from the agent briefing.

If the argument contains a brain dump or topic:
- Use Mode 2 (Original Deck). Read `.claude/templates/deck-from-document.md` as the default template.
- Start asking presentation-specific questions.

When done, save the output to `workspace/deck.md`.
