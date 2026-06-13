# AGENTS.md

> 可复用 AI 上下文模板。每个新项目克隆后只需填空，其余规则通用。
>
> AI 按文件名自动注入此文件，`experience/` 目录不会自动加载。

---

## ■ Before Coding — 必填问题

以下问题如有未回答的，AI 必须先问清再动手。

1. 你的角色是什么？（学生 / 全栈 / 后端 / 前端 / 独立开发）
2. 这个项目解决什么问题？
3. 你对当前技术栈熟练吗？（熟悉 / 能写 / 新手）
4. 项目名称 + 一句话描述？
5. 后端：语言 + 框架 + 版本？
6. 前端：框架 + UI 库 + 打包工具？
7. 数据库：类型 + 版本？
8. 部署方式：纯本地 / 云服务器 / Docker？服务器地址？
9. 当前进度：已做完什么 / 正在做什么 / 下一步做什么？

**版本兼容检查（必做）：**
回答完上述问题后，对比实际版本与下方 `技术栈约定` 中的版本。如果有大版本差异（如约定 Spring Boot 2.x 但项目用 3.x），标记差异并问用户选：
- A) 按实际版本调整约定
- B) 保留约定并标注差异
- C) 跳过该部分

---

## ■ Identity

- 角色：全栈开发
- 目标：一个工作项目，具体业务目标待定
- 技术熟练度：熟悉

---

## ■ Project Overview

- 项目名称：wk2
- 一句话描述：待定工作项目
- 仓库地址：D:\newproject\wk2
- 后端：Java + Spring Boot 3.x + MyBatis-Plus
- 前端：Vue3 + Element Plus + Vite
- 数据库：MySQL 8.0+（InnoDB, utf8mb4）
- 部署：本地
- 服务器信息：local dev

当前进度：
- 已完成：项目初始化
- 进行中：暂无
- 待做：待定

---

## ■ Deployment & Config

<!-- 生产部署时填写，纯本地项目可跳过 -->

### 服务器
- 云厂商：
- IP：
- 系统：
- 管理面板：

### 应用
- 后端端口：
- 前端端口：
- 部署路径：

### 数据库
- 地址：
- 库名：
- 用户：
- 端口：

### 配置规范
- 基础配置统一放 `application.yml` / `.env` / 对应框架的配置文件
- **密码、密钥不写死在配置文件里** → 用 `${ENV_VAR}` / 环境变量 / 密钥管理服务
- 本地开发用 gitignore 掉的私有配置文件
- 常用环境变量清单：

### 远程仓库
- Git 地址：
- 主分支：
- 部署分支：

---

## ■ 你的技术栈约定

### Java / Spring Boot 3.x + MyBatis-Plus

- Jakarta EE：用 `jakarta.*`，不用 `javax.*`
- Entity 用 Lombok：`@Data`，`@NoArgsConstructor`，`@AllArgsConstructor`
- camelCase 字段，snake_case 数据库列（自动映射）
- Service 层：接口 + 实现（`XxxService` + `XxxServiceImpl`）
- Controller 统一返回 `Result<T>`（`code`, `message`, `data`）
- 全局异常处理：`@RestControllerAdvice`
- Controller 路径：`@RequestMapping("/api/xxx")`，方法级 `@PostMapping("/action")` → 完整路径 `/api/xxx/action`
- 新建 Controller **先读一个已有的**，照抄风格
- 配置规范：`application.yml` 只放基础配置，密码用 `${ENV_VAR}`，本地用 `application-secret.yml`(gitignored)
- Spring Security 6.x：用 lambda DSL，不用 `antMatchers()` 和 `WebSecurityConfigurerAdapter`

### Vue3 + Element Plus + Vite

- Composition API + `<script setup>`
- 本地状态：`reactive` / `ref`；跨组件：Pinia
- API 调用集中到 `api/` 目录
- axios `baseURL = "/api"`，各 API 模块**不再重复加 `/api` 前缀**
- 新建 API 模块前先读一个已有的（如 `api/product.js`）
- 列表页有 loading 态和空数据提示
- 路由参数变化（同一组件不同 ID）：用 `watch` 监听 `route.params`，不用 `created` / `mounted`

### MySQL 8.0+（InnoDB, utf8mb4）

- 每表：`id`（自增）、`create_time`、`update_time`
- `update_time` 加上 `ON UPDATE CURRENT_TIMESTAMP`
- 软删除：`is_deleted`（tinyint, default 0），不做物理删除
- 高频查询字段和关联键建索引
- 每个字段写 `COMMENT`
- 列表页和详情页的图片字段分离：`cover_image`（单字段）vs `images`（TEXT/JSON），列表查询跳过大数据字段

### 其他约定
- 所有硬编码字符串/数字 → 常量或枚举
- 密码/密钥/Tokens → 配置文件 + 环境变量，gitignore 排除
- 日志：SLF4J，生产环境关 SQL 日志（`show-sql=false`，MyBatis-Plus 日志级别 WARN）
- **写任何新文件前**先读一个已有同类文件，保证风格一致

---

## ■ Skill 配置

### 常驻加载
| Skill | 用途 |
|-------|------|
| `caveman` | 对话压缩，省 token ~75% |
| `rtk-integration` | Shell 命令自动注入 RTK，减 token 开销 |

### 按需加载
| Skill | 触发词 |
|-------|--------|
| `frontend-design` | 创建页面、组件、UI 交互 |
| `ui-ux-pro-max` | "前端优化" / "美化页面" / "改进布局" / "优化交互" |
| `code-review` | 首次代码审查、建立规范 |
| `code-review-fix` | 功能模块完成后自动审查 |
| `Git` | 分支、合并、冲突解决、rebase |
| `caveman-commit` | "提交" / "commit" / "推送" |
| `caveman-compress` | "压缩上下文" / "总结一下" |
| `github` | PR、Issue、CI 操作 |
| `self-improvement` | 命令报错 / 用户纠正 / 发现新能力 |
| `find-skills` | 搜索新能力扩展 |
| `skill-creator` | 重复性工作流固化为 skill |
| `cloudstudio-deploy` | 静态站点部署到云预览 |

### 自动关联顺序
1. 功能模块完成 → 自动加载 `code-review-fix`
2. 用户说"提交" / "commit" / "推送" → 自动加载 `caveman-commit`
3. 用户说"压缩上下文" / "总结一下" → 自动加载 `caveman-compress`
4. 用户说"前端优化" / "美化页面" / "改进布局" / "优化交互" → 自动加载 `ui-ux-pro-max`
5. 执行 shell 命令 → 自动用 `rtk-integration`
6. 用户纠正 / 命令报错 → 触发 `self-improvement`，记录到 `experience/`
7. 同一操作重复 ≥3 次 → 询问是否用 `skill-creator` 固化为 skill

---

## ■ 交互规则

### 沟通
- 说中文，简洁直接，不废话
- 技术决策给理由和数据，不只列步骤
- 提供可直接复制运行的脚本、SQL、配置
- 先出方案再执行，等确认

### 边界
- **SQL 变更必先输出审批，绝不自动执行**
- 不主动 `git push`，等明确确认
- 不主动连接服务器，等明确授权
- 功能完成后自动审查（重复代码、异常处理、边界情况）

### 交付
- 每次改动结束时出分条总结：改了哪些文件 + 为什么改
- 多文件改动说明调用链路
- 上线前本地编译确认通过

### 质量保障
- 后端写完后跑编译验证（`mvn clean package` / `go build` / 对应命令）
- 前端写完后跑构建验证（`npm run build` / 对应命令）
- 每天工作结束时更新 `.workbuddy/memory/` 日志
- 提交前 `git status` + `git log --oneline -3` 确认改动范围

---

## ■ 功能开发流程

### 推荐顺序
1. 后端先行：模型设计 → SQL（先审）→ 逻辑 → 接口 → 编译验证
2. 前端跟上：API 封装 → 页面组件 → 构建验证
3. 收尾：`code-review-fix` 审查 → 写 memory 日志 → 问是否提交

---

## ■ Git 工作流

### 分支策略
```
main        ← 稳定版，仅从 develop 合入
develop     ← 开发集成分支
feature/*   ← 新功能（如 feature/chat）
fix/*       ← 修复缺陷
```

### 提交格式
```
<type>: <简短描述>
- 改动点 1
- 改动点 2
```
类型：`feat` / `fix` / `chore` / `perf` / `refactor`

commit message 语言：随开发者日常用语（默认中文）。

### 提交流程
1. `git status` 看文件状态
2. `git add <文件>` — 精确 add，不用 `git add .`
3. `git log --oneline -3` 回顾最近提交，避免重复
4. `git commit`
5. 等确认再 `git push`

---

## ■ 经验目录

开发者查阅用，AI 不自动扫描。

```
experience/
├── pitfalls.md       ← 踩坑记录（场景 + 原因 + 修复）
├── fixes.md          ← AI 纠错记录（错在哪 → 正确做法）
├── optimization.md   ← 已验证的优化方案（附数据对比）
├── decisions.md      ← 架构决策记录（为什么选 A 不选 B）
└── habits.md         ← 个人开发习惯
```

### AI 写入规则
- `self-improvement` 触发时 → 追加记录到对应的 `experience/` 文件
- 写入后告知文件名和摘要
- 同一模式重复 ≥3 次 → 询问是否记入 `habits.md`

---

## ■ 扩展说明

- 前三节（Identity、Project Overview、Deployment & Config）→ 每项目重填，**动态上下文**
- 中间规则（技术栈约定、交互规则、Git 流程）→ 稳定部分，有更好实践时才改
- `experience/` → 开发者自己看，不混入 AI 上下文
- **技术栈约定那一节**是整个模板最灵活的——每个项目按实际技术栈改写，不用 Spring Boot 就删掉，用 Python 就换成 Python 的约定

规则超 500 行或引入第二套技术栈时：
- 拆出各栈专属规则到 `profiles/` 目录
- 在本节加一条硬指令要求 AI 读取所有 profile
