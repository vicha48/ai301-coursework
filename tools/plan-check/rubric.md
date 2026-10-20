# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.

Answer the question "Is this plan ready to post and build from?"
-->

## Checks

| Check                | Evidence                                                                                                                                                | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Weight    |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| Reasonable diagnosis | Look at the plan's stated cause and the repro evidence as per the section "Diagnosis and grounding" in evidence-guide.md                                | Passes the "Diagnosis and grounding" section in evidence-guide.md. The stated cause would produce exactly the behavior the repro shows and contradicts nothing in it, including any control run. The fix lands at the stage the cause names. A cause borrowed from a thread commenter counts only if the repro supports it.                                                                                                                                              | required  |
| Bounded scope        | Look at the plan's in-scope statement, not-in-scope line, and files list as per the section "Scope" in evidence-guide.md                                | Passes the "Scope" section in evidence-guide.md. One bounded change: files named, at least one concrete thing named as not touched, and every file and piece of work traces to the diagnosis. Unrelated renames, migrations, refactors, new options, or "while I'm here" work fail. A plan smaller than the issue passes if it says what it defers.                                                                                                                      | required  |
| Executability        | Look at the plan's files and approach as per the section "Executability" in evidence-guide.md                                                           | Passes the "Executability" section in evidence-guide.md. A stranger could make the first edit without asking the author: files or code areas are named specifically enough to open, and the approach says what changes in each. A goal ("fix the bug", "look into it", "refactor as needed") fails. A flagged unknown that doesn't block the first edit passes.                                                                                                          | required  |
| Clear test plan      | Look at the plan's test plan against the repro evidence's steps and "before" output as per the section "Test plan" in evidence-guide.md                 | Passes the "Test plan" section in evidence-guide.md. The test plan re-runs the repro (or a test on the same input) and states a concrete expected result that differs from the "before" output. "Run the test suite", "see if it works", or "should feel faster" fails. A manual check passes if the expected result is concrete.                                                                                                                                        | required  |
| Faithful comments    | Look at the plan comment and the plan's approach against the thread highlights and the repo-facts block as per the section "Comms" in evidence-guide.md | Passes the "Comms" section in evidence-guide.md. Any collaborator, maintainer, or owner signal in the thread is engaged by the plan and the comment, not skipped or contradicted. The comment follows the repo's templates and review-capacity policy, carries an AI-use statement when the policy requires one, and promises only what the plan contains. Naming the next step passes. A dated deadline, a guaranteed outcome, or "please assign me" boilerplate fails. | required  |
| Honesty about skills | Look at the plan's risks and unknowns, and the Deviations heading, as per the section "Honesty" in evidence-guide.md                                    | Passes the "Honesty" section in evidence-guide.md. Risks name something specific that could go wrong, and anything unverified is written as an unknown, not a fact.                                                                                                                                                                                                                                                                                                      | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if all required checks pass. Unclear counts as fail. Preferred checks don't change the verdict, they only help rank accepted issues.

