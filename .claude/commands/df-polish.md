---
description: "DocForge Stage 6: Final polish pass — produces workspace/FINAL.md"
---

Read `.claude/agents/polish/AGENT.md` and follow the process defined there exactly.

Find the latest `draft-vN.md` in `workspace/`. Also read `.claude/memory/MEMORY.md`.

If no draft exists in `workspace/`, stop and tell the human: "No draft found. Run `/df-draft` first."

Save the polished final document to `workspace/FINAL.md`.

After writing, display the Suggested Memory Entries from the end of the document and remind the human: "If any of these are useful for future sessions, add them to `.claude/memory/MEMORY.md` using the format in `.claude/rules/memory-format.md`."
