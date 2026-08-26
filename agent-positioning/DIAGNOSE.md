# Diagnosing an existing agent product

Symptom this handles: it runs, it works, and nobody relies on it. Or: it processes
everything and the human still reviews everything.

## Check five positions, in this order

The order matters — an upstream gap makes the downstream ones unbuildable.

```
1. GRANTING ACT   Is there a moment where a user hands it a rule?
                  "The rules live in the prompt/code" -> there is none.
                  Without a grant there is no delegation, only a built-in rule.

2. HANDLE         To pause it, what object do you pause?
                  "Shut down the service" -> there is none.
                  Without a handle there is no governance, so nobody dares leave it running.

3. JUDGMENT ONE   Whether to act -- what does it read at that decision point?
                  Metadata trigger ("a message arrived") -> a rule, not judgment.

4. JUDGMENT TWO   Whether to speak / whether to veto -- does this step exist at all?
                  Missing -> it pushes everything to you -> it saves hands, not judgment.

5. MEMORY         Does this run's conclusion change the next run's behaviour?
                  No -> every run starts from zero -> the nuisance quadrant.
```

Then the gates: an act gate without a grant gate means effort went into the one that
should be loose.

## Read the diagnosis correctly — misdiagnosis reverses the fix

State which parts are **working**, not only which are missing. A worked example:

> An agent was granted the right to reject candidates. It rejected someone the user
> had said to keep. The user found out by reading the log.

```
judgment       PRESENT -- it is rejecting; this is the part that works
memory         MISSING -- yesterday's "keep this one" did not persist
auditability   MISSING -- discovery required reading the log
```

Calling judgment "missing" here leads to "revoke its rejection rights, have it push
everything to me again" — which walks the product back to saving hands. The correct
fix keeps judgment and adds the other two.

**A diagnosis that cannot name what is good produces a fix that goes backwards.**

## Common finding: one bot holding two jobs

Look for tasks of different duration inside one product.

```
minutes-scale piece: human present, delegation not needed, currently correct
days-scale piece:    human absent, needs the full stack, currently has none
```

When both sit in one bot, the whole thing degrades to the shallower tier — and the
usual reading, "this agent lacks judgment", sends you rebuilding the wrong half.
**Split into two jobs, build delegation into the days-scale one only.**

Three successive diagnoses of one real product, each cheaper than the last:
```
1st: it never says no          -> saves hands
2nd: two duration tiers mixed  -> split the tasks
3rd: one bot holding two jobs  -> split the jobs, leave the first alone
```
Only the third produces a fix that touches nothing already working.

## Reading the outcome numbers

```
does it ever tell you no?   never -> whatever the metrics say, it saves hands
what number is reported?    volume processed -> input-side, invalid once judgment flipped
                            share of output  -> correct shape
is there a false-negative rate?  no -> higher share is more dangerous, not better
```

Once judgment flips, every metric premised on "the user showed up" — active users,
session count, time spent — stops measuring anything, because the agent works while
the user is away. The replacement is **share**: its output over total work of this
kind. And share alone is unsafe: a wrong yes is visible and reversible, a wrong no
is invisible — you never learn who you missed. Without a false-negative rate, a
rising share may just mean it shrank the denominator by over-rejecting.

Where a false negative is genuinely unobservable (a screened-out candidate never
tells you they should have been called), that is a finding in itself: **it caps how
much subtraction you can responsibly delegate**, and the cap is set by how likely a
wrong rejection is to surface, not by how capable the model is.
