# Retro ledger

One entry per live retro, newest last. The `followup` lens reads this file to check whether earlier lessons held. Replay runs write their entry into their own run folder, not here.

Entry format:
```markdown
## <run id> (<family>)
- Target: <target>, built <dates>
- Numbers: <prompts> prompts, <wall time>, <subagents> subagents
- Accepted:
  - R1. <title>: predicted ~<n> prompts saved; <repo>@<commit>
- Escalated: <lessons that failed again, and what they became>
```

## captcha-2026-10-15 (music-video)
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
