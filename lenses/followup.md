# Lens: follow-up of earlier lessons

**Question:** did the lessons from earlier projects in this family hold on this one?

## Find the earlier lessons

1. **From the ledger.** Read `RSI-session-retro/ledger.md`. Take every entry in this target's family that is older than this project's first session. Each accepted proposal listed there is a lesson to check.
2. **If no ledger entry exists yet**, rebuild the lessons from git:
   - In the repo you were given, list the commits to the rule files between the previous project's last session and this project's first session: `git log --after=<a> --before=<b> --format='%h %aI %s' -- <rule files>`. Take the times from the target notes, or from `sessions.md`.
   - Each rule those commits added or changed is a lesson to check. If the window is empty, use the rule files' whole history up to this project's start.
   - Say clearly in the summary that the lessons were rebuilt from git, not from a ledger.

## Check each lesson

Did the problem come back on this project?
- **Held:** no sign of the problem. Say how you looked.
- **Failed:** the same kind of correction showed up. Quote it with its session and time, and say which rule should have prevented it.
- **Not tested:** this project never reached the situation.

## Propose

- For each **failed** lesson, escalate one step:
  - text rule → required report field or checklist item;
  - checklist item → test, hook or an agent that does it.
  If it already failed on two projects, say so in the title.
- For the ledger, the **prediction check**: where earlier entries predicted prompt savings, compare them with this project's actual counts from `metrics.md`.

Your findings use the usual format. Also give a table: lesson | source (ledger or git commit) | held, failed or not tested | evidence.
