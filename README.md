# agent-pm-skills

[English](README.md) · [中文](README.zh-CN.md)

Skills for people building agent products. One skill per idea, in the style of
[@mattpocock's skills](https://github.com/mattpocock/skills) — small, single-purpose,
and cross-referencing each other.

Built by tearing down four shipped products across two independent sources, then
keeping only what survived contact with a real product line.

## The skills

| Skill | Answers |
|---|---|
| **agent-positioning** | Is this a job or a capability pack? What shape is the task? Which dials should flip? |
| **agent-job-design** | The six-field job spec, three gates, and the standing-order runtime |
| **agent-north-star** | What counts as working? Which metrics went invalid when judgment flipped? |

They chain: positioning decides how deep to go, job-design builds it, north-star
measures it.

## The claim they share

**Delegation only exists against a defined job.** A capable agent with no defined
job is a capability pack — it does what you ask and stops when you stop asking.

```
what it can do      = judgment x memory
what you dare grant = judgment x memory x auditability
```

The test, applicable to anything regardless of its label — GPT, agent, assistant,
digital employee:

**Does the container carry its own memory and its own judgment?**

| | Container | Own memory | Own judgment | Verdict |
|---|---|---|---|---|
| Grok Bot | Bot | yes | yes | **job** |
| Claude Tag | Slack channel | yes | yes | **job** |
| Cowork | plugin | no | no | capability pack |

## Install

```bash
git clone https://github.com/libaoming/agent-pm-skills.git
cd agent-pm-skills && ./install.sh
```

Symlinks each skill into `~/.claude/skills/`, so `git pull` updates all of them.

## Structure

```
agent-positioning/     SKILL.md · DIALS.md · CASES.md · DIAGNOSE.md
agent-job-design/      SKILL.md · JOB-SPEC.md · GATES.md · MECHANICS.md
agent-north-star/      SKILL.md
```

## Sources

Four shipped products, two independent sources:

- **Claude Code, Cowork, Claude Tag** — Anthropic official talks and help-centre docs
- **Grok Bot** — a source-level teardown of a shipped resident-agent product

Mechanisms, architecture, and design reasoning only. No code or prompt text is
reproduced; wordings are paraphrase, with short quotations only where the exact
phrasing is itself the finding.

## License

MIT
