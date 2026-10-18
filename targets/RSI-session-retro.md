# Target notes: the retro pipeline (meta-retro)

- **Family:** retro-pipeline.
- **Aliases** (a target named any of these uses this file):
  - rsi, RSI project, RSI-session-retro;
  - retro, retro pipeline.
- **Projects in order** (for the `followup` lens): one project. Earlier lessons are the `ledger.md` entries with a `Pipeline:` line from every family, plus `## Open decisions`.

## Repos

- **Rules repo:** `~/antigravity-projects/RSI-session-retro`, a git repo on main. `runs/` is gitignored.
- **Session logs:** `~/.claude/projects/-Users-me-antigravity-projects/`. For this target, retro-run sessions ARE the target, so don't exclude them. Exclude only the launching session.

## Session kinds

- `precursor`: a manual retro done by hand before the pipeline existed (for example `7fea9bc0`, `e2c48038`).
- `build`: a session that writes or extends the pipeline (for example `5c14025c`).
- `retro-run`: a session that runs `/retro` on any target. Count only the retro part of the session, and say where it ends.
- `mention-only`: a session that names the pipeline but doesn't run or change it.

## Milestones

For the scout's `Prompts per milestone:` line, one set per retro run: stages 1–7 (scout, analyze, synthesize, approve, apply, verify, report and ledger). Times come from the run's `Retro N/7` progress lines in the log, then from the stage outputs: `metrics.md`, `findings/`, `report.md`, the `## Approved` section, `applied.md`, `checks/`, and the ledger commit. A stage a run didn't reach is written `not reached`.

## Rule files

- **This repo:** `lenses/*.md`, `SPEC.md`, `README.md`, `ledger.md`, `targets/*.md`, `evals/*.md`.
- **Claude Code** (live, guarded) under `~/antigravity-projects/.claude/`:
  - `skills/retro/SKILL.md`;
  - `agents/retro-scout.md`, `agents/retro-analyst.md`, `agents/retro-applier.md`, `agents/retro-checker.md`.
- **The 5 live↔copy pairs:** each live file `.claude/<f>` has a git copy `RSI-session-retro/claude-config/<f>`, for the 5 files above. Never edit the copies.
- **`.claude/` sync:** after editing a live file, from `~/antigravity-projects` run `cp .claude/<f> RSI-session-retro/claude-config/<f>`, then the check below, then commit only the copy paths.
- **User memory:** `~/.claude/projects/-Users-me-antigravity-projects/memory/MEMORY.md` and the files it links, for example `rsi-session-retro.md`, `subagent-model-effort.md` and `one-shot-delivery.md`.

## Quality domain

Correct counts (prompts, time, subagents), checked citations and claims, eval honesty, agents that load and run, and live `.claude/` files that match their git copies.

## Test command

This is a prompt-only project with no test suite. The frontmatter parse and the sync check are the test. Paste it as one command:

```bash
cd ~/antigravity-projects && fail=0; for f in skills/retro/SKILL.md agents/retro-{scout,analyst,applier,checker}.md; do for p in .claude/$f RSI-session-retro/claude-config/$f; do python3 -I -c 'import sys,re; t=open(sys.argv[1]).read(); m=re.match(r"^---\n(.*?)\n---\n",t,re.S); k={l.split(":",1)[0] for l in (m.group(1).splitlines() if m else []) if ":" in l and not l.startswith(" ")}; need={"name","description"}|({"tools","model"} if "/agents/" in sys.argv[1] else set()); miss=need-k; miss and print("BAD FRONTMATTER",sorted(miss),sys.argv[1]); sys.exit(1 if miss else 0)' $p || fail=1; done; diff -q .claude/$f RSI-session-retro/claude-config/$f >/dev/null || { echo STALE $f; fail=1; }; done; [ $fail = 0 ] && echo "OK: 5 files parse, live == copy"
```

It prints `OK: 5 files parse, live == copy` on a pass, and `STALE <file>` or `BAD FRONTMATTER` otherwise. The final note's Checks line takes its count from it: "`.claude/` copies: in sync (5)" or "STALE <files>".

## Forbidden actions for appliers

- **No push and no deploy.**
- **Live `.claude/` files:** only the main agent edits them. Claude Code's permission prompt for them is intended. Then it syncs the copies. Appliers write the exact change in their report.
- **Other projects' files** (for example `music-videos/`, `autojob/`), the workspace `AGENTS.md` and memory: never, unless a `needs OK` item was approved, and then only the main agent.

## Evals

- `evals/slop-replay.md`: replay with `/retro slop --replay a9bcb34`. Its R section is scored from this target's scout `prompts.md` at each meta-retro: in stage 7 the main agent adds a Results row (Run = the meta-retro's run id, Key = `key@<hash>`, M1–M4 `not run`, R `<hits>/2` citing the `prompts.md` row numbers) and commits it on its own.
