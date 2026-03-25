# DocForge

A document writing partner built with Claude Code. No application code — just markdown files that turn Claude into a structured writing collaborator.

## How It Works

Open this project and start chatting. DocForge automatically knows what stage you're at and what to do next.

```
You:    "I want to write a strategy doc about treating AI as specialized
         engineers instead of one general assistant"

Claude: [Assesses complexity → asks clarifying questions one at a time]
Claude: [After 8-10 questions → produces workspace/brief.md]
Claude: "Brief saved. Add grounding files and do your own research, then
         we'll validate your claims."

You:    [Copy existing docs, system inventories, research to workspace/grounding/]
You:    "Ready, validate my claims"

Claude: [Reads brief + grounding files → validates every claim]
Claude: [Produces workspace/research.md with evidence + gaps]
Claude: "Your grounding is solid. Missing: KTLO volume data. Ready to draft?"

You:    "Draft the problem statement and proposed approach first"

Claude: [Sectional drafting → produces first sections of workspace/draft-v1.md]
Claude: "First sections ready. Review them, then we'll draft architecture."

You:    "Looks good. Draft the architecture section. Here's the agent
         definition I want included verbatim: [code block]"

Claude: [Drafts architecture with author-specified content → adds to draft]

You:    "Review the full document for substance"

Claude: [Cold read — no brief/research context → focused substance review]
Claude: [Produces workspace/review-v1.md with findings]

You:    "Accept 1,3,5. Reject 2. Also add a governance section — here's
         what I want in it: autonomy policy, security, kill switch..."

Claude: [Implements finding fixes + author-directed content → workspace/draft-v2.md]

You:    "Polish it"

Claude: [Final pass → workspace/FINAL.md]
```

No commands to remember. You just talk. Claude figures out the stage and routes to the right agent.

## The Human's Role

DocForge is a **collaboration framework**. The quality depends on what you put in:

| What you provide | How it enters the pipeline |
|-----------------|---------------------------|
| Your raw thinking | Chat naturally — the ideation agent draws it out |
| Internal context (existing docs, inventories, metrics) | Copy files to `workspace/grounding/` |
| External research (industry data, competitive analysis) | Use ChatGPT Deep Research, Perplexity, Google Scholar, or whatever you prefer — save results to `workspace/grounding/` |
| Specific content (code, definitions, examples, tables) | Tell the editor to include it, or add to `workspace/grounding/author-content.md` |
| Judgment and direction | Accept/reject review findings, direct expansions, set priorities |
| Memory curation | Decide which learnings persist for future sessions |

For a short ADR, you might provide a brain dump and a few answers. For a Blueprint strategy document, expect to be actively involved throughout — detailed answers, grounding files, research, content injection, and review feedback.

## Slash Commands (Optional)

You don't need these — just chat. But if you prefer explicit control:

| Command | What it does |
|---------|-------------|
| `/df-ideation "brain dump"` | Start ideation |
| `/df-research` | Validate claims |
| `/df-draft` | Draft (or `sections:1-3` for sectional drafting) |
| `/df-review` | Adversarial review (or `structural` / `substance` / `audience`) |
| `/df-edit "feedback"` | Edit with feedback |
| `/df-polish` | Final polish |
| `/df-supplement "additions"` | Add context mid-pipeline |
| `/df-status` | Show pipeline state |

## Document Types

| Type | Template | When to use |
|------|----------|-------------|
| **Strategy** | `.claude/templates/strategy.md` | Technology bets, platform investments, multi-team initiatives |
| **Vision** | `.claude/templates/vision.md` | Future state, product direction, north star |
| **RFC** | `.claude/templates/rfc.md` | Technical proposals, architecture decisions |
| **Postmortem** | `.claude/templates/postmortem.md` | Incident analysis, root cause, action items |
| **ADR** | `.claude/templates/adr.md` | Single architectural decision records |

## Getting Started

1. Open this folder in your IDE with Claude
2. Start chatting about what you want to write
3. Add grounding files to `workspace/grounding/` when prompted
4. Follow the conversation through the pipeline
5. Your finished document is at `workspace/FINAL.md`

## Project Structure

```
docforge/
├── CLAUDE.md                    # Auto-routing orchestrator (always active)
├── DEVELOPMENT.md               # Instructions for modifying DocForge itself
├── .claude/
│   ├── commands/                # Slash command shortcuts (optional)
│   ├── agents/                  # Agent briefings
│   │   ├── ideation/AGENT.md
│   │   ├── researcher/AGENT.md
│   │   ├── drafter/AGENT.md
│   │   ├── reviewer/AGENT.md
│   │   ├── editor/AGENT.md
│   │   └── polish/AGENT.md
│   ├── templates/               # Document-type templates
│   ├── memory/MEMORY.md         # Cross-session learnings
│   └── rules/                   # Behavioral rules
└── workspace/                   # Active document session (gitignored)
    ├── brief.md
    ├── research.md
    ├── grounding/               # Your context files go here
    ├── draft-v*.md
    ├── review-v*.md
    └── FINAL.md
```
