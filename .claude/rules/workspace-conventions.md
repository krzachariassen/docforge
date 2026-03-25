# Workspace Conventions

## The workspace/ Directory

`workspace/` is the active document session. It is gitignored — its contents are not committed to the repository. This is intentional: the workspace is working state, not source of truth.

## What Goes in workspace/

Only pipeline artifacts:
- `brief.md`, `research.md` — stage outputs
- `grounding/` — files the human manually adds before drafting
- `draft-vN.md`, `review-vN.md` — versioned drafts and reviews
- `FINAL.md` — the finished document

## What Does NOT Go in workspace/

- Agent briefings (those live in `.claude/agents/`)
- Templates (those live in `.claude/templates/`)
- Memory (that lives in `.claude/memory/`)
- Rules (those live in `.claude/rules/`)

## Starting a New Document

To start a new document session, clear the workspace:
```
rm workspace/*.md workspace/grounding/*
```
(Keep `.gitkeep` files)

## Grounding Files

The human copies relevant files into `workspace/grounding/` before running `/df-draft`. Any file type that Claude can read is valid. Good grounding files: existing strategy docs, architecture decisions, data exports, API specs, team context.

The Drafter reads everything in `workspace/grounding/` and uses specifics from those files to make the document concrete rather than generic.
