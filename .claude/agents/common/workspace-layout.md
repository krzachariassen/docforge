# Workspace Layout

All active document artifacts live in `workspace/`. This directory is gitignored — it contains working state for the current document session.

## File Naming Convention

| File | Stage that creates it | Description |
|------|-----------------------|-------------|
| `workspace/brief.md` | Ideation | Structured brief: thesis, audience, key arguments, scope, structure notes, author-specified content |
| `workspace/research.md` | Research | Evidence package: validated claims, blind spots, grounding assessment |
| `workspace/grounding/` | Human (manual) | Files the human copies in before drafting — existing docs, data, code, system inventories |
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

The human manually copies relevant files into `workspace/grounding/` before running `/df-draft`. The Drafter and Researcher read everything in that directory. Files can be: existing strategy docs, architecture diagrams (as text), data exports, API specs, system inventories, metrics — anything that grounds the document in reality.

**Grounding files are what make documents concrete instead of generic.** A strategy document about AI engineering grounded with the team's actual CLAUDE.md, rule files, and MCP server inventory will be dramatically stronger than one written from general knowledge alone.

The brief's "Grounding Context Needed" section tells the human what specific files to provide.

## Mid-Pipeline Updates

The human can update the brief and research at any point using `/df-supplement`:
- New arguments or structure notes are added to `workspace/brief.md`
- New evidence or context is added to `workspace/research.md`
- Author-specified content (code blocks, definitions, examples) is added to the brief for the editor to incorporate

These updates are marked with "[added by author]" or "## Supplemental" headers so agents know they are human-provided additions.

## Starting a New Document

To start a new document session, clear the workspace:
```
rm workspace/*.md workspace/grounding/*
```
(Keep `.gitkeep` files)
