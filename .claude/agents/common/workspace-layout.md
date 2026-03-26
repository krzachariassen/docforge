# Workspace Layout

DocForge uses **project-scoped workspaces**. Each project gets its own folder under `workspace/`, with fully isolated artifacts. Projects can run in parallel across different sessions.

## Structure

```
workspace/
├── .active-project                    # Plain text file containing the active project slug
├── erd-catalog-notifications/         # One project
│   ├── PROJECT.md                     # Project memory (persistent across sessions)
│   ├── brief.md
│   ├── research.md
│   ├── grounding/
│   ├── draft-v1.md
│   ├── review-v1.md
│   ├── draft-v2.md
│   ├── FINAL.md
│   └── deck.md
├── inca-strategy-review/              # Another project
│   ├── PROJECT.md
│   ├── brief.md
│   ├── grounding/
│   └── deck.md
```

## Active Project

`workspace/.active-project` contains the slug of the current project (e.g., `erd-catalog-notifications`). All agents read from and write to `workspace/{active project}/`. The orchestrator (`CLAUDE.md`) resolves this on every interaction.

## PROJECT.md — Project Memory

Every project has a `PROJECT.md` file that persists across sessions. It contains:
- **Metadata**: project name, document type, created date, audience
- **Current stage**: where the pipeline stands
- **Progress log**: chronological entries of what happened each session
- **Key decisions**: decisions made and their rationale
- **Open items**: what's pending or blocked
- **Human preferences**: tone, style, audience expectations

The orchestrator reads `PROJECT.md` first when resuming a project and updates it after significant interactions.

## File Naming Convention

All paths below are relative to the active project folder (`workspace/{project}/`):

| File | Stage that creates it | Description |
|------|-----------------------|-------------|
| `PROJECT.md` | Ideation (project creation) | Project memory — persistent across sessions |
| `brief.md` | Ideation | Structured brief: thesis, audience, key arguments, scope |
| `research.md` | Research | Evidence package: validated claims, blind spots |
| `grounding/` | Human (manual) | Files the human copies in — existing docs, data, code |
| `draft-v1.md` | Drafting | First complete draft |
| `review-v1.md` | Review | Adversarial critique of draft-v1 |
| `draft-v2.md` | Editing | Revised draft after first edit cycle |
| `review-v2.md` | Review | Adversarial critique of draft-v2 (if looping) |
| `FINAL.md` | Polish | Final polished document |
| `deck.md` | Presentation | Slide deck outline |

## Version Numbering

Draft and review files are versioned together: `draft-v1.md` is reviewed in `review-v1.md`, then edited into `draft-v2.md`. Always match version numbers.

## Finding the Latest Draft

When a command says "find the latest draft", look for the `draft-vN.md` file in the active project folder with the highest N. Same logic applies to reviews.

## Grounding Files

The human manually copies relevant files into the active project's `grounding/` folder before running `/df-draft`. The Drafter and Researcher read everything in that directory. Files can be: existing strategy docs, architecture diagrams (as text), data exports, API specs, system inventories, metrics — anything that grounds the document in reality.

**Grounding files are what make documents concrete instead of generic.**

## Mid-Pipeline Updates

The human can update the brief and research at any point using `/df-supplement`:
- New arguments or structure notes are added to `brief.md`
- New evidence or context is added to `research.md`
- Author-specified content is added to the brief for the editor to incorporate

These updates are marked with "[added by author]" so agents know they are human-provided additions.

## Project Isolation

Never read from or write to a project folder other than the active one. Each project is its own world. The only shared resource is `.claude/memory/MEMORY.md` (cross-project learnings).

## Starting a New Project

To start a new project, tell DocForge what you want to write. The ideation agent will ask for a project name, create the folder structure, initialize `PROJECT.md`, and begin ideation.

## Switching Projects

Say "switch to [project name]" or "pick up [project name]". DocForge will update `.active-project`, read the project's `PROJECT.md`, and summarize where things stand.
