# agent-pm-skills

[English](README.md) · [中文](README.zh-CN.md)

给做 agent 产品的人用的 skill 集。**一个 skill 一个概念**，学 [@mattpocock 的 skills](https://github.com/mattpocock/skills)
风格——小、单一职责、彼此互引。

内容来自拆解四个已上线产品（两个独立来源），只保留了在真实产品线上经得起用的部分。

## 三个 skill

| Skill | 回答什么 |
|---|---|
| **agent-positioning**（定位分析） | 它是岗位还是能力包？任务是什么形状？该翻哪几格？ |
| **agent-job-design**（岗位设计） | 六栏岗位说明书、三道闸、standing order 运行时 |
| **agent-north-star**（北极星指标） | 什么算成了？翻了判断权之后哪些指标作废了？ |

三者成链：定位决定做多深，设计把它建出来，指标量它成没成。

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

```bash
git clone https://github.com/libaoming/agent-pm-skills.git
cd agent-pm-skills && ./install.sh
```

会把每个 skill 软链进 `~/.claude/skills/`，之后 `git pull` 就能一起更新。

## 结构

```
agent-positioning/     SKILL.md · DIALS.md · CASES.md · DIAGNOSE.md
agent-job-design/      SKILL.md · JOB-SPEC.md · GATES.md · MECHANICS.md
agent-north-star/      SKILL.md
```

## 来源

四个已上线产品，两个独立来源：

- **Claude Code / Cowork / Claude Tag** —— Anthropic 官方分享与帮助中心文档
- **Grok Bot** —— 对一个已上线常驻 agent 产品的源码级拆解

只取机制、架构与设计思路。不复制任何产品的代码与 prompt 原文；文中措辞为转述，
仅在「原话本身就是发现」处保留短引用。

## License

MIT
