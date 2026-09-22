# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check                                    | Evidence                                                                                                                                                                                           | Pass condition                                                                                                                                                            | Weight    |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| Recent commits exist                     | Look at recent default-branch commits as per "Family 1: is the maintainer alive?" in references/evidence-guide.md                                                                                  | The most recent commit on the default branch is less than 1 month old                                                                                                     | required  |
| PR merged within the past 1-3 months     | At the top of the repo, under the "Pull requests" tab, look at the "Closed" tab at the description of the 1st pull request listed. It should state when the PR is closed (ex: Closed 2 hours ago). | The date closed shouldn't be more than 3 months ago                                                                                                                       | preferred |
| Active responses                         | Look at the issue response latency as per "Family 1: is the maintainer alive?" in references/evidence-guide.md                                                                                     | The replies are within 24 hours to 2 weeks                                                                                                                                | preferred |
| Recent releases                          | Look at the release latency as per "Family 2: is the repo in use?" in references/evidence-guide.md                                                                                                 | For fast moving projects, the most recent releases should be within 1 week to 1 month. For standard projects, within 1-6 months. For mature projects, 6 months to 1 year. | preferred |
| Clear documentation and onboarding guide | Look at the files in the repo                                                                                                                                                                      | There is a clear "CONTRIBUTING.md", working local development setup script, and passing CI/CD checks                                                                      | preferred |
| No assignee                              | Look at assignee as per "Family 4: is anyone already on it?" in references/evidence-guide.md                                                                                                       | The issue has no assignee                                                                                                                                                 | required  |
| No open PR                               | Look at linked PRs as per "Family 4: is anyone already on it?" in references/evidence-guide.md                                                                                                     | The issue has no open linked pull requests                                                                                                                                | required  |
| No fresh claim                           | Look at claim comments as per "Family 4: is anyone already on it?" in references/evidence-guide.md                                                                                                 | The issue has no claim comments                                                                                                                                           | required  |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
Accept only if all required checks pass. Unclear counts as fail. Preferred checks don't change the verdict, they only help rank accepted issues.