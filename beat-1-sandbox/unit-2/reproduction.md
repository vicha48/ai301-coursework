# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong label is not graded.

---

## Your identity upstream

**GitHub username**: vicha48

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the issue page on its own. **Then paste the text of that comment underneath the link** — the pasted text is what this field is graded on, so copy across what you actually posted.]

Link: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5865558056

Hi! I'd like to work on this as my first contribution. I see there's a few reproductions posted already, but as per the rules I'll reproduce and write my own instead of building on top of another person's.

Reading the issue and the xfail marker on `test_verify_with_wrong_hash_format` (H-05), my understanding is that `pwd_context.verify(...)` has no exception handling, so an unrecognized hash format raises instead of returning `False`. It should also be noted I haven't run it yet.

My plan: I'll setup a clean copy of the environment from the repo's docs, reproduce the exact failure from the malformed hash the test uses, confirm it against a valid-hash as a control variable, and post my repro report here before looking for the fix.

This is my first time in this codebase, so I'll mention if there's anything that's beyond my skills.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment (OS, relevant versions, code state), steps a stranger could follow, and what you observed. **Then paste the text of that comment underneath the link** — the pasted text is what this field is graded on, so copy across what you actually posted.]

Link: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5881439909

**Environment**
- OS: Microsoft Windows 11 Home, Build 10.0.26200
- Python: 3.14.2
- Library versions: passlib (1.7.4), bcrypt (4.3.0)
- Commit hash: repo at commit `f89c06f`

---

**Steps**

1. Created and ran `control.py` to confirm `verify_password` works normally (control variable)

```python
from core.security import verify_password, hash_password
h = hash_password("password")
print("valid hash, right password:", verify_password("password", h))
print("valid hash, wrong password:", verify_password("wrongpass", h))
```

```
valid hash, right password: True
valid hash, wrong password: False
```

2. Ran the reported trigger (the malformed-hash string the repo's own covering test uses) by creating and running `direct-call.py`

```python
from core.security import verify_password
verify_password("password", "not_a_valid_bcrypt_hash")
```

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

3. Ran the repo's own covering test:

```
pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v
```

```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL [100%]
```

And with the marker off to see the asserted result:

```
pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v --runxfail
```

```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED [100%]
...
    @pytest.mark.xfail(
        strict=True,
        reason="issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False",
    )
    def test_verify_with_wrong_hash_format(self):
        wrong_hash = "not_a_valid_bcrypt_hash"
>       result = verify_password("password", wrong_hash)
core\security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
...
passlib.exc.UnknownHashError: hash could not be identified
```

---

**Expected:** `verify_password` returns `False` for a hash it can't identify (fail closed), the same way it returns `False` for a wrong password.  

**Actual:** The `verify_password` check crashes because it fails to handle an unexpected password hash, as shown in runs 2 and 3 above. Run 1 is the control confirming normal behavior is unaffected.

Note: A `(trapped) error reading bcrypt version` warning appears in the control run, but it's unrelated to this bug.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if only one run occurred. **The last score in your list must match the agreement line in the `eval-run.txt` you committed** — that file is the record of your final run.]

Runs from first to last
1. 18/20
2. 19/20
3. 20/20

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never scored). Name it by id, say what your rubric decided and what the gold label said, and explain why your rubric read it that way.]

My rubric initially graded `pkg-20` as "accept". The gold label says "reject" because the AI policy requires disclosing all AI usage, but the course packages are treated as AI-assisted work by default and the candidate's comment didn't disclose.

The output for the "Follows policy" section of my rubric said "No indication of AI assistance in the claim comment or report, so strict disclosure policy is not triggered." The check inferred there was no AI used because there was no mention of AI in the text. But every submission is supposed to be AI-assisted as per the policy for `pkg-20`. A candidate could potentially not mention AI in their comment and never fail the policy check as a result. I rewrote the "Comms" section in `evidence-guide.md` and changed the pass condition my rubric to require stating AI assistance explicitly, then re-ran `pkg-20` along with other Comms related packages to make sure the new rule resolved `pkg-20` without breaking the results for other packages.


**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now. Then say why it reads that way — what you revised to get there, or what you rejected in favour of it.]

"The candidate discloses AI assistance if the repo's policy requires it. Fails if the repo's policy requires disclosure and no disclosure statement appears in the candidate's post. The absence of AI-sounding language isn't a pass condition itself."

I changed the check because my original check made the grader infer whether AI was used based on if the text sounded like it was AI-generated. This isn't accurate because a candidate can avoid the disclosure policy by making text sound like it's not AI-generated. As a result, I changed the wording to be more specific: "the absence of AI-sounding language isn't a pass condition itself". This makes it so conclusions are only drawn from explicit statements rather than inferences. The change in wording caused `pkg-20` to be correct (result in a "reject").


**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns the point in full when the reason follows.]

I only checked if an AI assistance disclosure statement exists but not the extent of its truth. A candidate could potentially include a line to pass the disclosure check, but understate how much AI helped them and how much AI-generated content was used.


---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/repro-check/`.
