# RSI Session Retro

Turns the Claude Code sessions that built a project, subagents included, into fixes the human approves once. The fixes go into that project's guides, agents, hooks and tools. Each run is recorded so the next retro can check whether the fixes held. It works for any project, not only music videos.

There are no scripts. Every stage is done by agents through inference, so the project is one skill, four agents and the lens prompts.

Status: built (M1–M5). Run `/retro <project>`. Design: [SPEC.md](SPEC.md). Agents and skill: `claude-config/` (live copies in `antigravity-projects/.claude/`). Test: `evals/slop-replay.md`.

A newly installed or changed agent can take a few minutes to show up in a running session (skills reload at once). If `/retro` says an agent is missing, run it again shortly.

Tested: the Slop replay on 2026-10-14 scored M1 8/8, M2 10/10, M3 pass and M4 5/5, in about 32 minutes with no human prompts (`evals/slop-replay.md`).
