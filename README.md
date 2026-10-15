# RSI Session Retro

Turns the Claude Code sessions that built a project, subagents included, into fixes the human approves once. The fixes go into that project's guides, agents, hooks and tools. Each run is recorded so the next retro can check whether the fixes held. It works for any project, not only music videos.

There are no scripts. Every stage is done by agents through inference, so the project is one skill, four agents and the lens prompts.

Status: built (M1–M5). Run `/retro <project>`. Design: [SPEC.md](SPEC.md). Agents and skill: `claude-config/` (live copies in `antigravity-projects/.claude/`). Test: `evals/slop-replay.md`.

After installing or changing an agent in `antigravity-projects/.claude/agents/`, start a new Claude Code session. Agents load at session start, while skills reload live.
