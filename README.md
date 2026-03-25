# DocForge

A multi-agent document writing system built entirely with Claude Code custom commands. No application code. No Python. No infrastructure. Just `.claude/commands/` markdown files and agent briefing documents.

## What This Is

DocForge uses the same pattern as any Claude Code custom command (`/pr_create`, `/diff-coverage`, etc.): a markdown file in `.claude/commands/` that instructs Claude to follow a structured process. The difference is that DocForge defines a **multi-stage pipeline** where each stage is a separate command with a separate agent briefing, and the human orchestrates the flow by invoking commands in sequence.

## How It Works

The engineer runs commands in sequence. Each command instructs Claude to read a specific agent briefing, load the artifacts from previous stages, and produce the next artifact.

```
Human runs /df-ideation "my raw idea..."
  → Claude reads agents/ideation/AGENT.md
  → Claude asks clarifying questions
  → Claude produces workspace/brief.md

Human runs /df-research
  → Claude reads agents/researcher/AGENT.md
  → Claude reads workspace/brief.md
  → Claude produces workspace/research.md

Human runs /df-draft
  → Claude reads agents/drafter/AGENT.md
  → Claude reads workspace/brief.md + workspace/research.md + workspace/grounding/*
  → Claude produces workspace/draft-v1.md

Human runs /df-review
  → Claude reads agents/reviewer/AGENT.md
  → Claude reads workspace/draft-v1.md ONLY (no brief, no research -- cold read)
  → Claude produces workspace/review-v1.md

Human reviews the critique, decides what to accept/reject

Human runs /df-edit "accept findings 1,3,5 -- reject 2,4"
  → Claude reads agents/editor/AGENT.md
  → Claude reads workspace/draft-v1.md + the human's feedback
  → Claude produces workspace/draft-v2.md

(Optional: loop /df-review + /df-edit again)

Human runs /df-polish
  → Claude reads agents/polish/AGENT.md
  → Claude reads latest draft
  → Claude produces workspace/FINAL.md
```

## Key Design Decisions

1. **No application code.** Everything is Claude commands and markdown agent briefings. The human is the orchestrator.
2. **Each stage is a separate command.** The human decides when to move to the next stage, what feedback to accept, and when to loop.
3. **Agents are briefing documents.** Each agent's entire behavior is defined in its `AGENT.md` file -- same pattern as the INCA AI Engineering Strategy.
4. **The workspace directory is the state.** All artifacts (brief, research, drafts, reviews) are markdown files in `workspace/`. No database, no session management.
5. **Grounding files are explicit.** The human copies relevant files into `workspace/grounding/` before running `/df-draft`. The drafter reads everything in that directory.

## Project Structure

```
docforge/
├── .claude/
│   └── commands/                    # Claude Code custom commands
│       ├── df-ideation.md           # Stage 1: Brain dump → Structured brief
│       ├── df-research.md           # Stage 2: Brief → Evidence package
│       ├── df-draft.md              # Stage 3: Brief + research + grounding → Draft
│       ├── df-review.md             # Stage 4: Draft → Adversarial critique
│       ├── df-edit.md               # Stage 5: Draft + feedback → Revised draft
│       ├── df-polish.md             # Stage 6: Final pass → FINAL.md
│       └── df-status.md             # Utility: Show pipeline status
│
├── agents/                          # Agent briefing documents
│   ├── ideation/
│   │   └── AGENT.md                 # Ideation Partner role, process, output format
│   ├── researcher/
│   │   └── AGENT.md                 # Research Agent role, process, output format
│   ├── drafter/
│   │   └── AGENT.md                 # Drafter role, process, output format
│   ├── reviewer/
│   │   └── AGENT.md                 # Adversarial Reviewer role, process, output format
│   ├── editor/
│   │   └── AGENT.md                 # Editor role, process, output format
│   └── polish/
│       └── AGENT.md                 # Polish Agent role, process, output format
│
├── templates/                       # Document-type structure templates
│   ├── strategy.md                  # Strategy document section structure
│   ├── vision.md                    # Vision document section structure
│   ├── rfc.md                       # RFC section structure
│   ├── postmortem.md                # Postmortem section structure
│   └── adr.md                       # Architecture Decision Record structure
│
├── memory/
│   └── MEMORY.md                    # Cross-session operational learnings
│
├── workspace/                       # Active document workspace (gitignored)
│   ├── brief.md                     # Stage 1 output
│   ├── research.md                  # Stage 2 output
│   ├── grounding/                   # Files the human adds for context
│   ├── draft-v1.md                  # Stage 3 output
│   ├── review-v1.md                 # Stage 4 output
│   ├── draft-v2.md                  # Stage 5 output (after first edit)
│   ├── review-v2.md                 # Stage 4 output (second review cycle)
│   ├── draft-v3.md                  # Stage 5 output (after second edit)
│   └── FINAL.md                     # Stage 6 output
│
├── CLAUDE.md                        # Build instructions for the agent
├── README.md                        # This file
└── .gitignore
```

## Getting Started

1. Open this folder in Cursor
2. Run `/df-ideation` with your raw idea
3. Follow the pipeline stage by stage
4. Your finished document is at `workspace/FINAL.md`

## The Pipeline

| Command | Agent | Input | Output | Human Action |
|---------|-------|-------|--------|-------------|
| `/df-ideation` | Ideation Partner | Your raw brain dump | `workspace/brief.md` | Answer clarifying questions |
| `/df-research` | Research Agent | `brief.md` | `workspace/research.md` | Review evidence, add grounding files to `workspace/grounding/` |
| `/df-draft` | Drafter | `brief.md` + `research.md` + `grounding/*` + template | `workspace/draft-v1.md` | Read the draft |
| `/df-review` | Adversarial Reviewer | Latest draft ONLY | `workspace/review-vN.md` | Read the critique, decide what to accept |
| `/df-edit` | Editor | Latest draft + your feedback | `workspace/draft-vN.md` | Review the edits |
| `/df-polish` | Polish Agent | Latest draft + `memory/MEMORY.md` | `workspace/FINAL.md` | Final review, accept memory suggestions |
