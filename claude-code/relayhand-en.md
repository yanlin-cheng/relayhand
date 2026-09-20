---
description: Relay: compress the current conversation into a task handoff for the next session, and output a copy-paste prompt
argument-hint: "[focus of the next leg / cross-product, optional]"
disable-model-invocation: true
---

# /relayhand —— Session Relay

Compress the current conversation into a "baton" so the next fresh session (or a new conversation in a different AI product) can pick up the work immediately.

Writing doctrine (from Cline's compactor system prompt): **Restrained throughout, detailed only about the next step.**

$ARGUMENTS (optional):
- Plain text = the task for the next leg. The note is then tailored to that task (see writing discipline #5)
- Contains "cross-product" = additionally output the embedded prompt

## Step 1: Locate the source-of-truth transcript

The full record of the current conversation is a .jsonl file under <home>/.claude/projects/. Look first in the directory matching the current project (path rule: special and non-ASCII characters in the project path are replaced with -) for the most recently modified .jsonl; if not found, use Bash to take the most recently modified one globally (the current session is being written to continuously, so it is usually the newest). Note the path — Step 2 needs it.

## Step 2: Write the handoff note

Save it to relayhand-<YYYYMMDD-HHmm>.md in the OS temp directory (%TEMP% on Windows, /tmp on Linux/macOS).

### Template (drop any section that has nothing to say — never pad)

```markdown
# Handoff: <one sentence naming the task>

## Goal
<one sentence: what is being built/fixed, and why. If it takes more than a sentence, you haven't distilled it — rewrite>

## State
- Done: <checklist, one item per line>
- In progress: <what is being worked on right now>
- Blocked: <obstacles, open questions>

## Key decisions
<only technical choices that affect later work, and why>

## Next
<immediately executable actions, in order, concrete enough to run as-is>
<the $ARGUMENTS focus goes at the top of this section>

## Files
Read: <extracted from the conversation, real paths>
Edited: <extracted from the conversation, real paths>

## Source of truth
Full transcript: <jsonl path>. When this note lacks detail (a discussion, an error message), Grep that file.
```

### Writing discipline

1. The reader is the next agent, not the user: write a "baton", not a "retrospective"
2. Do not narrate the conversation ("we first discussed… then…"); only conclusive state
3. Facts only, no vibes; every word must help the next leg do the work
4. "Next" is the only section allowed detail; every other section serves it
5. **When $ARGUMENTS names the next task, the task is the filter**: summarize only the background, decisions, files, and pitfalls that task needs; however important, anything unrelated stays out, and the note's title is framed around that task. Only with no specified task do the general summary
6. File lists must be extracted from the conversation — never invented from memory
7. Redact: API keys, passwords, and personal information must not be written
8. Existing artifacts (plan docs, commits, issues): reference by path, never copy content

## Step 3: Show

Display the full handoff note in chat for review (rewrite on request).

## Step 4: Output the copy-paste prompt

At the end of the reply, first a one-line note "copy the following into a new conversation", then the code block:

**File version (default output)**:

```
Read <full path to the handoff note>. It is the handoff note from the previous session. Read it fully, then start executing the "Next" section directly.
```

If $ARGUMENTS carries a focus, append one line: `Focus this time: $ARGUMENTS`

**Embedded version (only when $ARGUMENTS contains "cross-product"; self-contained, pasteable into any AI product's new conversation)**:

```
You are taking over a relayed task. Below is the handoff note from the previous session. Read it and start executing the "Next" section directly:
<full text of the handoff note>
```

Finally report two things: the note's path, and that the prompt is ready.

## Personal extensions

This command is deliberately generic and contains no personal configuration (knowledge-base paths, machine-specific directories, etc.). Add personal enhancements to your own local copy, never commit them back to the repository — see the layering design in the repository's DESIGN.md.
