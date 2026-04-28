# Vibe-Coding 工作流模板

<p align="center">
  <img src="https://img.shields.io/badge/Vibe--Coding-Workflow-blueviolet?style=for-the-badge&logo=rocket&logoColor=white" alt="Vibe-Coding Workflow" height="40"/>
  <img src="https://img.shields.io/badge/中文版本-本地化-green?style=for-the-badge" alt="中文版本"/>
</p>

<h3 align="center">一个实用的 AI 工作流程，用于快速交付 MVP</h3>

<p align="center">
  <strong>通过结构化提示词、Agent 文档和 AI 辅助编码工作流程，将想法转化为 MVP。</strong>
</p>

<p align="center">
  <strong>⭐ 已针对 Trae Solo CN 优化 — 开箱即用！</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg?style=flat-square" alt="MIT License"/></a>
  <img src="https://img.shields.io/badge/Trae-字节跳动-4285F4?style=flat-square" alt="Trae"/>
  <img src="https://img.shields.io/badge/Claude-Anthropic-orange?style=flat-square" alt="Claude"/>
  <img src="https://img.shields.io/badge/Android-Kotlin-3DDC84?style=flat-square&logo=android" alt="Android"/>
</p>

---

## 目录

- [项目简介](#项目简介)
- [快速开始](#快速开始)
- [工作流程](#工作流程)
- [文件结构](#文件结构)
- [使用示例](#使用示例)
- [故障排除](#故障排除)

---

## 项目简介

这是一个**中文本地化**的 Vibe-Coding 工作流模板，专为已有明确开发需求的团队和个人设计。

### 核心特点

- **跳过市场调研** — 直接从需求到代码
- **Trae Solo CN 优化** — 开箱即用的国产 AI IDE 支持
- **多平台支持** — Web 前端 + Android 移动端
- **可移植设计** — `vibe-coding/` 文件夹可复制到任何项目

### 工作流程

```
💡 需求 ──► 📋 PRD ──► 🏗️ 技术设计 ──► 🤖 Agent配置 ──► 🚀 构建
```

### 支持的平台

| 平台 | 技术栈 |
|------|--------|
| Web 前端 | React / Vue / Next.js / Nuxt |
| Android | Kotlin + Jetpack Compose |
| 后端服务 | Node.js / FastAPI / Spring Boot |

---

## 快速开始

### 方式一：使用 Trae Solo CN（推荐）

1. 在 Trae 中打开本项目
2. 对 AI 说：

```
@agent 读取 vibe-coding/START.md，我已经有明确的需求，直接开始
```

3. AI 自动完成：
   - 询问 4 个问题确认需求
   - 生成 PRD 和技术设计文档
   - 复制模板文件到项目根目录
   - 开始构建 MVP

### 方式二：使用 vibe-coding/ 文件夹

将 `vibe-coding/` 文件夹复制到你的项目中，然后：

```
@agent 读取 vibe-coding/START.md，直接开始
```

---

## 工作流程

### 阶段说明

| 阶段 | 时间 | 说明 |
|------|------|------|
| 需求确认 | 5分钟 | 你描述功能，AI 整理 |
| PRD 生成 | 5分钟 | 明确功能范围和优先级 |
| 技术设计 | 5分钟 | 确定技术栈和架构 |
| Agent 配置 | 1分钟 | 生成编码指令 |
| 构建 | 开始 | 计划→执行→验证循环 |

### AI 询问的问题

1. "请描述你的项目需求，包括核心功能"
2. "列出必须有的 3 个核心功能"
3. "你偏好什么技术栈？"
4. "你的项目类型是什么？"

### 开发循环

```
╭──────────────╮      ╭──────────────╮      ╭──────────────╮
│   📝 计划    │ ───>│  ⚡ 执行  │ ───>│  🔍 验证  │
│  （审批）    │      │  （一个功能） │      │   （测试）   │
╰──────────────╯      ╰──────────────╯      ╰──────────────╯
       ▲                                           │
       └───────────────────────────────────────────┘
```

---

## 文件结构

```
vibe-coding-prompt-template-cn/
├── vibe-coding/                      # ⭐ 可移植的工作流模板
│   ├── START.md                      # 工作流入口
│   ├── README.md                     # 使用说明
│   ├── TRAE.md                       # Trae 配置
│   ├── templates/                    # Agent 配置模板
│   │   ├── AGENTS.md                # 主配置文件
│   │   ├── MEMORY.md                # 会话记忆
│   │   └── REVIEW-CHECKLIST.md      # 审查清单
│   ├── agent_docs/                   # Agent 知识库
│   │   ├── product_requirements.md  # 产品需求
│   │   ├── tech_stack.md            # 技术栈（Web + Android）
│   │   ├── code_patterns.md         # 代码规范
│   │   └── testing.md               # 测试策略
│   └── .trae/rules/
│       └── vibe-coding.md           # Trae 规则
│
├── templates/                        # 原始模板（完整版）
├── docs/                             # 详细文档
├── .claude/                          # Claude Code Skills
└── START.md                          # 简化版入口
```

### 生成的配置文件

使用后，AI 会在你的项目中生成：

```
your-project/
├── docs/
│   ├── PRD-[项目名]-MVP.md          # 产品需求文档
│   └── TechDesign-[项目名]-MVP.md   # 技术设计文档
├── agent_docs/                       # Agent 知识库
│   ├── product_requirements.md
│   ├── tech_stack.md
│   ├── code_patterns.md
│   └── testing.md
├── AGENTS.md                        # 主配置
├── MEMORY.md                        # 进度记录
└── REVIEW-CHECKLIST.md              # 审查清单
```

---

## 使用示例

### 示例 1：Web 前端项目

**你说：** "我想做一个待办事项 Web 应用，功能是添加、删除、完成待办项"

**AI 问：**
1. "需要登录功能吗？"
2. "数据存哪里？（本地/云端）"
3. "技术栈偏好？"
4. "需要后端吗？"

**AI 生成：** PRD、技术设计、Agent 配置 → 立即使用 React + TypeScript 开始构建

### 示例 2：Android 项目

**你说：** "我想做一个记账 Android 应用，可以记录收支、查看统计"

**AI 问：**
1. "需要登录/云同步吗？"
2. "有预算分类吗？"
3. "UI 风格偏好？Material Design 3？"
4. "数据存本地还是云端？"

**AI 生成：** PRD、技术设计、Agent 配置 → 立即使用 Kotlin + Jetpack Compose + Room 开始构建

---

## 故障排除

| 情况 | 命令 |
|------|------|
| AI 做多余调研 | "跳过调研，直接进入 PRD" |
| 过于复杂 | "简化方案，MVP 最简方式是什么？" |
| 进度不明 | "显示当前进度" |
| 不满意结果 | "调整 [功能]，重新生成" |

---

## 常见命令

| 命令 | 说明 |
|------|------|
| "读取 START.md，直接开始" | 从需求开始完整流程 |
| "提议第一个功能的实现计划" | 开始构建阶段 |
| "显示当前进度" | 查看 MEMORY.md |
| "下一个功能是什么？" | 继续开发 |
| "运行测试" | 执行测试 |
| "更新 MEMORY.md" | 记录当前状态 |

---

## 工具推荐

| 场景 | 推荐工具 |
|------|----------|
| **AI 原生 IDE** | Trae Solo CN（国产，免费） |
| **快速原型** | Lovable、v0 |
| **复杂逻辑/多 Agent** | Claude Code |
| **预算有限** | Gemini CLI + VS Code |

---

## 许可

根据 [MIT 许可](LICENSE) 发布。

---

<p align="center">
  <strong>⭐ 欢迎使用！直接告诉 AI 你的需求，开始构建你的 MVP。</strong>
</p>