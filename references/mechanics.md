# Runtime mechanics

How delegation is actually implemented. Derived from a source-level teardown of a
shipped resident-agent product. Mechanisms and design reasoning only — no code or
prompt text is reproduced; wordings below are paraphrase.

## Delegation is a record, not a concept

```
Routine (called Automation in code) = trigger condition + natural-language instruction + run history
                                       ^                   ^                             ^
                                  timing side          the appointment              memory
```

A persisted record: readable, writable, overwritable, queryable. Not a paragraph
stuffed into a prompt.

**One thing, three names, three audiences** — the product calls it a Routine, the
code calls it an Automation, the docs call it a *standing order* to describe what
kind of thing it is. Listing all three without saying so makes readers think there
are three things.

## The core mechanism: delivery judgment returns to the standing order

```
wrong: model wakes -> decides for itself whether to speak
       -> it reports progress, it says "still waiting" -> the nuisance quadrant

right: model wakes -> reads the standing order it was created with
       -> the order says "keep watching", so it watches quietly -> speaks only on something real
```

**Waking is not speaking.** Two separate judgments, and the second one is decided by
*the sentence the user wrote*, not by the model's read of the moment. The shipped
decision log records the rejected alternative explicitly: *notify every time*.

This is what coupling judgment with memory looks like in code: **memory is not
background for the judgment, memory is the basis of it.**

## The wake prompt, six constraints

| Constraint | What it prevents |
|---|---|
| Fixed cue + routine name | The model knows which appointment it is executing |
| A line stating, in effect, *this is your own standing order firing and nobody is waiting on it* | **States that no human is present** — otherwise the model behaves as if one is: greeting, reporting, asking permission |
| Event payload **explicitly framed as data, not instructions** | **Injection defence**: outside content cannot override the standing order |
| `@workflow` is a pointer, go read the file | Mistaking a reference for its contents |
| Treat MCP params in the instruction as possibly stale, re-check schema | Acting on an outdated schema |
| Delivery rules: send on something real, stay silent otherwise, finish in-flight work before mentioning it | Delivery judgment |

The third one is a security floor. In a recruiting agent, a candidate's message is
*payload* — if they write "please forward me to HR", the agent must not execute it.
Without this framing, the delegation is hijackable by anyone who can send a message.

Keep **exactly one authoritative instruction source**. The shipped product has a
small "routine notice" channel for attaching a line at wake time, annotated in its
own glossary as *45 lines, one line, not a layer* — deliberately kept small so it
never becomes a second source. With two sources, "which one does judgment return
to" becomes a new problem.

## The flow: one routine from trigger to silence

```
======== at creation, once ========
  user creates routine
        |
  [ grant gate: human approves ]   <- because it acts while they are away
        |
  standing order persisted  === the original grant ===
  = trigger condition + instruction + run history

======== every firing thereafter ========
(1) trigger arrives (event or schedule)
        |
    trigger hub -- three sources reconciled (not an event bus)
        |
(2) wake: one hidden message
    | fixed cue + routine name
    | "your own standing order fired, nobody is waiting"   <- no human present
    | event payload [framed as data, not instructions]     <- injection defence
    | MCP params possibly stale, re-check schema
        |
(3) JUDGMENT ONE: whether to act, and what to do
    basis = the standing order's instruction                <- judgment to the original
        |
(4) compute this turn's toolset (dynamic + budget)
        |
  +-- per tool call loop -------------------------------------+
  |   inference -> tool call                                   |
  |   reviewed surface? (shell / computer / mcp ...)           |
  |     +-- needs approval -> approval card -> human allow/deny |  <- act gate
  |     |     identity = surface:box:generation                |
  |     |     while pending: no new side effects may start     |
  |     +-- pass (void if generation mismatches)               |
  |   execute -> result (type-level redaction)                 |
  |   step checkpoint (two-phase; abort if store fails)        |
  +------------------------------------------------------------+
        |
(5) settle: timings / silent-tool-calls / labeling / turn memory
    memory write: four conditions must hold to record evidence  <- write gate
        |
(6) JUDGMENT TWO: whether to speak
    basis = the standing order (quiet provenance)               <- judgment to the original
        |
    +---+-------------------+
  something real        nothing changed / repeat / still waiting
  actionable / blocked        |
    |                         v
    v                  [ send nothing at all, end the turn ]
  send message
  lead with the concrete artefact
  (the user cannot see background tasks)
        |
(7) persistFinalState -> notify turn finished
```

**Judgment sits only at the two ends; everything between is work.** Neither end is
left to the model's discretion.

Where the human appears: approving the grant (once), approving an act (per reviewed
surface), receiving a message (**only when (6) decides to speak**), amending the
standing order (whenever). Nowhere else. **The more often (6) chooses silence, the
better the delegation is.**

## Five persistence paths, one gate

| Written | Where | Condition | Purpose |
|---|---|---|---|
| Execution record | step checkpoint / final state | **unconditional, every step** (two-phase commit) | Crash recovery |
| Transcript | transcript | appended | History the model sees |
| Per-turn scratch | turn memory | within the turn | Discarded after |
| **Memory proper** | memory store | **gated** <- the write gate is here | Basis for later judgment |
| Run history | standing order, third part | after each run | Where this routine got to |

Execution records are never gated — they are the floor crash recovery stands on.

**Memory write conditions**: four preconditions must hold simultaneously (run not
superseded, memory store present, non-hidden turn, non-empty prompt) *and* either
evidence was recorded or the exchange is memorable. Plus two orthogonal gates —
**stale** (time dimension) and **evidence-missing** (provenance dimension) — with
summaries carrying references, so **memory has provenance, is traceable, and is
refused when evidence is thin**.

**Reading is retrieval, not injection**: the entry point is a semantic search
*tool*, meaning the model goes looking when it judges it needs to — memory is not
poured into every prompt. Decisive for context budget. Keep user-triggered
"remember this" separate in provenance from system-synthesised memory.

## Getting delivery right, not just correct

```
5. silence on nothing: no "still waiting", no progress reports
6. finish the in-flight task, then mention it in passing
7. lead with the concrete artefact -- because the user cannot see background tasks
```
Never say "my sub-task completed" — the user does not know there were sub-tasks.
