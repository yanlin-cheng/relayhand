---
description: Relay: compress the current conversation into a task handoff for the next session, and output a copy-paste prompt
argument-hint: "[focus of the next leg / cross-product, optional]"
disable-model-invocation: true
---

# /relayhand —— Session Relay

Compress the current conversation into a "baton" so the next fresh session (or a new conversation in a different AI product) can pick up the work immediately.

Writing doctrine (from Cline's compactor system prompt): **Restrained throughout, detailed only about the next step.**

**Language: follow the conversation.** Talk to the user and write the handoff note in the language the current conversation uses (mixed conversation → prefer the user's own language). One template serves every language.

$ARGUMENTS (optional):
- Plain text = the task for the next leg. The note is then tailored to that task (see writing discipline #5)
- Contains "cross-product" (跨产品) = additionally output the embedded prompt

## Step 1: Locate the source-of-truth transcript

The full record of the current conversation is a .jsonl file under <home>/.claude/projects/. Look first in the directory matching the current project (path rule: special and non-ASCII characters in the project path are replaced with -) for the most recently modified .jsonl; if not found, use Bash to take the most recently modified one globally (the current session is being written to continuously, so it is usually the newest). Note the path — Step 2 needs it.

## Step 2: Write the handoff note

Save it to relayhand-<YYYYMMDD-HHmm>.md in the OS temp directory (%TEMP% on Windows, /tmp on Linux/macOS).

### Template (drop any section that has nothing to say — never pad)

Section titles follow the conversation language; shown here in English:

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

## Pitfalls (do not repeat)
<failed attempts and why they failed; debugging conclusions as symptom → root cause → fix>

## Next
<immediately executable actions, in order, concrete enough to run as-is>
<the $ARGUMENTS focus goes at the top of this section>

## Files
Read: <extracted from the conversation, real paths>
Edited: <extracted from the conversation, real paths; uncommitted working-tree changes count too — never claim a repo file is untouched while its changes are still pending>

## Source of truth
Full transcript: <jsonl path>. When this note lacks detail (a discussion, an error message), Grep that file.
```

### Writing discipline

1. The reader is the next agent, not the user: write a "baton", not a "retrospective"
2. Do not narrate the conversation ("we first discussed… then…"); only conclusive state
3. Facts only, no vibes; every word must help the next leg do the work
4. "Next" is the only section allowed detail; every other section serves it
5. **When $ARGUMENTS names the next task, the task is the filter**: summarize only the background, decisions, files, and pitfalls that task needs; however important, anything unrelated stays out, and the note's title is framed around that task. Only with no specified task do the general summary
6. **When the user's latest requirement changes what to do next, quote it verbatim in "Next"** — never paraphrase a direct instruction
7. **If this conversation itself began from a handoff note, add that note's path to "Source of truth"** to keep the relay chain traceable
8. File lists must be extracted from the conversation — never invented from memory
9. Redact: API keys, passwords, and personal information must not be written
10. Existing artifacts (plan docs, commits, issues): reference by path, never copy content

## Step 3: Show

Display the full handoff note in chat for review (rewrite on request).

## Step 4: Output the copy-paste prompt

At the end of the reply, first a one-line note "copy the following into a new conversation", then the code block (the prompt itself is also written in the conversation's language):

**File version (default output)** — the first line is the naming seed: the session's auto-generated title summarizes the first prompt, so this line steers the title toward the relay chain:

```
Relay relayhand-<YYYYMMDD-HHmm> — <one-sentence task, in the conversation's language>
Read <full path to the handoff note>. It is the handoff note from the previous session. Read it fully, do not recap its contents, then start executing the "Next" section directly. Run `git status` first to reconcile the repo's actual state with the note; if they disagree, reconcile before acting.
```

If $ARGUMENTS carries a focus, append one line: `Focus this time: $ARGUMENTS`

Below the code block, add one human-readable line (not inside it): `After pasting, run /rename relayhand-<YYYYMMDD-HHmm> to pin the session name to the relay chain (optional, but exact).`

**Embedded version (only when $ARGUMENTS contains "cross-product" / 跨产品; self-contained, pasteable into any AI product's new conversation)** — same naming-seed first line:

```
Relay relayhand-<YYYYMMDD-HHmm> — <one-sentence task, in the conversation's language>
You are taking over a relayed task. Below is the handoff note from the previous session. Read it fully, do not recap its contents, then start executing the "Next" section directly. Run `git status` first to reconcile the repo's actual state with the note; if they disagree, reconcile before acting.
<full text of the handoff note>
```

Finally report two things: the note's path, and that the prompt is ready.

## Personal extensions

This command is deliberately generic and contains no personal configuration (knowledge-base paths, machine-specific directories, etc.). Add personal enhancements to your own local copy, never commit them back to the repository — see the layering design in the repository's DESIGN.md.
