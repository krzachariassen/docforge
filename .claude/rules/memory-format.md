# Memory Format Rule

## Cross-Session Memory

`.claude/memory/MEMORY.md` accumulates learnings across document sessions. It is read by the Drafter, Editor, and Polish Agent. It is written to by humans (not automatically by agents).

## How Memory Gets Added

1. The Polish Agent suggests 1–3 memory entries at the end of each session
2. The human reads the suggestions
3. The human decides which entries to add to `.claude/memory/MEMORY.md`
4. No entry is added without human approval

## Entry Format

```markdown
### [YYYY-MM-DD] [document type]
**Category**: structure / tone / claims / audience / process
**Learning**: [one sentence — specific, reusable, non-obvious]
```

## Categories

- **structure**: How to organize this type of document
- **tone**: What register works for this audience
- **claims**: How to bound or validate claims in this context
- **audience**: What this specific audience cares about and how they read
- **process**: Learnings about the pipeline itself (what to do differently)

## Cap Rule

Maximum 50 entries. When at capacity, surface the oldest 10 entries for the human to review (keep or remove) before adding new ones.

## What Makes a Good Memory Entry

Good: specific, reusable, non-obvious
- "Leadership documents at this org always need an explicit resource ask with headcount numbers — a vague 'resource support needed' will be ignored."

Bad: generic, obvious, or not reusable
- "Make sure claims are backed by evidence." (This is in every agent's rules already.)
