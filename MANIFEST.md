# Manifest: what the retro pipeline is for, and how it gets better

Written 2026-10-18, after the first retro of the pipeline itself (`RSI-session-retro-2026-10-18`, see `ledger.md`). `SPEC.md` says how the pipeline works. This file says why, what "better" means, and what is still unproven.

## Two loops

- **Outer loop**, where the value is: a retro of a project (a music video, AutoJob) turns its logs into fixes, so the next project takes fewer prompts.
- **Inner loop:** a retro of the retro pipeline makes the outer loop better.

The flywheel is the inner loop speeding up the outer one. It only compounds if each turn is measured.

## What a retro of its own logs can and can't see

It can see:
1. **Where the human stepped in.** Corrections, repeated asks, "are you done?". The human is the only judge in the log, so this is the strongest signal.
2. **Failures that leave a trace in the files.** Tool errors, retries, files that disagree, or git history that contradicts a claim. For example, the M1 8/8 score was caught because the answer key changed in the same commit that scored it.

It can't see **quality nobody checked.** A lesson a run missed leaves no line in any log, and "Approve all" shows the fixes were accepted, not that they were right. That only shows up later, from outside the logs:
- in the next project's prompt counts, if the same problems come back;
- in a replay with known answers (`evals/slop-replay.md`).

**Trap:** fewer human prompts is both the goal and the main signal. A pipeline tuned only on that could learn to ask less when it should ask. The replay guards against it by scoring whether the right lessons were found, not how few prompts it took.

## What "better at retros" means

1. **Seeing problems:** finding the real lessons in a project's logs (scout, lenses).
2. **Choosing fixes:** picking the fixes that actually save prompts later (synthesis, ranking).
3. **Applying them safely:** edits that don't break or contradict other rules (appliers, checkers).
4. **Cost to the human:** prompts per run.

The 2026-10-18 meta-retro mostly improved 3 and 4: read-only mode, `--resume`, the report check (it caught 3 wrong claims before the approval question), stricter checkers, honest eval scores and self-target mode. It barely touched 1 and 2. Verdict: **probably a little better, not measured.** It is cheaper and safer to run, with no measured change in fix quality. Cheaper runs still feed the flywheel, because they get run more often, and more runs mean more evidence.

## What spins it, what stalls it

Spins it:
- `ledger.md` records every run's lessons, predictions and open decisions.
- The `followup` lens checks whether earlier lessons held and escalates the ones that failed. For example, "show the whole song" failed twice and became a Stop hook.
- One eval with known answers.

Stalls it:
- **Predictions are checked only on paper.** The `followup` lens's prediction check (`lenses/followup.md`, `SPEC.md` §6) has never run: no project has been built since a retro made predictions about it. Nothing yet deletes a fix that didn't pay off.
- **One eval case.** Slop is the only project with known answers, so a small change can't be told apart from noise.
- **Weight gain.** The 400-line rule budget covers project guides, not the pipeline's own files. The skill grew from 179 to 233 lines in one run. The checkers kept finding new issues that the previous round of fixes had introduced (38, then 7, then 6, then 10).
- **A fixed ceiling.** The fixes are instructions for the same model, approved by the human at each turn. This is a better scaffold, not a model improving itself. Once the instructions are good, the gains run out.

## Proposed: make the loop compound

Proposed 2026-10-18. **Not built; waiting on the user**, including whether to build these before or after the next Slop replay.

1. **Act on the prediction check.** When the `followup` lens finds that a fix saved under half of its prediction at the same milestone and scope, it proposes deleting or replacing that fix, not just reporting the ratio.
2. **Turn each finished retro into an eval case.** Captcha and AutoJob become replays with known answers, so the test set grows with every run.
3. **Budget the pipeline's own files.** A retro of the pipeline removes about as many lines from the skill and agents as it adds, or says which added rule earned its place.

## How we'll know

- **Slop replay** (`/retro slop --replay a9bcb34`): compare with the last row (M1 7/8, M2 10/10, M3 pass, M4 5/5). This tests whether it still finds the lessons.
- **AutoJob resume** (`/retro autojob --resume autojob-2026-10-18`): a different kind of project and a real prompt count. The target is about 2: the start prompt and the approval.
- **Next retro of the pipeline:** its eval R section against today's 0/2 baseline.

If the replay holds and AutoJob takes about 2 prompts, the meta-retro helped. If not, the added rules cost more than they saved, and the next step is trimming.
