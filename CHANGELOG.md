# Changelog

The versions before October 2026 are reconstructed from dated copies of the command files and session notes from those days.

## 2026-10-09

- In a claude.ai chat, the plugin's `/sum` hands both blocks over as a file to land later, `/resume` reads a ledger uploaded to the chat, and `/land` says it needs a project folder. Until then, the three commands assumed a project folder wherever they ran.

## 2026-10-08

- The chat skill reads the ledger's language from the user's instructions, as `/sum` in Claude Code does. It had always written English.

## 2026-10-04

- `/sum` adds a `Recommended (model)` line when the model recommended an option before the person chose. Until then, a yes to a recommendation looked like the person's own idea.
- The chat skill takes the authorship rule of September 6, which had never reached it.
- The commit message takes its attribution lines from the session. It named one model.
- The notes folder and the ledger's language are read from the user's instructions. Both had been written into the commands.

## 2026-09-06

- "When in doubt, leave blank" is removed. An empty `Why:` had two meanings, and nine of them stood in one project. Authorship is never left undetermined now, and the model asks when it cannot tell who decided.

## 2026-09-05

- Code first, ledger last. `/sum` holds the ledger commit back while the session's code is uncommitted.

## 2026-09-04

- `/sum` stages its own files by name. It used `git add -A`, which takes everything in the tree, including work the session never touched.
- `/resume` reads `open-questions.md` when the project keeps one.

## 2026-08-30

- `/sum` commits the ledger, only in a directory that is already a git repository.

## 2026-08-13

- The earliest version on file. One entry per real fork, three cases for `Why`, a summary note, and `/land` for the output of a chat.

## 2026-06-02

- First run, as a single command. It found two forks, and one of them was a locale the model had set without asking.
