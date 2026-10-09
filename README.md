# Who made the call

A decision ledger for work done with AI agents. At the end of a session, the model records every fork, each a choice between named alternatives, and who decided it. It writes its own reasons under its own name and must not write a reason the person never gave.

I have run it since June 2026 on my own projects. It is three commands for Claude Code and one skill for claude.ai. The thinking behind it is in [Who made the call](https://www.valentinnovitsky.com/writing/who-made-the-call).

## What a session looks like

| When | Command | What happens |
|---|---|---|
| End of a session | `/sum` | The model reviews the session and appends one entry per fork to `decisions.md`, including the forks it settled without asking. It saves a summary note if you named a folder for them, and commits the ledger if the project is a git repository and nothing else in it is left uncommitted |
| After a chat | `/land` | A chat has no disk, so `/sum` there hands you a file. Paste or upload it in Claude Code and run `/land`. It appends the entries to `decisions.md` without rewording them, adding only the session number, and treats the summary as `/sum` does. It does not commit |
| Start of a session | `/resume` | The model reads the latest entries back to you, with the open threads and the reasons still waiting for you |
| Between chats | `/handoff` | claude.ai only. The model writes a note on where the work stands, to paste as the first message of the next chat |

## The entry

```
**S<N>-K. <short title>**
- Context: <what the fork was>
- Options: <A / B (/ C)>
- Recommended (model): <its recommendation and argument, if it gave one before you chose>
- Decision: <what was chosen>
- Why (model): <its own account>          the model decided
- Why (context): <what you said>          you decided and said why
- Why:                                    you decided and said nothing
- Rule: <the project standard behind it, or "none">
```

`examples/decisions.md` holds three real entries, verbatim, from two ledgers kept with this tool. They show each kind of `Why`, and one includes a recommendation.

## Who may write the reason?

- The model decided. It writes its own account of why every time.
- You decided and said why. It writes down what you said and adds nothing.
- You decided and said nothing. The field stays empty. Repeating your choice back to you does not count as a reason.

An empty `Why:` means you made the call and the reason is still in your head. Fill it in by hand in `decisions.md`, which `/sum` keeps in the directory Claude Code runs in and creates if it is missing. `/resume` lists the empty fields of the last few sessions when you run it.

If the model cannot tell who decided, it asks before it writes. If it recommended an option before you chose, the entry carries that recommendation and its argument, whether you took it or not.

## Install

### Claude Code

```
/plugin marketplace add sacredvalentin/who-made-the-call
/plugin install who-made-the-call@novitsky
```

The commands appear under the plugin's name, for example, `/who-made-the-call:sum`. For the short names, copy the three folders in `skills/` to `~/.claude/skills/` instead of installing the plugin. The copies get no updates, and a copied `resume` replaces Claude Code's own `/resume`, which reopens a past conversation; `/continue` still does that.

### claude.ai

Zip the folder `claude-ai/session-log` and upload it under Customize > Skills. In a chat, `/sum` gives you a file to land later, and `/handoff` gives you a note to paste into the next chat.

## Tell it where things go

`/sum` reads two things from your `CLAUDE.md`, and `/land` uses the same folder.

| What | If you say nothing |
|---|---|
| The folder for session summaries | No note is written, and the summary is printed in the report |
| The language of the ledger | English |

Two lines are enough.

```
Session summaries go to ~/notes/sessions/.
The ledger is written in German, regardless of the conversation's language.
```

## What it does not do

- The model's `Why` is its own account of itself. Nothing checks it against what happened inside the model.
- Empty reasons pile up; only you can fill them, and `/resume` shows only the recent ones.
- Every fork gets an entry, and all entries weigh the same. A locale counts as much as a design decision.
- One person has used it. Treat it as a working practice, not as a tested product.

If you run it, tell me what happened in [Discussions](https://github.com/sacredvalentin/who-made-the-call/discussions). If it breaks one of its own rules, open an [issue](https://github.com/sacredvalentin/who-made-the-call/issues).

## History

`CHANGELOG.md` lists the versions since June 2026, with the two rules that had to be repaired.

## License

MIT
