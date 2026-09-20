# deep-prd 迭代记录

不常驻。规则正文在 SKILL.md，这里只记「什么时候为什么改的」。

## 迭代记录

- 2026-07-07 立项。骨架实证自 `~/delphi-clone/docs/prd-memory-system.md`(分身记忆系统 PRD v4)——该 PRD 在四轮 owner 追加要求(决策全覆盖 / 直给研发 / 产品可读)下逼出了八段式 + 决策登记表 + 零推断实现卷 + 两层验收。§5 释疑与 §12 决策表确认为相对普通 PRD 的核心增量。
- 2026-07-07 定位深化。owner 点破真痛点:AI 时代 PRD 从「实现的输入」反转为「已完成实现的可转述表征」——AI 方案齐全但取舍/现状全在 AI 和代码里,PM 讲不清、转述不出。据此把**可转述性提为第一目标**,新增三机制:逆向萃取取舍 / 现状锚定(as-built) / 转述测试;流程加「第 0 步逆向审讯」。本 skill 明确为「大改动交付前 quiz」的持续文档版。
- 2026-07-07 调研补足(GitHub + 业界方法论)。对标 Amazon PR/FAQ、Shreyas Doshi、`vittobh/prd-templates`(AI-native)、Pendo/Product School。确认 deep-prd 已覆盖业界共识(问题开场/决策记录/零推断/两层验收);补三点:①**三方受众入口**(老板/产品/研发各有入口,§0 加 PR/FAQ 式「老板视角一段话」)②**AI 产品必答三问**(边界=模型不许做什么 / 人在环 / 校准≠正确,来自 vittobh,做 AI 功能必填)③**成功指标**(§10 补「上线后看什么数字」,来自 Doshi「PRD 常漏 metrics」)。
- 2026-07-17 owner 反馈补「可视化三件套」(用记忆系统 PRD v6→v7 实证):①§3 必配**架构图谱**(静态:组件/进程/表与边界,mermaid flowchart,身份/安全边界画成图上的「不存在的箭头」)+ **数据 flow**(动态:一次请求/一条数据的完整旅程,mermaid sequenceDiagram)——文字流程读三遍不如两张图各看一眼;②§6 DDL 外必加**字段词典**(逐字段:类型/含义与取值/谁写/谁读)——「谁写/谁读」两列是相对 DDL 注释的关键增量,数据血缘一表看穿,也是「防串桶」类隔离约束的可视化落点。另:产出默认配 artifact 阅读视图(md 落 docs/ 为事实源,artifact 渲染 mermaid;同一 PRD 迭代更新同一链接)。
- 2026-07-17(同日二迭)owner 反馈「artifact 里 mermaid 图不能放大查看」——宽图被压缩到不可读。修复固化为必带件:artifact 页面必须内联 `references/artifact-mermaid-zoom.html` 片段(pre.mermaid 点击 → lightbox,+/− 按钮 + 滚轮缩放 + 适应宽度 + Esc 关闭,纯 vanilla JS 过 CSP;角标提示「🔍 点击放大」)。以后每份 deep-prd artifact 出厂自带,不等 owner 再提。
