# Lens: ignored rules

**Question:** which of the human's corrections were already covered by a written rule at that moment, and why didn't the rule work?

This lens matters most. When a written rule is ignored, writing more text doesn't fix it.

1. For each correction, repeat, nudge and open/show request in `prompts.md`, look for a rule that covered it **at that time**. Look:
   - in the rule files as they were then: `git log --before=<timestamp in ISO> -1 --format=%h`, then `git show <hash>:<file>` in the repo you were given;
   - in `CLAUDE.md` and `AGENTS.md` files;
   - in the skill and agent files the session loaded;
   - in the user's memory files, if the target notes point to them.
2. When you find one, quote it with `file:line` and the commit that was current at the time. Then work out **why it didn't work**:
   - the agent never read that file in this session (check its Read calls);
   - it read the file, but the rule was buried, vague or contradicted by another file;
   - it read and understood the rule, and still didn't follow it at the moment of acting (no trigger, no check);
   - the rule depended on something the agent can't do (feel time, see a window, remember across compaction).
3. The proposal is **enforcement, not more words**. Pick what fits the reason:
   - a hook that blocks the turn's end;
   - a required report field;
   - a test;
   - moving the rule to the file that is always read;
   - an agent that does the step itself;
   - deleting the contradicting text.

Example from "Slop":
- `guide/workflow.md` rule 2 ("never end a turn with work left") existed, yet the human said "keep going" and asked for 100-item lists 5 times.
- The `quality-bar.md` instrument rules existed and were ignored twice.
- `making-a-video.md` 2.2 (the agent picks the take) conflicted with `suno.md` (download every take).
