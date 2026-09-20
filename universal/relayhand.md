# relayhand Universal Core Prompt (manual paste-in version)

Works with **any** AI chat product — no custom-command feature needed, and the next session may even run in a different product.

**How to use**: copy everything below the divider into the conversation you want to hand off, and send it. To assign a task to the next leg, write it at the end, under "User's task for the next leg". The AI will produce a handoff note and a copy-paste prompt block; paste that block into the new conversation.

---

Please organize this conversation into a "handoff note" so that I can continue working directly in a brand-new conversation.

Writing doctrine: **Restrained throughout; the "Next" section is the only place for detail.**

**Language: follow the conversation.** Write the handoff note and the copy-paste prompt in the language this conversation uses (mixed conversation → prefer the user's own language). One template serves every language.

## Template (drop any section that has nothing to say — never pad)

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

## Files
Read: <extracted from the conversation, real paths>
Edited: <extracted from the conversation, real paths; uncommitted working-tree changes count too — never claim a repo file is untouched while its changes are still pending>
```

## Writing discipline

1. The reader is the next agent, not the user: write a "baton", not a "retrospective"
2. Do not narrate the conversation ("we first discussed… then…"); only conclusive state
3. Facts only, no vibes; every word must help the next leg do the work
4. "Next" is the only section allowed detail; every other section serves it
5. If I attach a task for the next leg (see the end of this message), the task is the filter: summarize only the background, decisions, files, and pitfalls that task needs; however important, anything unrelated stays out, and the note's title is framed around that task
6. **When the user's latest requirement changes what to do next, quote it verbatim in "Next"** — never paraphrase a direct instruction
7. If this conversation itself began from a handoff note, add that note's path to a "Source of truth" section to keep the relay chain traceable
8. File lists must be extracted from the conversation — never invented from memory
9. Redact: API keys, passwords, and personal information must not be written
10. Existing artifacts (plan docs, commits, issues): reference by path or link, never copy content

**User's task for the next leg** (omit for a general summary):
<fill in what the next leg should do here>

## Output requirements

1. Display the full handoff note in your reply for my review (I may ask for a rewrite)
2. At the end of your reply, output a prompt code block that can be copied straight into a new conversation, with this fixed content (in the conversation's language). The first line is the naming seed: many AI products auto-title a conversation from its first prompt, so this line steers the title toward the relay chain. Also suggest saving the handoff note as <relayhand-YYYYMMDD-HHmm>.md using the same timestamp so file name and session name stay aligned:

```
Relay relayhand-<YYYYMMDD-HHmm> — <one-sentence task, in the conversation's language>
You are taking over a relayed task. Below is the handoff note from the previous session. Read it fully, do not recap its contents, then start executing the "Next" section directly. Run `git status` first to reconcile the repo's actual state with the note; if they disagree, reconcile before acting.
<full text of the handoff note>
```
3. Below the code block, add one human-readable line (not inside it) telling me to rename the new conversation to relayhand-<YYYYMMDD-HHmm> after pasting — via `/rename` in Claude Code, or the product's own conversation-rename feature — so the relay chain stays traceable in the session list (optional, but exact)
