# PM Stack

[English](README.md) · [中文](README.zh-CN.md)

给做 agent 产品的人用的 skill 集。**一个 skill 一个概念**，学 [@mattpocock 的 skills](https://github.com/mattpocock/skills)
风格——小、单一职责、彼此互引。

内容来自拆解四个已上线产品（两个独立来源），只保留了在真实产品线上经得起用的部分。

**命名与 [lenny-skills](https://github.com/RefoundAI/lenny-skills) 对齐**：同一个话题用同一个名字，本仓库是它的 agent 产品版。
每个 skill 回答的都是同一个问题：做 agent 产品时，这个话题的通用做法哪些要换掉、换成什么。

## 六个 skill

| Skill | 回答什么 | 对应 Lenny |
|---|---|---|
| **agent-positioning**（产品形态） | 它是岗位还是能力包？任务是什么形状？该翻哪几格？ | 接在 `positioning` 之后，不替换它 |
| **north-star-metrics**（北极星指标） | 什么算成了？翻了判断权之后哪些指标作废了？ | `north-star-metrics` |
| **measuring-pmf**（PMF） | 用户是真依赖还是图新鲜？停了它要收回多少活？ | `measuring-pmf` |
| **user-onboarding-activation**（激活与信任爬坡） | 激活时刻是哪一刻？用户怎么一步步敢放手？ | `user-onboarding-activation` |
| **ai-evals**（评估） | 这一格判断权现在能不能交出去？ | `ai-evals` |
| **writing-prds**（深度 PRD） | AI 做完了方案，PM 怎么写清、讲清取舍和现状？ | `writing-prds` |

成链：先用 Lenny 的 `positioning` 做市场定位 → `agent-positioning` 判产品形态、决定做多深 →
`ai-evals` 决定能不能放权 → `user-onboarding-activation` 让用户一步步放权 →
`north-star-metrics` 和 `measuring-pmf` 量它成没成。`writing-prds` 是 AI 时代的通用写法，不限于 agent 产品。

## 共同的内核

**通用委托不存在——委托只能针对具体岗位。** 一个能力很强却没有岗位的 agent 是能力包：
你说什么它做什么，你不说它就停。

```
它能做多深      = 判断权 × 记忆
你敢让它做多深  = 判断权 × 记忆 × 可审计性
```

判据（不看名字，只查两样——GPT、agent、助手、智能体、数字员工一律适用）：

**容器带不带自己的记忆和判断权？**

| | 容器 | 自己的记忆 | 判断权 | 判定 |
|---|---|---|---|---|
| Grok Bot | Bot | 有 | 有 | **岗位** |
| Claude Tag | Slack 频道 | 有 | 有 | **岗位** |
| Cowork | plugin | 无 | 无 | 能力包 |

## 安装

这些 skill 互相引用，建议一起装。

### 用 skills CLI（Claude Code、Codex、Cursor 等都能用）

```bash
npx skills add libaoming/pm-stack --skill '*'
```

会弹出菜单让你选装给哪些 agent、装全局还是当前项目。也可以直接指定：

```bash
# 只装给 Claude Code，全局
npx skills add libaoming/pm-stack --skill '*' -a claude-code -g

# 同时装给 Claude Code 和 Codex
npx skills add libaoming/pm-stack --skill '*' -a claude-code -a codex -g

# 只装到当前项目
npx skills add libaoming/pm-stack --skill '*' -a claude-code
```

| Agent | `-a` 参数 | 全局路径 | 项目路径 |
|---|---|---|---|
| Claude Code | `claude-code` | `~/.claude/skills/` | `.claude/skills/` |
| Codex | `codex` | `~/.codex/skills/` | `.agents/skills/` |
| Cursor | `cursor` | `~/.cursor/skills/` | `.agents/skills/` |
| Gemini CLI | `gemini-cli` | `~/.gemini/skills/` | `.agents/skills/` |
| OpenCode | `opencode` | `~/.config/opencode/skills/` | `.agents/skills/` |

其他 agent 见 [skills CLI 支持列表](https://github.com/vercel-labs/skills#supported-agents)。更新用 `npx skills update`。

### 用 git（仅 Claude Code）

```bash
git clone https://github.com/libaoming/pm-stack.git
cd pm-stack && ./install.sh
```

会把每个 skill 软链进 `~/.claude/skills/`，之后 `git pull` 就能一起更新。

## 结构

```
agent-positioning/           SKILL.md · DIALS.md · CASES.md · DIAGNOSE.md
north-star-metrics/          SKILL.md
measuring-pmf/               SKILL.md
user-onboarding-activation/  SKILL.md
ai-evals/                    SKILL.md
writing-prds/                SKILL.md · references/
```

## 来源

四个已上线产品，两个独立来源：

- **Claude Code / Cowork / Claude Tag** —— Anthropic 官方分享与帮助中心文档
- **Grok Bot** —— 对一个已上线常驻 agent 产品的源码级拆解

只取机制、架构与设计思路。不复制任何产品的代码与 prompt 原文；文中措辞为转述，
仅在「原话本身就是发现」处保留短引用。

`measuring-pmf`、`user-onboarding-activation`、`ai-evals` 还用到了作者自己做 agent 评估的实践；
其中一部分判据是从前面几个 skill 推出来的，还需要更多产品来验证。

## 参考

命名和体系参考了两套通用 PM skill 集。它们覆盖通用产品管理，这里只做 agent 产品特有的部分，可以搭配使用：

- [RefoundAI/lenny-skills](https://github.com/RefoundAI/lenny-skills)：86 个 skill，内容来自 Lenny's Podcast。本仓库的命名跟它对齐。⚠️ 除 `agent-positioning` 外，每个 skill 在它那里都有一个同名的通用版，装在同一处会互相覆盖，请按话题二选一：做 agent 产品用本仓库的，其他产品用 Lenny 的。`agent-positioning` 是例外——它和 Lenny 的 `positioning` 回答的不是同一个问题（一个判市场站位，一个判产品形态），两个都装、先后使用。每个 skill 的「相关 skill」一节都写了对应的 Lenny 版本
- [phuryn/pm-skills](https://github.com/phuryn/pm-skills)：9 个插件，覆盖发现、策略、执行、上市与增长

## License

MIT
