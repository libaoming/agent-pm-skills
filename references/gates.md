# Gates

**A gate costs delegation.** Push gates to the strictest setting and every action
asks the human; decision count returns to baseline; by the outcome test the product
is back to saving hands; delegation reaches zero. The design goal is not maximum
safety — it is **the fewest questions you dare accept**.

## Four criteria

```
1. For every gate added, state how much delegation it spends
2. Prefer visible over blocking
3. Stopping must be a refusal, never silence
4. Prefer rollback over approval
```

**Why blocking is an order of magnitude more expensive than visibility**: a hard
gate requires you to enumerate the ways it can go wrong in advance — and inability
to enumerate those is exactly why you are delegating. Visibility needs no such list.
The exception is irreversible acts: money sent, message delivered — seeing it
afterwards is too late, so those get hard gates regardless.

**Why refusal beats silence**: silent truncation is not one task lost, it dismantles
the relationship. Delegation runs on predictability; after one silent failure, every
subsequent silence needs reinterpreting — finished, or dead? — and that question
sends the human back to checking every item.

**Why rollback beats approval**: approval spends one human decision every time,
rollback spends one only when something breaks. This is what the surface's
*reversible* condition was buying — a reversible surface lets gates sit after the
act, and gates placed after the act cost no delegation.

## Three gates, three positions

```
grant gate   outside the loop, passed once      <- tightest; leverage is N-fold
act gate     inside the loop, passed every time <- keep loose
write gate   at settle, once per turn           <- guards whether a memory stands up
```

Must-be-human criteria, derived from what a shipped product actually gates:
```
irreversible                (touch-key auth, publishing publicly)
acts while they are away    (creating a routine)
touches the user's machine  (local tool execution)
```

## The grant gate is a governance entrance, not a safety check

It only appears when the *rule* changes — that is the definition, not a gap, and it
is where the leverage comes from: approve one rule, cover N executions.

The deeper reason it earns its place even for low-risk rules: **you cannot manage
what you have not named.** That click creates a *handle*. Without it an agent is
running and you have nothing to grab — the only control is shutting the whole thing
off.

It is also placed at the one moment when approving is free: at creation the human
is present with attention already on this thing. Asking mid-run costs far more
(interruption, lost context). **The value is deferred** — the day you approve it you
feel nothing; three months later, when the routine has drifted, it is what saves you.

Grant is a lifecycle, not a point:
```
grant    creating a routine -> human approves
amend    changing it -> approve again
pause    unattended signals -> pause all      <- the system withdraws the grant itself
resume   one human reply -> snooze
```

## Watch for nobody watching, not for spend

Runaway spend comes from **the user forgetting something is running**, not from unit
price. Watching spend needs accurate metering; watching absence needs only timestamps.

Three signals — absence duration, unread backlog, fires-since-last-viewed — then
nudge, then pause all, then snooze on one reply. Shipped values as a calibration
reference: idle 3 days / 15 unread / 20 fires / pause delay 3 days / snooze 30 days.

This design does not try to stop the user forgetting, which is not achievable.
**It makes forgetting a recoverable state**: signals accumulate, the system pauses
using the handle, the human returns to "these were paused" and decides again.

## Self-review only counts on verifiable facts

```
verifiable fact (did it build / did it write / is the format right / did it leak)
    -> self-verification works, it is a gate
subjective quality (is this piece any good)
    -> self-assessment, not a gate
```
One shipped agent's auto-review classifier judges *whether anything leaked* — a
decidable fact. Another product's "auto-review" judging whether a draft reads well
is the same word for a different thing. Ask which kind it checks.
