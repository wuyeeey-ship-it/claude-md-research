# GitHub 项目管理流程

> 用于管理 wuyeeey-ship-it 账号下的 GitHub 项目

## 账号信息

- **用户名**: `wuyeeey-ship-it`
- **邮箱**: `wuyeeey-ship-it@users.noreply.github.com`
- **认证**: gh CLI (已登录)

## 推送代码到仓库

### 步骤 1: 检查状态
```bash
cd /path/to/repo && git status
```

### 步骤 2: 设置身份 (如果是新仓库)
```bash
git config user.email "wuyeeey-ship-it@users.noreply.github.com"
git config user.name "wuyeeey-ship-it"
```

### 步骤 3: 提交并推送
```bash
git add . && git commit -m "message" && git push
```

## 常用仓库列表

| 仓库名 | 类型 | 用途 |
|--------|------|------|
| `my-hummingbot` | private | Hummingbot 策略 |
| `quant-trading` | private | 量化交易 |
| `vectorbtpro` | private | VectorBT Pro |
| `claude-md-research` | public | CLAUDE.md 研究 |

## 快速命令

### 查看所有仓库
```bash
gh repo list wuyeeey-ship-it --limit 50
```

### 创建新仓库
```bash
# 私有仓库
gh repo create <name> --private

# 公开仓库
gh repo create <name> --public
```

### 克隆仓库
```bash
gh repo clone wuyeeey-ship-it/<name>
```

### 查看仓库信息
```bash
gh repo view wuyeeey-ship-it/<name>
```

### 创建 PR
```bash
gh pr create --title "Title" --body "Description"
```

### 查看 Issues
```bash
gh issue list --repo wuyeeey-ship-it/<name>
```

## 部署流程

### 推送策略到 my-hummingbot
```bash
# 1. 克隆仓库
cd /tmp && rm -rf my-hummingbot
gh repo clone wuyeeey-ship-it/my-hummingbot

# 2. 复制文件
cp /path/to/strategy.py /tmp/my-hummingbot/controllers/market_making/
cp /path/to/config.yml /tmp/my-hummingbot/conf/controllers/

# 3. 提交推送
cd /tmp/my-hummingbot
git config user.email "wuyeeey-ship-it@users.noreply.github.com"
git config user.name "wuyeeey-ship-it"
git add . && git commit -m "feat: Add new strategy"
git push origin main
```

### 从仓库部署到另一台电脑
```bash
# 1. 克隆仓库
gh repo clone wuyeeey-ship-it/my-hummingbot

# 2. 复制到 hummingbot 目录
cp my-hummingbot/controllers/market_making/*.py /path/to/hummingbot/controllers/market_making/
cp my-hummingbot/conf/controllers/*.yml /path/to/hummingbot/conf/controllers/
```
