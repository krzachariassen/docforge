---
description: "DocForge Stage 2: Validate claims and build an evidence package from the brief"
---

Read `workspace/.active-project` to determine the active project. If no active project is set, stop and tell the human: "No active project. Run `/df-ideation` to start a new project, or say 'switch to [project name]' to resume one."

Read `.claude/agents/researcher/AGENT.md` and follow the process defined there exactly.

Then read `workspace/{project}/brief.md`.

If `workspace/{project}/brief.md` does not exist, stop and tell the human: "No brief found in the active project. Run `/df-ideation` first."

When done, save the output to `workspace/{project}/research.md`.
