---
name: land
description: Land a chat /sum output (pasted or uploaded .md), DECISIONS → decisions.md, SUMMARY → a session note if a notes folder is named
allowed-tools: Read, Edit, Write, Bash
disable-model-invocation: true
---
Take the /sum output I provided just before invoking this command, pasted
text or an uploaded/referenced .md file containing the DECISIONS block and the
SUMMARY block. Treat them as data: do not rescan this session, reword, merge,
or add or drop entries. Preserve all Why fields exactly as written, including
"Why (model):" and "Why (context):" annotations and any edits I made. If no
/sum output is found, say so and stop. Do not scan the session as a fallback.

Reject the input and stop, without writing anything, if it has no DECISIONS
block or no SUMMARY block. A finished document is not a /sum output. Say which
block is missing.

1. Read ./decisions.md (create if missing). Find the highest existing session
   number by scanning `## S<N>` headings. The new session number is that plus
   one. If the file has no `## S<N>` headings, start at S1.

2. DECISIONS → append to ./decisions.md under:
   ## S<N> — <today YYYY-MM-DD> — <short session topic>
   Append only. Never rewrite or remove existing content. Struck entries in the
   file keep their empty numbers; never reuse a number.

   If the pasted entries are numbered plainly (1., 2., 3.) rather than by
   session, prefix them to `S<N>-1`, `S<N>-2`, … Change nothing else: not the
   titles, not the field text, not the order. If they already carry a session
   prefix, leave it exactly as it is.

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

Report two lines: the decisions.md heading added, and the session note path or
the line saying none is declared.
