---
name: session-log
description: Session decision-logging and context-handoff commands. Always trigger when the user types /sum or /handoff. /sum produces a DECISIONS block (real forks in context / options / decision / why / rule format) plus a SUMMARY block, delivered as an editable .md file, in English unless the user's instructions name another language for the ledger. /handoff produces a continuation passport for resuming work in a new chat. Also use when the user asks to summarize session decisions, log decisions, create a handoff, or transfer context to another chat or session.
---

# Session Log

Two end-of-session commands with different jobs. `/sum` writes the **ledger**, the durable record of what was decided. `/handoff` writes the **passport**, a disposable note that lets a cold chat resume the work. The ledger is for the archive; the passport is for the next session. They can be invoked separately or together.

**Language rule: all output from both commands is in English**, regardless of the conversation language, unless the user's instructions name another language for the ledger. The output is a deliverable (it lands in a decision ledger and a session note), not meta-communication.

Reasoning rule: the model records reasoning it witnessed or owns; it never fabricates the user's. Details under the Why field below.

---

## /sum — decision ledger + summary

Review the whole conversation and produce two blocks. **Deliver them as a single .md file** (create the file and present it to the user), not as inline chat text. The user edits the Why fields before landing the file elsewhere. Filename: `sum_<YYYY-MM-DD>_<short-topic>.md`.

### Block 1 — DECISIONS

One numbered entry per real fork: a point where a choice was made between named alternatives. Not every edit is a fork; skip anything with no genuine option on the other side. Fixing the model's own mistake is not a fork unless the fix itself had competing options. Include forks the model resolved silently and never raised in the dialogue. Those are the highest-value entries, because the user cannot log what they never knew was decided.

Format each entry:

```
**N. <short title>**
- Context: <what the fork was, one line; the exact string if it was a copy edit>
- Options: <A / B (/ C), the alternatives actually on the table>
- Recommended (model): <only under the recommendation rule below>
- Decision: <what was chosen; verbatim wording for a wording change>
- Why: <see attribution rules>
- Rule: <which of the user's standards drove it, or "none">
```

**Why — attribution rules (three cases):**
1. Fork decided by the model (silently or explicitly) → `Why (model): <the model's actual reasoning>`. Always filled. The user cannot supply reasoning for a decision they didn't make.
2. Fork decided by the user, and their reasoning was stated or is unambiguous in the conversation → `Why (context): <faithful paraphrase of what the user actually said>`. This is transcription, not reconstruction. Never infer a motive the user did not voice. The user may edit it.
3. Fork decided by the user, reasoning not stated → `Why:` left blank for the user to fill. A restated choice is not a reason. If the user only picked an option ("option B", "да", "1б/2а") without saying why, the field stays blank. Do not dress the fact of the choice up as its justification.

**Authorship is never left undetermined.** A blank `Why:` asserts that the user decided; it is not a place to park uncertainty. If who decided is genuinely unclear, ask before writing the block, and never guess.

**Recommended — the model's recommendation before the user's choice:**
- Fork decided by the user after the model had recommended one of the options → add `Recommended (model): <that option, with the argument the model gave for it>` between Options and Decision, whether the user took it or not. Give the argument as it was given then, not as the model would put it now.
- Only an explicit recommendation counts, in words or as a label on the option. The order the options were listed in is not one.
- The line records the model's influence on the choice. It never fills `Why:`. Taking the recommendation is a choice, not a reason the user voiced, so `Why:` follows the rules above and stays blank unless they said why.
- No recommendation before the choice, or the fork was the model's → no line.

**Rule** names the standard that drove the call: a style or wording rule, an overclaim or accuracy check, a confidentiality or metric-disclosure rule, a naming convention. Those standards live in the user's persistent layer (project instructions, memory, CLAUDE.md). Reference them, do not restate them. Use "none" for pure scope or consistency calls.

### Block 2 — SUMMARY

Three short parts, prose or tight bullets:
- **What we discussed** — topics covered this session.
- **What we concluded** — settled outcomes.
- **What remains open** — carry-forward items, unresolved questions, anything still pending.

---

## /handoff — continuation passport

Purpose: let the user paste one block into a brand-new chat and continue working with minimal loss. Where `/sum` compresses to conclusions, `/handoff` preserves **working state**, the things a ledger deliberately filters out. Delivered **inline as chat text** (it gets pasted, not edited).

Produce one block, in the ledger's language:

```
## HANDOFF — <date> — <short session topic>
- Task: <what we are working on, one line>
- Now: <exact stopping point: active artifact, current step, any half-finished edit>
- Next: <the first action the new session should take>
- Tried & dropped: <approaches considered and rejected, with one-line reasons, so the next chat does not re-propose them>
- Open: <unresolved questions awaiting the user or external input>
- Decided this session: <2-3 lines max; the full record lives in the /sum ledger>
- Standing context: <pointer to where the durable context lives: project instructions, memory, source-of-truth files>
```

Rules:
- **Now must be precise.** "Editing the About page" is too loose; "About page hero locked, second paragraph rewrite pending user review" is right.
- **Tried & dropped is not optional.** Losing it is the main way a new chat wastes the user's time by re-suggesting rejected paths.
- **Do not inline the persistent layer.** Conventions, standards, and stable facts live in project instructions and memory; the passport points at them.
- The passport is disposable. It is meant to be pasted once and superseded by the next one.

When the user pastes a HANDOFF block at the start of a conversation, treat it as the working state: adopt Task/Now/Next as the immediate agenda, respect Tried & dropped (do not re-propose rejected approaches without new information), and consult the standing-context pointers before asking the user to repeat themselves.

---

## Delivery

`/sum` → one editable .md file, in the ledger's language. The user fills or edits Why fields, then lands it: pasted or uploaded into Claude Code, where the `/land` command routes DECISIONS → decisions.md and SUMMARY → a session note. `/handoff` → inline text in the same language, pasted as the first message of the next chat. Never mix the two deliveries.
