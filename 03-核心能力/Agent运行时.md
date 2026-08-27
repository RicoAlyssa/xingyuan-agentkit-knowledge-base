---
title: Agent 运行时 AgentEngine
tags: [AgentKit, AgentEngine, Runtime, Agent-Infra]
source: [S01, S03]
---

# Agent 运行时 AgentEngine

## 定位

AgentEngine 是平台的运行时中枢，承接 Agent 的开发、部署、运行、资源调度和运行监控。立项路线图中，CLI/SDK、运行时控制台与 OpenClaw 部署能力在 2026 Q1 出现，后续规划扩展资源与事件监控、资源切换、Mem0 和 Skills 接入。

## 核心职责

- 为应用开发者提供 CLI/SDK 和入口契约，封装运行环境与部署操作。
- 管理 Agent 的版本、实例生命周期、会话、资源规格和底层资源选择。
- 在运行中编排模型、MCP、Skills、Sandbox、记忆库和知识库。
- 向可观测/评测层发送 Trace、运行事件、资源指标和结果。
- 与 Serverless/云资源计费链路关联，支持按部署和运行消耗归因。

## 典型执行闭环

`请求接入 → 会话/身份解析 → 检索记忆与知识 → 模型规划 → 调用 MCP 或 Sandbox/Skill → 汇总结果 → Trace 与评测 → 返回响应`

## 与 OpenClaw 的关系

材料显示控制台支持部署 OpenClaw，并规划对接 Mem0、内网 SkillHub。可将 OpenClaw 视为运行在 AgentEngine 承载面的 Agent 应用/框架适配对象；Runtime 负责部署与运营治理，OpenClaw 负责其自身的 Agent 执行逻辑。

## 关键非功能要求

- 多租户身份和资源隔离。
- 部署版本可回滚、可灰度、可追溯。
- 实例/会话/工具调用链路可关联 Trace。
- 上游模型和下游工具故障时提供明确降级与错误分类。
- 云函数、容器或其他底层资源切换不改变应用侧入口契约。
