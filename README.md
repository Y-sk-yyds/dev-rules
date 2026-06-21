# dev-rules

个人 AI 上下文规则仓库。含一套可复用的 AGENTS.md 模板 + 持续积累的经验记录。

## 结构

```
dev-rules/
├── AGENTS.md           ← 技术栈约定模板（编码规范，不含行为规则）
├── README.md           ← 本文件
└── experience/         ← 开发者查阅（AI 不读）
    ├── pitfalls.md     ← 踩坑记录
    ├── fixes.md        ← 纠错记录
    ├── optimization.md ← 优化方案
    ├── decisions.md    ← 架构决策
    └── habits.md       ← 开发习惯
```

## 使用方式

1. **新项目**：复制 AGENTS.md 到根目录 → 填空（Identity/Overview/Deploy）→ 完事
2. **行为规则不放进 AGENTS.md**：统一在跨项目 MEMORY.md（`~/.workbuddy/MEMORY.md`），全项目生效
3. **开发积累**：踩坑/决策通过 self-improvement 回写到 experience/

## 规则分工

| 放哪 | 内容 | 例子 |
|------|------|------|
| 跨项目 MEMORY.md | 行为规则、Git 流程 | 方案先行、commit 前确认、不自动 push |
| AGENTS.md（项目根） | 技术栈约定、配置 | Jakarta EE、Vue3 写法、数据库端口 |
| experience/ | 经验教训 | 踩坑、决策 ADR |

## 设计原则

- 通用行为规则只写一处（跨项目 MEMORY），不在 AGENTS.md 重复
- AGENTS.md 只放这个技术栈的代码写法约定
- experience/ 纯开发者看，不占 token
