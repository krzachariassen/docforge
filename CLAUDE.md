# CLAUDE.md

Instructions for the AI agent building DocForge.

## What You Are Building

DocForge is a **Claude Code custom commands project**. There is NO application code. No Python. No CLI tool. No package manager. No dependencies.

You are building:
1. **7 Claude Code custom commands** (`.claude/commands/*.md`) -- these are the pipeline stages
2. **6 agent briefing documents** (`agents/*/AGENT.md`) -- these define each agent's behavior
3. **5 document-type templates** (`templates/*.md`) -- these define section structures
4. **1 memory file** (`memory/MEMORY.md`) -- cross-session learnings
5. **Supporting files** (`.gitignore`, `workspace/` directory)

That's it. Everything is markdown files. Read `README.md` first for the full project structure and pipeline flow.

## CRITICAL: What NOT to Build

- **NO Python files.** Not even a script. Nothing with `.py` extension.
- **NO package managers.** No `pyproject.toml`, no `requirements.txt`, no `package.json`.
- **NO application code.** No source directories, no modules, no imports.
- **NO database.** The `workspace/` directory IS the state. Markdown files are the artifacts.
- **NO CLI tool.** The Claude Code commands ARE the CLI.
- **NO configuration files** beyond what's listed. No YAML config, no `.env`.

If you find yourself writing code, stop. Everything in this project is a markdown file.

## Build Order

Build in this exact order:

### Step 1: Project Setup
- Create `.gitignore` (ignore `workspace/` contents except `.gitkeep`)
- Create `workspace/.gitkeep`
- Create `workspace/grounding/.gitkeep`

### Step 2: Agent Briefing Documents (all 6)
These are the core of the system. Each one is a complete role definition with process, rules, and output format. Build them from the specifications below.

Create these files:
- `agents/ideation/AGENT.md`
- `agents/researcher/AGENT.md`
- `agents/drafter/AGENT.md`
- `agents/reviewer/AGENT.md`
- `agents/editor/AGENT.md`
- `agents/polish/AGENT.md`

### Step 3: Document-Type Templates (all 5)
Each template defines the section structure for a type of document.

Create these files:
- `templates/strategy.md`
- `templates/vision.md`
- `templates/rfc.md`
- `templates/postmortem.md`
- `templates/adr.md`

### Step 4: Memory File
- Create `memory/MEMORY.md` with the initial structure (empty, with format instructions)

### Step 5: Claude Code Custom Commands (all 7)
These are the pipeline commands the human invokes. Each one instructs Claude to read the right agent briefing, load the right artifacts, and produce the right output.

Create these files:
- `.claude/commands/df-ideation.md`
- `.claude/commands/df-research.md`
- `.claude/commands/df-draft.md`
- `.claude/commands/df-review.md`
- `.claude/commands/df-edit.md`
- `.claude/commands/df-polish.md`
- `.claude/commands/df-status.md`

## Agent Briefing Specifications

Each `AGENT.md` file should contain:
- **Role**: Who the agent is and what its job is
- **Process**: Step-by-step instructions for how it operates
- **Input**: What artifacts it reads (with exact file paths relative to workspace/)
- **Output**: What it produces, with exact format specification
- **Rules**: Hard constraints on behavior
- **Output Format**: The exact markdown structure of its output

### Ideation Partner (`agents/ideation/AGENT.md`)

**Role**: Helps the human turn unstructured thinking into a structured brief.

**Process**:
1. Read the human's brain dump (passed as the command argument)
2. Ask 3-5 clarifying questions, one at a time:
   - What is the core thesis?
   - Who is the audience and what do they care about?
   - What decision should the reader make after reading?
   - What is in scope vs. out of scope?
   - What does the human know that isn't obvious?
3. When the human signals they're done, produce the structured brief

**Output format** (`workspace/brief.md`):
```
# Document Brief

## Thesis
[One paragraph: the core argument]

## Audience
[Who reads this, what they care about, what detail level they expect]

## Key Arguments
1. [Main point 1]
2. [Main point 2]
...

## Open Questions
- [Things to resolve in research stage]

## Scope
**In scope**: ...
**Out of scope**: ...

## Recommended Document Type
[strategy / vision / rfc / postmortem / adr] -- [why]
```

**Rules**:
- Ask questions before producing the brief. Do not jump to output.
- One question at a time.
- The brief reflects the HUMAN'S ideas, not the agent's.
- When the human says "done", "that's it", "go ahead", or similar -- produce the brief.

### Research Agent (`agents/researcher/AGENT.md`)

**Role**: Validates claims, tests hypotheses, finds external evidence, surfaces blind spots.

**Process**:
1. Read `workspace/brief.md`
2. Identify the 3-5 most important claims that need validation
3. For each claim: find supporting evidence, counter-arguments, and confidence level
4. Address each open question from the brief
5. Identify blind spots the brief doesn't mention

**Output format** (`workspace/research.md`):
```
# Research & Evidence Package

## Claims Validation

### Claim: [statement]
**Supporting Evidence**: [specific examples, companies, data]
**Counter-Arguments**: [what could make this wrong]
**Confidence**: HIGH / MEDIUM / LOW

[repeat for each claim]

## Open Questions Addressed
[For each open question from the brief]

## Blind Spots
[Things the brief doesn't mention but should]

## Market Context
[How this direction aligns with industry trends]
```

**Rules**:
- Be specific. Name companies, cite examples.
- Do NOT assume the thesis is correct. Test it.
- If you can't find evidence for a claim, say so.
- Separate facts from interpretation.

### Drafter (`agents/drafter/AGENT.md`)

**Role**: Produces the complete document from brief + research + grounding files + template.

**Process**:
1. Read `workspace/brief.md`
2. Read `workspace/research.md`
3. Read all files in `workspace/grounding/` (if any exist)
4. Read `memory/MEMORY.md`
5. Read the appropriate template from `templates/` based on the document type in the brief
6. Produce the COMPLETE document

**Output**: `workspace/draft-v1.md` (the full document)

**Rules**:
- Produce the FULL document, not an outline
- Every major claim must be backed by evidence from research or grounding files
- Follow the template's section structure
- Match tone to the audience in the brief
- If evidence confidence is MEDIUM or LOW, bound the claim
- Write for the specific audience, not a generic reader

### Adversarial Reviewer (`agents/reviewer/AGENT.md`)

**Role**: Reads the draft cold and finds every weakness.

**Process**:
1. Read the latest draft ONLY (`workspace/draft-vN.md` -- the most recent version)
2. Do NOT read the brief, research, or grounding files. You are reading cold.
3. Produce a numbered list of findings with severity ratings

**Output format** (`workspace/review-vN.md`):
```
# Adversarial Review

## Findings

### Finding 1: [Short title]
**Severity**: CRITICAL / MAJOR / MINOR / POLISH
**Section**: [Which section]
**Issue**: [What's wrong]
**Suggestion**: [How to fix it]

[repeat for each finding]

## What's Working Well
[2-3 specific things the document does effectively]

## Overall Assessment
[One paragraph: is this ready? What's the single most important fix?]
```

**Severity guide**:
- CRITICAL: Cannot send without fixing. Factual errors, fundamental argument gaps, credibility-damaging claims.
- MAJOR: Significantly weakens the document. Missing failure modes, unbounded claims, structural problems.
- MINOR: Worth fixing. Tone issues, redundancy, unclear phrasing.
- POLISH: Nice to have. Word choice, formatting.

**Rules**:
- You are the skeptic. Find problems, not encouragement.
- Do not soften findings.
- Focus on substance over style.
- Flag strong claims without evidence.
- Flag missing failure modes.

### Editor (`agents/editor/AGENT.md`)

**Role**: Incorporates the human's filtered feedback into the draft while maintaining voice.

**Process**:
1. Read the latest draft
2. Read the human's feedback (passed as the command argument -- which findings to accept, reject, or modify)
3. Read the corresponding review file to understand the full context of accepted findings
4. Apply each accepted finding
5. Produce the complete revised document

**Output**: `workspace/draft-vN.md` (next version number)

**Rules**:
- Only change what the feedback asks for
- Maintain the document's existing voice and tone
- If two feedback points conflict, implement the higher-severity one and note the conflict
- Do NOT add new content beyond what feedback requests
- After the document, add a "## Changes Made" section listing what changed and why

### Polish Agent (`agents/polish/AGENT.md`)

**Role**: Final pass for durability, tone, claims, and skimmability.

**Process**:
1. Read the latest draft
2. Read `memory/MEMORY.md`
3. Check for: claims that will age poorly, vendor-specific facts that belong in appendices, tone inconsistencies, unbounded promises, weak headers, weak endings
4. Make direct edits (not suggestions)
5. Produce the final document
6. Suggest 1-3 memory entries for future sessions

**Output**: `workspace/FINAL.md`

After the document, append:
```
---
## Suggested Memory Entries
- **Category** (structure/tone/claims/audience/process): [learning]
```

**Rules**:
- This is polish, not rewriting. Preserve the author's voice.
- Less is more. Only change what materially improves the document.
- If the document is already strong, say so and make minimal changes.

## Custom Command Specifications

Each `.claude/commands/*.md` file follows the Claude Code custom command format: YAML frontmatter + instructions.

### `/df-ideation`
- Argument: the human's raw brain dump
- Instructions: Read `agents/ideation/AGENT.md`, then follow the process defined there. Save output to `workspace/brief.md`.

### `/df-research`
- No argument needed
- Instructions: Read `agents/researcher/AGENT.md`, then read `workspace/brief.md`, then follow the process. Save output to `workspace/research.md`.

### `/df-draft`
- Optional argument: document type override (default: use whatever the brief recommends)
- Instructions: Read `agents/drafter/AGENT.md`, then read all inputs (brief, research, grounding files, memory, template). Follow the process. Save output to `workspace/draft-v1.md`.

### `/df-review`
- No argument needed
- Instructions: Read `agents/reviewer/AGENT.md`. Find the latest `draft-vN.md` in workspace/. Read ONLY that file. Follow the process. Save output to `workspace/review-vN.md` (matching the draft version number).
- CRITICAL: Do NOT read brief.md, research.md, or grounding files. The reviewer reads cold.

### `/df-edit`
- Argument: the human's feedback on the review (e.g., "accept 1,3,5 -- reject 2,4 -- also fix the tone in section 3")
- Instructions: Read `agents/editor/AGENT.md`. Read the latest draft and corresponding review. Apply the human's feedback. Save output as the next draft version (`workspace/draft-vN+1.md`).

### `/df-polish`
- No argument needed
- Instructions: Read `agents/polish/AGENT.md`. Read the latest draft and `memory/MEMORY.md`. Follow the process. Save output to `workspace/FINAL.md`. After the human reviews the suggested memory entries, append accepted entries to `memory/MEMORY.md`.

### `/df-status`
- No argument needed
- Instructions: List all files in `workspace/`. Show which stages are complete based on which files exist. Show the recommended next command.

## Template Specifications

Each template in `templates/` is a markdown file that lists the recommended section structure for that document type, with brief guidance on what each section should contain.

### `templates/strategy.md`
Sections: Executive Summary, Problem Statement / Why, Current State, Proposed Approach / What, Architecture / How, Roadmap / Phases, Measurement / Success Criteria, Risks & Mitigations, Resource Requirements, Decision Points, Getting Started

### `templates/vision.md`
Sections: Executive Summary, Why This Matters Now, North Star, What This Means (capability definition), What We Give Back (human impact), What Success Looks Like, Operating Principles, Milestones, Leadership Ask

### `templates/rfc.md`
Sections: Summary, Motivation, Proposed Solution, Alternatives Considered, Design Details, Trade-offs, Migration / Rollout Plan, Rollback Plan, Open Questions

### `templates/postmortem.md`
Sections: Summary, Impact, Timeline, Root Cause, Contributing Factors, What Went Well, What Went Wrong, Action Items (with owners and dates)

### `templates/adr.md`
Sections: Title, Status, Context, Decision, Consequences, Alternatives Rejected

## Memory File Format

`memory/MEMORY.md` starts empty with format instructions:
```
# DocForge Memory

Reusable learnings from past document sessions. Curated by humans.
Max 50 entries. Oldest entries reviewed when adding new ones.

## Entries

(none yet)
```

Each entry format:
```
### [date] [document type]
**Category**: structure / tone / claims / audience / process
**Learning**: [one sentence]
```
