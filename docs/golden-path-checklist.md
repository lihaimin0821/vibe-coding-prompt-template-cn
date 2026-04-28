# 黄金路径集成检查清单

使用此检查清单验证端到端工作流程在每个步骤都生成了预期的文件。

## 步骤 1：深度研究

**输入：** 用户的想法描述 + `part1-deepresearch.md` 提示词
**输出：**
- [ ] `docs/research-[AppName].md` 存在（`.txt` 也可接受，兼容旧版本）
- [ ] 文档包含：市场分析、竞品分析、技术建议、MVP功能优先级排序

**交接给步骤 2：** 研究文档或活跃的聊天会话

## 步骤 2：产品需求文档（PRD）

**输入：** 研究输出 + `part2-prd-mvp.md` 提示词
**输出：**
- [ ] `docs/PRD-[AppName]-MVP.md` 存在
- [ ] 文档包含：产品概述、目标用户、必备功能、成功指标、设计方向

**交接给步骤 3：** PRD文档或活跃的聊天会话

## 步骤 3：技术设计

**输入：** PRD输出 + `part3-tech-design-mvp.md` 提示词
**输出：**
- [ ] `docs/TechDesign-[AppName]-MVP.md` 存在
- [ ] 文档包含：技术栈、项目结构、实施方法、部署计划、成本估算

**交接给步骤 4：** 技术设计文档

## 步骤 4：代理配置

**输入：** PRD + 技术设计 + `part4-notes-for-agent.md`
**输出：**
- [ ] 项目根目录存在 `AGENTS.md`
- [ ] 项目根目录存在 `MEMORY.md`
- [ ] 项目根目录存在 `REVIEW-CHECKLIST.md`
- [ ] `agent_docs/tech_stack.md` 存在且已填充内容
- [ ] `agent_docs/code_patterns.md` 存在且已填充内容
- [ ] `agent_docs/project_brief.md` 存在且已填充内容
- [ ] `agent_docs/product_requirements.md` 存在且已填充内容
- [ ] `agent_docs/testing.md` 存在且已填充内容
- [ ] 根据用户选择存在工具特定配置：
  - Claude Code: `CLAUDE.md`
  - Cursor: `.cursor/rules/` 或 `.cursorrules`
  - Gemini CLI: `GEMINI.md`
  - VS Code + Copilot: `.github/copilot-instructions.md`

**交接给步骤 5：** 项目根目录中的所有上述文件

## 步骤 5：构建 MVP

**输入：** 步骤 4 的所有输出 + 用户的编码环境
**预期行为：**
- [ ] 代理首先读取 `AGENTS.md`
- [ ] 代理在编码前提出第一阶段计划
- [ ] 代理一次构建一个功能
- [ ] 代理在每个功能完成后运行测试/验证
- [ ] 代理在取得进展后更新 `AGENTS.md` 的当前状态
- [ ] 代理遵循 `agent_docs/code_patterns.md` 中的模式

## 文件契约摘要

```
your-app/
├── docs/
│   ├── research-[AppName].md       ← 步骤 1 输出
│   ├── PRD-[AppName]-MVP.md        ← 步骤 2 输出
│   └── TechDesign-[AppName]-MVP.md ← 步骤 3 输出
├── AGENTS.md                       ← 步骤 4 输出（主计划）
├── MEMORY.md                       ← 步骤 4 输出（会话连续性）
├── REVIEW-CHECKLIST.md             ← 步骤 4 输出
├── agent_docs/                     ← 步骤 4 输出（详细文档）
│   ├── tech_stack.md
│   ├── code_patterns.md
│   ├── project_brief.md
│   ├── product_requirements.md
│   └── testing.md
├── [工具特定配置]                  ← 步骤 4 输出
├── specs/                          ← 步骤 5 期间创建（交接产物）
└── src/                            ← 步骤 5 期间创建（应用代码）
```

## Claude 技能发现检查

如果使用 Claude Code 技能，请验证：
- [ ] `/vibe-research` 能找到并读取 `docs/research-*.md`（或 `.txt`）
- [ ] `/vibe-prd` 能找到并读取 `docs/research-*.md`，并写入 `docs/PRD-*.md`
- [ ] `/vibe-techdesign` 能找到并读取 `docs/PRD-*.md`，并写入 `docs/TechDesign-*.md`
- [ ] `/vibe-agents` 能找到 `docs/PRD-*.md` 和 `docs/TechDesign-*.md`，并生成所有配置文件
- [ ] `/vibe-build` 能找到 `AGENTS.md` 和 `agent_docs/`，并开始构建循环
