# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it live:**

- *Eval bundle:* the `## Plan context` section contains the plan in prose: the repro evidence it built on, the diagnosis, then "Scope, one bounded change: ...", a "Not in scope: ..." sentence, "Files: ...", and "Test plan: ...". Any deferral or known limit the plan states ("will be deferred with a note", "NOT covered by this change") lives in the same paragraph; there is no separate Deviations heading, so a deviation note is any plan sentence that names a change beyond or short of the stated scope. The change itself is `### Diff` and `### Commits` under `## Candidate PR`. The description's claims are in `### Description` and `### Title`.
- *Live mode:* `plan.md` (its scope, "not in scope", and files lines, and its `## Deviations` heading), the output of `git diff main...HEAD` and `git diff main...HEAD --stat`, the branch's commit messages (`git log main..HEAD`), and the Summary and Changes sections of `pr_draft.md`.

**What good looks like:**

- Every changed file in the diff's file list and every hunk inside it, falls inside the plan's stated scope and files, or inside a deviation note that says what changed and why. A necessary extra change (e.g., removing the issue's own `xfail` marker) is in order once a note records it, and the description restates it.
- Every deliverable the plan names (the fix, a regression test, a docs page, a changelog entry) is in the diff, or a note or the description says what was left out and why.
- Every claim in the description ("tests added", "CHANGELOG entry added", "docs updated", "no other changes", "exactly the plan") points to a hunk, and nothing in the diff contradicts a claim.

**The tells:**

- *More than the plan:* a new option, flag, config setting, or API the plan never mentioned; a refactor or rename riding along; a docstring or error-message rewrite outside the change; a commit message that names work the plan does not ("harmonize", "rationalize naming", "misc cleanups"); a hunk in a file the plan lists as not in scope.
- *Less than the plan:* a planned regression test, docs page, or changelog entry that has no hunk and no note.
- *A claim the diff contradicts:* the description says a changelog or docs update was added and the diff has no such file; says "exactly the plan" over a diff with extra work; or cites a test that checks something other than the fix (a casing test under a fix about something else).
- *Honest vs silent:* a deviation or shortfall that is recorded in the plan and restated in the description is honest and still passes. The same change with no note anywhere is the silent kind.

## Test evidence (harness category: not-tested)

**Where it lives:**

- *Eval bundle:* `### Test evidence` under `## Candidate PR`, read against the plan's "Test plan: ..." sentence and the repro evidence at the top of `## Plan context` (the exact steps, the observed wrong output, and any control run). The Testing section of `### Description` often repeats the evidence and ticks boxes, so read it against `### Test evidence` too. The repo's own checks (e.g., `make lint`, `cargo test`, `yarn test`) are named in `## Repo facts` under "pull requests" or "contribution policy".
- *Live mode:* `test_evidence.md` (the repro steps re-run on `main` for the before and on your branch for the after, plus the output of the repo's checks) and the Testing section of `pr_draft.md`, the plan's test plan in `plan.md`, the repo's check commands from `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.

**What good looks like:**

- For every repro the plan names, a before result and an after result are both shown, for the same case the plan names, with the expected-after stated and the after visibly different from the before (e.g., 41 rows before, 42 after; a truncated URL before, the full URL after). A control the plan names (a case that should not change) has its outcome stated.
- Each of the repo's listed checks is named by its command or suite with its outcome stated or pasted. A pass count is best; a named command with "passes" is enough. A check that failed or had nothing to run ("no tests ran") is fine when the real output and the reason are given.

**The tells:**

- "Works on my machine", "verified locally", "colors work now", "ran it for a day": a claim with no output.
- "All tests pass" or "tests pass" with no command named.
- Only one side shown (an after with no before), or only one of the plan's two repros (one failure mode of two, or a single-file case where the repro is two-file).
- Evidence that runs a different case than the plan's repro or a test whose assertion has nothing to do with the fix.
- A box ticked in the Testing section with no output behind it, a failing check left out. (An unticked CI box in a draft is correct and not a tell.)

## Diff quality (harness category: unreviewable)

**Where it live:**

- *Eval bundle:* `### Diff` and `### Commits` under `## Candidate PR`: every `+` and `-` line, and the commit messages.
- *Live mode:* `git diff main...HEAD` (the full text, not just `--stat`) and `git log main..HEAD`. Only committed changes count.

**What good looks like:** A reviewer can read the fix without wading through noise: each hunk is the fix, the planned test, or a planned docs or changelog entry, and nothing unrelated rides along. A comment that explains the fix is part of the fix.

**The tells (debris).**

- Debug output left in `eprintln!`, `console.log`, `print`, `DBG`, `DEBUG`.
- Commented-out code, including commented-out debug lines.
- Dead or unused code(e.g., an unused helper, an `#[allow(dead_code)]` function).
- Stray `TODO` or `WIP` notes.
- Formatting-only changes: reordered imports, re-indented or rewrapped lines that are identical in content, whitespace edits, on code the fix does not otherwise change. Lines inside a statement the fix really alters are not formatting churn.
- Drive-by edits: a refactor, rename, or extra option with no part in the plan's change, even when the description discloses it.
- A commit message such as "fmt pass" or "misc cleanups" that points at any of the above.

## Standards and comms (harness category: standards-wall)

**Where it live:**

- *Eval bundle:* `## Repo facts` states the asks in its "pull requests:" line (the template's sections or checklist items: issue reference like "closes #xxxx", tests added, a changelog or what's new entry, pre-commit or lint passed, and similar) and its "contribution policy" line (the contributing guide's asks, and any AI-use or disclosure policy, or "no stated AI policy"). The PR's response is `### Description` (and `### Title`), and the changelog, docs, or test files in `### Diff`. Maintainer direction in `## Thread highlights` counts when it states an ask for the PR.
- *Live mode:* the repo's real `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`, and the stated AI policy in them, read against `pr_draft.md` (title on the first line, then the template's sections filled in, with the AI-use disclosure in Notes for Reviewers) and against the diff for file-based asks.

**What good looks like:**

- Every section the template lists is present with real content for this change, and the issue is referenced the way the repo asks (`Closes #123`, `fixes #123`). "N/A" appears only with a reason.
- Every file-based ask the repo states (a changelog or what's new entry, a test, docs) has a hunk in the diff. Checklist asks no diff can show ("code formatted") are stated honestly in the description with nothing contradicting them.
- The AI-use disclosure is in the author's own words and includes whatever the policy demands (the tool, the extent of help, that a human reviewed it). In live mode it is always present, whatever the repo's policy says.
- The title says what changed and where.

**The tells:**

- A required template section left blank, left as prompt text, or filled with a placeholder.
- A stated issue-reference ask with no `Closes #...` line anywhere in the description.
- A changelog or what's new entry the repo asks for, with no hunk in the diff.
- A repo that states a strict AI policy and a description with no disclosure; a disclosure that is boilerplate or a placeholder.
- A vague title ("update", "fixed the bug!!").
- Where nothing is asked, nothing is grade. A repo that states no template, no asks, and no AI policy makes these checks pass. (Whether the description's claims match the diff is plan fidelity, above, not this family.)
