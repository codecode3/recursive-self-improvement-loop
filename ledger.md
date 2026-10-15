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
