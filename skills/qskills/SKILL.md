# Qskills - AI 技能管理工具

## 概述

Qskills 是一款面向个人开发者的 CLI 技能管理工具，支持多 AI 编程助手的技能、知识库、Agent 配置的统一管理与多源同步。

## 核心能力

### 多环境支持
- **claude** - Claude Code (Anthropic)
- **cursor** - Cursor AI 编辑器
- **qwen** - 通义灵码 (阿里云)
- **codex** - OpenAI Codex
- **codebuddy** - CodeBuddy Code (腾讯)
- **common** - 跨环境通用资源

### 资源管理
- 技能脚本管理 (add/list/remove/copy)
- 知识库管理 (document/code-snippet/template/note)
- Agent 配置管理
- Git 多源同步 (public/private)

## 安装与初始化

```bash
# 使用 npx 直接运行
npx qskills config init

# 或全局安装
npm install -g qskills
qskills config init
```

## 常用命令

### 技能管理 (skill / s)

```bash
# 添加技能到指定环境
qskills s add ./my-skill.js -n my-skill -e claude

# 添加技能到所有环境
qskills s add ./my-skill.js -n my-skill --all

# 列出技能
qskills s list
qskills s ls --env cursor

# 删除技能
qskills s remove skill-name

# 在环境间复制技能
qskills s copy skill-name --from claude --to cursor

# 查看可用环境
qskills s envs
```

### 知识库管理 (knowledge / k)

```bash
# 添加知识条目
qskills k add ./doc.md -t "API文档" --type document -c api

# 列出知识
qskills k list --type document

# 删除知识
qskills k remove <id>
```

### Agent 管理 (agent / a)

```bash
# 添加 Agent 配置
qskills a add ./agent-config/ -n code-reviewer -e claude

# 列出 Agent
qskills a list

# 删除 Agent
qskills a remove agent-name
```

### 同步功能

```bash
# 同步到远程仓库
qskills sync

# 只同步公共仓库
qskills sync --source public
```

## 配置文件

配置文件位于 `~/.qcli/config.json`

```json
{
  "version": "1.0.0",
  "initialized": true,
  "storage": {
    "baseDir": "~/.qcli/data",
    "skillsDir": "skills",
    "knowledgeDir": "knowledge",
    "agentsDir": "agents"
  },
  "environments": {
    "enabled": ["claude", "cursor", "qwen", "codex", "codebuddy", "common"],
    "default": "common"
  }
}
```

## 存储结构

```
~/.qcli/
├── config.json              # 配置文件
├── data/
│   ├── index.json           # 本地索引
│   ├── skills/              # 技能存储
│   │   ├── claude/
│   │   ├── cursor/
│   │   └── ...
│   ├── knowledge/           # 知识库
│   └── agents/              # Agent 配置
├── public-repo/             # 公共仓库克隆
└── private-repo/            # 私人仓库克隆
```

## 安全特性

- 自动扫描敏感信息（API Key、Token、私钥等）
- 支持跳过扫描（--skip-scan）
- 推送前安全检查

## 使用场景

1. **多设备同步** - 在不同设备间同步技能和知识库
2. **多工具管理** - 统一管理多个 AI 编程助手的配置
3. **技能共享** - 通过 Git 仓库共享公共技能
4. **知识积累** - 构建个人知识库，方便查阅和复用

## 相关链接

- GitHub: https://github.com/hlrlive/Qskills
- npm: https://www.npmjs.com/package/qskills
