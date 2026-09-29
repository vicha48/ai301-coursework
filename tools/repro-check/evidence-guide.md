# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->


| Signal                 | On github.com               | In the eval bundle                         |
| ---------------------- | --------------------------- | ------------------------------------------ |
| Candidate repro report | Within the candidate's post | Under the section "Candidate repro report" |
How to grade what you find:
- Pass if the following are explicitly stated: the version number, operating system they ran on.
- Not outright ban, but preferred: If commit hashes were given in the original issue, it should be included.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

| Signal                  | On github.com               | In the eval bundle                         |
| ----------------------- | --------------------------- | ------------------------------------------ |
| Steps to recreate issue | Within the candidate's post | Under the section "Candidate repro report" |
Conditions that the steps are good:
- From what the candidate wrote, a stranger could reach the same starting state and trigger the same command regardless of format.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

| Signal         | On github.com               | In the eval bundle                         |
| -------------- | --------------------------- | ------------------------------------------ |
| Explicit delta | Within the candidate's post | Under the section "Candidate repro report" |

How to grade what you find:
- Output should be copied and pasted as any of the following formats (output excerpts or in its entirety, logs, screenshots)
- Candidate provides the expected and actual output

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

| Signal            | On github.com                                                          | In the eval bundle                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Candidate honesty | Look within the candidate's post for both the claim comment and proof. | Look under the section "Candidate claim comment" for the claim comment, and under the section "Candidate repro report" for the proof. |
How to grade what you find:
- Pass if either one of the following is true:
	- The artifact shows the issue's actual reported failure
	- The candidate states they can't reproduce the issue, backed by a real attempt with their own artifact and explicitly states the difference from the original issue's conditions. 
- Fail if the candidate recreates or asserts an adjacent symptom while claiming to match or silently deviates

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

| Signal              | On github.com                                                                                                                                                      | In the eval bundle                                                                                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Contribution policy | The repo-facts block's contribution-policy line (states the AI-disclosure stance: none stated / permissive / conditional / strict), read against the claim comment | The repo-facts block's contribution-policy line (states the AI-disclosure stance: none stated / permissive / conditional / strict), read against the claim comment |
How to grade what you find:
- It is a given that every candidate submission in this assignment is AI-assisted by course convention. So if the repo's policy requires disclosure (conditionally or unconditionally), that requirement is always triggered, and the candidate's post must contain an explicit disclosure statement naming the tool and extent. A missing disclosure statement is a fail whenever the policy requires one. It is never inferred as unnecessary because the text doesn't otherwise sound AI-assisted.
- The candidate doesn't promise more than they can deliver. They state what is specific to this issue (ex: names the actual bug and behavior) and promises only investigation, not a fix or date.
- Prefer objective (ex: I have recreated the issue and below is my proof) over subjective (ex: I believe I can fix this) responses in the claim comment 


