# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

| Signal                      | On github.com                            | In the eval bundle                                                                     |
| --------------------------- | ---------------------------------------- | -------------------------------------------------------------------------------------- |
| Stated cause                | The diagnosis or "Cause" part of plan.md | Under the section "Candidate plan", in its Diagnosis (or Cause) part                   |
| Repro evidence and controls | A posted repro comment                   | Under the section "Repro evidence" (the steps, the observed output, and every control) |
| Where the fix is            | The approach or change part of plan.md   | Under the section "Candidate plan", in its Changes or Approach part                    |

How to grade what you find:
- Passes if the stated cause produces exactly the output the repro shows and no contradictions are found. Every control run must still make sense under the cause (ex: a "ran with the feature off, still fails" control means any cause that needs the feature on is invalid).
- Pass only if the fix is at the stage the cause names. Fail if it patches where the wrong output appears while the evidence points upstream.
- A cause taken from a thread comment ("as identified in this thread") counts only if the repro evidence supports it on its own. Check the repro's no-pager, feature-off or other-version runs first.
- Fail if the plan states no cause. If the package has no repro evidence, grade unclear.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

| Signal             | On github.com                                            | In the eval bundle                                                           |
| ------------------ | -------------------------------------------------------- | ---------------------------------------------------------------------------- |
| In-scope statement | The scope part of plan.md                                | Under the section "Candidate plan", in its Scope (or "Change") part          |
| Not-in-scope line  | The same scope part of plan.md                           | The same part, usually a line starting "Not in scope" or "Out"               |
| Files list         | The files part of plan.md                                | Under the section "Candidate plan", in its Files (or "Files and areas") part |
| Deferrals          | Any line saying what part of the issue is left for later | Anywhere in the Candidate plan or plan comment                               |

How to grade what you find:
- Pass if the files are named and at least one concrete thing is named as not touched, and every file and every piece of work traces to the diagnosis (the fix, its test, or a doc made false by the fix).
- Fail if the plan adds renames, migrations, refactors, new options or flags, a new abstraction, or "while I'm here" fixes the cause does not need. Count the proposed changes, several unrelated ones are unwanted rewrites.
- A plan that fixes only part of the issue and says plainly what it defers to passes. Smaller than the issue is not a fail.
- Fail if the plan has no stated boundary at all.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

| Signal                | On github.com                              | In the eval bundle                                                              |
| --------------------- | ------------------------------------------ | ------------------------------------------------------------------------------- |
| Files or code areas   | The files part of plan.md                  | Under the section "Candidate plan", in its Files (or "Files and areas") part    |
| Approach and order    | The approach part of plan.md               | Under the section "Candidate plan", in its Approach, Changes, or Steps part     |

How to grade what you find:
- Pass if a stranger can make the first edit without asking the author. The files or code areas are specifically named enough to open (a path, module, or function), and the approach says what changes in each.
- Pass if exact details can be figured out through running, as long as the area and the approach are already named.
- Fail if the approach is a goal instead of an action ("fix the bug", "investigate", "try different protocols", "refactor as needed"), or if the first step waits on a decision the plan has not made.
- A flagged unknown that does not block the first edit is fine.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

| Signal                    | On github.com                 | In the eval bundle                                                    |
| ------------------------- | ----------------------------- | --------------------------------------------------------------------- |
| Planned test and expected | The test plan part of plan.md | Under the section "Candidate plan", in its Test plan part             |
| The "before" behavior     | A posted repro comment        | Under the section "Repro evidence", the steps and the observed output |

How to grade what you find:
- Pass if the test plan re-runs the repro steps (or a test on the same input) and states an explicit expected result after the fix (ex: number, string, exit code, pass/fail outcome)
- Pass only if the expected result differs from the "before" output, so it can't be true without the fix.
- A manual check passes if the expected result is concrete. An automated test isn't required.
- Fail on "run the test suite", "make sure it works", "should feel faster", or an expected result that was also true before the fix.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

| Signal             | On github.com                                                | In the eval bundle                                              |
| ------------------ | ------------------------------------------------------------ | --------------------------------------------------------------- |
| Risks and unknowns | The risks part of plan.md                                    | Under the section "Candidate plan", in its Risk (or Risks) part |
| Deviations         | The "Deviations" heading at the end of plan.md (after build) | N/a in eval bundles                                             |

How to grade what you find:
- Pass if the risks name something specific that could go wrong (a caller, an edge case, an untested path), and anything the author has not verified is written as an unknown, not as a fact.
- Fail if the plan says "none identified" when the change obviously touches shared code or states a guess as certain.
- In live mode, an honest Deviations statement (what changed and why) passes, and so does "nothing changed" in the author's own words. Blank doesn't.
- This check is preferred and it never changes the verdict.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

| Signal              | On github.com                                                                                                           | In the eval bundle                                                                                                                                                               |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Thread signals      | The issue thread.Comments by collaborators, maintainers, and owners (constraints, pointers, "known problem", direction) | Under the section "Thread highlights": each line, with the author's association (COLLABORATOR, MEMBER, OWNER, or NONE)                                                           |
| Plan comment        | comment.md (and the comment as posted)                                                                                  | Under the section "Candidate plan comment"                                                                                                                                       |
| Contribution policy | The repo's CONTRIBUTING file, issue and PR templates, and any AI policy                                                 | Under the section "Repo facts". The bug-report template line and the contribution-policy line (states the AI-disclosure stance: none stated / permissive / conditional / strict) |

How to grade what you find:
- Pass if every signal from a collaborator, maintainer, or owner is engaged by both the plan and the comment, and neither contradicts it. Fail if the plan builds on a direction the maintainer already rejected, ignores a fix a maintainer already posted, or skips a pointer
- Signals from outside commenters matter only if the repro supports them.
- If the policy limits disclosure to pull requests, or says it asks nothing of issue comments, no statement is needed in the plan comment.
- Pass if the comment follows the repo's template and review-capacity policy (ex: a repo that reviews outside PRs only selectively shouldn't be told "PR coming shortly" with no acknowledgement).
- Pass if the comment promises only what the plan contains. Naming the next step ("I'll open a PR") is fine. A dated deadline, a guaranteed outcome, extra features, or "please assign me" comments in place of a plan is a fail.
- Prefer a comment that points to the author's own posted repro and states the expected result over a subjective one ("I want to fix this properly").
- If the thread has no comments and the repo's rules are not broken, this check passes.
