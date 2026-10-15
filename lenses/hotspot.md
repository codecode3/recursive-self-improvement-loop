# Lens: hotspot (one subject)

**Question:** the human spent the most prompts on one subject, given in your prompt as SUBJECT. Why did it take so many rounds, and how would a future agent get it right in one?

1. Gather every prompt, subagent and commit about SUBJECT in time order, across all build sessions, including side sessions. Build a round-by-round timeline:
   - what the human asked;
   - what the agent changed (which files, from the tool calls or commits);
   - what the agent claimed;
   - what the human said next.
2. Find the turning points:
   - the round that finally worked, and what was different about it;
   - asks that came back ("spine too long" asked twice);
   - fixes that undid earlier asks;
   - rounds where the agent reported success without looking.
3. Name the **missing inputs**: references, measurements, views or locked decisions that would have let the agent get it right sooner. Did the agent ask for them, or should it have?
4. Propose a recipe for this **kind** of subject, not just this one instance, so it applies to the next character, asset or feature. Write it as the steps an agent follows, with the checks it runs and what it shows the human.

Example from "Slop": Juno took 8 subagent rounds and a 17-request side session, and the Hydra had its own side session. The round that worked read every reference first, rendered views framed like each reference, and critiqued itself for 5 rounds.
