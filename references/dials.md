# The three dials, in full

## Surface — where it works, for whom

Three hard conditions. A surface failing any one of them is the wrong surface.

| Condition | Ask | Passes / fails |
|---|---|---|
| Bounded | Can you say what is inside and what is outside? | folder, channel, repo / an open browser |
| Grantable | Can a user hand the boundary over in one act, knowing what they handed over? | "pick this folder" / "access my computer" |
| Reversible | Is a mistake visible and rollable back? | file diff, visible messages / a sent email |

Surface and user move together in practice, so they occupy one dial. Changing the
user group **or** flipping any parameter makes it a new product; changing only the
surface while user and parameters hold makes it a **channel extension**; changing
none of the three makes it an **iteration**.

## Presence — how many watch, how often they are away

Two axes, and the second one is what separates products the first one calls identical.

```
headcount  single <-> multi
frequency  always present <-> long absent
```

Cowork and Grok Bot are both single-user. Cowork's user watches the task run;
Grok Bot's user is gone for days. Same headcount, different products.

Frequency is not an independent knob — it is set by task duration (see Step 0) and
in turn decides whether the delegation dial is worth flipping. **A product whose
human is always present gains nothing from strong memory and judgment.**

Flipping headcount to multi forces identity, billing, and visibility to be re-decided
in the same act — not as follow-on work, but as the same decision. Multi-player
also supplies witnesses: with several people watching, a wrong call gets caught by
someone. A single-user job has no witnesses, which makes pushed receipts the only
audit channel it has.

## Judgment — what it may decide

Judgment covers two decisions, and most designs only build the first:

```
whether to act   -> timing judgment (looks like "initiating" from outside)
whether to veto  -> content judgment (this is where subtraction lives)
```

### The half-step trap

```
human triggers        cron / worklist          agent judges
1 act = 1 run         1 act = N runs           1 act = N runs
                      N fixed by you           N judged by it
                      (schedule, name list)
not flipped           HALF flipped             fully flipped
```

Cron and worklist-driven agents look autonomous — one act covers many runs. But N
is yours: you supplied the schedule or the list. **Scheduling handed over, judgment
retained.**

### Rule vs judgment

Write the trigger condition down and see whether it can be finished with one `if`
and no model call.

```
if new message -> reply           metadata-level, content unread  -> RULE
if this is a bug -> open a PR     semantic-level, must comprehend -> JUDGMENT
```

### Judgment is not one model call

A model call yields an opinion. Judgment means the opinion counts.

```
can it veto anything?                    no -> opinion only
can the user rewrite the standard and have it retained?   no -> built-in rule, not a grant
can a veto be traced to a specific standard?              no -> unaccountable, so ungrantable
are conclusions stable across like inputs?                no -> the grant cannot be handed over
```

The fourth is the one most often skipped. An agent that is 80% accurate with
erratic confidence is harder to delegate to than one that is 70% accurate and knows
when it is unsure — the second can escalate to a human on its own. **Calibration is
a hidden precondition for holding judgment**, and evals earn their place here by
making judgment *predictable enough to grant*, not by raising accuracy.

## Memory — what it retains

Three questions, and the first one is usually missing.

```
how it writes   synthesised with write gates (stale / evidence-missing), or written raw
how long        session / project / resident
how it forgets  overwrite / decay / eviction / never   <- "never" is the bomb setting
```

A resident memory that only grows poisons itself: the "don't send me these" from
three months ago and the "these are fine now" from last week both sit in the store,
the older grant never expires, and judgment drifts. **"Remembers forever" is only
safe when there is an overwrite rule** — in Claude Tag, telling it to expand scope
makes it *adjust*, and that adjustment is the forgetting mechanism.

Separate two things that get conflated: **data retention** (delete 30 days after
uninstall — compliance) and **semantic forgetting** (an instruction ceasing to
apply — a stability mechanism for judgment).

## Memory versus judgment — they are different in kind

```
memory   what it knows            knowledge, accumulates on its own
judgment what it may decide       a grant, only ever conferred
```

An intern who has read every company document (memory full) still signs nothing
(judgment zero). An incoming executive who knows nothing (memory zero) holds
signing authority (judgment full) — that second one is the failure quadrant, and it
is worse than doing nothing.

**Memory is the letter of appointment; judgment is the signing authority.** What
memory stores is *the boundary the user drew* — "watch only this kind of issue" is
an act of granting, and memory is where that act persists. Without memory the grant
evaporates when the sentence ends and the agent reverts to factory settings.

At runtime, exercising judgment reads memory — there they are upstream/downstream.
At design time they are not: **memory improves on its own, judgment never does**.
Building better retrieval will not produce an agent that dares decide anything,
because "what it may veto" was never designed.
