# Procedure: how this skill grades a plan package

## Read order

1. Read the issue context and the thread highlights first. List each signal as one line and mark who said it (collaborator/maintainer/owner, or an outside commenter): a constraint, a pointer, a preference, a claimed cause, or a request. If there are no comments, write "no thread signals". You need this list for `faithful comments` and it tells you what the issue actually asks for.
2. Read the repro evidence block before you read the plan. Write down three things: the exact steps or command, the observed (wrong) output, and every experiment that ruled something out (ex: "disabled X, still fails"). The repro is the fixed baseline. Reading it first stops the plan's own framing from shaping what you think the evidence says.
3. Read the repo-facts block. List each template, contributing step, contribution policy, and AI-use disclosure rule it states.
4. Read the plan in this order: diagnosis, scope (in and not-in), files, approach, test plan, risks. Note the plan's cause in one line, its fix location in one line, and its not-in line verbatim.
5. Read the plan comment last. Note every commitment it makes (what it says it will do, any timeline, any request to be assigned).

## Evidence gathering

1. For `Reasonable diagnosis`, put two lines next to each other: the plan's stated cause and the repro's observed output. Add the repro's ruled-out experiments. Also record where the plan's fix lands (which function or stage) and where the wrong output first appears in the repro. If the plan says its cause comes from the thread, check whether the repro evidence supports it on its own. Try the repro's no-pager or feature-off runs first: if the failure persists with the claimed cause removed, the cause is contradicted.
2. For `Bounded scope`, copy the in-scope statement, the not-in line, and the full files list. Next to each file and each piece of work, write which part of the diagnosis it comes from. Anything you cannot trace is a creep candidate. Check whether the plan says it is deferring part of the issue.
3. For `Executability`, copy the files list and the approach. For each file, record whether the approach says what changes in it. Record any step that depends on something the plan has not decided.
4. For `Clear test plan`, copy the test plan's command or input and its stated expected result. Copy the repro's "before" output next to it, and note whether the expected result differs from it.
5. For `Faithful comments`, put your list of maintainer signals and repo-facts rules next to the comment's commitments and the plan's approach. Mark each signal as engaged, ignored, or contradicted. Treat collaborator signals as required to engage. For any AI policy in repo-facts, decide whether it asks for disclosure or own-words comments in issue comments, then look for that statement in the comment. If it is required and absent, grade F. Outside commenters' signals matter only if the repro supports them. Then check each commitment in the comment: a next step is fine, a dated deadline or outcome guarantee is not. With no thread signals and no repo-facts rule broken, this check passes.
6. For `Honesty about skills`, copy the risks and unknowns text and mark each item as specific or generic, and as an unknown or a claim.

## Check execution

1. Run the checks in this order: `reasonable diagnosis`, `Bounded scope`, `Executability`, `Clear test plan`, `Faithful comments`, `Honesty about skills`. Grade each one from the evidence you gathered for it. You don't need to re-read the whole package for each check, except `Reasonable diagnosis`, which always uses the repro evidence.
2. Grade each check P (pass), F (fail), or `unclear`, applying only that check's pass condition from rubric.md. Do not grade on polish, length, or headings.
3. If the plan doesn't state the thing a check needs, grade F. If the package doesn't contain the evidence the check reads against (no repro block), grade `unclear` and say which part is missing.
4. If the plan is smaller than the issue, don't fail it for that. Pass `Bounded scope` if the plan says what it is deferring.
5. For every grade, write one line that quotes the submission's own words, taken from the plan, the repro evidence, or the comment. Do not use words of your own as evidence.

## Verdict assembly

1. Apply the verdict rule from rubric.md: accept only if every required check is P. Any required F or `unclear` makes the verdict reject. `Honesty about skills` is preferred and never changes the verdict.
2. If the verdict is reject, name the deciding check. If more than one required check failed, the deciding check is the first failed one in the execution order above. Quote its evidence lines: for `Reasonable diagnosis`, the plan's cause and the repro line it conflicts with.
3. If the verdict is accept, quote the line that best supports the check that was closest to failing.
4. Print each check's grade with its quoted line, then the verdict (accept for ready, reject for hold) in the output format the skill requires.
