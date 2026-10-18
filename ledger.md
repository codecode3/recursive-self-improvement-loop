# Retro ledger

One entry per run, newest last. The `followup` lens reads this file to check whether earlier lessons held. A run that stops before applying (read-only, or no set picked) writes its entry to `runs/<run>/ledger-entry.md` instead, with `Status: proposed, not applied` and no commit. Stage 0 and the `followup` lens read those files too. The next run that commits here (the `--resume` apply, or any later run) moves the entry here and lists its pending sets under Open decisions. Replay runs write their entry into their own run folder, not here. Check: `grep -c "^- Status:" ledger.md` and `grep -c "^- Pipeline:" ledger.md` both equal `grep -c "^## .*(" ledger.md`, the number of run entries (each count includes the format block below).

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

Every "waiting on you" item, one line each, oldest first. Stage 0 lists the target's open items, stage 4 offers any item open across 2 or more runs, and the `followup` lens reports it as a finding. Close an item in place with its date and answer.

Format: `- [<run>] <item>, asked <date>; status open | closed <date>: <answer>`

- [slop replay, 5c14025c] The music-videos guide fixes the Slop replay found and the live guides still lack, proposed 2026-10-14 21:38 and never answered: the CLAUDE.md standing list, a setup-form split field, a known-bugs section plus a `Rendered:` line, an 8/10 stopping bar, a take-switch impact table, a BrowserOS fallback, optional `lint_geometry.py`, compaction re-inject and backlog Stop hooks; needs OK: a hero sign-off stop (memory `rsi-session-retro.md`, "Still missing, proposed to the user and NOT applied"), asked 2026-10-14; status open.
- [captcha-2026-10-15] Ban `fork` as a missing-agent fallback (HANDOFF "Open" 1), asked 2026-10-15; status closed 2026-10-18: not banned. R10's wait-a-turn retry makes the fallback rare, and the user left the call to the main agent.
- [autojob-2026-10-18] Sets A, B, C and N1–N4 from `runs/autojob-2026-10-18/report.md`, asked 2026-10-18; status open. Resume: `/retro autojob --resume autojob-2026-10-18`.

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
