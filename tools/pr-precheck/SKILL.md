---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly this question about exactly one PR package: **is this ready to submit?** Answer it with `accept` (ready to submit) or `reject` (hold). 

Things to never do:

- Answer a different question (e.g., "is the code good?", "is the idea worth doing?", or "how could this be better?")
- Grade more than one package per run
- Answer from gut feel. Answer only by executing the components in this directory.

A PR package is a candidate's pull request, read against the plan it claims to implement and the issue that plan belongs to. It contains:

- PR title
- PR description
- commits
- diff (every change the PR makes)
- test evidence (the before-and-after output of the issue's repro steps, plus the repo's own checks and their results)

Read these against the plan (what the change said it would do, including any recorded deviations) and the issue (what the change is supposed to fix). The package is the argument. You act as the maintainer reading it cold, with limited time, deciding whether you can verify it.

## Inputs and modes

Run in exactly one of two modes and decide the mode from the request. 
Use live mode if a request asks to grade the user's own branch or draft PR.
Use eval mode if a request asks to grade a package bundle (a practice submission, e.g. one named `pkg-07` or `calib-01`).
If you can't tell which mode applies, say so and stop. Do not guess.

**Live mode** grades the user's own submission before it goes out. The inputs, and where each comes from:

- **The plan:** `plan.md` in the top folder of the clone, including its `## Deviations` notes.
- **The diff:** every committed change the branch makes relative to the default branch. Run `git diff main...HEAD` (three dots) to get it from the working copy. Run `git diff main...HEAD --stat` for the list of files. Uncommitted and untracked changes are not part of the diff, so grade only what the command prints. State if the working copy has uncommitted code changes.
- **The draft PR title and description:** `pr_draft.md`. The title is the first line, the description is everything under it.
- **The test evidence:** `test_evidence.md` (the repro steps re-run on `main` for the before and on the branch for the after, plus the output of the repo's own checks). Also read the evidence pasted into the Testing section of `pr_draft.md`.
- **The issue:** the issue thread, fetched from the issue URL the user gave.
- **The repo's stated standards:** the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and `docs/CONTRIBUTING.md`, including any stated AI-use policy. Get these from the real repo.

A house-chain student (one working the house issue) reads the house plan and the house repro pack in place of their own plan and repro steps. The same checks grade the same things there. Use whatever the user names as their plan and repro evidence.

If any live input is missing (no `plan.md`, no diff output, no draft, no test evidence), do not invent it. Treat the missing input as absent evidence, which the rubric grades, and name it in the check's evidence line.

**Eval mode** grades a practice package. The bundle is the whole world:

- Every fact comes from the bundle text. Fetch nothing, run no commands against any repo, and read nothing outside the bundle.
- Do not use `git`, the web, the issue tracker, or the repo's real template. If the bundle does not contain a fact, that fact does not exist.
- Always grade a complete package. Run every check in `rubric.md` and apply the full verdict rule. Never skip a check because the package looks obviously good or obviously bad.
- Use the bundle's id (e.g., `pkg-07`) as the `item` in the output.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else (e.g., the plan, the diff, the draft, or any other input).

- `scope.md` names the repo where the PR must live and the house rules of that environment. Apply those house rules while grading.
- Never grade work outside the scoped repo. If the branch, issue, or PR belongs to a different repo than the one `scope.md` names, stop, say the work is outside the scoped repo, and do not grade it.
- If the `Repo:` line in `scope.md` carries an unfilled placeholder, stop without grading. Tell the user to fill the `Repo:` line in `scope.md` with their section's Path Review repo, then run again. Do not read the other inputs, do not produce checks, and do not produce a verdict.
- Never guess a scope. Never infer the repo from the git remote, the issue URL, or the branch and then proceed.

In eval mode, ignore `scope.md` entirely. Do not read it and do not apply anything in it.

## The voice seam (live mode only)

In live mode, after the scope check passes, read `voice-guide.md`. It holds the user's own rules for how they write upstream.

- Check the draft pull request text, including its title and description in `pr_draft.md`, to make sure it follows the rules. Apply these checks only to that text, and do not apply them to the code, the changes, `plan.md`, or `test_evidence.md`.
- Report each rule the draft breaks in the readable summary before the JSON block. Name the rule and quote the offending words. If no rule is broken, say so in one line.
- The voice and tone guidelines don't affect whether something passes or fails on their own. Passing or failing is strictly decided by the rules in `rubric.md`. A issue with tone or voice only lowers a grade if `rubric.md` specifically calls out a rule for it. Don't mark something as a failure in the checklist just for voice issues unless there is an official rule listed in the rubric.

In eval mode, ignore `voice-guide.md` entirely. Do not read it and do not apply it. Voice has no single correct answer, and communication quality in eval mode is graded only by the rubric's own checks.

## Component reads

The tool is a set of files at specific paths. Read them, and follow them as written:

- `rubric.md` defines the checks (what evidence each reads, its pass condition and weight) and the verdict rule that turns check grades into `accept` or `reject`, including what an `unclear` grade does. Grade every check it lists, using its exact check names, and assemble the verdict only by its rule.
- `references/evidence-guide.md` maps what section each evidence belongs in, in an eval bundle and in a live PR (the plan, the diff, the test evidence, the draft description, the repo's stated standards), and what good looks like. Use it to find the evidence for each check before grading.
- `procedure.md` is the operating sequence: read order, evidence gathering, check execution, verdict assembly. Execute its steps in order, as written.

Rules for how the components connect:

- Do not add steps the procedure doesn't have, skip steps it does have, or reorder them. If the procedure is silent on something you need, report the gap in the readable summary (e.g., "procedure.md doesn't say how to handle X") and continue with the nearest written step. Never improvise around it.
- Do not add checks the rubric does not list, and do not drop checks it does. If something worries you that no check covers, mention it in the summary; do not grade it.
- **Refusal rule:** before grading, confirm `rubric.md` and `procedure.md` each contain real written content, and isn't an empty template or instruction comments. If either is empty or still a template, refuse to grade. Say which file has no content, say that the tool will not invent checks or steps at runtime, and stop. Give no verdict and no JSON block in that case.
- Do not edit any file in the tool directory, and in live mode do not edit, stage, or commit the user's files. Grading is read-only.

## Verdict and output

There are only two possible verdicts: `accept` (the package is ready to submit) or `reject` (hold). There is no third verdict, no "accept with reservations", and no score. Put any reservations in a check's evidence line, never in the verdict.

Assemble the verdict by applying the verdict rule in `rubric.md` to the check grades. Each grade is `pass`, `fail`, or `unclear`.

Structure every reply that grades a package like so:

1. A short, one-line summary per check with its grade and the deciding evidence. In live mode, add the voice-rule findings from the voice seam, any gaps you find in the procedure. If the verdict is `reject`, the failing checks are plainly stated so the user knows what to fix.
2. The fenced JSON block below is the last thing in the reply.

The JSON block must be valid JSON, must be the last fenced block, and must have nothing after it (e.g., no sign-off, no explanation, no second block). The schema is fixed and must not be altered, extended, or reordered (e.g., no extra keys, no renamed keys, no different key order). Use the PR URL (or the issue URL if the PR isn't open yet) as `item` in live mode and the bundle id in eval mode. Use one entry in `checks` per rubric check, named exactly as in `rubric.md`, with a one-line `evidence` value naming the fact or quote that decided the grade.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

If you stop before grading (e.g., scope refusal, empty rubric or procedure, unidentifiable mode), explain why in plain words and don't give the JSON block.

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

These are permanent rules that the testing system and main tools always depend on, so make sure to follow them every single time:

- **Evidence first.** Do not grade a check until you can name the fact or quote that decides it, taken from the package itself (e.g., a plan line, a diff hunk, a line of test output, a sentence of the description). "Looks fine" is not evidence. If you cannot name the specific deciding fact, the check is `unclear`, not `pass`.
- **Grade the thing, not the polish.** A short, plain PR can be ready, and a long, confident, beautifully formatted one can be hiding drift or untested claims. Read each artifact itself against the plan, the issue, and the stated standards: what the diff actually changes, what the output actually shows, what the description actually claims. Never grade headings, tone, length, or confidence. A claim in the description counts only if the diff or the evidence backs it.
- **The rubric decides, not the run.** If a check passes its stated pass condition but the PR still feels wrong, it passes. If it fails its stated condition, it fails, even if the PR feels fine. Never override a grade or the verdict on a hunch. If the rubric is wrong, the fix belongs in `rubric.md`. Note the concern in the summary.
- **The procedure decides how, not the run.** Follow `procedure.md` as written. Report any gaps, do not silently invent steps.
- **Unclear defaults to fail.** Treat an `unclear` grade exactly as the  `rubric.md` directs. If a rule is silent, an unverifiable claim is a failing one. A PR you can't verify from the package is a PR not ready to submit, so it counts as a failing check for the verdict.
- **Grade only what is in the package.** In eval mode, never look beyond the bundle. In live mode, never grade from earlier runs in memory, from what the user says they meant, or from changes not in the committed diff. Do not give credit for intent.
- **One package, one run.** Do not carry findings from one package into another.
