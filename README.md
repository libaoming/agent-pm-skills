# agent-delegation

[English](README.md) · [中文](README.zh-CN.md)

A Claude Code skill for designing and diagnosing agent products through one frame:
**delegation**.

Most "AI employee" products are capability packs wearing a job title. They can do
the work; nobody is responsible for the work. This skill gives you the test that
separates the two, and the six-field spec that turns one into the other.

## The claim

**Delegation only exists against a defined job.** A capable agent with no defined
job does what you ask and stops when you stop asking.

```
what it can do      = judgment x memory
what you dare grant = judgment x memory x auditability
```

Judgment and memory are one coupled pair. Flip judgment alone and the agent acts
without learning your rules — it repeats one mistake a hundred times. Flip memory
alone and it knows you well but never moves until you open it.

## The test

**Does the container carry its own memory and its own judgment?**

| | Container | Own memory | Own judgment | Verdict |
|---|---|---|---|---|
| Grok Bot | Bot | yes | yes | **job** |
| Claude Tag | Slack channel | yes | yes | **job** |
| Cowork | plugin | no | no | capability pack |

Applies to anything regardless of its name — GPT, agent, assistant, digital
employee. Check the two properties, ignore the label.

## What it does

| You are | It gives you |
|---|---|
| Designing a new AI job | A six-field job spec, filled in order, with the two fields that decide whether the rest is real |
| Diagnosing an agent nobody relies on | Five positions checked in dependency order, and why misdiagnosis reverses the fix |
| Implementing a resident agent | The standing-order runtime: wake prompt constraints, the two judgment points, five persistence paths |
| Designing gates | Grant gate vs act gate vs write gate — and why gates cost delegation |
| Comparing against shipped products | Four products across three layers, two independent sources |

## Install

```bash
git clone https://github.com/libaoming/agent-delegation.git ~/.claude/skills/agent-delegation
```

Then ask Claude Code anything the skill covers — designing an AI employee, granting
an agent judgment, or why an agent turned out to be an automation script. It loads
on its own.

## Structure

```
SKILL.md                  the frame: task shape, three dials, the job/pack test
references/
  dials.md                surface, presence, judgment x memory — in full
  job-spec.md             the six fields, plus who pays the definition cost
  gates.md                three gates, four criteria, the governance entrance
  mechanics.md            standing order, wake prompt, the runtime flow
  diagnose.md             five positions, and reading the outcome numbers
  cases.md                four products across three layers
```

## Sources

Built from four shipped products, two independent sources:

- **Claude Code, Cowork, Claude Tag** — Anthropic official talks and help-centre
  documentation.
- **Grok Bot** — a source-level teardown of a shipped resident-agent product.

Mechanisms, architecture, and design reasoning only. No code or prompt text from any
product is reproduced; quoted wordings are paraphrase, and short quotations appear
only where the exact phrasing is the finding.

## License

MIT
