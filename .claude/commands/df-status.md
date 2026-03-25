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

Then determine the current stage and recommended next command:

- **No files** → Run `/df-ideation "your idea"` to begin
- **brief.md only** → Run `/df-research`
- **brief + research, no draft** → (Optionally add files to `workspace/grounding/`) Run `/df-draft`
- **draft exists, no matching review** → Run `/df-review`
- **review exists, no newer draft** → Read `workspace/review-vN.md`, then run `/df-edit "your feedback"`
- **multiple drafts, no FINAL.md** → Run `/df-review` for another cycle, or `/df-polish` if content is ready
- **FINAL.md exists** → Pipeline complete. Document at `workspace/FINAL.md`

Show the recommended next command clearly.
