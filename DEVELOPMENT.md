# DocForge Development Guide

Instructions for modifying DocForge itself. If you're using DocForge to write a document, you don't need this file — just start chatting.

## What This Project Is

DocForge is a **Claude Code custom commands project**. There is NO application code. No Python. No CLI tool. No package manager. No dependencies.

The project consists of:
1. **CLAUDE.md** — the auto-routing orchestrator (always active)
2. **8 slash commands** (`.claude/commands/*.md`) — explicit command shortcuts
3. **6 agent briefings** (`.claude/agents/*/AGENT.md`) — define each agent's behavior
4. **5 document-type templates** (`.claude/templates/*.md`) — section structures
5. **1 memory file** (`.claude/memory/MEMORY.md`) — cross-session learnings
6. **Supporting files** — common docs, rules, workspace skeleton

Everything is markdown files.

## CRITICAL: What NOT to Build

- **NO Python files.** Not even a script.
- **NO package managers.** No `pyproject.toml`, no `requirements.txt`, no `package.json`.
- **NO application code.** No source directories, no modules, no imports.
- **NO database.** The `workspace/` directory IS the state.
- **NO CLI tool.** CLAUDE.md IS the interface.

If you find yourself writing code, stop.

## Architecture

### The Orchestrator (CLAUDE.md)

CLAUDE.md is the auto-routing orchestrator. On every interaction, it tells Claude to:
1. Check `workspace/` state to determine the current pipeline stage
2. Read the user's message to determine intent
3. Route to the appropriate agent by reading its `AGENT.md`
4. Act accordingly

The user never needs to remember slash commands — they just chat. The orchestrator figures out what to do.

### Agent Briefings

Each agent is a complete role definition in `.claude/agents/<role>/AGENT.md`:
- **Ideation Partner** — turns brain dumps into structured briefs
- **Research Agent** — validates claims, reads grounding files, flags gaps
- **Drafter** — produces the document (supports sectional drafting)
- **Adversarial Reviewer** — cold-read critique (focused modes: structural/substance/audience)
- **Editor** — implements finding fixes AND author-directed content
- **Polish Agent** — final pass for durability, consistency, and quality

### Templates

Each template (`.claude/templates/*.md`) defines:
- Core sections with per-section writing guidance
- Optional sections (governance, appendices, etc.)
- Recommended sectional drafting order for complex documents
- Format guidance (tables, diagrams, code blocks)
- What the human needs to contribute

### Slash Commands

The `/df-*` commands in `.claude/commands/` are explicit shortcuts. They're optional — the orchestrator in CLAUDE.md handles routing automatically from plain chat. Commands exist for users who prefer explicit control.

### Supporting Files

- `.claude/agents/common/` — pipeline overview, workspace layout
- `.claude/rules/` — adversarial review constraint, workspace conventions, memory format
- `.claude/memory/MEMORY.md` — cross-session learnings (curated by humans)

## File Inventory

### Agent Briefings
- `.claude/agents/ideation/AGENT.md`
- `.claude/agents/researcher/AGENT.md`
- `.claude/agents/drafter/AGENT.md`
- `.claude/agents/reviewer/AGENT.md`
- `.claude/agents/editor/AGENT.md`
- `.claude/agents/polish/AGENT.md`

### Templates
- `.claude/templates/strategy.md`
- `.claude/templates/vision.md`
- `.claude/templates/rfc.md`
- `.claude/templates/postmortem.md`
- `.claude/templates/adr.md`

### Commands
- `.claude/commands/df-ideation.md`
- `.claude/commands/df-research.md`
- `.claude/commands/df-draft.md`
- `.claude/commands/df-review.md`
- `.claude/commands/df-edit.md`
- `.claude/commands/df-polish.md`
- `.claude/commands/df-supplement.md`
- `.claude/commands/df-status.md`

### Supporting
- `.claude/agents/common/pipeline-overview.md`
- `.claude/agents/common/workspace-layout.md`
- `.claude/rules/adversarial-review.md`
- `.claude/rules/workspace-conventions.md`
- `.claude/rules/memory-format.md`
- `.claude/memory/MEMORY.md`

## Modifying Agents

To change an agent's behavior, edit its `AGENT.md`. The key sections:
- **Role**: Who the agent is
- **Process**: Step-by-step instructions
- **Rules**: Hard constraints
- **Output Format**: Exact structure of output

Changes take effect immediately — there's no build step.

## Adding a New Document Type

1. Create `.claude/templates/<type>.md` with section structure
2. Add the type to the ideation agent's Recommended Document Type options
3. That's it — the drafter reads the template automatically

## Adding a New Agent

Not currently needed — the 6 agents cover the full pipeline. But if you want to add one:
1. Create `.claude/agents/<name>/AGENT.md`
2. Add a routing rule in CLAUDE.md
3. Optionally create a `/df-<name>` command shortcut
