# 更新日志

本文档记录了Vibe-Coding Prompt Template的所有重要更改。

## [未发布] - 2026年3月 — Agent时代2.0版

本次重大更新将仓库从"基于聊天的提示生成"转变为**产物优先记忆**和**多Agent编排**，反映了2026年2月和3月的大规模工具更新（Cursor云Agent、Claude Agent团队和Copilot自定义Agent）。

### 新增
- **产物优先记忆：** 引入 `MEMORY.md` 和 `spec.md` 概念，以防止长时间编码会话中的上下文窗口过载。
- **Claude Agent团队指南：** 添加了 `docs/claude-agent-teams.md`，涵盖并行子Agent和团队负责人审批流程。
- **Cursor云Agent指南：** 添加了 `docs/cursor-cloud-agents.md`，聚焦动态上下文发现和以文件为中心的记忆。
- **可视化README循环：** 为执行→验证工作流提供现代化的 `╭──╮` 循环图。

### 更改
- **README重新设计：** 用可折叠的 `<details open>`、目录和更快的5步快速开始重新设计了主README。
- **工具矩阵：** 更新了工具推荐矩阵，清晰区分原型工具（Lovable）和生产工具（v0），并突出多Agent能力。
- **第4部分提示（`part4-notes-for-agent.md`）：** 用2026 Agentic Boilerplate约定替换了遗留的提示结构，包括明确的禁止目录和严格的TypeScript指南。

### 移除
- **MCP支持指南：** 移除了 `mcp-support.md`，因为标准工具现在原生处理上下文检索要好得多，将重点转向原生插件工作流和Agent团队。