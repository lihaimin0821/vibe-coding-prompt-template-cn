# Claude Code 集成

此目录包含 Vibe-Coding 工作流程的 Claude Code 技能和钩子。

## 快速设置

### 选项 A：克隆仓库

```bash
# 克隆仓库
git clone https://github.com/KhazP/vibe-coding-prompt-template.git
cd vibe-coding-prompt-template

# 启动 Claude Code
claude
```

### 选项 B：使用 npx 安装独立技能

直接将需要的技能安装到任何项目中：

```bash
# 安装主协调器技能
npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-workflow

# 同时安装所有技能
npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-research
npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-prd
npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-techdesign
npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-agents
npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-build
```

> **浏览所有技能：** [skills.sh/khazp/vibe-coding-prompt-template](https://skills.sh/khazp/vibe-coding-prompt-template)

设置完成！技能会自动生效。

## 可用技能

| 命令 | 描述 | 时长 | npx 安装命令 |
|---------|-------------|------|-------------|
| `/vibe-workflow` | 从想法到 MVP 的完整引导工作流程 | 完整流程 | `npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-workflow` |
| `/vibe-research` | 深度研究和市场验证 | 20 分钟 | `npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-research` |
| `/vibe-prd` | 创建产品需求文档 | 15 分钟 | `npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-prd` |
| `/vibe-techdesign` | 规划技术架构 | 15 分钟 | `npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-techdesign` |
| `/vibe-agents` | 生成 AGENTS.md 和 AI 配置 | 10 分钟 | `npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-agents` |
| `/vibe-build` | 按照计划构建 MVP | 1-3 小时 | `npx skills add https://github.com/khazp/vibe-coding-prompt-template --skill vibe-build` |

## 技能详情

### /vibe-workflow

**主协调器** - 自动引导你完成全部 5 个步骤。

```
> /vibe-workflow
```

或者直接说："帮我构建一个 MVP"

此技能将：
1. 检查你的当前进度
2. 确定你处于哪个步骤
3. 引导你完成剩余步骤
4. 跨会话跟踪完成情况

### /vibe-research

**市场研究和想法验证**

触发条件：
- "研究我的想法"
- "验证我的应用"
- "帮我开始一个新项目"

问题会根据你的经验水平进行调整：
- **Vibe-coder**：简单、友好的问题
- **开发者**：技术性、详细的问题
- **中间级别**：平衡的方法

输出：`docs/research-[应用名称].md`

### /vibe-prd

**产品需求文档生成器**

触发条件：
- "创建 PRD"
- "定义我的产品"
- "编写需求"

创建全面的 PRD，包含：
- 产品概述和目标
- 用户画像和用户旅程
- 功能优先级（MoSCoW 方法）
- 成功指标
- 设计方向

输出：`docs/PRD-[应用名称]-MVP.md`

### /vibe-techdesign

**技术架构规划**

触发条件：
- "规划技术设计"
- "选择技术栈"
- "我应该怎么构建这个"

帮助你决定：
- 平台（网页、移动端、桌面端）
- 技术栈及备选方案
- 架构模式
- 部署策略
- 成本估算

输出：`docs/TechDesign-[应用名称]-MVP.md`

### /vibe-agents

**AI 配置生成器**

触发条件：
- "创建 AGENTS.md"
- "配置 AI 助手"
- "生成代理文件"

创建：
- `AGENTS.md` - 主构建计划
- `agent_docs/` - 详细规格说明
- 工具特定配置（CLAUDE.md、GEMINI.md、`.cursor/rules/` 或旧版 `.cursorrules` 等）

### /vibe-build

**MVP 构建器**

触发条件：
- "构建我的 MVP"
- "开始编码"
- "实现项目"

遵循计划 → 执行 → 验证工作流程：
1. 读取 AGENTS.md 获取当前阶段
2. 提出实施计划
3. 一次构建一个功能
4. 每个功能后进行测试
5. 在 AGENTS.md 中更新进度

## 预配置的钩子

此项目包含自动运行的钩子：

### PreToolUse 钩子

**文件保护** - 阻止意外修改：
- `.env` 文件（密钥）
- `package-lock.json`（使用 npm）
- `.git/` 目录

### PostToolUse 钩子

**自动格式化** - 文件编辑后：
- 对 `.ts`、`.tsx`、`.js`、`.jsx` 文件运行 Prettier（仅当 `node_modules/.bin/prettier` 存在时）

### Stop 钩子

**Git 状态** - Claude 结束时：
- 运行 `git status --porcelain` 并打印修改的文件
- 提醒你在提交前检查变更
- 如果工作区干净则显示"没有未提交的更改"

## 钩子配置

钩子定义在 `.claude/hooks/hooks.json` 中。自定义方式：

```json
{
  "hooks": {
    "PreToolUse": [...],
    "PostToolUse": [...],
    "Stop": [...]
  }
}
```

### 禁用钩子

临时禁用所有钩子：
```bash
claude --no-hooks
```

要禁用特定钩子，编辑 `hooks.json` 并删除钩子条目。

## 目录结构

```
.claude/
├── README.md              # 本文件
├── hooks/
│   └── hooks.json         # 自动钩子配置
└── skills/
    ├── vibe-research/
    │   └── SKILL.md
    ├── vibe-prd/
    │   └── SKILL.md
    ├── vibe-techdesign/
    │   └── SKILL.md
    ├── vibe-agents/
    │   └── SKILL.md
    ├── vibe-build/
    │   └── SKILL.md
    └── vibe-workflow/
        └── SKILL.md
```

## 自定义技能

技能是带有 YAML 前置元数据的 Markdown 文件。修改技能：

1. 打开技能的 `SKILL.md` 文件
2. 编辑前置元数据（名称、描述、工具）
3. 编辑前置元数据下方的说明
4. 更改会立即生效

### 技能前置元数据选项

```yaml
---
name: skill-name
description: 何时使用此技能
allowed-tools: Read, Write, Bash  # 限制可用工具
model: sonnet  # 可选：sonnet、opus、haiku
---
```

## 故障排除

### 首先要确保会话连续性

如果你的构建开始偏离方向，避免打开新的空白聊天。用以下方式重新锚定：

1. `AGENTS.md` 当前阶段
2. 最后完成的任务
3. 待处理任务的简短摘要

### 技能不显示

1. 检查你位于项目目录中
2. 运行 `claude --debug` 查看加载错误
3. 验证 SKILL.md 文件有有效的 YAML 前置元数据

### 钩子不运行

1. 检查 `.claude/hooks/hooks.json` 存在
2. 验证 JSON 语法有效
3. 检查钩子脚本可执行

### 技能不触发

技能的 `description` 决定了何时触发。包含用户自然会说出的关键词：
- 正确："当用户说'创建 PRD'或'定义产品需求'时使用"
- 错误："PRD 生成工具"

### 插件/规则故障排除

如果使用启用插件的 IDE 工作流程：

1. 确认插件/规则包已加载
2. 确认所需工具已启用
3. 使用明确指令重试："先读取 AGENTS.md，然后再继续"

### 模型命名指导

在文档和示例中优先使用模型系列名称（Claude Sonnet、Claude Opus、Gemini Pro、Gemini Flash），以减少因提供商版本更新带来的变动。

## 贡献

添加新技能：

1. 创建目录：`.claude/skills/your-skill/`
2. 添加带有前置元数据和说明的 `SKILL.md`
3. 用 `/your-skill` 测试
4. 提交 PR

## 资源

- [Claude Code 技能文档](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Claude Code 钩子文档](https://docs.anthropic.com/en/docs/claude-code/hooks)
- [Vibe-Coding 工作流程指南](../README.md)