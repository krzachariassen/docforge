# Workspace Conventions

## Project-Scoped Workspaces

`workspace/` contains project folders. Each project has its own isolated workspace with its own artifacts. The active project is tracked in `workspace/.active-project`.

```
workspace/
├── .active-project          # Contains the active project slug
├── {project-slug}/          # Isolated project workspace
│   ├── PROJECT.md           # Project memory (metadata, progress, decisions)
│   ├── brief.md             # Structured brief
│   ├── research.md          # Evidence package
│   ├── grounding/           # Human-provided context files
│   ├── draft-vN.md          # Versioned drafts
│   ├── review-vN.md         # Versioned reviews
│   ├── FINAL.md             # Finished document
│   └── deck.md              # Presentation deck
```

## What Goes in a Project Folder

Only pipeline artifacts and project memory:
- `PROJECT.md` — project memory (persistent across sessions)
- `brief.md`, `research.md` — stage outputs
- `grounding/` — files the human manually adds before drafting
- `draft-vN.md`, `review-vN.md` — versioned drafts and reviews
- `FINAL.md` — the finished document
- `deck.md` — presentation deck

## What Does NOT Go in workspace/

- Agent briefings (those live in `.claude/agents/`)
- Templates (those live in `.claude/templates/`)
- Memory (cross-project memory lives in `.claude/memory/`)
- Rules (those live in `.claude/rules/`)

## Project Isolation

Never read from or write to a project folder other than the active one. Each project is its own world. The only shared resource is `.claude/memory/MEMORY.md`.

## Grounding Files

The human copies relevant files into the active project's `grounding/` folder before running `/df-draft`. Any file type that Claude can read is valid. Good grounding files: existing strategy docs, architecture decisions, data exports, API specs, team context.

The Drafter reads everything in the project's `grounding/` folder and uses specifics from those files to make the document concrete rather than generic.

## PROJECT.md — Project Memory

Every project has a `PROJECT.md` that persists across sessions. The orchestrator reads it first when resuming a project and updates it after significant interactions. It tracks: metadata, current pipeline stage, progress log, key decisions, open items, and human preferences. See `workspace-layout.md` for the full format.
