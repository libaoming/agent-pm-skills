# From spec to running system

The job spec says what to build. This says **what to build it out of** — which
modules, in what order, wired how. Module breakdown comes from a source-level
replication of a shipped resident-agent product (nine slices, 48 dependency edges),
translated into product terms.

## Each field maps to a module

| Spec field | Module | Slice |
|---|---|---|
| Scope of work | Bot identity and init (one description + one toolset) | S1 |
| Surface | Isolation scope + secret injection (what it may touch) | S2 |
| Presence | Trigger hub + scheduler (when it wakes) | S7 |
| Judgment | Dynamic toolset (what it has this turn) + decision gate (may it do this one) | S3 + S4 |
| Memory | Synthesis + two write gates (stale / evidence-missing) + persistent blocks | S6 |
| Grant gate / act gate | Authorisation state machine + ledger / decision gate | S4 |
| Unattended guard | Runaway guard | S7 |
| Receipts | Turn settle (decides whether to speak) + async messaging | S3 + S8 |
| **Outcome** | **Event ledger** | **S0.9** |

**The last row is the trap.** Every metric's data source is the event ledger, and it
sits in the foundation. **No ledger, no outcome column** — this is why "ship first,
add instrumentation later" never actually gets added later.

## Five steps from tool to employee

The serial chain is the order in which capabilities become true:

```
S0.9  Foundation: injectable clock · persistence · event ledger
        v   without this it remembers nothing and you can measure nothing
S1    Protocol + identity: what a bot is, its description and toolset
        v   now "a bot" exists as a concept
S3    Turn loop + settle: the five-beat loop · dynamic toolset + budget
        v   it can do one round of work — but forgets, and never wakes itself
S6    Memory with write gates: synthesis · stale gate · evidence gate
        v   it remembers across turns = quadrant [upper-left: a tool that knows you]
S7    Scheduling + runaway guard: trigger hub · unattended watch
        v   it wakes itself = crosses to [upper-right: delegation]
```

**S6 → S7 is the jump from upper-left to upper-right.** The formula
`judgment x memory` is, in implementation, exactly these two slices.

The four parallel slices can come later, at different costs:

| Slice | What | Cost of deferring |
|---|---|---|
| S2 isolation | security boundary | running exposed until then |
| **S4 authorisation + decision gate** | **governance** | **no handle, so nobody dares leave it running** — least deferrable |
| S5 subagents | multi-agent | fine to defer |
| S8 messaging | bot-to-bot | depends on S5 |

## The wiring, one trigger end to end

```
trigger hub (S7) --> wake
     |               reads the standing order (S1 identity + its rules)
     v
compute this turn's toolset (S3) --> judgment's "what it may do" is set here
     |
     v
  +- turn loop (S3) --------------------------------+
  |   inference -> tool call                        |
  |      v                                          |
  |   decision gate (S4) -- needs approval? --> human |  <- act gate
  |      v                                          |
  |   execute (inside S2's isolation scope)         |
  |      v                                          |
  |   write to event ledger (S0.9)                  |  <- every metric's source
  +--------------------------------------------------+
     |
     v
settle (S3) --> memory write passes both gates (S6)   <- write gate
     |
     v
decide whether to speak (S3 settle) --> async message (S8) --> you
     |
     +- runaway guard (S7) watching alongside: nobody looking -> pause all
```

## What an agent SDK gives you, and what it does not

```
SDK gives:     S3 turn loop + tool calling          <- the "doing work" ring only

SDK omits:     S4   authorisation state machine (governance)
               S6   memory write gates (remembering across turns)
               S7   scheduling + runaway guard (waking itself)
               S0.9 event ledger (being measurable)
```

**Delegation needs five rings; the SDK supplies one.** The other four are your
product's job — and they are exactly what separates a capability pack from a job.

This also explains why a plugin is a capability pack: **it only touches S1 and S3**
(description + toolset), never S6 or S7.
