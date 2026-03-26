---
description: "DocForge Stage 3: Draft the complete document from brief + research + grounding files"
argument-hint: "Optional: document type override (strategy/vision/rfc/erd/abstract/postmortem/adr) or 'sections:1-3' for sectional drafting"
---

Read `workspace/.active-project` to determine the active project. If no active project is set, stop and tell the human: "No active project. Run `/df-ideation` to start a new project, or say 'switch to [project name]' to resume one."

Read `.claude/agents/drafter/AGENT.md` and follow the process defined there exactly.

If the argument ($ARGUMENTS) contains a document type (strategy, vision, rfc, erd, abstract, postmortem, adr), use that type instead of the one in the brief.

If the argument contains "sections:" followed by section numbers or names, draft only those sections (see Sectional Drafting in the agent briefing).

Check that both `workspace/{project}/brief.md` and `workspace/{project}/research.md` exist. If either is missing, stop and tell the human which stage to run first.

When done, save the output to `workspace/{project}/draft-v1.md`.
