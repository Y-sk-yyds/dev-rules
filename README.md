# dev-rules

AI 开发规则仓库。模板文件给 AI 读，经验记录给人看。

## 结构

```
dev-rules/
├── AGENTS.md           ← 技术栈编码规范（每项目复制 + 填空）
├── README.md           ← 本文件
├── global/             ← 跨项目共享文件（手动维护）
│   ├── MEMORY.md       ← 13 条行为规则 + Skill 约定（AI 每次自动读）
│   ├── SOUL.md         ← AI 人格设定
│   └── USER.md         ← 用户档案
└── experience/         ← 开发者查阅（AI 不读，省 token）
    ├── pitfalls.md     ← 踩坑记录
    ├── fixes.md        ← 纠错记录
    ├── optimization.md ← 优化方案
    ├── decisions.md    ← 架构决策
    └── habits.md       ← 开发习惯
```

## 使用方式

1. **新项目**：复制 `AGENTS.md` 到项目根 → 填空（Identity / Project Overview / Deploy）→ 完事
2. **行为规则**：在跨项目 MEMORY.md（`~/.workbuddy/MEMORY.md`），不与 AGENTS.md 混放。本项目维护一份副本在 `global/MEMORY.md`
3. **积累经验**：开发中遇到坑/决策 → 通过 self-improvement skill 自动追加到 `experience/`

## 规则分层

| 层 | 位置 | 内容 | 谁读 |
|----|------|------|------|
| 行为规则 | 跨项目 MEMORY.md | 13 条规则 + Skill 矩阵 | AI 自动 |
| 技术栈约定 | AGENTS.md | 代码写法、框架规范 | AI 自动 |
| 项目进度 | 项目 .workbuddy/memory/ | 每日日志 + 长期记忆 | AI 手动 |
| 经验教训 | dev-rules/experience/ | 踩坑、决策、习惯 | 人 |

## 13 条行为规则速览

| # | 规则 | 类型 |
|---|------|------|
| 1 | 方案先行，确认后动手 | 工作流 |
| 2 | commit 前问用户确认 | Git |
| 3 | 改 Java 后提醒重启 | 工作流 |
| 4 | 写完代码自动编译验证 | 质量 |
| 5 | SQL 先审批不自动执行 | 安全 |
| 6 | 不自动 push | Git |
| 7 | 结束后总结（清单+经验+计划） | 总结 |
| 8 | 新文件先读同类照抄风格 | 规范 |
| 9 | 完成功能后自动 code-review | 质量 |
| 10 | 开场主动读记忆 | 自治 |
| 11 | 结束自动写进度 | 自治 |
| 12 | 主动跟进下一步计划 | 自治 |
| 13 | 遇坑自动记录 | 自治 |

## Skill 约定

| Skill | 触发时机 |
|-------|----------|
| caveman | 默认压缩模式 |
| caveman-commit | commit / push 操作 |
| code-review-fix | 功能模块完成后 |
| ui-ux-pro-max | 前端优化 / 美化布局 |
| frontend-design | 创建页面 / 组件 |
| self-improvement | 报错 / 纠正 / 新能力 |
| skill-creator | 重复 ≥3 次的操作固化 |
| rtk-integration | Shell 命令执行 |
| github | PR / Issue / CI |

## 设计原则

- 行为规则只在一处维护（跨项目 MEMORY），不在 AGENTS.md 赘述
- AGENTS.md 是纯技术栈约定模板，零行为指令
- experience/ 纯人读，AI 不加载，省 token
- global/MEMORY.md 是跨项目规则的本地副本，你手动同步
