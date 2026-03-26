---
description: "DocForge: Add context, content, or direction to the pipeline mid-process"
argument-hint: "What to add: context for a section, content to include, corrections to the brief, additional research questions, etc."
---

Read `workspace/.active-project` to determine the active project. If no active project is set, stop and tell the human: "No active project. Run `/df-ideation` to start a new project, or say 'switch to [project name]' to resume one."

This command lets the human inject new context, content, or direction at any point in the pipeline. It updates the appropriate artifact(s) without restarting the pipeline.

The human's input is: $ARGUMENTS

If no argument was provided, ask the human what they want to add and where it should go.

## Determine What to Update

Based on the input, update one or more of these files in the active project folder (`workspace/{project}/`):

### Adding to the brief (`brief.md`)
If the human provides new arguments, scope changes, structure notes, or author-specified content:
- Read `workspace/{project}/brief.md`
- Add the new information to the appropriate section (Key Arguments, Structure Notes, Author-Specified Content, Scope, etc.)
- Save the updated brief
- Tell the human: "Brief updated. If a draft already exists, run `/df-edit` with instructions to incorporate the new brief content, or `/df-draft` to redraft."

### Adding research context (`research.md`)
If the human provides new evidence, data, corrections to claims, or answers to open questions:
- Read `workspace/{project}/research.md`
- Add a new section `## Supplemental Research (added by author)` at the end
- Include the human's additions with clear attribution
- Save the updated research
- Tell the human: "Research supplemented. If a draft already exists, run `/df-edit` with instructions to incorporate the new evidence."

### Adding grounding files
If the human mentions files they want to add to grounding:
- Remind them to copy files to `workspace/{project}/grounding/`
- Tell them: "After adding files, run `/df-edit` with instructions on how to use them, or `/df-draft` to redraft with the new grounding."

### Providing content for a specific section
If the human provides specific content (code, definitions, examples, data tables) for a specific section:
- Read `workspace/{project}/brief.md`
- Add or update the Author-Specified Content section with the new content and which section it belongs in
- Save the updated brief
- Tell the human: "Author-specified content added to brief. Run `/df-edit add the author-specified content from the brief to [section]` to incorporate it into the current draft."

After any update, also update `workspace/{project}/PROJECT.md`: append to progress log noting what was supplemented.

## Rules

- **Preserve existing content.** Supplement, don't overwrite. Mark additions clearly.
- **Attribute author additions.** Use "[added by author]" or "## Supplemental" markers so the drafter/editor knows this is human-provided context.
- **Be specific about next steps.** Tell the human exactly which command to run to incorporate their additions.
- **Don't modify the draft directly.** Supplements update the brief and research artifacts. The editor incorporates them into the draft.
