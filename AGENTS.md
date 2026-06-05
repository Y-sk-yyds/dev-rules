# AGENTS.md

> 个人 AI 上下文模板。新项目启动时，填写顶部两个区块，其余规则框架保持不变。
> 本文件为 AI 全量读取模式，不可遗漏任何章节。

---

## ■ 身份（本次项目中的角色）

<!-- 按实际项目填写，删掉不贴合的，保留当前角色 -->
- 角色：（学生开发者 / 个人开发者 / 后端工程师 / 全栈 / ……）
- 目标：本次项目要解决什么问题？
- 技能水平：（熟悉 / 掌握 / 初学）当前技术栈

---

## ■ 项目概述（从零开始描述本次项目）

<!-- 每个新项目重新填写此区域，让 AI 从零理解你在做什么 -->

- 项目名称：
- 一句话描述：
- 仓库地址：
- 后端：（语言 + 框架 + 版本）
- 前端：（框架 + UI 库 + 打包工具）
- 数据库：（类型 + 版本）
- 部署方式：（本地 / 云服务器 / Docker / ……）
- 服务器信息：（IP / 管理面板 / SSH 条件。本地开发则写"本地开发"）

当前进度：
- 已完成：
- 进行中：
- 待开发：

---

## ■ Skill 使用矩阵

### 默认始终加载
| Skill | 用途 |
|-------|------|
| `caveman` | 压缩通信，减少 token 消耗 |

### 按场景加载
| Skill | 触发条件 |
|-------|---------|
| `frontend-design` | 创建前端页面、组件、UI 交互 |
| `ui-ux-pro-max` | 设计讨论、信息架构、UX 流程 |
| `code-review` | 初次审查、建立审查标准 |
| `code-review-fix` | 功能完成后自动审查修复 |
| `Git` | 分支、合并、冲突解决、rebase |
| `caveman-commit` | 生成 commit message |
| `github` | PR、Issue、CI 操作 |
| `self-improvement` | 命令失败、被纠正、发现新能力 |
| `find-skills` | 搜索新的能力扩展 |
| `skill-creator` | 固定可复用的重复流程 |
| `cloudstudio-deploy` | 部署静态站点到云端预览 |

### 联动规则
- 功能开发完成 → 自动加载 `code-review-fix`
- 生成 commit message → 自动用 `caveman-commit`
- 被纠错或命令失败 → 触发 `self-improvement`，输出记录写入 `experience/` 目录
- 重复操作 ≥3 次 → 主动询问是否用 `skill-creator` 固化为 skill

---

## ■ AI 交互规则

以下规则适用于所有项目，不随项目切换而改变。

### 沟通
- 用中文交流，简洁直接，不要废话套话
- 技术决策需要原理性解释 + 数字对比，不要只列步骤
- 直接给可复制执行的脚本、SQL、配置，不要让我截图
- 方案讨论先列选项和利弊，等我确认再动手

### 操作边界
- SQL 改动（DDL / DML）先输出内容让我确认，不自动执行
- 不主动 `git push`，等我明确说"推"
- 不主动连接服务器执行命令，除非我明确授权
- 功能完成后自动做一轮 code review（重复代码、异常处理、边界条件）

### 交付
- 每次改动结束给出总结：分条列出改了什么、为什么改
- 涉及多个文件时，说清楚文件之间的调用关系
- 新功能上线前，本地先跑编译确认通过

---

## ■ 代码规范（按实际技术栈选择）

<!-- 以下章节为模板。当前项目用什么就填什么，不用的章节可整块删除。 -->

### Java / Spring Boot（如适用）
- 实体类用 Lombok：`@Data`、`@NoArgsConstructor`、`@AllArgsConstructor`
- 字段驼峰命名，数据库下划线自动映射（`map-underscore-to-camel-case=true`）
- Service 层：接口 + 实现类（`XxxService` + `XxxServiceImpl`）
- Controller 返回统一 `Result<T>`（`code`、`message`、`data`）
- 异常走 `@RestControllerAdvice` 全局处理
- 时间字段用 `LocalDateTime`，序列化格式 `yyyy-MM-dd HH:mm:ss`
- 分页用 MyBatis-Plus `Page<T>`，不自造轮子

### Vue3 / Element Plus（如适用）
- Composition API + `<script setup>`
- 简单状态 `reactive`/`ref`，跨组件用 Pinia
- API 调用统一在 `api/` 目录封装
- 列表页必须有 loading 和空数据提示
- 图片懒加载（`v-lazy`），减少首屏请求

### SQL / 数据库（如适用）
- 所有表包含 `id`（自增）、`create_time`、`update_time`
- `update_time` 设置 `ON UPDATE CURRENT_TIMESTAMP`
- 逻辑删除用 `is_deleted`（tinyint，默认 0），不用物理删除
- 高频查询字段 + 外键字段加索引
- 表结构和字段必须加 `COMMENT`

### 通用（所有项目适用）
- 硬编码抽常量或枚举
- 敏感信息走配置文件 + 环境变量，不入 `.gitignore`
- 日志用 SLF4J，生产环境关闭 SQL 日志

---

## ■ Git 流程（所有项目适用）

### 分支策略
```
main        ← 稳定版本，只从 develop 合并
develop     ← 开发主分支
feature/*   ← 新功能分支（如 feature/chat、feature/review）
fix/*       ← bug 修复分支
```

### Commit Message
```
<type>: <简述>
- 改动点1
- 改动点2
```
type：`feat`（新功能）/ `fix`（修复）/ `chore`（工程化）/ `perf`（性能）/ `refactor`（重构）

### 提交流程
1. `git status` 确认文件状态
2. `git add <files>` 精确添加目标文件
3. `git commit`
4. 等我确认后 `git push`

### 文件状态速查
| 状态 | 含义 | 操作 |
|------|------|------|
| Untracked | 新文件，Git 不跟踪 | `git add` 纳入管理 |
| Modified | 已跟踪文件的修改 | `git add` 暂存修改 |
| Staged | 已 add 待 commit | `git commit` |

---

## ■ 经验目录

以下目录仅供开发者查阅，**AI 不自动读取，不注入上下文**：

```
experience/
├── pitfalls.md       ← 踩坑记录（场景 + 原因 + 解法）
├── fixes.md          ← AI 被我纠正的记录（错什么 → 应该怎样）
├── optimization.md   ← 验证过的优化方案 + 数据对比
├── decisions.md      ← 架构决策记录（选 A 不选 B，为什么）
└── habits.md         ← 个人开发习惯记录
```

### AI 写入规则
- 触发 `self-improvement` 时，将记录追加到 `experience/` 对应文件
- 写入后说明文件名和条目摘要
- 检测到重复 ≥3 次的操作模式时，主动询问是否沉淀到 `habits.md`

---

## ■ 扩展说明

本文件按"模板 + 填空"设计：
- 顶部两个区块（身份、项目概述）→ 每次新项目填写，是动态上下文
- 中下部规则 → 跨项目稳定，只在发现更好的做法时修改
- 经验沉淀 → 见同目录 `experience/`，纯开发者查阅，不与 AI 上下文混合

当规则超过 500 行或引入第二个技术栈时，技术栈规范拆到 `profiles/` 目录，并在本章节加硬指令要求 AI 全量读取。
