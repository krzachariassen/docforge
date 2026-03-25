# DocForge Pipeline Overview

DocForge is a multi-stage document writing pipeline. Each stage is a separate Claude Code command that invokes a specific agent. The human orchestrates the flow by running commands in sequence.

## Pipeline Stages

| Command | Agent | Input | Output |
|---------|-------|-------|--------|
| `/df-ideation` | Ideation Partner | Human's brain dump | `workspace/brief.md` |
| `/df-research` | Research Agent | `brief.md` | `workspace/research.md` |
| `/df-draft` | Drafter | `brief.md` + `research.md` + `grounding/*` | `workspace/draft-v1.md` |
| `/df-review` | Adversarial Reviewer | Latest `draft-vN.md` ONLY | `workspace/review-vN.md` |
| `/df-edit` | Editor | Latest draft + human feedback | `workspace/draft-vN+1.md` |
| `/df-polish` | Polish Agent | Latest draft + `memory/MEMORY.md` | `workspace/FINAL.md` |

## Key Constraints

- **The reviewer reads cold.** It sees only the draft — no brief, no research, no grounding files. This is the most important architectural rule in the system.
- **The reviewer uses a different model than the drafter.** Independent review requires genuine independence.
- **The human decides what feedback to accept.** Review findings pass through human judgment before reaching the editor.
- **The workspace is the state.** All artifacts are markdown files in `workspace/`. No database.
- **Memory accumulates over time.** The Polish Agent suggests learnings; humans decide what goes into `memory/MEMORY.md`.

## Review Loop

After `/df-edit`, the human can loop: run `/df-review` again on the new draft, then `/df-edit` again with new feedback. Maximum recommended: 3 cycles. Then `/df-polish` to finalize.
