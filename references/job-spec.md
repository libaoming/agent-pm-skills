# The job spec

Delegation attaches to a job, never to a product. One product can host several
jobs; **each job fills this form separately**.

## First: which quadrant are you building

```
                    job-shaped (carries delegation)
                          ^
   generic job container  |   vertical job
   Claude Tag: a channel  |   duty officer / screener / reviewer
   customer names the job |   vendor names the job
   ----------------------+----------------------> domain-vertical
   generic capability     |   vertical capability pack
   Cowork, bare           |   Cowork + legal plugin
                          |   (can review a contract, does not own contract review)
```

Bottom-right is where most products sit while believing they are top-right.

**Container or vertical job:**
```
customer can state the scope themselves      -> ship a container, let them fill it
scope needs domain knowledge to state at all -> the vendor fills it
```
Recruiting is the second kind: a customer can state "3+ years of Java" (a filter),
but not "give up after the second exchange" or "follow up two days after a maybe" —
that is job knowledge, not a requirement.

**Who pays the definition cost** is what actually separates the tiers:

| | Who pays |
|---|---|
| Borrowed structure (Claude Tag: channels already exist) | nobody — the definition is a by-product |
| User-defined (Grok Bot: a Bot is a new abstraction) | the user — which filters out users who cannot define jobs |
| Vendor-defined | the vendor — limited to jobs the vendor thought of |
| Marketplace | third-party sellers — the cost becomes reusable and tradable |

**Borrow a container before inventing one.** An invented container has to be
learned before it can be filled, and filling it is product-manager work.

## The six fields

```
Job name: ____________

SURFACE     terminal: ________   user: ________
            bounded ___ / grantable ___ / reversible ___

PRESENCE    headcount: single | multi     frequency: always | mixed | long absent
            (frequency follows from task duration — it is not chosen freely)

DELEGATION  judgment: none | half (list/cron) | full (whether to act + whether to veto)
            memory:   how it writes ______ / how long ______ / how it forgets ______
            both flip together, or neither is worth flipping

GATES       grant gate (approve the rule):  ________   <- tight; one grant covers N acts
            act gate  (approve this action): ________   <- loose, or delegation hits zero
            must-be-human when: irreversible / acts while they are away / touches their machine
            stopping looks like: refusal | silence     <- refusal
            unattended guard: ________                 <- watches for nobody watching

RECEIPTS    form: pushed | stored                      <- pushed
            output along the way -> interruption policy: ________
            output only at the end -> visible progress: ________

OUTCOME     has it ever told you no? ___               <- if never, it saves hands, not judgment
            the number: share = its output / total work of this kind
            false-negative rate: ________              <- without this, higher share is more dangerous
            calibration: does it know when it is unsure? ___
```

**Two fields decide whether the rest is real**, and they sit inside GATES:

- **Where is the granting act?** If the answer is "the rules live in the code",
  there is no grant — only a built-in rule.
- **What is the handle?** If pausing it means shutting down the whole service,
  there is no handle, and therefore no governance.

Without a handle, no amount of judgment quality makes it safe to leave running.

## Anti-pattern: one bot holding two jobs

Tasks of different duration inside one bot drag the whole thing down to the
shallowest tier.

```
File clerk:    surface=inbox   presence=high  delegation=none (and none needed)
               minutes-scale — saving hands is the correct design here
Duty officer:  surface=chat    presence=low   delegation=full
               days-scale — needs every field above
```

The fix is not "give the bot judgment". **Split into two jobs and build delegation
into the second only**, leaving the first as it is.
