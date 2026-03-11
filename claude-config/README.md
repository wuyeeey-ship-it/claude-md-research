# Claude Code 配置文件备份

> 2026-03-11 整理

## 目录结构

```
claude-config/
├── memory/              # 项目记忆
│   └── MEMORY.md       # 跨会话持久化记忆
├── rules/               # 开发规则
│   ├── coding-style.md      # 代码风格
│   ├── git-workflow.md      # Git 工作流
│   ├── testing.md           # 测试要求
│   ├── performance.md       # 性能优化
│   ├── patterns.md          # 设计模式
│   ├── hooks.md             # Hooks 系统
│   ├── development-workflow.md  # 开发流程
│   ├── agents.md            # Agent 协调
│   ├── claude.md            # AI 工作流
│   └── security.md          # 安全指南
├── skills/              # 技能文件
│   └── github-workflow.md  # GitHub 操作流程
├── agents/              # Agent 配置
│   ├── README.md
│   └── claude-md-guardian.md
├── settings.json        # Claude Code 设置
└── mcp.json             # MCP 服务器配置
```

## 使用方法

将文件复制到 `~/.claude/` 目录：

```bash
# 复制规则
cp -r rules/* ~/.claude/rules/common/

# 复制技能
cp -r skills/* ~/.claude/skills/

# 复制记忆
cp memory/MEMORY.md ~/.claude/projects/-Users-guanwang/memory/

# 复制设置 (可选)
cp settings.json ~/.claude/
cp mcp.json ~/.claude/
```

## 重要配置说明

### MEMORY.md
- 存储 Hummingbot 项目配置和启动命令
- Notion API Token 配置
- 跨会话持久化

### rules/common/
- 通用开发规则，适用于所有项目
- 包含 TDD、安全、Git 工作流等

### skills/github-workflow.md
- wuyeeey-ship-it 账号的 GitHub 操作流程
- 常用仓库列表和快速命令
