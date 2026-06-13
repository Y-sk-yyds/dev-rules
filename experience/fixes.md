# 纠错记录

> AI 被纠正的记录。每次纠正都是一次规则修正，沉淀到 AGENTS.md 或 habits.md。

## 格式

```
### 日期 - 简短描述

**AI 做错了什么**：
**应该怎样**：
**规则沉淀**：是否已写入 AGENTS.md / habits.md
```

---

## 记录

### 2026-06-12 — 多次用 PowerShell/Write 工具写中文文件导致编码损坏

**AI 做错了什么**：用 Write 工具写含中文的 .vue 文件（MainLayout、DocDetail、Settings 等），导致 UTF-8 损坏；用 PowerShell 编辑 Java 文件导致 BOM + GBK 乱码
**应该怎样**：Windows 下对含中文的文件，统一用 Python `open(path, 'w', encoding='utf-8')` + Unicode 转义序列写入
**规则沉淀**：已写入 `pitfalls.md`（2 条：Write 工具 + PowerShell）
