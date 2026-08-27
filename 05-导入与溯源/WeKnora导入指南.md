---
title: WeKnora 导入指南
tags: [WeKnora, Import, Knowledge-Base]
---

# WeKnora 导入指南

## 推荐导入批次

| 批次 | 路径 | 目的 | 推荐标签 |
| --- | --- | --- | --- |
| 1 | `00-导航/`、`01-项目综述/`、`02-架构与关系/` | 先建立项目语义、导航与核心关系 | AgentKit, Agent-Infra, Architecture |
| 2 | `03-核心能力/` | 建立面向技术问答的专题索引 | Sandbox, Runtime, Skills, MCP, Memory, RAG |
| 3 | `04-治理与落地/`、`05-导入与溯源/` | 支撑风险、实施、验收和资料追溯 | Security, Governance, Evidence |
| 4 | `sources/` | 保存原文证据与图表/截图 | Source, Original |

## 为什么 Markdown 优先

- 每篇文档只覆盖一个清晰主题，利于分块和召回。
- 文件名按能力和阅读顺序组织，便于整目录导入。
- YAML Front Matter 保留标题、标签与来源，无法识别时也不会影响正文检索。
- 原始 PDF、HTML 和截图独立保留，适合在需要原图、原表或细节时回溯。

## 建议生成的 FAQ

1. 星源 AgentKit 的目标客户、核心痛点与差异化是什么？
2. Agent Runtime、Sandbox、MCP、Skills 的职责边界是什么？
3. 为什么 Agent Runtime 是与 Agent Infra 关联度最大的模块？
4. Sandbox 如何处理代码、浏览器、Skill、存储和网络安全？
5. Skills 的按需下载、缓存与版本失效如何工作？
6. MCP 与 Sandbox 的区别及协作方式是什么？
7. 记忆库与知识库分别承担什么角色？
8. 如何将 Trace、评测、成本和安全事件形成闭环？

## 导入后验证问题

- 检索“沙箱如何处理 Skill 执行”，应同时命中 Sandbox 和 Skills 文档。
- 检索“Agent Infra”，应优先命中 Agent-Infra 关联度分析与 Runtime 文档。
- 检索“数据不出域/安全隔离”，应命中项目立项摘要、Sandbox 和治理文档。
- 检索“OpenClaw Mem0”，应命中项目立项摘要、Runtime 和记忆库文档。

## 资料更新流程

1. 将新原始资料放入 `sources/` 并在资料清单登记。
2. 更新受影响的专题 Markdown，标注来源事实和分析判断。
3. 检查链接、标签、术语和重复内容。
4. 提交 Git 后，在 WeKnora 触发增量导入或重新解析对应目录。
