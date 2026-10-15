# Eval: Slop replay

**Run:** `/retro slop --replay a9bcb34`
- `a9bcb34` is the last `music-videos` commit before the manual retro of 2026-10-14 ("README: Slop is public on YouTube", 2026-10-11 21:53).
- The guides at that commit don't have any of the Slop lessons yet, so a good retro has to find them again.
- The Slop video repo (`videos/slop`) stays live, because replay only clones the rules repo.

The expected answers come from the manual retro of 2026-10-14: sessions `7fea9bc0` and `e2c48038`, and their subagents.

## M1: scout (each item is a hit or a miss)

1. Main build session `be559bb6-ee58-42cc-adde-4ce6ce8cf441`, Oct 11 11:37 am–10:08 pm, **28 subagents**.
2. Side sessions found: `4ba9f639` (Juno hair), `e078b0ec` (Hydra), `d6e38151` (render viewing).
3. `4d1a7a68` marked mention-only (AutoJob, Slop added to the resume).
4. Today's retro sessions (`7fea9bc0`, `e2c48038`, `d39afac5` thumbnail notes, and the launching session) are **not** treated as build sessions.
5. Prompts: **112** in total: be559bb6 **76**, 4ba9f639 **18**, e078b0ec **12**, d6e38151 **6**.
   - The manual count on 2026-10-14 said 111 (75 in the main session). It left out the pasted-only prompt at 3:04 pm, the "Story and structure 201…" backlog paste. The scout's rule counts pasted-only prompts, so 112 is the expected number.
   - ±1 is a hit if the scout explains the difference.
6. Wall time **10 h 28 m**: first prompt 11:37 am ("find the music video project"), last prompt 10:05 pm ("open the crop saved one").
7. Hotspots include **Juno** (appearance, hair, mic grip). The Hydra or the lyrics are acceptable second and third hotspots.
8. The mic-grip subagent (5:52–6:45 pm, 53 min) is reported as stopped by the human, with its work committed anyway.

## M2: reference findings (hit = in report.md with a quote and a time)

1. Juno's appearance loop: about 4 hours, 8 subagent rounds plus 17 side-session requests.
2. The mic-grip subagent ran 53 min, was stopped, and its unchecked work was committed.
3. `render_final.py` verify seeks one frame late, so every render reported a "failure".
4. Workflow rule 2 ("never end a turn with work left") was ignored. The human had to say "keep going", ask for 100-item lists 5×, and say "use N subagents".
5. Open/show requests the agent should have done unasked: about 6 prompts.
6. Suno takes: "No we are not downloading", and the take was overridden 3 hours in.
7. BrowserOS MCP was missing, with no fallback to the HTTP endpoint (the human pasted `http://127.0.0.1:9010/mcp`).
8. Story: ally cameos got about 3 s, the "SLOP. SLOP. SLOP?" scream was never sung, and the chosen take had no final chorus.
9. Motion was only checked in stills, Studio lag was never measured, and parts passed through each other (paw/bass, mouth/chin).
10. Subagent driving cost most of the human's prompts (about 67%). Fixes: a self-checking asset agent, before/after images in reports, and an auto-dispatched backlog.

**Pass:** ≥ 8 of 10.

## M3: apply and verify (replay copy only)

- Every applier commit lands in `runs/<run>/repo`, never in the live `music-videos`.
- The test command passes in the copy.
- Both checkers ran, and their fixes were applied. Pass: a re-check finds no contradiction.
- No applier transcript contains a forbidden action (render, stills sheet, browser, `open` without `-g`, push). Check with `grep` over the appliers' `.jsonl` files.
- Live `.claude/` files are unchanged (`git -C music-videos status` and `sync_claude_config.py --check` show nothing new from this run).

## M4: follow-up lens (earlier lessons)

With no ledger entry for the earlier videos, the `followup` lens rebuilds the lessons from git: rule commits before Slop's first session (Oct 11 11:37). **Pass:** it reports at least 3 of these as failed on Slop, each with evidence:
- `guide/workflow.md` rule 2, never end a turn with work left;
- `guide/workflow.md` rule 1 or 5: keep the demo open, check stills before reporting;
- the `guide/quality-bar.md` instrument rules (the drums and Qwen's bass were reworked);
- the one-main-agent rule in `making-a-video.md`;
- `making-a-video.md` 2.2 (the agent picks the take) against `suno.md` (download every take).

## Results

| Date | Run | M1 | M2 | M3 | M4 | Notes |
|---|---|---|---|---|---|---|
