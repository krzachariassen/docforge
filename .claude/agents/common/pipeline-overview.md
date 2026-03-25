# DocForge Pipeline Overview

DocForge is a multi-stage document writing pipeline. Each stage is a separate Claude Code command that invokes a specific agent. The human orchestrates the flow by running commands in sequence — and contributes context, content, and judgment throughout.

## The Human's Role

DocForge is a collaboration framework, not an autonomous document generator. The quality of the final document depends directly on what the human puts in:

- **Ideation**: The human provides the raw thinking and answers clarifying questions. More detailed answers = richer brief.
- **Grounding & research**: The human copies relevant files into `workspace/grounding/` — existing docs, system inventories, metrics, and their own external research (from ChatGPT Deep Research, Perplexity, Google Scholar, internal wikis, expert conversations, or any other source). This is what makes documents concrete instead of generic.
- **Reviewing**: The human reads the adversarial review, decides what to accept/reject, and adds their own feedback.
- **Editing**: The human talks to the editor like a normal AI conversation — "expand this section", "add a governance section with these details", "here's the data for the metrics table". The editor handles both finding-level fixes and author-directed content. For large amounts of content, the human can also add a file to `workspace/grounding/` (e.g., `author-content.md`) and tell the editor to incorporate it.
- **Memory**: The human curates what goes into cross-session memory.

For complex documents (strategies, visions), expect the human to be actively involved throughout. A strategy document written with minimal human input will be thin. One written with the human contributing context, research, and specific content at every stage will be publication-quality.

## Pipeline Stages

| Command | Agent | Input | Output |
|---------|-------|-------|--------|
| `/df-ideation` | Ideation Partner | Human's brain dump | `workspace/brief.md` |
| `/df-research` | Research Agent | `brief.md` + `grounding/*` | `workspace/research.md` |
| `/df-draft` | Drafter | `brief.md` + `research.md` + `grounding/*` | `workspace/draft-v1.md` |
| `/df-review` | Adversarial Reviewer | Latest `draft-vN.md` ONLY | `workspace/review-vN.md` |
| `/df-edit` | Editor | Latest draft + human feedback | `workspace/draft-vN+1.md` |
| `/df-polish` | Polish Agent | Latest draft + `memory/MEMORY.md` | `workspace/FINAL.md` |
| `/df-supplement` | (utility) | Human's additions | Updates `brief.md` or `research.md` |
| `/df-status` | (utility) | — | Pipeline status + next step |

## Key Constraints

- **The reviewer reads cold.** It sees only the draft — no brief, no research, no grounding files. This is the most important architectural rule in the system.
- **The human decides what feedback to accept.** Review findings pass through human judgment before reaching the editor.
- **The workspace is the state.** All artifacts are markdown files in `workspace/`. No database.
- **Memory accumulates over time.** The Polish Agent suggests learnings; humans decide what goes into `.claude/memory/MEMORY.md`.
- **Complex documents need multiple human touchpoints.** The pipeline supports mid-process context injection via `/df-supplement` and content-rich feedback to the editor.

## Review Loop

After `/df-edit`, the human can loop: run `/df-review` again on the new draft, then `/df-edit` again with new feedback. For complex documents, use focused review modes:
- `/df-review structural` — organization and flow
- `/df-review substance` — argument quality and evidence
- `/df-review audience` — audience fit and clarity

Maximum recommended: 3 full review cycles. Then `/df-polish` to finalize.

## Sectional Drafting (Complex Documents)

For long documents, the human can draft section by section:
1. `/df-draft sections:1-3` — draft the first three sections
2. Review, supplement with context
3. `/df-draft sections:4-6` — draft the next sections
4. Continue until all sections are drafted, then review the full document

This allows the human to provide context between sections, which produces much stronger documents than a single full-draft pass.
