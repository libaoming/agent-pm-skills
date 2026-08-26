---
name: agent-delegation
description: Design or diagnose an agent product with the delegation frame — judge whether it is a job or a capability pack, fill the six-field job spec (surface / presence / judgment x memory / gates / receipts / outcome), find why an agent "runs but nobody relies on it", and implement the standing-order runtime. Use when designing an AI employee, a resident agent, a routine, or a long-running assistant; when deciding whether to grant an agent judgment; when an agent turns out to be an automation script; or when comparing against Claude Code, Cowork, Claude Tag, or Grok Bot.
---

# Delegation

**Delegation only exists against a defined job.** A capable agent with no defined
job is a capability pack — it does what you ask, and stops when you stop asking.

Derived from four shipped products (Claude Code, Cowork, Claude Tag, Grok Bot);
evidence and per-product breakdown in [references/cases.md](references/cases.md).

## Step 0 — Task shape, before anything else

Task duration is given by the scenario, not chosen by the designer. It decides
whether delegation is needed at all.

```
duration < how long a human can watch  -> human is present  -> presence is a design choice
duration > how long a human can watch  -> human is absent   -> judgment x memory must both flip
```

| Duration | Human | What to build |
|---|---|---|
| Seconds/minutes | Watching | Speed and interaction. Delegation machinery goes unused. |
| Hours | Back same day | Completion receipt + visible progress |
| Days/weeks | Long absent | Full stack: judgment, memory (3 questions), gates, receipts, unattended guard |

**Two tasks of different duration belong to different jobs**, even inside one product.
A product that mixes them degrades to the shallowest one.

Also split total duration from output rhythm: output-along-the-way needs an
**interruption policy** (failure mode: flooding); output-only-at-the-end needs
**visible progress** (failure mode: silence).

## The three dials

```
Surface   (terminal + user)      where it works, for whom
Presence  (headcount x frequency) how many watch, how often they are away
Delegation (judgment x memory)    what it may decide, what it retains
```

Surface must pass three hard conditions: **bounded** (you can say what is inside
and outside), **grantable** (a user can hand the boundary over in one act and know
what they handed over), **reversible** (a mistake is visible and can be rolled back).
A folder passes all three; an open browser passes none.

**Judgment and memory are one coupled pair, not two dials.** Flip judgment alone
and the agent acts without learning the rules — it repeats one mistake a hundred
times. Flip memory alone and it knows you well but never moves until you open it.

```
what it can do      = judgment x memory
what you dare grant = judgment x memory x auditability
```

Full definitions of each dial — the half-step trap (cron and worklists hand over
scheduling, keep judgment), rule vs judgment, the three memory questions
(how it writes / how long / how it forgets) — in
[references/dials.md](references/dials.md).

## Judge: job or capability pack

**Does the container carry its own memory and its own judgment?**

| | Container | Own memory | Own judgment | Verdict |
|---|---|---|---|---|
| Grok Bot | Bot | Yes, one store per bot | Yes, routines | **Job** |
| Claude Tag | Slack channel | Yes, channel-resident | Yes, knows when to jump in | **Job** |
| Cowork | plugin | No | No | Capability pack |

A plugin (skills + commands + MCP + sub-agents) fills exactly one field of the job
spec: **scope of work**. Installing a legal plugin makes Claude able to review a
contract; it does not make Claude responsible for reviewing contracts.

This judgment applies to anything regardless of what it is called — GPT, agent,
assistant, digital employee. Check the two properties, ignore the name.

## Then take one branch

| You are | Read |
|---|---|
| Defining a new job | [references/job-spec.md](references/job-spec.md) — the six fields, filled in order |
| Diagnosing an existing product | [references/diagnose.md](references/diagnose.md) — five positions, checked in order |
| Implementing the runtime | [references/mechanics.md](references/mechanics.md) — standing order, wake prompt, the flow |
| Designing the gates | [references/gates.md](references/gates.md) — grant gate, act gate, write gate |
| Comparing against shipped products | [references/cases.md](references/cases.md) — four products, three layers |

**Done means**: every one of the six job-spec fields carries a concrete value or an
explicit `none` — and each `none` is a deliberate decision you can defend, not a blank.

## Two rules that override local judgment

**Gates cost delegation.** Push gates to the strictest setting and every action
asks the human, decision count returns to baseline, and delegation reaches zero.
The goal is not maximum safety — it is *the fewest questions you dare accept*.
Spend the budget backwards: **act gates loose, grant gates tight**, because one
grant covers N acts.

**Whoever holds judgment is decided by what gets read at the decision point.**
```
judgment to the model          -> reads its own take on the current context
judgment to the standing order -> reads the original instruction, re-injected
judgment to the human          -> reads a live prompt (human in the loop)
```
Use this to audit any decision point in any agent.
