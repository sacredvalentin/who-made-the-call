---
name: sum
description: Appends this session's forks to the decision ledger in decisions.md, saves a session note if a notes folder is named, and commits the ledger if the project is a git repo with nothing else uncommitted. In a claude.ai chat, hands both blocks over as a file to land later
allowed-tools: Read, Edit(./decisions.md), Write(./decisions.md), Bash(git rev-parse:*), Bash(git status:*), Bash(git add:*), Bash(git commit:*)
disable-model-invocation: true
---
In a claude.ai chat there is no project folder, and a file you write there
stays in a sandbox the user does not see. There, produce the two blocks below
but skip the landing steps. Number the entries plainly, 1., 2., 3., since no
ledger is there to give the session number. Deliver both blocks as one .md
file for the user to download, named `sum_<YYYY-MM-DD>_<short-topic>.md`, and
tell them that `/land` in Claude Code appends it to `decisions.md`. In Claude
Code, and in Cowork working in the user's folder, follow every step.

Review this session and produce two blocks, in English regardless of the
conversation language, unless the user's instructions name another language
for the ledger. Include forks you resolved silently and never raised in
the dialogue (a locale, a default, a library version). Those are the
highest-value entries.

1. DECISIONS — one numbered entry per real fork (a choice between named
   alternatives). Skip anything with no genuine option on the other side.
   Fixing your own mistake is not a fork unless the fix itself had competing
   options.
   Number entries `S<N>-1`, `S<N>-2`, … where `<N>` is the session number
   resolved in step 1 of the landing instructions below.
   Format:
   **S<N>-K. <short title>**
   - Context: <what the fork was>
   - Options: <A / B (/ C)>
   - Recommended (model): <only under the recommendation rule below>
   - Decision: <what was chosen>
   - Why: <attribution rules below>
   - Rule: <which standard from CLAUDE.md drove it, or "none">

   A filled entry, adapted from a real ledger. The user took the recommendation and
   gave no reason, so the line records the recommendation and "Why:" stays
   blank.

   **S64-23. A recommendation gets a line of its own, `Recommended (model)`**
   - Context: three ways to record that the model had recommended an option before the user chose.
   - Options: a tag on the option inside Options / a separate line between Options and Decision, carrying the option and the argument as given / a new Why label holding the model's argument.
   - Recommended (model): the separate line. It shows the argument and the cases where the user chose against the recommendation, and the Why rules do not change. Its cost is one more line in an entry.
   - Decision: the separate line, by two edits to this command. Only an explicit recommendation counts, the line never fills Why, and it is absent when nothing was recommended or the fork was the model's.
   - Why:
   - Rule: none.

   Why attribution:
   - Fork decided by you, the model, silently or explicitly →
     "Why (model): <your actual reasoning>". Always filled.
   - Fork decided by the user, reasoning stated or unambiguous in the
     conversation → "Why (context): <faithful paraphrase of what they said>".
     Transcription only. Never infer a motive they did not voice.
   - Fork decided by the user, reasoning not stated → leave "Why:" blank.
     A restated choice is not a reason. If the user only picked an option
     without saying why, the field stays blank.
   - Authorship is never left undetermined. A blank "Why:" asserts that the
     user decided; it is not a place to park uncertainty. If who decided is
     genuinely unclear, ask before writing the block, and never guess.

   Recommendation:
   - Fork decided by the user after you had recommended one of the options →
     add "Recommended (model): <that option, with the argument you gave for
     it>", whether they took it or not. Give the argument as you gave it then,
     not as you would put it now.
   - Only an explicit recommendation counts, in words or as a label on the
     option. The order you listed the options in is not one.
   - The line records your influence on the choice. It never fills "Why:".
     Taking your recommendation is a choice, not a reason the user voiced, so
     "Why:" follows the rules above and stays blank unless they said why.
   - No recommendation before the choice, or the fork was yours → no line.

2. SUMMARY — what we discussed, what we concluded, what remains open.

Then land the blocks:

1. Read ./decisions.md (create if missing). Find the highest existing session
   number by scanning `## S<N>` headings. The new session number is that plus
   one. If the file has no `## S<N>` headings, start at S1. Renumber nothing.

2. DECISIONS → append verbatim to ./decisions.md under:
   ## S<N> — <today YYYY-MM-DD> — <short session topic>
   Append only. Never rewrite or remove existing content. Struck entries in
   the file keep their empty numbers; never reuse a number.

3. SUMMARY → save as a new session note, in the folder the user's instructions
   name for session summaries (CLAUDE.md at any level). If they name none, do
   not pick one: skip the file, print the SUMMARY in the report, and say that
   no notes folder is declared.
   - Title: 3-5 words, kebab-case, from the summary.
   - File: <that folder>/[title].md
   - Frontmatter:
     ---
     date: <today YYYY-MM-DD>
     tags: [session-log]
     ---
     plus any fields the user's instructions ask for.
   - Summary text below the frontmatter as-is. Create the folder if missing.

4. Commit the session, only if the project directory is already a git
   repository (`git rev-parse --is-inside-work-tree` succeeds). If it is not,
   skip this step in silence: never run `git init`, and never create a
   repository as a side effect of summarising.

   - CODE FIRST, LEDGER LAST. Before staging anything, run `git status
     --short`. If it lists any change outside this command's own files, do not
     commit. Report what is outstanding, say the ledger is held back until
     the code it describes is in, and stop at this step. A ledger commit
     landing on a tree where the session's code is still uncommitted produces
     a point in the history that describes code it does not carry, and the
     repository stops matching what it says about itself. The user lands the
     code and re-runs this command, or tells you to land the ledger anyway,
     which is the only thing that lifts this.
   - Stage by name, never `git add -A`: `./decisions.md`, plus the session
     note if it happens to resolve inside this working tree. Those are the
     files this command produced; nothing else is its business to commit.
   - Message:

     S<N>: <the same short session topic used in the decisions.md heading>

     <the opening paragraph of SUMMARY>

     <the commit attribution lines from this session's system reminder, if any>

   - Never push. Never create or switch branches. Never amend or rewrite an
     existing commit. The ledger is append-only and so is this history.
   - If there is nothing to commit, say so and move on. An empty commit is
     not a record of a session, it is noise in the log.
   - Where the gate above is lifted, everything else the session changed still
     stays uncommitted, deliberately: this command records decisions, it does
     not decide what belongs in the project's history. Do not stage it, and do
     not guess which stray change "belongs" to the session. That judgement is
     the user's.
   - Uncommitted work must not disappear quietly. After committing, run
     `git status --short` and list what is still outstanding in the report, so
     the user sees exactly what they are left to commit themselves.

Report five lines: the decisions.md heading added, the decisions.md path, the
session note path or the line saying none is declared, the commit hash (or a
line saying why no commit was made, the ledger being held back for
outstanding code among the reasons), and the files left uncommitted in the
working tree, or "working tree clean".
