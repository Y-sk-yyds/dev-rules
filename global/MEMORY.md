# 跨项目记忆

## dev-rules 仓库
- Y-sk-yyds/dev-rules
- AGENTS.md：技术栈编码规范（每项目复制 + 填空）
- experience/：开发者查阅，AI 不读
- 迭代：开发中积累 → 追加到 experience/ → commit + push

## 行为规则

1. **方案先行**：改动前先列方案，确认后再动手
2. **commit 确认**：commit 前必须问用户确认
3. **后端重启提醒**：改 Java 文件后主动提醒
4. **自动编译验证**：写完代码后自动 build/compile，不等提醒
5. **SQL 审批**：SQL 变更先输出审批，不自动执行
6. **不自动 push**：等用户明确确认
7. **结束后总结**：改动文件清单 + 经验记录 + 下一步计划
8. **读已有文件**：写新文件前先读同类文件照抄风格
9. **code-review-fix**：功能模块完成后自动审查

## Skill 约定

| Skill | 触发条件 |
|-------|----------|
| caveman | 默认压缩模式 |
| rtk-integration | Shell 命令 |
| caveman-commit | 提交/commit/推送 |
| code-review-fix | 功能模块完成后 |
| caveman-compress | 压缩上下文/总结 |
| ui-ux-pro-max | 前端优化/美化/改进布局 |
| frontend-design | 创建页面/组件/UI |
| github | PR/Issue/CI |
| self-improvement | 报错/纠正/新能力 |
| skill-creator | 重复 ≥3 次固化 |

## 会话自检

1. **开场读记忆**：主动读项目 MEMORY.md 和本文件
2. **结束写进度**：更新项目日记忆 + 长期记忆
3. **主动跟进**：根据下一步计划推进
4. **经验积累**：遇坑自动记录，避免重复
