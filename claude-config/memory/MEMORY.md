# 用户偏好和项目记忆

## Hummingbot 项目

### ⚠️ 重要规则
**每次运行 Hummingbot 必须参考 `~/.openclaw/workspace/hummingbot/CLAUDE.md`**

### 项目文档位置
```
~/.openclaw/workspace/hummingbot/
├── CLAUDE.md                    # 主开发指南 (必读)
└── doc/
    ├── hummingbot-startup-guide.md
    └── MAC_STRATEGY_TEST_PLAN.md
```

### 一键启动
```bash
cd ~/.openclaw/workspace/hummingbot && /Users/guanwang/miniconda3/envs/hummingbot/bin/python ./bin/hummingbot_quickstart.py
```

### 密码
`1234`

### 已连接交易所
- okx_perpetual ✅

### Claude 自动化命令
```bash
tmux send-keys -t hummingbot "命令" Enter
tmux capture-pane -t hummingbot -p
```

### tmux 使用规则

**当使用 tmux 启动 Hummingbot 后，必须自动打开新终端窗口供用户观察：**
```bash
osascript <<EOF
tell application "Terminal"
    activate
    do script "tmux attach -t hummingbot"
end tell
EOF
```

**提醒用户 tmux 快捷键：**
- `Ctrl+B` 然后 `D` - 退出但保持运行
- `Ctrl+B` 然后 `[` - 进入滚动模式 (按 `q` 退出)

---

## Notion 配置

### API Token
```
YOUR_NOTION_API_TOKEN_HERE
```
> ⚠️ 在本地使用时，请将 `YOUR_NOTION_API_TOKEN_HERE` 替换为实际的 Token

### 配置文件位置
```
~/.claude/mcp.json
```

### 默认父页面
- **claude 工作流**: `3188b2b6-c4c8-8068-8bc0-f489b785ae0d`
- 新建 Notion 页面默认放在此页面下

### 使用方式
通过 Notion API 直接创建/更新页面，无需通过 MCP 服务器。

### API 调用示例
```bash
curl -X POST 'https://api.notion.com/v1/pages' \
  -H 'Authorization: Bearer YOUR_NOTION_API_TOKEN_HERE' \
  -H 'Notion-Version: 2022-06-28' \
  -H 'Content-Type: application/json' \
  -d '{"parent": {"type": "page_id", "page_id": "3188b2b6-c4c8-8068-8bc0-f489b785ae0d"}, "properties": {...}}'
```

---

## GitHub 配置

### 账号信息
- **用户名**: `wuyeeey-ship-it`
- **认证方式**: gh CLI (HTTPS)
- **Token权限**: repo, gist, workflow

### 常用仓库
| 仓库 | 用途 | 地址 |
|------|------|------|
| `my-hummingbot` | Hummingbot 策略 | https://github.com/wuyeeey-ship-it/my-hummingbot |
| `quant-trading` | 量化交易 | https://github.com/wuyeeey-ship-it/quant-trading |
| `vectorbtpro` | VectorBT Pro | https://github.com/wuyeeey-ship-it/vectorbtpro |
| `claude-md-research` | CLAUDE.md 研究 | https://github.com/wuyeeey-ship-it/claude-md-research |

### 常用命令
```bash
# 查看仓库列表
gh repo list wuyeeey-ship-it

# 克隆仓库
gh repo clone wuyeeey-ship-it/<repo-name>

# 推送代码 (需要先设置 git config)
git config user.email "wuyeeey-ship-it@users.noreply.github.com"
git config user.name "wuyeeey-ship-it"
git add . && git commit -m "message" && git push

# 创建新仓库
gh repo create <repo-name> --private

# 查看 PR/Issues
gh pr list
gh issue list
```

### Git 配置模板
```bash
# 在新仓库中设置身份
git config user.email "wuyeeey-ship-it@users.noreply.github.com"
git config user.name "wuyeeey-ship-it"
```

---

# currentDate
Today's date is 2026-03-11.
