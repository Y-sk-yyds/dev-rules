# 踩坑记录

> 记录开发中遇到的问题、原因分析、解决方案。每条包含场景描述。

## 格式

```
### 标题（简短描述问题）

**场景**：什么情况下触发
**现象**：看到什么异常/错误
**原因**：根因分析
**解法**：怎么修复的
**教训**：以后怎么避免
```

---

## 记录

<!-- 以下为示例条目，可删除或保留作为模板 -->

### Google Fonts 导致国内加载超时

**场景**：Element Plus 默认引用 Google Fonts CSS
**现象**：页面白屏 30s+，控制台显示 fonts.googleapis.com 请求挂起
**原因**：国内网络环境访问 Google 服务不稳定
**解法**：移除 Google Fonts 引用，改用系统字体栈（`-apple-system, ...`）
**教训**：面向国内用户的 Web 项目，避免依赖境外 CDN 资源

### Vue Router 切换路由时页面不刷新数据

**场景**：从商品列表跳转到商品详情，再跳转到另一个商品详情
**现象**：详情页数据不更新，仍显示上一个商品
**原因**：Vue 复用了同一个组件实例，`created`/`mounted` 不会重新触发
**解法**：用 `watch` 监听 `route.params.id` 变化，在回调中重新请求数据
**教训**：同路由不同参数的跳转，必须处理参数变化的生命周期

### Write 工具写含中文的文件导致 UTF-8 损坏（Windows）

**场景**：使用 Write 工具创建/覆盖含中文的 .vue 或 .java 文件
**现象**：文件看似正常，但 `iconv -f UTF-8` 报 invalid，Vite 构建报 "stream did not contain valid UTF-8"，或 Java 编译器报非法字符
**原因**：Write 工具在 Windows 环境下将中文多字节 UTF-8 序列错误编码为 GBK/ISO-8859-1 字节
**解法**：用 Python 脚本写文件，`open(path, 'w', encoding='utf-8')`，中文用 `\uXXXX` Unicode 转义序列
**教训**：Windows 下对含中文的文件，不要直接用 Write 工具，用 Python 中转

### PowerShell Set-Content 导致 BOM + 中文乱码

**场景**：用 PowerShell 编辑含中文的 Java/Vue 文件
**现象**：Java 编译器报 `非法字符: '\ufeff'`（BOM），中文变成乱码（如 "用户不存在" → "鐢ㄦ埛涓嶅瓨鍦?）
**原因**：PowerShell Set-Content 默认编码非 UTF-8，`-Encoding UTF8` 会加 BOM，无 `-Encoding` 则用系统默认编码（GBK）
**解法**：对含中文的文件，避免用 PowerShell 编辑，改用 Python UTF-8 写入
**教训**：Windows 下 PowerShell 不适合编辑含多字节字符的源代码文件

### Java Map 中 Long 序列化后 Vue Router 跳转失效

**场景**：后端用 `Map.put("docId", vh.getDocId())` 返回 JSON，前端 `$router.push(\`/docs/${item.docId}\`)`
**现象**：点击无反应或跳转 404
**原因**：Long 在 JSON 中序列化为数字，Vue Router 期望字符串参数；大数值可能 JS 精度丢失
**解法**：后端显式 `.toString()` — `item.put("docId", vh.getDocId().toString())`
**教训**：后端返回给前端的 ID 类字段，统一序列化为字符串
