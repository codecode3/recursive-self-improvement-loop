# RSI Session Retro

Turns the Claude Code sessions that built a project, subagents included, into fixes the human approves once. The fixes go into that project's guides, agents, hooks and tools. Each run is recorded so the next retro can check whether the fixes held. It works for any project, not only music videos.

There are no scripts. Every stage is done by agents through inference, so the project is one skill, four agents and the lens prompts.

Status: M1–M4 built and tested; M5 written, untested (no AGY/Codex target yet). Run `/retro <project>`. Design: [SPEC.md](SPEC.md). Agents and skill: `claude-config/` (live copies in `antigravity-projects/.claude/`). Test: `evals/slop-replay.md`, and the sync check in `targets/RSI-session-retro.md`.

Options: `--read-only` (report only, no edits outside `runs/`), `--resume <run>` (pick up a stopped run at the approval step), `--goal "<text>"` (the report opens with a goal verdict). Saying "the RSI project" ("run the RSI project on AutoJob logs") also starts the skill.

A new or changed agent appears at the next turn boundary, not after a delay (skills reload at once). If one is missing, the skill starts a background `sleep 15`, ends the turn and retries when the timer fires, up to 3 turns. Never open a new session for it.

Tested: the Slop replay on 2026-10-14 scored M1 7/8, M2 10/10, M3 pass and M4 5/5, in about 32 minutes with no human prompts. The 10 pipeline fixes it found are untested until the next replay (`evals/slop-replay.md`).
