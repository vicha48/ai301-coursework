# Plan: issue #72, `verify_password` raises `UnknownHashError` instead of returning `False`

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72
My repro: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5881439909 

Environment: commit `f89c06f`, Windows 11, Python 3.14.2, passlib 1.7.4, bcrypt 4.3.0

## Diagnosis

`verify_password` in `core/security.py` calls `pwd_context.verify(...)` with no exception handling. When the stored hash is in an unrecognizable, passlib raises an `UnknownHashError`. Nothing in `verify_password` catches it, so the error escapes to the caller instead of returning `False`.

Evidence from my repro:

- The traceback shows the exception `raise exc.UnknownHashError("hash could not be identified")` comes from `context.py`
- The control run's output shows verification itself works (`valid hash, right password: True` and `valid hash, wrong password: False`). So the failure is due to the stored hash being unrecognizable, not the verify call itself.
- The repo's own test reproduces it. `test_verify_with_wrong_hash_format` normally has the flag `XFAIL`, but with `--runxfail` it failed with the error `passlib.exc.UnknownHashError: hash could not be identified`.

The cause is at the call (missing handling around `pwd_context.verify`) where the traceback ends in repo code, so the fix is there and not further upstream.

## Scope

In scope: Make `verify_password` return `False` when passlib raises `UnknownHashError`, and removing the xfail marker from the test that covers it.

Not in scope: 
- The warning `(trapped) error reading bcrypt version` that appears in the control run—unrelated to this bug
- Logging/alerting on malformed hashes
- Other exceptions from passlib/bcrypt
- Changing the hash that's accepted

## Files

Files that will be touched on:
- `core/security.py`, specifically the call for `verify_password`
- `tests/unit/test_security.py`—remove `@pytest.mark.xfail(strict=True, ...)` from `test_verify_with_wrong_hash_format`

## Approach

1. Before editing, we want to know if any caller for `verify_password`  depends on the exception. Search the repo for `verify_password` callers and read how each one handles its return value and exceptions.
2. In `core/security.py`, wrap the `pwd_context.verify(plain_password, hashed_password)` call in a `try` and catch only `passlib.exc.UnknownHashError`, returning `False`. Keep the existing `bool(...)` wrapping for the normal path. Add the import if it isn't already there.
	1. Wrap the call `pwd_context.verify(plain_password, hashed_password)` in a try, then only catch `passlib.exc.UnknownHashError`. Return False.
3. Update `verify_password` docstring to "returns `False` for an unrecognized hash format" (Google style, as per CONTRIBUTING.md).
4. In `tests/unit/test_security.py`, read the assertion in `test_verify_with_wrong_hash_format`, then delete the marker `@pytest.mark.xfail`. 
	- CONTRIBUTING.md says the marker is set to `strict=True`. Leaving it in after the fix would fail CI with `XPASS(strict)`.
5. Search for other tests carrying "issue #72" or H-05 xfail reason and remove their markers too, as per CONTRIBUTING.md.
6. `ruff check --fix --unsafe-fixes`will not be run, and `# noqa` lines I didn't add won't be touched.
7. Commit in small steps using Conventional Commits.
8. `plan.md` and `comment.md` will be kept out of the commits.

## Test plan

Re-run the three runs from my repro.

1. `python direct-call.py`, changed to `print(verify_password("password", "not_a_valid_bcrypt_hash"))`. 
	- Before: The traceback ends with  `passlib.exc.UnknownHashError: hash could not be identified`. 
	- Expected result: No traceback, prints `False`. Otherwise my catch is in the wrong place.
2. Run `pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v`.
	- Before: `XFAIL` marker is used
	- Expected result (after code fix with the `XFAIL` marker): `FAILED` with `XPASS(strict)`, which confirms the fix works
	- Expected result (after removing the `XFAIL` marker): `PASSED`
3. `python control.py`. 
	- Expected unchanged: `valid hash, right password: True` and `valid hash, wrong password: False`.

Run `make lint`, `make typecheck`, and `make test-unit`. 
- Expected result: All pass

## Risks and unknowns

- I don't know where else `verify_password` is called and if returning `False` would change their behavior. Step 1 in the approach checks this before I edit the code.
	- Ex: Catching `UnknownHashError` itself, relying on the exception to signal bad data
- This issue only catches`UnknownHashError`so I'll only concentrate on that. I haven't checked if passlib/bcrypt raises other exceptions for a malformed hash with a recognized prefix. If that happens, I'll make a note of it in my comment but leave it alone because it's not in the scope of this issue.
- I'm only running this on Windows 11 with Python 3.14.2, so I don't know if my results will match those on other operating systems.
- I haven't read the current assertion in `test_verify_with_wrong_hash_format`, but I'm assuming it checks for a `False` result. I'll read it before removing the marker.

## Deviations

I changed how I built and checked it, but otherwise edited the files according to plan. Here is a summary of what changed and what didn't:

1. Modified commands to run on Windows 11 Powershell (ran commands from the Makefile because `make` isn't installed on Windows 11, used `Select-String` instead of `grep`)
2. Only `api/routes/auth.py` line 80 returned a real caller for `verify_password`
3. The only `xfail` marker appears in `test_verify_with_wrong_hash_format`
4. Commits were created after every change to a file
5. Pre-existing warnings were left alone