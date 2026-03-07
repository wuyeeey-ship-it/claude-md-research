# CLAUDE.md 配置文件深度研究报告

> 研究日期: 2025-03-07
> 研究深度: Deep (4 hops)
> 置信度: High

---

## 执行摘要

CLAUDE.md 是 Claude Code 中**最高杠杆的配置点**，它直接影响每个会话的每个阶段。本研究综合了官方文档、社区最佳实践和专家经验，为构建一个让 AI 像专业量化开发工程师一样工作的规则系统提供完整指南。

### 核心发现

1. **LLM 无状态性** - CLAUDE.md 是唯一默认进入每个会话的文件
2. **少即是多** - 指令越少效果越好，建议 < 300 行，理想 < 60 行
3. **渐进式披露** - 任务特定指令应放在独立文件中
4. **Claude 会忽略不相关内容** - 只有普遍适用的内容才会被持续关注

---

## 一、CLAUDE.md 的本质与价值

### 1.1 为什么 CLAUDE.md 如此重要

```
LLM 是无状态函数
↓
权重在推理时冻结，不随时间学习
↓
模型对代码库的唯一了解是你输入的 tokens
↓
CLAUDE.md 是唯一默认进入每个会话的文件
```

### 1.2 三个关键含义

| 含义 | 说明 |
|------|------|
| AI 每次会话开始时对代码库一无所知 | 必须在 CLAUDE.md 中提供关键信息 |
| 每次会话都必须告诉 AI 重要信息 | CLAUDE.md 是最佳载体 |
| CLAUDE.md 影响工作流的每个阶段 | 一个糟糕的 CLAUDE.md 会产生连锁反应 |

### 1.3 CLAUDE.md 应该包含什么

**WHAT** - 技术/栈/项目结构
- 项目使用的技术栈
- 代码库的地图
- monorepo 中的应用和共享包

**WHY** - 项目目的和各部分功能
- 项目存在的目的
- 不同部分的职责

**HOW** - AI 如何工作
- 使用 `bun` 而不是 `node`
- 如何验证更改（测试、类型检查、编译）
- 关键命令和工作流程

---

## 二、Claude 忽略 CLAUDE.md 的原因

### 2.1 系统提示

Claude Code 会注入以下提醒：

```
IMPORTANT: this context may or may not be relevant to your tasks.
You should not respond to this context unless it is highly relevant to your task.
```

### 2.2 忽略的机制

- Claude 会判断 CLAUDE.md 内容是否与当前任务相关
- **非普遍适用的内容更容易被忽略**
- 指令越多，**所有指令的遵循质量都会下降**（非仅新指令）

### 2.3 指令容量研究

| 模型类型 | 指令容量 | 衰减特性 |
|----------|----------|----------|
| 前沿思考模型 | ~150-200 指令 | 线性衰减 |
| 较小模型 | 更少 | 指数衰减 |

**关键洞察**: Claude Code 的系统提示已包含约 50 条指令，占用了约 1/3 的指令容量。

---

## 三、最佳实践原则

### 3.1 少即是多

```
❌ 错误做法: 把所有可能的命令都塞进 CLAUDE.md
✅ 正确做法: 只包含普遍适用的指令

原因:
- 更多指令 = 所有指令遵循质量下降
- LLM 偏向提示词的两端（开头和结尾）
- 指令增加时，遵循质量均匀下降
```

### 3.2 文件长度与适用性

| 指标 | 推荐 | 理想 |
|------|------|------|
| 行数 | < 300 行 | < 60 行 |
| 内容 | 普遍适用 | 高度聚焦 |

### 3.3 渐进式披露

**核心思想**: 不要告诉 Claude 所有可能需要的信息，而是告诉它**如何找到**重要信息。

**推荐结构**:
```
agent_docs/
├── building_the_project.md
├── running_tests.md
├── code_conventions.md
├── service_architecture.md
├── database_schema.md
└── service_communication_patterns.md
```

**在 CLAUDE.md 中**:
```markdown
## 重要文档

开始任务前，阅读相关文档：
- `agent_docs/building_the_project.md` - 构建指南
- `agent_docs/running_tests.md` - 测试指南
- `agent_docs/service_architecture.md` - 架构说明
```

### 3.4 指针优于副本

```
❌ 错误: 在文档中包含代码片段
✅ 正确: 使用 file:line 引用指向权威源

原因: 代码片段会快速过时
```

---

## 四、不要用 Claude 做的事情

### 4.1 不要把 Claude 当作 Linter

| Linter | Claude |
|--------|--------|
| 快速、便宜 | 昂贵、缓慢 |
| 确定性 | 非确定性 |
| 专门化 | 通用 |

**替代方案**:
- 使用 Biome、ESLint、Pylint 等工具
- 设置 Claude Code `Stop` hook 自动运行格式化工具
- 创建 Slash Command 处理格式化

### 4.2 不要自动生成 CLAUDE.md

```
CLAUDE.md 影响范围:
├── 每个会话
│   └── 工作流的每个阶段
│       └── 生成的每个工件
│           └── 最终的代码质量

一条糟糕的代码 → 一条糟糕的代码
一条糟糕的计划 → 多条糟糕的代码
一条糟糕的研究 → 更多糟糕的计划 → 更多糟糕的代码
一条糟糕的 CLAUDE.md → 影响一切
```

---

## 五、三层规则系统设计

### 5.1 分层架构

```
┌─────────────────────────────────────────┐
│  第一层: GLOBAL_AI_RULES.md              │
│  - 通用规则                              │
│  - AI 基本行为控制                       │
│  - 与项目无关                            │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  第二层: PROJECT_RULES.md (CLAUDE.md)    │
│  - 项目特定规则                          │
│  - 项目架构描述                          │
│  - 技术栈说明                            │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  第三层: WORKFLOW_TEMPLATES/             │
│  - 执行流程模板                          │
│  - 任务特定指南                          │
│  - Agent 定义文件                        │
└─────────────────────────────────────────┘
```

### 5.2 各层职责

| 层级 | 文件 | 内容类型 | 更新频率 |
|------|------|----------|----------|
| 全局 | GLOBAL_AI_RULES.md | 通用原则 | 很少 |
| 项目 | CLAUDE.md | 项目信息 | 按需 |
| 模板 | agent_docs/*.md | 执行细节 | 频繁 |

---

## 六、Agent 架构系统

### 6.1 四层 Agent 结构

```
┌────────────────────────────────────────────────────────────┐
│                    Master_Control                          │
│  职责: 定义目标、控制循环、协调其他 Agent                  │
└────────────────────────────────────────────────────────────┘
                            │
            ┌───────────────┴───────────────┐
            ↓                               ↓
┌──────────────────────┐      ┌──────────────────────┐
│   Analysis_Agent     │      │  Executor_Experiment │
│  职责: 分析结果      │      │  职责: 执行最小实验  │
│        生成假设      │      │        验证假设      │
└──────────────────────┘      └──────────────────────┘
            │                               │
            └───────────────┬───────────────┘
                            ↓
               ┌──────────────────────┐
               │    Strategy_Lab      │
               │  职责: 记录研究过程  │
               │        保存学习成果  │
               └──────────────────────┘
```

### 6.2 执行循环

```
目标定义
    │
    ↓
┌─────────────────┐
│ Master_Control  │ ──→ 分解目标为子任务
└─────────────────┘
    │
    ↓
┌─────────────────┐
│ Analysis_Agent  │ ──→ 分析现状，生成假设
└─────────────────┘
    │
    ↓
┌─────────────────────┐
│ Executor_Experiment │ ──→ 执行最小实验验证
└─────────────────────┘
    │
    ↓
┌─────────────────┐
│  Strategy_Lab   │ ──→ 记录结果，更新知识
└─────────────────┘
    │
    ↓
目标达成？ ──否──→ 循环继续
    │
   是
    ↓
  完成
```

### 6.3 Executor 的核心价值

- **实验驱动开发** 而非猜测开发
- **一次只验证一个假设**
- 输出标准化 Result 格式

---

## 七、标准化输出格式

### 7.1 Analysis Agent 输出

```yaml
Analysis:
  hypothesis:
    - MACD histogram indicates trend start
    - Volume confirms signal strength
  next_task:
    - calculate MACD indicator
    - analyze volume patterns
  goal_progress:
    progress: 0.2
  confidence: 0.6
  blockers:
    - none
```

### 7.2 Executor Agent 输出

```yaml
Result:
  status: success | partial | failed
  experiment:
    - MACD indicator calculated
    - Volume analysis complete
  metrics:
    signal_count: 124
    accuracy: 0.72
  issues:
    - none | [list of issues]
  next_steps:
    - implement signal filtering
  confidence: 0.8
```

---

## 八、开发流程七阶段

```
PHASE 1: 需求分析 (Requirement Analysis)
├── 理解问题
├── 定义成功标准
└── 识别约束

PHASE 2: 代码调研 (Code Research)
├── 搜索现有实现
├── 分析代码结构
└── 记录发现

PHASE 3: 方案设计 (Solution Planning)
├── 设计方案
├── 评估风险
└── 获得批准

PHASE 4: 实施开发 (Implementation)
├── 按方案编码
├── 最小修改范围
└── 遵循现有模式

PHASE 5: 验证运行 (Verification)
├── 运行测试
├── 检查类型
└── 验证功能

PHASE 6: 需求复核 (Requirement Validation)
├── 对照原始需求
├── 验证完整性
└── 记录偏差

PHASE 7: 循环修复 (Iteration Loop)
├── 如有问题
└── 返回 PHASE 1
```

---

## 九、量化开发特化规则

### 9.1 必须遵循的架构参考

- Controller/Executor 架构模式
- pandas_ta 指标库使用
- candles feed 数据结构

### 9.2 策略开发流程

```
研究 → 设计 → 回测 → 优化 → 实盘
```

### 9.3 禁止事项

- **禁止**发明新的代码结构
- **禁止**凭空编写代码
- **禁止**跳过代码调研阶段
- **禁止**超出最小修改范围

---

## 十、推荐项目结构

```
project/
├── CLAUDE.md                    # 主配置文件 (< 60 行)
│
├── agent_docs/                  # 渐进式披露文档
│   ├── building_the_project.md
│   ├── running_tests.md
│   ├── code_conventions.md
│   ├── service_architecture.md
│   └── research_workflow.md
│
├── .claude/
│   ├── commands/                # 自定义 Slash 命令
│   │   ├── review.md
│   │   ├── test.md
│   │   └── research.md
│   └── rules/                   # 项目规则（可选）
│
├── research/                    # 研究资料
├── backtest/                    # 回测
├── strategies/                  # 策略
└── data/                        # 数据
```

---

## 十一、关键洞察总结

### CLAUDE.md 的本质

> CLAUDE.md 的作用不是解释项目，而是**控制 AI 行为**

### 三个核心要求

1. **可执行** - AI 知道每一步具体做什么
2. **强约束** - 防止 AI 乱写代码
3. **循环闭环** - 问题→方案→代码→验证→回到问题

### 最强的一句话规则

```
Never write code before completing the Code Research step.
```

---

## 十二、参考资料

### 官方资源
- [Skill authoring best practices - Claude Docs](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)

### 社区资源
- [Writing a good CLAUDE.md - HumanLayer Blog](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
- [The Only CLAUDE.md Guide You Need - Generative AI](https://generativeai.pub/the-only-claude-md-482b771431b2)
- [Claude Code Best Practices - Sidetool](https://www.sidetool.co/post/claude-code-best-practices-tips-power-users-2025/)
- [7 Essential Claude Code Best Practices - Eesel](https://www.eesel.ai/blog/claude-code-best-practices)

### 讨论资源
- [Hacker News Discussion](https://news.ycombinator.com/item?id=46098838)
- [Reddit - How I structure Claude Code projects](https://www.reddit.com/r/ClaudeAI/comments/1r66oo0/how_i_structure_claude_code_projects_claudemd/)

---

## 最终模板

### v1: 标准版 (推荐)
文件: `templates/CLAUDE.md` (125 行)

**特点**:
- 6 条 Critical Rules
- 7 阶段开发流程
- 标准输出模板 (Research + Files + Plan)
- 禁止重写模块
- 禁止实施时添加文件

**适用**: 大多数项目

### v2: Agent Mode 版
文件: `templates/CLAUDE_v2.md` (135 行)

**特点**:
- 包含 v1 所有特性
- 双模式切换: [PLANNER] / [EXECUTOR]
- 强制模式声明
- 分离读写权限

**适用**: 复杂项目、需要严格控制的场景

---

## 快速使用

```bash
# 标准版 (推荐)
cp templates/CLAUDE.md /your/project/CLAUDE.md

# Agent Mode 版
cp templates/CLAUDE_v2.md /your/project/CLAUDE.md

# 创建 agent_docs
mkdir -p /your/project/agent_docs
cp templates/agent_docs/*.md /your/project/agent_docs/
```

---

## 文件清单

```
claude-md-research/
├── docs/
│   ├── RESEARCH_REPORT.md      # 研究报告
│   └── DISCUSSION_SUMMARY.md   # 讨论总结
│
└── templates/
    ├── CLAUDE.md               # v1 标准版 (推荐)
    ├── CLAUDE_v2.md            # v2 Agent Mode 版
    ├── CLAUDE_QUANT.md         # 量化开发专用
    ├── QUICKSTART.md           # 快速入门
    ├── README.md               # 模板说明
    │
    └── agent_docs/
        ├── architecture.md
        ├── code_conventions.md
        ├── testing_guide.md
        ├── debugging.md
        ├── master_control.md
        ├── analysis_agent.md
        ├── executor_agent.md
        └── strategy_lab.md
```
