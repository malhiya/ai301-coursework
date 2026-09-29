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

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

# Voice guide: how I talk upstream

## Who I am in threads

I'm new to open-source contribution, this is my first real issue. I've practiced the workflow on a training repo. I want to investigate carefully and report back exactly what I found. 

## Rules I write by

### Rule: No promised timelines

I don't promise a fix or a delivery date. I only say what I'm going to investigate next.

- Wrong: "I'll have a fix up by tomorrow!"
- Right: "Repro report on the way."

### Rule: Name the version and the behavior

I never refer to a bug vaguely. I name the exact version and the exact behavior I'm looking at, not "this bug" or "the issue."

- Wrong: "I'm looking into this bug."
- Right: "v1.20.0 ignores the `--style` flag — that's what I'm reproducing."

### Rule: Say it like I'd say it out loud

I don't perform enthusiasm and I don't sound like a bot. If I wouldn't say it in a normal conversation, I don't write it.

- Wrong: "Amazing project!! So excited to help out here!!"
- Right: "Thanks for maintaining this,  here's what I found."

### Rule: No filler

I get straight to the point. What I post should be easy to read and follow at a glance. I only go longer when the context genuinely needs it to make sense.

- Wrong: "So I went ahead and took a look at this, and I think what might be happening here, if I'm understanding it correctly, is possibly something to do with how the config gets loaded?"
- Right: "v1.20.0 isn't loading `--style` from the config. Here's what I found:"


## Things I never post

- A promised fix date or delivery timeline
- Enthusiasm I don't actually feel ("amazing project!!", exclamation-heavy praise)
- A long, hedgy explanation when a short, direct one would do
- A vague reference to "this bug" without naming the version and behavior
- "Can confirm" or similar, posted without actually having rerun it myself