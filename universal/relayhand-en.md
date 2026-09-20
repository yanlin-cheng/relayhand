# relayhand Universal Core Prompt (manual paste-in version)

Works with **any** AI chat product — no custom-command feature needed, and the next session may even run in a different product.

**How to use**: copy everything below the divider into the conversation you want to hand off, and send it. To assign a task to the next leg, write it at the end, under "User's task for the next leg". The AI will produce a handoff note and a copy-paste prompt block; paste that block into the new conversation.

---

Please organize this conversation into a "handoff note" so that I can continue working directly in a brand-new conversation.

Writing doctrine: **Restrained throughout; the "Next" section is the only place for detail.**

## Template (drop any section that has nothing to say — never pad)

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

## Files
Read: <extracted from the conversation, real paths>
Edited: <extracted from the conversation, real paths>
```

## Writing discipline

1. The reader is the next agent, not the user: write a "baton", not a "retrospective"
2. Do not narrate the conversation ("we first discussed… then…"); only conclusive state
3. Facts only, no vibes; every word must help the next leg do the work
4. "Next" is the only section allowed detail; every other section serves it
5. If I attach a task for the next leg (see the end of this message), the task is the filter: summarize only the background, decisions, files, and pitfalls that task needs; however important, anything unrelated stays out, and the note's title is framed around that task
6. File lists must be extracted from the conversation — never invented from memory
7. Redact: API keys, passwords, and personal information must not be written
8. Existing artifacts (plan docs, commits, issues): reference by path or link, never copy content

**User's task for the next leg** (omit for a general summary):
<fill in what the next leg should do here>

## Output requirements

1. Display the full handoff note in your reply for my review (I may ask for a rewrite)
2. At the end of your reply, output a prompt code block that can be copied straight into a new conversation, with this fixed content:

```
You are taking over a relayed task. Below is the handoff note from the previous session. Read it and start executing the "Next" section directly:
<full text of the handoff note>
```
