# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong label is not graded.

---

## Posted upstream

**GitHub username**

vicha48

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own permalink. **Then paste the text of that comment underneath the link** — the pasted text is what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-6246023622

This is my plan for issue #72, based on my repro.

**My repro:** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5881439909

**Environment:** commit `f89c06f`, Windows 11, Python 3.14.2, passlib 1.7.4, bcrypt 4.3.0

**What I found:** `verify_password` calls `pwd_context.verify(...)` in `core/security.py` but has no exception handling. My repro shows `UnknownHashError` from that call for `"not_a_valid_bcrypt_hash"`, while a valid hash returns `True` and `False` as expected.

**What I plan to do:** Catch `UnknownHashError` in `verify_password` and return `False`. Then remove the `xfail` marker from `test_verify_with_wrong_hash_format` in `tests/unit/test_security.py`. I won't touch `hash_password`, the bcrypt version warning or other exception types.

**How I'll check it:** I'll re-run my repro. The malformed hash call should print `False` instead of raising an exception. The repo's test should go from `XFAIL` to `PASSED` once the marker is gone, and my control run should be unchanged.

**What I haven't verified:** I haven't read the callers for `verify_password` yet, so I don't know if any of them depend on the exception. I'll check that before editing. So far I've only run this on Windows, not on other operating systems.

My next step will be to create a new branch `fix/72-verify-password-unknown-hash` to fix this issue.

---

## Your branch

**Branch**

fix/72-verify-password-unknown-hash

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the after. Paste oth, including the commands you ran and their output.]

Before (from my Unit 2 reproduction, commit `f89c06f`):

Control, `python control.py`:

```
valid hash, right password: True
valid hash, wrong password: False
```

Malformed hash, `python direct-call.py`:

```
Traceback (most recent call last):
  File "...\direct-call.py", line 2, in <module>
    verify_password("password", "not_a_valid_bcrypt_hash")
  File "...\core\security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
  File "...\passlib\context.py", line 2343, in verify
    record = self._get_or_identify_record(hash, scheme, category)
  File "...\passlib\context.py", line 2031, in _get_or_identify_record
    return self._identify_record(hash, category)
  File "...\passlib\context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified
```

Repo test, `pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v`:

```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
```

After (on branch `fix/72-verify-password-unknown-hash`):

These are the commands I ran followed by their output after the fix:
1. `python control.py` (expect the same two lines as above)
```
valid hash, right password: True
valid hash, wrong password: False
```
2. `python direct-call.py`, changed to `print(verify_password("password", "not_a_valid_bcrypt_hash"))` 
```
False
```
3. `pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v` (with the marker removed )
```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED
```

---

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if only one run occurred. **The last score in your list must match the agreement line in the `eval-run.txt` you committed** — that file is the record of your final run.]

19/20

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never scored). Name it by id, say what your rubric decided and what the gold label said, and explain why your rubric read it that way.]

pkg-09 (fd, `--glob` patterns with a path separator on Windows)

My rubric said `reject`, but the gold label said `accept`. In the `eval-run.txt`, it says "pkg-09 clear-accept accept reject NO failed: Reasonable diagnosis".

I tightened the criteria for the diagnosis because my former `rubric.md` blindly copied an incorrect guess from a former comment. I added the requirement to allow a borrowed explanation only if the test example actually supports it. But because of the tightened ruling, the package was failed.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan check/`, exactly as it reads now. Then say why it reads that way — what you revised to get there, or what you rejected in favour of it.]


| Check                | Evidence                                                                                                                 | Pass condition                                                                                                                                                                                                                                                                                                              | Weight   |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| Reasonable diagnosis | Look at the plan's stated cause and the repro evidence as per the section "Diagnosis and grounding" in evidence-guide.md | Passes the "Diagnosis and grounding" section in evidence-guide.md. The stated cause would produce exactly the behavior the repro shows and contradicts nothing in it, including any control run. The fix lands at the stage the cause names. A cause borrowed from a thread commenter counts only if the repro supports it. | required |

I wrote this rule like such because the previous wording was too loose for `calib-03`. The previous rule only required the plan to name a cause, but didn't check for validity. So a flawed plan for `calib-03`  passed even though its explanation contradicted the actual test data.

I tightened the rule so the explanation must actually produce the test's behavior and pass all control tests without contradictions. I also added a safeguard because the original rubric copied an explanation from an online comment without checking if the test actually backed it up for `calib-03`.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns the point in full when the reason follows.]

This rule only evaluates an explanation based on the test evidence provided in the report. If a plan gives a wrong explanation that happens to fit all the test data, the grader won't catch it because they can't test the actual program themselves.

The rule also fails plans that have weak or missing test evidence, but I'm fine with the trade-off because a plan that isn't backed by concrete evidence isn't ready to be built anyway in my opinion.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in `tools/plan-check/`.
