# Workspace Layout

All active document artifacts live in `workspace/`. This directory is gitignored — it contains working state for the current document session.

## File Naming Convention

| File | Stage that creates it | Description |
|------|-----------------------|-------------|
| `workspace/brief.md` | Ideation | Structured brief: thesis, audience, key arguments, scope |
| `workspace/research.md` | Research | Evidence package: validated claims, blind spots, market context |
| `workspace/grounding/` | Human (manual) | Files the human copies in before drafting — existing docs, data, code |
| `workspace/draft-v1.md` | Drafting | First complete draft |
| `workspace/review-v1.md` | Review | Adversarial critique of draft-v1 |
| `workspace/draft-v2.md` | Editing | Revised draft after first edit cycle |
| `workspace/review-v2.md` | Review | Adversarial critique of draft-v2 (if looping) |
| `workspace/draft-v3.md` | Editing | Second revision (if looping) |
| `workspace/FINAL.md` | Polish | Final polished document |

## Version Numbering

Draft and review files are versioned together: `draft-v1.md` is reviewed in `review-v1.md`, then edited into `draft-v2.md`. Always match version numbers.

## Finding the Latest Draft

When a command says "find the latest draft", look for the `draft-vN.md` file in `workspace/` with the highest N. Same logic applies to reviews.

## Grounding Files

The human manually copies relevant files into `workspace/grounding/` before running `/df-draft`. The Drafter reads everything in that directory. Files can be: existing strategy docs, architecture diagrams (as text), data exports, API specs — anything that grounds the document in reality.
