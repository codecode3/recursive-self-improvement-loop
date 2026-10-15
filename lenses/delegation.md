# Lens: delegation (why the human drove subagents)

**Question:** why did the human have to tell the agent to use subagents, how many prompts did that cost, and how can delegation happen without being asked?

1. List every prompt where the human:
   - asked for a subagent, or a number of them;
   - wrote a prompt for another agent;
   - relayed a message between sessions;
   - asked what a subagent was doing, or stopped one.
2. For each, work out the **reason**:
   - to run work in parallel;
   - to get a fresh eye, because the main agent kept saying it was better when it wasn't;
   - a long job, kept off the main thread;
   - the main agent was busy, slow or bloated (compactions, very large transcript);
   - the agent stopped instead of continuing;
   - a side session the human opened themselves.
3. Read each subagent's task and final report. Ask:
   - Did it check its own work?
   - Did the human have to ask to see its result?
   - Was it stopped or rerun?
   - Was its work committed without being checked?
4. Propose automation:
   - named agents that launch unasked for a known kind of job;
   - a backlog the main agent fans out to workers;
   - results shown in the report (before/after images, links) so the human doesn't have to ask;
   - time boxes with clock checks;
   - a stop rule that keeps unchecked work out of commits.

   Count the prompts each change saves.

Example from "Slop": about 67% of the human's prompts went into driving subagents, and the Juno appearance loop alone took about 43. The resulting fixes were a self-checking asset-builder agent, before/after sheets in every report, and an auto-dispatched backlog.
