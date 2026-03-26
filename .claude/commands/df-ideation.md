---
description: "DocForge Stage 1: Turn a brain dump into a structured document brief"
argument-hint: "Your raw idea, brain dump, or rough thinking about the document you want to write"
---

Read `.claude/agents/ideation/AGENT.md` and follow the process defined there exactly.

**Project setup**: Read `workspace/.active-project` to check for an active project. If no active project exists (or the human is starting a new document), follow the Project Setup process in the agent briefing to create a new project folder before proceeding with ideation.

The human's input is: $ARGUMENTS

If no argument was provided, ask the human to describe what document they want to write before proceeding.

When done, save the output to `workspace/{project}/brief.md` (where `{project}` is the active project slug).
