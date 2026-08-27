---
title: Skills 中心与 SkillHub
tags: [AgentKit, Skills, SkillHub, Reuse]
source: S03
---

# Skills 中心与 SkillHub

## 定位

Skills 中心将可复用的 Agent 能力包装、管理、授权并分发到 Agent。它解决的是“开发一次、跨 Agent/跨业务复用”的问题；SkillHub 则面向更大范围的能力发现与共享。

## 能力模型

- **Skills 空间**：Skill 的组织、隔离和授权边界。
- **Skill**：包含名称、描述、版本、内容哈希、ZIP 包路径、执行要求和权限声明的能力单元。
- **版本与缓存**：会话启动拉取元数据；以内容哈希判断本地/沙箱缓存是否仍可使用。
- **执行路径**：可由远程 Skills Sandbox 执行，也可按配置落到 Agent 本地资源；高风险脚本应强制进入 Sandbox。

## 与 Runtime、Sandbox 的关系

1. Runtime 在初始化阶段向 Skills API 查询可用 Skill 元数据。
2. Runtime 仅向模型暴露名称和描述，避免完整 Skill 内容占满提示词。
3. Runtime 选择 Skill 后，由执行环境从对象存储下载 ZIP、校验版本并解析 `SKILL.md`。
4. Sandbox 在隔离边界内运行脚本和处理资产，返回受控结果。

## 治理要点

- Skill 发布应有作者、审批、版本、依赖和回滚信息。
- 元数据要包含执行模板、所需网络、所需存储、最大资源和敏感操作声明。
- 区分“可被模型发现”与“可被当前 Agent 调用”；二者都需要授权。
- 对有副作用的 Skill（写库、发消息、支付、外网下载）要求显式确认或策略审批。
