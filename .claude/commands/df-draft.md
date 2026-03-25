---
description: "DocForge Stage 3: Draft the complete document from brief + research + grounding files"
argument-hint: "Optional: document type override (strategy / vision / rfc / postmortem / adr)"
---

Read `.claude/agents/drafter/AGENT.md` and follow the process defined there exactly.

If a document type argument was provided ($ARGUMENTS), use that type instead of the one in the brief.

Check that both `workspace/brief.md` and `workspace/research.md` exist. If either is missing, stop and tell the human which stage to run first.

When done, save the output to `workspace/draft-v1.md`.
