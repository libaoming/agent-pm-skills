# agent-delegation

[English](README.md) · [中文](README.zh-CN.md)

一个 Claude Code skill，用**委托**这一个框架设计和诊断 agent 产品。

多数「AI 员工」产品是挂着岗位名的能力包：它会干这个活，但没人对这个活负责。
这个 skill 给你区分两者的判据，以及把前者变成后者的六栏说明书。

## 核心论断

**通用委托不存在——委托只能针对具体岗位。** 一个能力很强却没有岗位的 agent，
你说什么它做什么，你不说它就停。

```
它能做多深      = 判断权 × 记忆
你敢让它做多深  = 判断权 × 记忆 × 可审计性
```

判断权与记忆是一对耦合项。只翻判断权，它会主动做事却学不会你的规矩——同一个错犯一百遍；
只翻记忆，它很懂你，但你不打开它就一次都不动。

## 判据

**容器带不带自己的记忆和判断权？**

| | 容器 | 自己的记忆 | 判断权 | 判定 |
|---|---|---|---|---|
| Grok Bot | Bot | 有 | 有 | **岗位** |
| Claude Tag | Slack 频道 | 有 | 有 | **岗位** |
| Cowork | plugin | 无 | 无 | 能力包 |

不看名字，只查这两样——GPT、agent、助手、智能体、数字员工，一律适用。

## 它能做什么

| 你要 | 它给你 |
|---|---|
| 设计一个新的 AI 岗位 | 六栏岗位说明书，按序填；其中两栏决定其余是否成立 |
| 诊断「没人依赖」的 agent | 按依赖顺序检查五个位置，以及误诊为何会让修法倒退 |
| 实现一个常驻 agent | standing order 运行时：唤醒 prompt 约束、两个判断点、五条持久化路径 |
| 设计闸门 | 授权闸 / 执行闸 / 写入闸，以及闸门为什么花掉委托 |
| 对照已上线产品 | 四个产品、三个层次、两个独立来源 |

## 安装

```bash
git clone https://github.com/libaoming/agent-delegation.git ~/.claude/skills/agent-delegation
```

之后正常提问即可——设计 AI 员工、要不要给 agent 判断权、为什么这个 agent 只是自动化脚本，
它会自己加载。

## 结构

```
SKILL.md                  框架：任务形状、三格尺、岗位/能力包判据
references/
  dials.md                落点、在场、判断权 × 记忆——完整版
  job-spec.md             六栏说明书，以及谁承担岗位定义成本
  gates.md                三道闸、四判据、治理入口
  mechanics.md            standing order、唤醒 prompt、运行时 flow
  diagnose.md             五个位置，以及怎么读 outcome 数字
  cases.md                四产品 × 三层对照
```

## 来源

建立在四个已上线产品之上，两个独立来源：

- **Claude Code / Cowork / Claude Tag** —— Anthropic 官方分享与帮助中心文档。
- **Grok Bot** —— 对一个已上线常驻 agent 产品的源码级拆解。

只取机制、架构与设计思路。不复制任何产品的代码与 prompt 原文；文中措辞为转述，
仅在「原话本身就是发现」处保留短引用。

## License

MIT
