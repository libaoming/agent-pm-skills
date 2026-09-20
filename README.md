# PM Stack

[English](README.md) · [中文](README.zh-CN.md)

Skills for people building agent products. One skill per idea, in the style of
[@mattpocock's skills](https://github.com/mattpocock/skills) — small, single-purpose,
and cross-referencing each other.

Built by tearing down four shipped products across two independent sources, then
keeping only what survived contact with a real product line.

**Names follow [lenny-skills](https://github.com/RefoundAI/lenny-skills)**: same topic, same name, and this repo is
the agent-product edition. Every skill answers one question: when the product is an
agent, which of the usual practices on this topic need replacing, and with what.

## The skills

| Skill | Answers | Lenny counterpart |
|---|---|---|
| **agent-positioning** | Is this a job or a capability pack? What shape is the task? Which dials should flip? | follows `positioning`, does not replace it |
| **north-star-metrics** | What counts as working? Which metrics went invalid when judgment flipped? | `north-star-metrics` |
| **measuring-pmf** | Real reliance or novelty? How much work would come back to you if it stopped? | `measuring-pmf` |
| **user-onboarding-activation** | Which moment is activation? How do users come to let go, step by step? | `user-onboarding-activation` |
| **ai-evals** | Can this piece of judgment be handed over yet? | `ai-evals` |
| **writing-prds** | The AI built the solution; how does the PM write down and explain the trade-offs and current state? | `writing-prds` |

They chain: Lenny's `positioning` sets the market position → `agent-positioning` reads the
product shape and decides how deep to go → `ai-evals` decides whether judgment can be
handed over → `user-onboarding-activation` lets users hand it over step by step →
`north-star-metrics` and `measuring-pmf` measure whether it worked. `writing-prds` covers
AI-era PRDs in general, not only agent products.

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

The skills reference each other, so install them together.

### With the skills CLI (Claude Code, Codex, Cursor and more)

```bash
npx skills add libaoming/pm-stack --skill '*'
```

A menu asks which agents to install for and whether to install globally or into the
current project. Or pass them directly:

```bash
# Claude Code only, global
npx skills add libaoming/pm-stack --skill '*' -a claude-code -g

# Claude Code and Codex together
npx skills add libaoming/pm-stack --skill '*' -a claude-code -a codex -g

# Current project only
npx skills add libaoming/pm-stack --skill '*' -a claude-code
```

| Agent | `-a` value | Global path | Project path |
|---|---|---|---|
| Claude Code | `claude-code` | `~/.claude/skills/` | `.claude/skills/` |
| Codex | `codex` | `~/.codex/skills/` | `.agents/skills/` |
| Cursor | `cursor` | `~/.cursor/skills/` | `.agents/skills/` |
| Gemini CLI | `gemini-cli` | `~/.gemini/skills/` | `.agents/skills/` |
| OpenCode | `opencode` | `~/.config/opencode/skills/` | `.agents/skills/` |

For other agents see the [skills CLI supported list](https://github.com/vercel-labs/skills#supported-agents).
Update with `npx skills update`.

### With git (Claude Code only)

```bash
git clone https://github.com/libaoming/pm-stack.git
cd pm-stack && ./install.sh
```

Symlinks each skill into `~/.claude/skills/`, so `git pull` updates all of them.

## Structure

```
agent-positioning/           SKILL.md · DIALS.md · CASES.md · DIAGNOSE.md
north-star-metrics/          SKILL.md
measuring-pmf/               SKILL.md
user-onboarding-activation/  SKILL.md
ai-evals/                    SKILL.md
writing-prds/                SKILL.md · references/
```

## Sources

Four shipped products, two independent sources:

- **Claude Code, Cowork, Claude Tag** — Anthropic official talks and help-centre docs
- **Grok Bot** — a source-level teardown of a shipped resident-agent product

Mechanisms, architecture, and design reasoning only. No code or prompt text is
reproduced; wordings are paraphrase, with short quotations only where the exact
phrasing is itself the finding.

`measuring-pmf`, `user-onboarding-activation` and `ai-evals` also draw on the author's own
work evaluating agents. Some of their criteria are derived from the other skills and
still need more products to test them against.

## References

Naming and scope take their cue from two general-purpose PM skill sets. They cover
product management in general; this repo covers only what is specific to agent
products, so they work well side by side:

- [RefoundAI/lenny-skills](https://github.com/RefoundAI/lenny-skills) — 86 skills drawn
  from Lenny's Podcast. Names here follow its convention.
  ⚠️ Every skill here except `agent-positioning` has a general-purpose namesake there,
  and the two overwrite each other when installed in the same place. Pick one per
  topic: this repo's for agent products, Lenny's for everything else. `agent-positioning`
  is the exception: it answers a different question from Lenny's `positioning` (product
  shape vs market position), so install both and use them in that order. Each skill's
  Related Skills section names its Lenny counterpart
- [phuryn/pm-skills](https://github.com/phuryn/pm-skills) — 9 plugins covering
  discovery, strategy, execution, go-to-market and growth

## License

MIT
