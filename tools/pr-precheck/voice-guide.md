# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

- I mainly do backend and use Python, but have coded in C, Java and have done some frontend with Javascript, HTML and CSS. 
- I'm open to trying things so long as it's within my abilities, and this will be my first contribution ever to an open source repo. 
- I am honest about my abilities and will explicitly state if I'm out of my depth and will provide a repro report before I speculate about causes.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Match my confidence to what I actually ran  
I state how sure I am according to what I've verified, not how I feel.

- Wrong: "This is clearly the bug, no doubt about it."
- Right: "Reproduced this once locally (output below); haven't dug into why yet."

### Rule: Promise the next step, not the outcome  
My claim comment states what I'll look into, not what I'll deliver or when.

- Wrong: "I'll have a patch up by the weekend."
- Right: "My plan is to trace how the input is handled and report back."

### Rule: Say when I'm out of my depth  
If the issue requires skill(s) outside what I actually know, I'll say so instead of dodging or downplaying it.

- Wrong: "The fix is obviously in the destructuring path here."
- Right: "I don't know how this works well yet. My best guess based on what I've observed, but I could be wrong."

### Rule: My title says what changed and where  
The PR title names the behavior I changed and the place I changed it, so a maintainer can tell what the PR does without opening it. It never states an outcome bigger than the diff.

- Wrong: "Fixed the bug!!" or "Fix everything in the parser"
- Right: "Fix off-by-one in line counter when the CSV ends without a newline"

### Rule: Disclose my AI use in my own words  
My Notes for Reviewers says plainly which AI tool I used, what it did (for example drafted the first version of the fix, or explained the code), and what I wrote, ran, and checked myself. I never copy boilerplate or leave it vague.

- Wrong: "AI was used as a helper."
- Right: "I used Claude to help me understand the tokenizer and draft the first version of the fix. I ran the repro and the tests myself and rewrote the test to match the issue."

### Rule: Say what I left out or changed from my plan  
If the diff does less than my plan, or includes a change my plan didn't name, I say so in the description and say why, instead of letting the diff speak for itself.

- Wrong: "Implements the plan." (when I left out the docs update)
- Right: "I left the docs update out because I wasn't sure which page covers this. I'd like a pointer from a maintainer. I also removed the xfail marker on this issue's test, because the test passes now."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- I do not claim to be a master at any of the programming languages nor will I overstate my abilities. 
- I do not promise a fix or a date before I reproduce anything.
- I will not use an authoritative, argumentative, disrespectful voice.
- I will not use language that conveys certainty (ex: 100% confirmed, conclusively demonstrates, guaranteed) without providing the actual output to prevent an over-confident tone
- I will never skip stating a version or environment I ran on.
- I will not post a comment that can be pasted onto a different issue unchanged.
- I will not post comments that act like cheerleading instead of a repro.
- I will not tick a Testing box in a PR description for a check I did not run, and I will not leave out a check that failed.
- I will not hide or downplay that I used AI on a change.
