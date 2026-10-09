---
name: resume
description: "Rehydrate context at session start: read recent decisions.md entries and report where we are"
allowed-tools: Read, Grep, Glob
disable-model-invocation: true
---
Rehydrate my working context for this repo. Read-only. Change nothing.

In a claude.ai chat there is no ./decisions.md. There, use a decisions.md I
uploaded or pasted in this conversation, and an open-questions.md only if I
gave one too. If no ledger is in the conversation, ask me for it and stop.

1. Read ./decisions.md. If it does not exist, say so and stop. Do not create
   it, do not scan the repo as a substitute.

2. Take the last 2-3 `##` sections in file order, whatever their heading
   format. Sections may be headed `## S<N> — <date> — <topic>`, or by date
   alone, or by session label alone. Do not match on a date pattern, and do not
   sort: the file is append-only, so the last sections are the recent ones.
   Read the file's own preamble if it has one, since it may say which entries
   were struck and how numbering works.

3. Read ./open-questions.md if it exists. If it does not, skip this step
   silently. Most repos have no such file, and its absence is not worth a
   line in the report. Do not create it, and do not substitute anything for it.

4. Report back, briefly and in the ledger's language:
   - **Last session:** label, date if present, and topic of the final section.
   - **Recent decisions:** the decision lines only (titles + what was chosen),
     not the full entries. One line each.
   - **Open threads:** anything the recent entries flag as unresolved,
     deferred, or "offer stands". If a SUMMARY "remains open" list exists in
     the session note, do not go fetch it. Work from decisions.md only.
   - **Open questions:** every item still listed in open-questions.md, one line
     each, grouped as the file groups them. Omit this section entirely if the
     file does not exist. These outlive the 2-3 section window above, so do not
     drop one because it looks old. The file is maintained by deletion, and a
     line that is still there is still open.
   - **Empty Why fields:** list entry titles from the recent sections whose
     "Why:" line is still blank. Those are waiting for me to fill.

5. End with one line: "Ready. What are we working on?" Do not propose next
   steps yourself; the decision ledger records what was chosen, not what to
   do next.

Keep the report under ~15 lines, plus one line per open question. This is
orientation, not analysis.
