---
description: "DocForge: Show all projects, pipeline status, and recommended next step"
---

## Multi-Project Status

1. List all project folders in `workspace/` (each subdirectory that contains a `PROJECT.md`)
2. Read `workspace/.active-project` to determine the active project (if set)
3. For each project folder, read its `PROJECT.md` and extract:
   - Project name
   - Document type
   - Current stage
   - Last session date (from the most recent progress log entry)

Display a project overview table:

```
| Project | Type | Stage | Last Active | Active? |
|---------|------|-------|-------------|---------|
| [slug]  | erd  | draft-v2 complete | Mar 25 | ← active |
| [slug]  | strategy | research complete | Mar 20 | |
```

If no projects exist, tell the human: "No projects found. Run `/df-ideation "your idea"` to start your first project."

## Active Project Detail

For the active project, also check for specific artifacts in the project folder and show detailed status:

| File | Status |
|------|--------|
| `PROJECT.md` | exists |
| `brief.md` | exists / missing |
| `research.md` | exists / missing |
| `grounding/` | N files / empty |
| `draft-v1.md` | exists / missing |
| `review-v1.md` | exists / missing |
| [any additional draft-vN / review-vN] | exists |
| `FINAL.md` | exists / missing |
| `deck.md` | exists / missing |

Then determine the recommended next command for the active project:

- **No brief** → Run `/df-ideation "your idea"` to begin
- **brief only** → Add grounding files to `workspace/{project}/grounding/`, then run `/df-research`
- **brief + research, no draft** → Review the Grounding Assessment in `research.md`. Add any missing grounding files, then run `/df-draft`
- **draft exists, no matching review** → Run `/df-review` (or `/df-review structural` / `substance` / `audience` for a focused review)
- **review exists, no newer draft** → Read the review, then run `/df-edit "your feedback"`
- **multiple drafts, no FINAL.md** → Run `/df-review` for another cycle, or `/df-polish` if content is ready
- **FINAL.md exists, no deck** → Pipeline complete. Run `/df-present` to build a slide deck, or `/df-present strategy-review` for a leadership review deck.
- **deck.md exists** → Presentation deck ready

## Project Management Commands

Remind the human of project management options:
- **Switch projects**: "switch to [project name]"
- **Start new project**: `/df-ideation "your idea"` or "start a new project"
- **List projects**: `/df-status` (this command)

**At any point**: Run `/df-supplement` to add context, content, or direction to the active project.

Show the recommended next command clearly.
