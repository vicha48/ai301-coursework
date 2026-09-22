# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Required checks — all pass, all three

┌────────────────────────┬──────────────────────────────────────────┬─────────────────────────────┬───────────────────┐
│                        │                   #68                    │             #72             │        #65        │
├────────────────────────┼──────────────────────────────────────────┼─────────────────────────────┼───────────────────┤
│ Recent commits (<1 mo) │ ✅ 2026-09-16, 6 days                    │ ✅ same                     │ ✅ same           │
├────────────────────────┼──────────────────────────────────────────┼─────────────────────────────┼───────────────────┤
│ No assignee            │ ✅ []                                    │ ✅ []                       │ ✅ []             │
├────────────────────────┼──────────────────────────────────────────┼─────────────────────────────┼───────────────────┤
│ No open linked PR      │ ✅ only commit refs in a student fork    │ ✅ lone cross-ref is closed │ ✅ timeline empty │
├────────────────────────┼──────────────────────────────────────────┼─────────────────────────────┼───────────────────┤
│ No fresh claim         │ ✅ classmate claim, waived by house rule │ ✅ 0 comments               │ ✅ 0 comments     │
└────────────────────────┴──────────────────────────────────────────┴─────────────────────────────┴───────────────────┘

Preferred checks — identical across all three, so they don't rank

Closed PRs: none exist (1 PR ever, #74, open) → unclear. Releases: none → fail. Maintainer response latency: no maintainer has ever replied to a student thread (Aburke225's only comments are 2026-09-16 seeding on #52/#43) → unclear. Docs/onboarding: pass — docs/CONTRIBUTING.md, docs/SETUP.md, a make setup target, and all 4 recent CI runs success.

Because the preferred checks tie, ranking is entirely on your fit profile.

Ranked: accepted, in fit order

1. #72 — verify_password raises UnknownHashError  Best fit. Pure Python backend in an API auth path, the smallest scope of the three (1–2 hours, two files: core/security.py, tests/unit/test_security.py), carries good first issue, and the thread is completely untouched — zero comments, and the one cross-reference is another student's coursework submission, not a fix. The fix is one legible idea (catch UnknownHashError, fail closed to False, drop the xfail on manifest H-05), which is exactly the shape that lets you practice tight, low-token prompting: the whole task fits in a small context with a crisp test to verify it.

2. #65 — review_service async mock misconfiguration — Also untouched and also Python backend, and the body hands you the recipe (AsyncMock for execute, MagicMock for the result object) with a one-command success signal: pytest tests/unit/test_review_service.py -q goes from 13 failed to passing. Ranked below #72 only because it's the one candidate without a good first issue label, carries no effort estimate, and async-mock plumbing across 19 tests is a wider blast radius than a two-line guard.

3. #68 — Keyword search ZeroDivisionError — Genuinely fine work and squarely in your Python wheelhouse (rag/retriever/keyword_search.py), but ranked last: the longest estimate of the three (2–4 hours), and a classmate has already posted a full reproduction, traceback, control run, and fix plan two days ago. The house rule means that doesn't block you and you should claim anyway if you want it — but with two equally valid untouched issues on the table, there's nothing to gain from duplicating work already done in public.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
    "checks": [
      {"name": "Recent commits exist", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16T21:48:26Z by Aburke225 — 6 days before today (2026-09-22)."},
      {"name": "PR merged within the past 1-3 months", "grade": "unclear", "evidence": "Closed PR list is empty — the repo has 1 PR ever (#74, open, never closed); preferred, so no verdict impact."},
      {"name": "Active responses", "grade": "unclear", "evidence": "#72 has 0 comments and no maintainer has replied on any issue in the repo, so no first-response latency can be measured."},
      {"name": "Recent releases", "grade": "fail", "evidence": "/releases and /tags both return empty — the repo has never cut a release."},
      {"name": "Clear documentation and onboarding guide", "grade": "pass", "evidence": "docs/CONTRIBUTING.md + docs/SETUP.md + a `make setup` target; last 4 CI runs (ci.yml, eval.yml) all concluded success."},
      {"name": "No assignee", "grade": "pass", "evidence": "Issue #72 assignees: []."},
      {"name": "No open PR", "grade": "pass", "evidence": "Only cross-reference is foojanbabaeeian/ai301-coursework-Fozhan#1, state closed (merged 2026-09-21), a Unit 1 coursework submission — no open linked PR."},
      {"name": "No fresh claim", "grade": "pass", "evidence": "Issue #72 has comments: 0; the 2026-09-19 referenced event is a commit in newairforces' own coursework fork, and scope.md's house rule waives classmate claims regardless."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/65",
    "checks": [
      {"name": "Recent commits exist", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16T21:48:26Z — 6 days before today (2026-09-22)."},
      {"name": "PR merged within the past 1-3 months", "grade": "unclear", "evidence": "Closed PR list is empty — the repo has 1 PR ever (#74, open, never closed); preferred, so no verdict impact."},
      {"name": "Active responses", "grade": "unclear", "evidence": "#65 has 0 comments and no maintainer reply exists anywhere in the repo to time."},
      {"name": "Recent releases", "grade": "fail", "evidence": "/releases and /tags both return empty — the repo has never cut a release."},
      {"name": "Clear documentation and onboarding guide", "grade": "pass", "evidence": "docs/CONTRIBUTING.md + docs/SETUP.md + a `make setup` target; last 4 CI runs all concluded success."},
      {"name": "No assignee", "grade": "pass", "evidence": "Issue #65 assignees: []."},
      {"name": "No open PR", "grade": "pass", "evidence": "Timeline for #65 contains only three labeled events — no connected, cross-referenced, or referenced PR in any state."},
      {"name": "No fresh claim", "grade": "pass", "evidence": "Issue #65 has comments: 0 — no claim language in the thread."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "Recent commits exist", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16T21:48:26Z — 6 days before today (2026-09-22)."},
      {"name": "PR merged within the past 1-3 months", "grade": "unclear", "evidence": "Closed PR list is empty — the repo has 1 PR ever (#74, open, never closed); preferred, so no verdict impact."},
      {"name": "Active responses", "grade": "unclear", "evidence": "yulijasso commented 2026-09-20T21:54Z with no maintainer answer ~2 days later — still inside the 24h-2wk window, and no maintainer reply exists anywhere in the repo to sample."},
      {"name": "Recent releases", "grade": "fail", "evidence": "/releases and /tags both return empty — the repo has never cut a release."},
      {"name": "Clear documentation and onboarding guide", "grade": "pass", "evidence": "docs/CONTRIBUTING.md + docs/SETUP.md + a `make setup` target; last 4 CI runs all concluded success."},
      {"name": "No assignee", "grade": "pass", "evidence": "Issue #68 assignees: []."},
      {"name": "No open PR", "grade": "pass", "evidence": "Timeline shows two referenced events pointing at commits in yulijasso/ai301-coursework (a student's own fork) — no linked PR in any state."},
      {"name": "No fresh claim", "grade": "pass", "evidence": "yulijasso's 2026-09-20 'I'd like to take this bug' is author_association NONE (a classmate); scope.md's Path Review house rule states classmate claim comments do not block an issue."}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if only one run occurred. **The last score in your list must match the agreement line in the`eval-run.txt` you committed** — that file is the record of your final run.]

Runs are ordered from oldest (first) to newest (last).
1. 18/20
2. 18/20
3. 18/20

(I had to run the same files a couple of times because the hash for `rubric.md` wasn't changing.)

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-issues are not scored). State your rubric's decision, the gold label, and the reasoning that produced your rubric's result.]

My rubric rejected `issue-09` (old but valid bounded feature; the 2022 claim is stale and the maintainer invited takers), but the gold label stated "accept". This is because "no fresh claim" is a required check in my rubric.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is currently written, with the reasoning behind its current form.]

| No fresh claim | Look at claim comments as per "Family 4: is anyone already on it?" in references/evidence-guide.md | The issue has no claim comments | required

Check: No fresh claim
Evidence: Look at claim comments as per 'Family 4: is anyone already on it?' in references/evidence-guide.md
Pass condition: The issue has no claim comments
Weight: required

I wrote this check so that there was an explicit way to determine if someone was working on an issue already. 

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns the point in full when the reason follows.]

My check doesn't recognize when a claim is re-opened, so it mistakenly thinks an old claim comment is still significant.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:]

1. The issue's fit to your interests and to the time available.
	- Issue #72 is a good fit for me because it's a small Python bug with an estimated 1-2 hours of work. Since it fits my current skillset and the estimated time is also manageable, I have more time to spend on the work itself (instead of picking up a new framework).
2. What the verdict identified correctly, and what you weighed that the rubric could not.
	- The rubric caught all expected details (ex: no assignee, no open linked Pr, etc), but not the scope of the issues. Upon further inspection, I realized #72 doesn't require me to manage/look over as many files, which makes it less complicated and appealing to me.
3. The anticipated difficulty in claiming it.
	- Not hard because there's no evidence someone has claimed it (no assignee, no claim comments).

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
