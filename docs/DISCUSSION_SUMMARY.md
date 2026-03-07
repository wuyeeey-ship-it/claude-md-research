# CLAUDE.md 配置文件系统研究总结

## 研究目标
设计一套完整的 AI 开发规则系统，让 AI 像专业量化开发工程师一样工作。

---

## 一、核心问题

### AI 编程的常见问题
1. **凭空写代码** - 不参考已有代码结构
2. **没有强制查代码结构** - AI 容易自己造代码
3. **没有限制修改范围** - 改动不可控
4. **没有验证步骤** - 代码质量无法保证
5. **没有错误循环机制** - 问题无法迭代解决

### 用户的原始逻辑
```
1. 分析问题需求
2. 参考已有代码资料（不要凭空想象）
3. 根据资料全面规划，检查方案
4. 按方案写代码
5. 运行检查代码
6. 对比问题需求是否完成，有问题循环从1开始
```

---

## 二、分层规则系统

### 为什么必须分层

| 层级 | 文件 | 作用 | 内容类型 |
|------|------|------|----------|
| 第一层 | GLOBAL_AI_RULES.md | 控制 AI 基本行为 | 通用规则 |
| 第二层 | PROJECT_RULES.md | 描述项目架构 | 项目特定 |
| 第三层 | STRATEGY_TEMPLATE.md | 告诉 AI 如何开发 | 流程模板 |

### 分层原因
- **全局规则**不能包含项目细节（如 Hummingbot、pandas_ta）
- **项目规则**只适用于当前项目
- **模板**是具体执行流程

---

## 三、CLAUDE.md 核心结构

### 六大模块
```
1. Project Rules      - 项目规则
2. Development Workflow - 开发流程
3. Code Research Rules  - 代码研究规则
4. Implementation Rules - 实施规则
5. Testing Rules        - 测试规则
6. Debug Loop          - 调试循环
```

### 关键原则
1. **Never invent code structures** - 永远不要发明代码结构
2. **Always analyze existing code first** - 先分析已有代码
3. **Only modify minimal necessary files** - 只修改必要的最小文件
4. **Every solution must be verified** - 每个方案必须验证

### 最强的一句话规则
```
Never write code before completing the Code Research step.
```

---

## 四、开发流程七阶段

```
PHASE 1 — 需求分析    (Requirement Analysis)
PHASE 2 — 代码调研    (Code Research)
PHASE 3 — 方案设计    (Solution Planning)
PHASE 4 — 实施开发    (Implementation)
PHASE 5 — 验证运行    (Verification)
PHASE 6 — 需求复核    (Requirement Validation)
PHASE 7 — 循环修复    (Iteration Loop)
```

---

## 五、Research Workflow 八阶段

```
Phase 1 — Problem Definition     (问题定义)
Phase 2 — Existing Code Research (已有代码研究)
Phase 3 — Signal Design          (信号设计)
Phase 4 — Risk Management Design (风控设计)
Phase 5 — Architecture Planning  (架构规划)
Phase 6 — Implementation Plan    (实施计划)
Phase 7 — Backtest Plan          (回测计划)
Phase 8 — Final Research Report  (最终研究报告)
```

---

## 六、Agent 架构系统

### 四层 Agent 结构

| Agent | 角色 | 职责 |
|-------|------|------|
| Master_Control | 总控 | 定义目标、控制循环 |
| Analysis_Agent | 分析 | 分析结果、生成假设 |
| Executor_Experiment | 执行 | 执行最小实验 |
| Strategy_Lab | 记录 | 记录研究过程 |

### 执行循环
```
Goal → Master_Control → Analysis_Agent → Executor_Experiment
  ↑                                                    ↓
  └──────────── Strategy_Lab ←───────────────────── Result
```

### Executor 的核心价值
- **实验驱动开发** 而非猜测开发
- **一次只验证一个假设**
- 输出标准化 Result 格式

---

## 七、标准化输出格式

### Analysis 输出
```yaml
Analysis:
  hypothesis:
    - MACD histogram indicates trend start
  next_task:
    - calculate MACD indicator
  goal_progress:
    - progress: 0.2
```

### Executor 输出
```yaml
Result:
  status: success
  experiment:
    - MACD indicator calculated
  metrics:
    - signal_count: 124
  issues:
    - none
  confidence: 0.6
```

---

## 八、推荐项目结构

```
quant_ai_lab/
├── CLAUDE.md                    # AI 规则（项目级）
├── GLOBAL_AI_RULES.md           # 全局规则
├── PROJECT_RULES.md             # 项目规则
├── RESEARCH_WORKFLOW.md         # 研究流程
├── STRATEGY_TEMPLATE.md         # 策略模板
├── Master_Control.md            # 总控
├── Analysis_Agent.md            # 分析 Agent
├── Executor_Experiment.md       # 执行 Agent
├── Strategy_Lab.md              # 研究记录
│
├── research/                    # 研究资料
├── backtest/                    # 回测
├── strategies/                  # 策略
└── data/                        # 数据
```

---

## 九、关键洞察

### CLAUDE.md 的本质
> CLAUDE.md 的作用不是解释项目，而是 **控制 AI 行为**

### 三个核心要求
1. **可执行** - AI 知道每一步具体做什么
2. **强约束** - 防止 AI 乱写代码
3. **循环闭环** - 问题→方案→代码→验证→回到问题

### 量化开发的 AI 规则特点
- 必须参考已有 Controller/Executor 架构
- 必须使用 pandas_ta 指标
- 必须使用 candles feed 数据
- 策略开发流程固定：研究→设计→回测→优化→实盘

---

## 十、待完成事项

- [ ] 深度研究 Claude Code 官方 CLAUDE.md 最佳实践
- [ ] 收集社区 CLAUDE.md 模板
- [ ] 设计完整的分层规则文件
- [ ] 创建 Agent 架构文件
- [ ] 验证系统可行性
