# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check                      | Evidence                                                                                          | Pass condition                                                                                                                                                                                                                                         | Weight    |
| -------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------- |
| Version + OS               | Look at the candidate's repro report as per the section "Environment" in evidence-guide.md        | Candidate mentions all of the following: version number, operating system                                                                                                                                                                              | required  |
| Commit hash                | Look at the candidate's repro report as per the section "Environment" in evidence-guide.md        | Candidate mentions a commit hash when recreating the environment                                                                                                                                                                                       | preferred |
| Easy-to-follow steps       | Look at the candidate's repro report as per the section "Steps" in evidence-guide.md              | Passes the "Steps" section in evidence-guide.md. A stranger should be able to reach the same conclusion as the candidate regardless of format.                                                                                                         | required  |
| Explicit delta             | Look at the candidate's repro report as per the section "Behavior shown" in evidence-guide.md     | Passes the "Behavior shown" section in evidence-guide.md. Artifact is provided in the accepted formats and there is an expected and actual output.                                                                                                     | required  |
| Honesty                    | Look at the candidate's claim comment and proof as per the section "Honesty" in evidence-guide.md | Passes the "Honesty" section in evidence-guide.md. Either the artifact matches the reported failure, or the report claims to fail to reproduce with proof.                                                                                             | required  |
| Follows policy             | Look at the candidate's claim comment as per the section "Comms" in evidence-guide.md             | The candidate discloses AI assistance if the repo's policy requires it. Fails if the repo's policy requires disclosure and no disclosure statement appears in the candidate's post. The absence of AI-sounding language isn't a pass condition itself. | required  |
| No over-promising          | Look at the candidate's claim comment as per the section "Comms" in evidence-guide.md             | The candidate promises to deliver no more than what they can handle.                                                                                                                                                                                   | required  |
| Proof driven claim comment | Look at the candidate's claim comment as per the section "Comms" in evidence-guide.md             | The candidate's claim comment is backed by objective facts, not subjective feelings.                                                                                                                                                                   | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if all required checks pass. Unclear counts as fail. Preferred checks don't change the verdict, they only help rank accepted issues.
