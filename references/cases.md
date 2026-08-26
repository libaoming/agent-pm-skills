# Four products, three layers

The frame holds because it fits these four, from two independent sources: three
Anthropic products (official talks and help-centre docs) and one third-party
resident-agent product (source-level teardown).

## The three dials

| | Claude Code | Cowork | Claude Tag | Grok Bot |
|---|---|---|---|---|
| **Task duration** | minutes~hours | minutes | open-ended | days |
| **Surface** | terminal + repo | desktop + one folder | Slack channel | desktop app + sandboxed box |
| **User** | engineers | knowledge workers | a whole team | single heavy user |
| **Headcount** | single | single | **multi** | single |
| **Frequency** | high | high (watches it run) | medium | **low (absent for long)** |
| **Judgment** | none (human acts) | none (human acts) | **yes: knows when to jump in** | **yes: routines, granted at creation** |
| **Memory: writes** | raw (hand-edited file) | raw | extracted from conversation | **synthesised + two gates** |
| **Memory: duration** | project | session/project | **channel-resident** | **resident store** |
| **Memory: forgets** | manual edit | — | adjust (new overrides old) | decay + eviction |
| **Quadrant** | upper-left: a tool that knows you | lower-left: one-shot tool | **upper-right: delegation** | **upper-right: delegation** |

Cowork and Claude Code did not fail to flip judgment and memory — **their task shape
does not need it.** The human is present; flipping would go unused.

## Job container: job or capability pack

| | Container | Own memory | Own judgment | Verdict |
|---|---|---|---|---|
| Grok Bot | Bot per job | yes | yes | **job** |
| Claude Tag | one Claude per channel | yes | yes | **job** |
| Cowork | plugin (skills + commands + MCP + sub-agents) | no | no | capability pack |

All three converged on *some* job container — a Bot, a channel, a plugin — which
suggests the shape is forced by reality rather than chosen: **generic delegation
does not exist.** What a generic product can offer is the ability to define jobs.

Claude Tag's container costs nothing to define because channels already exist and
`#bug-reports` is already a job description. Grok Bot's Bot is a new abstraction the
user must create, name, and configure — which filters its user base to people who
can define a job.

## Governance layer

| | Claude Tag | Grok Bot |
|---|---|---|
| Hard gate | spend caps, org and channel level | approval on **every** local tool use; leak classifier |
| **Grant gate** | Team/Enterprise beta only | **creating/amending a routine needs a confirmation card** — *"acts while they're away"* |
| Unattended | not observed | **watches for absence**: idle 3d / 15 unread / 20 fires -> pause all |
| Stopping | **refused, not silently truncated** | refusal state and blocked state get **different copy** ("it judged it shouldn't" vs "it couldn't judge") |
| Receipts | posts a video of the fix back to the channel | **revival prompt wakes the parent agent** |
| Self-review checks | did the code run (sandbox) | whether anything leaked |
| Permissions | org / workspace / private channel | box isolation + secrets scoping + protected paths |
| Judgment transfer | — | **adopt moves parentage and memory, never judgment** — otherwise a parent spawns a child to escape its own gate |

## Outcome layer

| | Claude Tag | Grok Bot |
|---|---|---|
| Number reported | **65% of the product org's PRs written by it** (share) | five memory-synthesis failure states, **counted separately** |
| Calibration | not observed | loop and ban detection carry `confidence: high|low` |
| Regression | not observed | record/playback of real model calls |
| **False-negative rate** | **not published** | **not published** |

That last row is worth noticing. Both report share; neither publishes a
false-negative rate. This may be a category-wide blind spot or simply undisclosed —
either way it is where a product can differentiate.

## Timeline: same engine, two routes

```
2026-01  Cowork research preview -- desktop, one folder, human present
2026-04  Cowork GA -- macOS + Windows, all paid plans
2026-06  Claude Tag -- Slack, Team/Enterprise beta; judgment and memory both flipped
2026-07  Cowork on web and mobile
2026-08  Claude in Slack fully replaced by Tag
```

Eight months, three "new products", **zero new engines** — Cowork shares Claude
Code's foundation; Tag runs in the same remote sandbox on the same agent SDK.
What changed each time was surface, user, and which dials were flipped.

**The capability-pack route and the job route are both viable**, and the same
company shipped both. Which one applies is decided by task shape, not ambition.
