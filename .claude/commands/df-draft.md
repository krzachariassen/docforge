---
description: "DocForge Stage 3: Draft the complete document from brief + research + grounding files"
argument-hint: "Optional: document type override (strategy/vision/rfc/postmortem/adr) or 'sections:1-3' for sectional drafting"
---

Read `.claude/agents/drafter/AGENT.md` and follow the process defined there exactly.

If the argument ($ARGUMENTS) contains a document type (strategy, vision, rfc, postmortem, adr), use that type instead of the one in the brief.

If the argument contains "sections:" followed by section numbers or names, draft only those sections (see Sectional Drafting in the agent briefing).

Check that both `workspace/brief.md` and `workspace/research.md` exist. If either is missing, stop and tell the human which stage to run first.

When done, save the output to `workspace/draft-v1.md`.
