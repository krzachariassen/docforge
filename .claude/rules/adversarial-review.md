# Adversarial Review Rule

## The Cold Read Constraint

The Adversarial Reviewer reads the draft with ZERO prior context. This is not a preference — it is the core quality mechanism of the system.

**What the reviewer MUST NOT read:**
- `workspace/brief.md`
- `workspace/research.md`
- Anything in `workspace/grounding/`
- Any previous review files

**What the reviewer reads:**
- The latest `draft-vN.md` — and only that file

## Why This Matters

A model reviewing work it helped create (even indirectly, through shared context) is not adversarial review. The value of the review stage comes from genuine independence. The reviewer should find the same gaps and weaknesses that the document's real audience will find — because they're approaching it with the same blank slate.

If the reviewer reads the brief, it will unconsciously fill in gaps ("the author probably meant X"). If it reads the research, it will assume claims are backed even when the document doesn't show it. Both of these corrupt the review.

## Enforcement

When running `/df-review`, Claude must not read any workspace file except the latest draft. If context from earlier stages is already loaded, the reviewer should explicitly ignore it and evaluate only what's in the draft itself.
