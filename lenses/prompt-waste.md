# Lens: prompt waste

**Question:** how could the human have finished this project with half the prompts?

Start from `prompts.md`. Every prompt marked `Avoidable: yes` or `partly` is a candidate.

1. Group the avoidable prompts by **cause**, not by subject:
   - the agent stopped with work left (nudges: "keep going", "list 100 more", "use N subagents");
   - the agent didn't show its work (open/show requests: "open it", "show me");
   - the agent got it wrong first time (corrections, repeat corrections);
   - the agent asked about or did something a rule already settled;
   - the environment broke (a tool missing, a login, a lost connection);
   - the human had to relay messages between sessions or write prompts for other agents.
2. For each cause, find the moment it started. Then ask: what single change would have stopped it? The answer might be a rule, a default, a setup-form field, a check before reporting, or an agent that does the step unasked.
3. Count the prompts each change removes. Be honest about overlap: one prompt can't be saved twice.
4. End the summary with a projection: total prompts → expected prompts after the fixes, with a range. List the prompts that can't be removed (real decisions and creative choices).

**Don't count against the agent:** the human's own creative edits, taste and new ideas, and their first decision on anything. These are the work, not waste.

Example from "Slop" (music video, 2026-10-11): 75 main-session prompts, about 43 avoidable. The biggest causes were the agent ending turns with first-cut work left (8 prompts), unasked open/show steps (6), and the Juno appearance loop (16).
