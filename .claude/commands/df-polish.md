---
description: "DocForge Stage 6: Final polish pass — produces FINAL.md in the active project"
---

Read `workspace/.active-project` to determine the active project. If no active project is set, stop and tell the human: "No active project. Run `/df-ideation` to start a new project, or say 'switch to [project name]' to resume one."

Read `.claude/agents/polish/AGENT.md` and follow the process defined there exactly.

Find the latest `draft-vN.md` in `workspace/{project}/`. Also read `.claude/memory/MEMORY.md`.

If no draft exists in `workspace/{project}/`, stop and tell the human: "No draft found in the active project. Run `/df-draft` first."

Save the polished final document to `workspace/{project}/FINAL.md`.

After writing, display the Suggested Memory Entries from the end of the document and remind the human: "If any of these are useful for future sessions, add them to `.claude/memory/MEMORY.md` using the format in `.claude/rules/memory-format.md`."
