# Retro ledger

One entry per run, newest last. The `followup` lens reads this file to check whether earlier lessons held. A run that stops before applying (read-only, or no set picked) writes its entry to `runs/<run>/ledger-entry.md` instead, with `Status: proposed, not applied` and no commit. Stage 0 and the `followup` lens read those files too. The `--resume` apply of that run moves the entry here. Any run that commits here lists the entry's pending sets under Open decisions. Replay runs write their entry into their own run folder, not here. Check: `grep -c "^- Status:" ledger.md` and `grep -c "^- Pipeline:" ledger.md` both equal `grep -c "^## .*(" ledger.md`, the number of run entries (each count includes the format block below).

Entry format:
```markdown
## <run id> (<family>)
- Status: done | proposed, not applied
- Target: <target>, built <dates>
- Numbers: <prompts> prompts, <wall time>, <subagents> subagents
- Accepted:
  - R1. <title>: predicted: <n> prompts to <milestone>, <scope>; <repo>@<commit>
- Escalated: <lessons that failed again, and what they became>
- Pipeline: <lessons about the pipeline itself, or none>
- Checks: <per checker: found, fixed, skipped, open>
```

A prediction names its milestone and scope, for example `predicted: 3 prompts to first cut, all target sessions incl. side sessions`, so the next run compares like with like.

## Open decisions

Every "waiting on you" item, one line each, oldest first. Stage 0 lists the target's open items, stage 4 offers any item open across 2 or more runs, and the `followup` lens reports it as a finding. Close an item in place with its date and answer. "Open across N runs" counts the asking run plus every later run folder in `runs/` (any target; scout-only runs and replays excluded) dated on or after the `asked` date (`ls runs/`).

Format: `- [<run>] <item>, asked <date>; status open | closed <date>: <answer>`

- [slop replay, 5c14025c] The music-videos guide fixes the Slop replay found and the live guides still lack, proposed 2026-10-14 21:38 and never answered: the CLAUDE.md standing list, a setup-form split field, a known-bugs section plus a `Rendered:` line, an 8/10 stopping bar, a take-switch impact table, a BrowserOS fallback, optional `lint_geometry.py`, compaction re-inject and backlog Stop hooks; needs OK: a hero sign-off stop (memory `rsi-session-retro.md`, "Still missing, proposed to the user and NOT applied"), asked 2026-10-14; status open.
- [captcha-2026-10-15] Ban `fork` as a missing-agent fallback workspace-wide and in the music-video guides (HANDOFF "Open" 1), asked 2026-10-15; status closed 2026-10-18: not banned outside the retro skill (which already bans it for retro agents, `SKILL.md` "Agents"). R10's wait-a-turn retry makes the fallback rare, and the user left the call to the main agent.
- [autojob-2026-10-18] Sets A, B, C and N1–N4 from `runs/autojob-2026-10-18/report.md`, asked 2026-10-18; status open. Resume: `/retro autojob --resume autojob-2026-10-18`.
- [RSI-session-retro-2026-10-18] Confirm the clause added inside the approved N2 (workspace AGENTS.md "Rule edits get one independent check": "plus the before/after text of any edited file outside git (this AGENTS.md, memory)"), asked 2026-10-18; status open.

## captcha-2026-10-15 (music-video)
- Status: done
- Target: Captcha / "Ghost" (`music-videos/videos/captcha`), built 2026-10-14 (19:19–22:34 CT); not finished (lyrics v17, 14 Suno batches, no take picked)
- Numbers: 135 prompts (130 typed + 5 queued), 3 h 13 m, 5 subagents (asset-builders); 4 sessions (main `f9f4f2f2`, side `969b2c63`, `972f4a1a`, `2ae230d2`); 8 lenses, 48 findings; projected 135 → ~100 (A–C) → ~92 (with R13, R14)
- Accepted (music-videos = mv, videos/captcha = ca):
  - R1. Whole song after every lyric change (lyrics_check.py + Stop hook): ~11 prompts; mv@36b0afe, hook mv@ddffb09
  - R2. `## Locked` block for the song: ~5; mv@36b0afe, ca@106387d
  - R3. Density and metre numbers: ~4; mv@36b0afe (avg added mv@375920a)
  - R4. Edit literally, one step, "go back" = that version: ~5; mv@36b0afe
  - R5. Sound anchor and the smallest edit; generation method: ~8; mv@493d1f2, ca@d87cd00
  - R6. "Build on X" carries the song over: ~3; mv@493d1f2
  - R7. Take-pick leftovers (correctness): ~1–2; mv@493d1f2
  - R8. Story assets wait for the lyrics OK; keep/adapt/drop on a concept change: ~2 + ~90 agent-min; mv@3120280, ca@243feaf, SKILL mv@ddffb09
  - R9. Builders prove why they stopped: ~2 + a rebuild; mv@3120280, asset-builder mv@ddffb09
  - R10. CATALOG status column: ~2 later; mv@3120280
  - R11. Likeness reference for characters: ~1; mv@3120280, ca@243feaf
  - R12. `lyric-critic` agent: ~5; mv@3120280, agent mv@ddffb09
  - R13 (needs OK, approved). Up to 5 song questions when Song is blank; quiz after 2 rejected drafts: ~8; mv@493d1f2, SKILL mv@ddffb09
  - R14 (needs OK, approved). AGENTS.md "Pasted text, critique only": ~2; antigravity-projects/AGENTS.md (not a git repo)
  - Checker fixes: mv@375920a, ca@3f6feb8; re-check (0 contradictions) fix mv@030c30f
- Escalated (failed again):
  - "Republish / show the whole song" (Hello Tomorrow, Slop) → Stop hook via lyrics_check.stop_hook_reason (R1)
  - workflow rule 4 "write corrections down" (ignored for lyrics) → `## Locked` + lyrics_check exit 1 on Banned/Keep (R2)
  - "Read it once as the singer" (Hello Tomorrow) → measured density/metre in lyrics_check (R3)
  - "Never make the user run side sessions" (Slop: 4 relays) → `lyric-critic` agent (R12)
  - "Build while you wait" (Slop) backfired → story assets wait for the lyrics OK (R8)
- Pipeline: a scratchpad `--run-dir` disappears with the session, so live runs use `runs/`; appliers wrote cross-set text ahead of time; screen checker fixes against standing rules (the fork ban); they/them for the user. Added 2026-10-18 from `runs/captcha-2026-10-15/HANDOFF.md`; not applied until RSI-session-retro-2026-10-18. The fork-ban question is closed (see Open decisions).
- Checks: checker-1, checker-2, then checker-3 re-check with 0 contradictions (fix mv@030c30f); per-checker counts not recorded

## RSI-session-retro-2026-10-18 (retro-pipeline)
- Status: done
- Target: the retro pipeline itself (`RSI-session-retro/`, live `.claude/skills/retro` + 4 `retro-*` agents): precursors 10-14 (`7fea9bc0`, `e2c48038`), build 10-14 (`5c14025c`), runs captcha-2026-10-15 (`1e3fd6b9`), captcha-2026-10-17 scout-only (`122d9fba`), autojob-2026-10-18 read-only (`c8afdfcf`)
- Numbers: 74 prompts (66 typed + 8 queued; +19 machine-queued lines dropped), 93 h 55 m calendar (active 4 h 1 m + 56 m + 4 m + 38 m), 57 subagents; 8 lenses; projected build + runs 21 → ~13 (11–15), a full run 4 → 2 (start + approval)
- Accepted (all of A, B, C and N1–N3; the user left the choice to the main agent, "It is up to you to decide these."):
  - A (R1 read-only mode, R2 status + resume, R3 ledger records + Open decisions, R4 RSI triggers, R5 goal-led runs): predicted ~5 prompts over the next 3 runs, all retro sessions; RSI@72f812c, skill via RSI@565d915
  - B (R6 report check before the question, R7 outside facts sourced, R8 checker rigor): predicted ~4 prompts ("double-check" asks) over the next 3 runs; skill + agents via RSI@565d915
  - C (R9 scout queued rule, R10 agents load without a new session, R11 pipeline target notes + drift check, R12 eval honesty, correctness): predicted ~4 prompts + 1 correctness fix; RSI@62a24ce, 2f42403, 3f575d0, 0d1880f
  - N1 (needs OK, decided yes): AGENTS.md RSI routing bullet; antigravity-projects/AGENTS.md (not a git repo)
  - N2 (needs OK, decided yes): AGENTS.md "Rule edits get one independent check"; same file
  - N3 (needs OK, decided yes): retro agents follow the memory model/effort (opus 5.5 high), checkers included; skill "Agents" paragraph
  - N4 (fork ban): closed, not banned outside the retro skill (see Open decisions)
  - Cross-set text RSI@340eebc; checker fixes RSI@93ff804; re-check fixes RSI@474cbcb, RSI@6344e60
- Escalated (failed again):
  - "Double-check your work" (asked 3× in 5c14025c, 3 passes in 7fea9bc0) → report-mode checker before the question, re-check pass = 0 open issues (R6, R8), AGENTS.md independent check (N2)
  - one-shot delivery memory ignored in the build ("what next?" / "do it" 5×) → not fixed by a rule this run; tracked by eval R2
  - "find the RSI project" before the start prompt (2 runs) → skill triggers + AGENTS.md routing (R4, N1)
- Pipeline:
  - The scout's `Rule deviations:` (smoke test): its category list has no plain `repeat`, only `repeat correction`; not fixed this run.
  - The report check caught 3 wrong claims (the projection and two citations) before the question; keep it.
  - The checkers found 38 issues in a self-edit, the re-check 7 more (4 contradictions), and the 4th checker 6 more, all introduced by the previous fix round. Most came from the same rule written in SKILL, SPEC, README, target notes and ledger.md; prefer one source and pointers.
  - This run edited the live skill and agents it was running on (the tool was also the target). The user asked on 2026-10-18 for a rule: a retro of the pipeline edits `claude-config/` only and promotes to live `.claude/` after the checks and a replay. Added after this run (see its own commit).
- Agents (from transcripts): stages 1–3 ran on the frontmatter, before N3 extended the memory setting to retro agents: scout opus-5-5/medium ×1, analysts opus-5-5/medium ×8, report checker sonnet-5-5/medium ×1. From stage 5: appliers opus-5-5/high ×2, checkers opus-5-5/high ×4, smoke tests (scout, analyst, applier) opus-5-5/high ×3
- Checks: report check 3 wrong, fixed (open 0); checker-1 18 found, 18 fixed (2 memory items in stage 7); checker-2 20 found, 20 fixed; checker-3 re-check 7 open, 7 fixed in 474cbcb; checker-4 (2nd re-check) 6 open, 6 fixed in 6344e60, confirmed by grep in `checks/fixes.md` (no fifth checker by rule; `Stage 6 passed`)
