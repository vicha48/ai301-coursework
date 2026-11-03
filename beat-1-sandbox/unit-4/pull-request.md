# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/251

**Branch**

fix/72-verify-password-unknown-hash

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these fields.

**Run history**

From oldest to newest run:
1. 18/19 
2. 4/6 (partial run)
3. 20/20

**Package analysis**

I picked `pkg-11` (BurntSushi/ripgrep#3477, the escaped trailing space in `.gitignore`). The gold label is `accept`. My rubric said `reject`. The run's note was "failed: Repro before and after". After I loosened the check, it still said `reject` with "failed: Description matches diff".

The package is a clean accept—the plan, the diff, the evidence and the AI disclosure all line up. My rubric read it as a reject because two of my checks judged the form of the write-up. The first version of `Repro before and after` wanted pasted output for everything the plan's test plan named, but this package states its results next to the commands ("after: searches normally, no error", "'foo ' not listed (ignored)") and puts the rest in the `cargo test -p ignore passes (214 tests)` line. The first version of `Description matches diff` treated a loose phrase in the description ("One function touched") as a claim the diff contradicts, although the change and tests it points to are in the diff.

**Check rationale**

"Passes the "Test evidence" section in evidence-guide.md. The issue's main repro (the script or command the plan's test plan re-runs) was re-run on the change, with a before result and an after result for that same case and the expected-after stated. The before can be the original error or output quoted from the repro. The after can be pasted output or a concrete observable result ("no parse error", "`foo` not listed", "42 rows") that differs from the before and shows the fix working. Any other item the plan's test plan names (a second case, a control, a regression test) needs only a stated concrete outcome, or a test in the diff that covers it, and does not need its own pasted output. Fail if the main repro is missing, if the evidence is only a claim with no observable result ("works on my machine", "verified", "colors work now", "a day of syncing"), shows only one side, shows an after that does not show the fix, runs a different case than the plan's repro (a single-file case for a two-file repro), or leaves a second failure mode the plan names with neither a stated outcome nor a covering test."

It reads this way because my first version required every repro and control in the plan to have its own pasted before and after output, which rejected `pkg-11` (and `pkg-05`), both gold accepts. I changed it to require a before and after for the main repro only, and a stated outcome or a covering test for anything else. I kept the failures that mark a not-tested package: a bare claim with no observable result, one side only, a different case than the plan's repro, and a second failure mode with no outcome or test.

**Trade-offs**

The loosened check can now pass a PR that states a concrete after result without pasting the raw output, so it misses a PR that describes a result that never really happened. I accepted that because the check grades what the package shows and the other checks still read the diff against the claims. After loosening it, I re-ran canaries with `--only`: `pkg-04`, `pkg-07`, `pkg-10` and `pkg-14` stayed `reject`.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
