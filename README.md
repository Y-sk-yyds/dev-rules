# dev-rules

个人 AI 上下文规则仓库。包含一套可复用的 AGENTS.md 模板，以及开发过程中持续积累的经验记录。

## 结构

```
dev-rules/
├── AGENTS.md           ← AI 上下文（模板 + 规则 + Skill 矩阵）
├── README.md           ← 本文件
└── experience/         ← 开发者查阅（AI 不读）
    ├── pitfalls.md     ← 踩坑记录
    ├── fixes.md        ← 纠错记录
    ├── optimization.md ← 优化方案
    ├── decisions.md    ← 架构决策
    └── habits.md       ← 开发习惯
```

## 使用方式

1. **新项目启动时**：复制 `AGENTS.md` 到项目根目录，填写顶部两个区块（身份 + 项目概述）
2. **开发过程中**：AI 触发 `self-improvement` 时，自动写入 `experience/` 对应文件
3. **日常维护**：发现更好的规则或操作模式时，直接修改 `AGENTS.md` 或追加到 `experience/`

## 设计原则

- **AGENTS.md 是 AI 吃的**：全量读取，不漏规则
- **experience/ 是你看的**：AI 不自动扫描，纯开发者查阅
- **框架是稳定的，身份是流动的**：换项目只改顶部填空，规则不动
