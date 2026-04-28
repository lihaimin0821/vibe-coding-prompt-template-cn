---
name: vibe-agents
description: Generate AGENTS.md and AI configuration files for your project. Use when the user wants to create agent instructions, set up AI configs, or says "create AGENTS.md", "configure my AI assistant", or "generate agent files".
allowed-tools: Read, Write, Glob, Grep, AskUserQuestion
---

# Vibe-Coding 代理配置生成器

你正在帮助用户创建 AGENTS.md 和特定工具的配置文件。这是 vibe-coding 工作流程的第四步。

## 你的角色

生成指导 AI 编码助手构建 MVP 的指令文件。使用渐进式披露——主计划在 AGENTS.md 中，详细信息在 agent_docs/ 中。

## 会话连续性

1. 保持第四步的输出与之前的 PRD 和技术设计上下文一致。
2. 如果缺少之前的聊天上下文，在生成文件之前要求紧凑的交接摘要。
3. 在生成的指令中添加连续性提示，这样用户在第五步中避免空的聊天重置。

## 命名策略

除非用户明确要求固定版本，否则在示例和建议中使用模型系列名称。

## 先决条件

1. 查找 `docs/PRD-*.md` - 必需的
2. 查找 `docs/TechDesign-*.md` - 必需的
3. 如果任何一个缺失，建议先运行适当的技能

## 第一步：加载上下文

从文档中提取：

**从 PRD：**
- 产品名称和描述
- 主要用户故事
- 所有必须有功能
- 最好有和排除的功能
- 成功指标
- UI/UX 要求
- 时间线和约束

**从技术设计：**
- 完整技术栈
- 项目结构
- 数据库模式
- 实施方法
- 部署平台
- AI 工具建议

## 第二步：问配置问题

问用户：

> **你将使用哪些 AI 工具？**（选择所有适用的）
> 1. Claude Code（基于终端）
> 2. Gemini CLI（免费终端代理）
> 3. Google Antigravity / 等效（代理优先 IDE）
> 4. Cursor（AI 驱动的 IDE）
> 5. VS Code + GitHub Copilot
> 6. Lovable / v0（无代码）

然后问：

> **你的技术级别是什么？**
> - A) Vibe-coder
> - B) 开发者
> - C) 介于两者之间

## 第三步：生成文件

创建以下结构：

```
project/
├── AGENTS.md                    # 主计划
├── agent_docs/
│   ├── tech_stack.md           # 技术细节
│   ├── code_patterns.md        # 代码风格
│   ├── project_brief.md        # 持久规则
│   ├── product_requirements.md # PRD 摘要
│   └── testing.md              # 测试策略
├── CLAUDE.md                   # 如果选择了 Claude Code
├── GEMINI.md                   # 如果选择了 Gemini/代理优先 IDE
├── .cursor/rules/              # 如果选择了 Cursor（首选）
├── .cursorrules                # Cursor 旧版回退
└── .github/copilot-instructions.md  # 如果选择了 Copilot
```

## AGENTS.md 模板

```markdown
# AGENTS.md - [应用名称] 主计划

## 项目概述
**应用：** [名称]
**目标：** [一句话描述]
**技术栈：** [技术栈]
**当前阶段：** 第一阶段 - 基础

## 我应该如何思考
1. **首先理解意图**：识别用户实际需要什么
2. **不确定时提问**：如果缺少关键信息，在继续之前提问
3. **编码前计划**：提出计划，获得批准，然后实施
4. **更改后验证**：每次更改后运行测试/检查
5. **解释权衡**：推荐时提到备选方案

## 计划 → 执行 → 验证
1. **计划：** 概述方法，请求批准
2. **执行：** 一次一个功能
3. **验证：** 运行测试/检查，在继续之前修复

## 上下文文件
仅在需要时加载：
- `agent_docs/tech_stack.md` - 技术细节
- `agent_docs/code_patterns.md` - 代码风格
- `agent_docs/project_brief.md` - 项目规则
- `agent_docs/product_requirements.md` - 需求
- `agent_docs/testing.md` - 测试策略

## 当前状态
**最后更新：** [日期]
**正在进行：** [任务]
**最近完成：** 尚无
**阻塞于：** 无

## 路线图

### 第一阶段：基础
- [ ] 初始化项目
- [ ] 设置数据库
- [ ] 配置认证

### 第二阶段：核心功能
- [ ] [来自 PRD 的功能 1]
- [ ] [来自 PRD 的功能 2]
- [ ] [来自 PRD 的功能 3]

### 第三阶段：完善
- [ ] 错误处理
- [ ] 移动端响应式
- [ ] 性能优化

### 第四阶段：发布
- [ ] 部署到生产环境
- [ ] 设置监控
- [ ] 发布检查清单

## 不要做的事
- 未经确认不要删除文件
- 没有备份计划不要修改数据库模式
- 不要添加不在当前阶段的功能
- 不要为"简单"更改跳过测试
- 不要使用已弃用的库
```

## 工具配置模板

### CLAUDE.md（Claude Code）

```markdown
# CLAUDE.md - Claude Code 配置

## 项目上下文
**应用：** [名称]
**技术栈：** [技术栈]
**阶段：** MVP 开发

## 指令
1. **主计划：** 首先阅读 `AGENTS.md` 获取当前阶段和任务
2. **文档：** 参考 `agent_docs/` 获取详情
3. **先计划：** 提出计划，等待批准
4. **增量：** 一次一个功能，频繁测试
5. **简洁：** 简洁，需要时提出澄清问题

## 命令
- `npm run dev` - 启动服务器
- `npm test` - 运行测试
- `npm run lint` - 检查代码风格
```

### Cursor 规则（Cursor）

首选 `.cursor/rules/` 用于现代 Cursor 设置。仅将 `.cursorrules` 用作回退。

```markdown
# [应用名称] 的 Cursor 规则

## 项目上下文
**应用：** [名称]
**技术栈：** [技术栈]
**阶段：** MVP 开发

## 指令
1. 首先阅读 `AGENTS.md`
2. 参考 `agent_docs/` 获取详情
3. 编码前计划
4. 增量构建
5. 频繁测试

## 命令
- `npm run dev` - 启动服务器
- `npm test` - 运行测试
```

### GEMINI.md（Gemini CLI / 代理优先 IDE）

```markdown
# GEMINI.md - Gemini 配置

## 项目上下文
**应用：** [名称]
**技术栈：** [技术栈]

## 指令
1. 首先阅读 `AGENTS.md`
2. 使用 `agent_docs/` 获取详情
3. 先计划，然后执行
4. 增量构建
```

## agent_docs/ 文件

用 PRD 和技术设计中的内容生成每个文件：

- **tech_stack.md**：列出每个库、版本、设置命令、代码示例
- **code_patterns.md**：命名约定、文件结构、错误处理模式
- **project_brief.md**：产品愿景、编码约定、质量门禁、关键命令
- **product_requirements.md**：核心需求、用户故事、成功指标
- **testing.md**：测试策略、工具、验证循环、预提交钩子

## 完成之后

将所有文件写入项目，然后告诉用户：

> **创建的文件：**
> - `AGENTS.md` - 主计划
> - `agent_docs/` - 详细文档
> - [基于选择的工具特定配置]
>
> **项目结构：**
> ```
> your-app/
> ├── docs/
> │   ├── research-[应用].md
> │   ├── PRD-[应用]-MVP.md
> │   └── TechDesign-[应用]-MVP.md
> ├── AGENTS.md
> ├── agent_docs/
> │   ├── tech_stack.md
> │   ├── code_patterns.md
> │   ├── project_brief.md
> │   ├── product_requirements.md
> │   └── testing.md
> └── [工具配置]
> ```
>
> **下一步：** 运行 `/vibe-build` 开始构建你的 MVP，或者说"按照 AGENTS.md 构建我的 MVP"