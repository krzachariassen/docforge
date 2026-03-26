---
description: "DocForge: Show pipeline status and recommended next step"
---

Check `workspace/` for the following files and report status:

| File | Status |
|------|--------|
| `workspace/brief.md` | exists / missing |
| `workspace/research.md` | exists / missing |
| `workspace/grounding/` | N files / empty |
| `workspace/draft-v1.md` | exists / missing |
| `workspace/review-v1.md` | exists / missing |
| [any additional draft-vN / review-vN] | exists |
| `workspace/FINAL.md` | exists / missing |
| `workspace/deck.md` | exists / missing |

Then determine the current stage and recommended next command:

- **No files** → Run `/df-ideation "your idea"` to begin
- **brief.md only** → Add grounding files to `workspace/grounding/`, then run `/df-research`
- **brief + research, no draft** → Review the Grounding Assessment in `research.md`. Add any missing grounding files, then run `/df-draft`
- **draft exists, no matching review** → Run `/df-review` (or `/df-review structural` / `substance` / `audience` for a focused review)
- **review exists, no newer draft** → Read `workspace/review-vN.md`, then run `/df-edit "your feedback"` — you can accept/reject findings AND add new content
- **multiple drafts, no FINAL.md** → Run `/df-review` for another cycle, or `/df-polish` if content is ready
- **FINAL.md exists, no deck** → Pipeline complete. Document at `workspace/FINAL.md`. Run `/df-present` to build a slide deck, or `/df-present strategy-review` for a leadership review deck.
- **deck.md exists** → Presentation deck ready at `workspace/deck.md`

**At any point**: Run `/df-supplement` to add context, content, or direction to the pipeline.

Show the recommended next command clearly.
