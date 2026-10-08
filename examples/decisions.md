# decisions.md

Excerpts from two real ledgers. S28 is from the one kept while this tool was being repaired; S64 is from the one behind the site that describes it. The entries are verbatim. S28-9 is a call the person made, with the reason in his own words. S28-11 is a call the model made. S64-23 is a call the person made on the model's recommendation, and its Why is empty.

## S28 — 2026-09-06 — Every blank `Why` closed, and the convention that produced them repaired

**S28-9. A third label refused in favour of a guaranteed author**
- Context: two sessions had lost a turn to a blank `Why` that could mean either «the user decided and said nothing» or «`/sum` could not tell». I proposed a third label for the undetermined case.
- Options: add a `Why (unattributed)` label / leave the convention alone / forbid the undetermined state outright
- Decision: the third
- Why (context): there must always be an author.
- Rule: none

**S28-11. The doubt clause split rather than deleted**
- Context: «When in doubt, leave blank» sits in the same sentence as «A restated choice is not a reason», and only the first half was being retired.
- Options: delete the sentence and write the new rule in its place / split it, keep the restated-choice half, and add authorship as its own bullet
- Decision: split it
- Why (model): the two halves answer different doubts — who decided, and whether what they said is a reason — and only the first is being forbidden. Deleting both would have removed the rule that had fired in this very session on S3-18, an hour before the edit. Keeping the surviving half as its own bullet also makes the blank single-valued in the text itself, rather than by inference from what is missing.
- Rule: none

## S64 — 2026-10-05 — The decision ledger gets a post, a `Recommended (model)` line and a repository, and the Writing section is built locally

**S64-23. A recommendation gets a line of its own, `Recommended (model)`**
- Context: three ways to record that the model had recommended an option before he chose.
- Options: a tag on the option inside Options / a separate line between Options and Decision, carrying the option and the argument as given / a new Why label holding the model's argument.
- Recommended (model): the separate line. It shows the argument and the cases where he chose against the recommendation, and the Why rules do not change. Its cost is one more line in an entry.
- Decision: the separate line, by two pairs in `~/.claude/commands/sum.md`. Only an explicit recommendation counts, the line never fills Why, and it is absent when nothing was recommended or the fork was the model's.
- Why:
- Rule: none.
