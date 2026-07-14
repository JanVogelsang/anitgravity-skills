---
name: manage-handoff
description: Generates a terse session delta for agent resumption, or loads an existing handoff document to resume work.
argument-hint: "Next session objective (to CREATE) OR absolute file path (to LOAD)."
---

# Handoff Management Constraints

You handle both creating and loading handoff documents to maintain context across sessions. Evaluate the provided argument to determine the execution mode.

## Execution Mode: LOAD (If argument is a valid file path)
1. **Read**: Read the file at the provided absolute path.
2. **Ingest**: Silently ingest the context, metadata, delta, and next steps.
3. **Cleanup**: Delete the handoff document file. 
4. **Acknowledge**: Output a terse confirmation strictly detailing:
   - The loaded file path.
   - The #1 Immediate Next Step you are about to execute.
   - Do not output conversational filler.

## Execution Mode: CREATE (If argument is a text objective or empty)
1. **Location**: Save strictly to OS temp directory (`/tmp` or `%TEMP%`) as `YYYY-MM-DD-HHMMSS-[slug].md`.
2. **User Transport**: You MUST output the absolute file path of the generated document to the user in a code block so they can copy it for the next session.
3. **Zero Duplication**: Reference existing PRDs/issues by absolute path/URL only.
4. **Tone**: Zero conversational filler. No introductory or concluding paragraphs.

## Required Structure (For CREATE Mode Only)

Output exactly these sections in the document using strict bullet points.

### 1. Session Delta
* High-level objective and specific progress made in *this session only*.

### 2. Decisions & Failures
* Non-obvious decisions, blocked paths, or system limitations discovered.

### 3. Immediate Next Steps
* Start with the #1 immediate action item. Actionable commands only.

### 4. Required Skills
* [Comma-separated list of Antigravity skills/plugins to load]
