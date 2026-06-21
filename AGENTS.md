# AGENTS.md

> 每项目复制此文件到根目录，填前三个区块，其余规则通用。
> AI 自动注入 · 行为规则在跨项目 MEMORY.md，此处不重复。

---

## Identity

- 角色：
- 目标：
- 技术熟练度：

---

## Project Overview

- 项目名称：
- 一句话描述：
- 仓库路径：
- 后端：
- 前端：
- 数据库：

当前进度：
- 已完成：
- 进行中：
- 待做：

---

## Deployment & Config

- 后端端口：
- 前端端口：
- 数据库库名：
- 远程仓库：

---

## 技术栈约定

### Spring Boot 3.x + MyBatis-Plus
- Jakarta EE（`jakarta.*`），不用 `javax.*`
- Entity：`@Data` `@NoArgsConstructor` `@AllArgsConstructor`，camelCase→snake_case
- Service：接口 + Impl
- Controller：`@RequestMapping("/api/xxx")`，统一返回 `Result<T>`
- 全局异常：`@RestControllerAdvice`
- 新建 Controller 先读已有照抄风格
- 密码/密钥走环境变量，本地用 gitignored 的私有配置
- Spring Security 6.x：lambda DSL

### Vue3 + Element Plus + Vite
- `<script setup>` + Composition API
- 状态：ref/reactive 本地，Pinia 跨组件
- API 集中 `api/` 目录，axios baseURL `/api`，模块不加前缀
- 列表必须有 loading + 空态
- 同组件不同路由参数用 watch

### MySQL 8.0
- 每表：id（自增）+ create_time + update_time（ON UPDATE）
- 软删除 is_deleted，字段 COMMENT
- 高频查询和关联键建索引
- 列表页跳过 TEXT/JSON 大字段

### 通用
- 写新文件前先读已有同类文件
- 硬编码值 → 常量/枚举
- 日志 SLF4J，生产关 SQL 日志

### 设计原则
- **从实际出发**：做功能前先参考真实产品（淘宝/京东/闲鱼），布局和交互照抄成熟产品，不自造
- 先想用户体验再写代码，不做"技术能跑但用户不会用"的功能

---

## 经验回写

项目开发中通过 self-improvement 回写到 `D:\newproject\wk2\dev-rules\experience/`
