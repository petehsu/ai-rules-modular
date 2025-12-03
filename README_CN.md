# AI Rules - 模块化代码质量指南（AI 辅助开发专用）

一套全面、模块化的规则集，旨在指导 AI 编码助手（如 GitHub Copilot、Claude、ChatGPT）生成生产级、可维护且安全的代码。

## 📖 概述

本仓库包含一套精心策划的最佳实践、架构指南和编码规范，并按模块化方式组织。相比于单一的 2000 多行规则文件,这些规则被拆分为聚焦的模块,您可以根据项目需求灵活组合。

**总规模:** 约 2100 行（模块化文件）  
**核心功能:** Token 效率优化、专家指导、止损机制、规则灵活性分级

## 🗣️ 交流语言配置

**在哪里设置 AI 的交流语言：**
- 位置：`00_Core_Protocol.md` → 第 0 节：Communication Protocol
- 默认：AI 使用 **简体中文** 交流
- 代码（变量名、注释、提交信息）：**始终使用英文**

**如何更改 AI 语言：**
1. 编辑 `00_Core_Protocol.md`
2. 找到 "Section 0. Communication Protocol (CRITICAL)"
3. 修改语言设置为你的偏好

## 📖 概述

1. **质量优于数量**：小而精、经过充分测试的代码
2. **安全第一**：永不在安全上妥协
3. **以用户为中心**：始终优先考虑用户体验
4. **务实主义**：规则是指导方针，而非枷锁
5. **持续改进**：根据项目需求调整规则

## 📁 文件结构

```
Modular_Rules/
├── 00_Core_Protocol.md          [348 行] ⭐ 所有项目必选
├── 10_Frontend_Web.md           [165 行] 前端框架 & 移动端
├── 11_UI_UX_Design.md           [ 53 行] 设计指南 & 无障碍访问
├── 20_Backend_General.md        [ 88 行] 数据库、DevOps、API 设计
├── 30_Lang_Python.md            [ 42 行] Python 专属规则
├── 31_Lang_TypeScript.md        [ 39 行] TypeScript/Node.js 规则
├── 32_Lang_Java.md              [ 20 行] Java/Spring Boot 规则
├── 33_Lang_Go.md                [ 25 行] Go 专属规则
├── 34_Lang_Kotlin.md            [ 99 行] Kotlin (Android/后端)
├── 40_Testing.md                [250 行] 测试标准 & 模式
├── 50_Edge_Cases.md             [240 行] 特殊场景 & 遗留代码
└── 60_AI_Workflow.md            [1445 行] AI 交流 & 工作流
```

## 🚀 快速开始

### 给 AI 助手使用

根据项目类型投喂对应的文件组合：

#### React 前端项目
```
00_Core_Protocol.md + 10_Frontend_Web.md + 11_UI_UX_Design.md + 31_Lang_TypeScript.md
```
**总上下文:** 302 + 166 + 43 + 40 = **551 行**

#### Python 后端 (FastAPI)
```
00_Core_Protocol.md + 20_Backend_General.md + 30_Lang_Python.md + 40_Testing.md
```
**总上下文:** 302 + 89 + 43 + [待定] = **约 500 行**

#### Android 应用 (Kotlin + Jetpack Compose)
```
00_Core_Protocol.md + 34_Lang_Kotlin.md + 11_UI_UX_Design.md
```
**总上下文:** 302 + 100 + 43 = **445 行**

#### 全栈 Next.js
```
00_Core_Protocol.md + 10_Frontend_Web.md + 11_UI_UX_Design.md + 20_Backend_General.md + 31_Lang_TypeScript.md
```
**总上下文:** 302 + 166 + 43 + 89 + 40 = **640 行**

### 给开发者使用

只需将相关的 markdown 文件复制到你的 AI 助手的上下文窗口中，或在你的自定义指令中引用它们。

## 📋 文件说明

### 核心（始终必选）
- **00_Core_Protocol.md** - 沟通协议、架构原则、类型安全、错误处理、Git 规范、安全检查清单、重构工作流、文档规范。

### 领域专属
- **10_Frontend_Web.md** - React、Vue、Angular、React Native、Flutter、性能模式、无障碍访问（代码示例）。
- **11_UI_UX_Design.md** - 现代设计美学、配色方案、布局原则、响应式设计、交互反馈。
- **20_Backend_General.md** - SQL/NoSQL 数据库、Docker、CI/CD、缓存策略、API 文档、监控。

### 语言专属
- **30_Lang_Python.md** - FastAPI/Django/Flask、Pydantic 验证、异步模式、类型提示。
- **31_Lang_TypeScript.md** - Node.js 项目结构、Zod/Joi 验证、类型安全、错误处理。
- **32_Lang_Java.md** - Spring Boot、Lombok、Bean Validation、分层架构。
- **33_Lang_Go.md** - 项目结构、gofmt、显式错误处理。
- **34_Lang_Kotlin.md** - Android/Ktor、协程、Jetpack Compose、空安全、数据类、Hilt 依赖注入。

### 进阶主题
- **40_Testing.md** - 测试策略、覆盖率要求、单元/集成测试模式。
- **50_Edge_Cases.md** - 遗留代码迁移、国际化、WebSocket/SSE、性能优化。
- **60_AI_Workflow.md** - AI 应如何与用户沟通、任务分解、自我纠错。

## 💡 使用示例

### 示例 1：启动新的 React 项目
```markdown
我正在构建一个使用 TypeScript 的 React 18 仪表板。

需要遵循的规则：
- 00_Core_Protocol.md
- 10_Frontend_Web.md
- 11_UI_UX_Design.md
- 31_Lang_TypeScript.md
```

### 示例 2：添加 Python 微服务
```markdown
我需要创建一个用于用户认证的 FastAPI 微服务。

需要遵循的规则：
- 00_Core_Protocol.md
- 20_Backend_General.md
- 30_Lang_Python.md
- 40_Testing.md
```

### 示例 3：重构遗留代码
```markdown
我正在将 Vue 2 应用现代化为 Vue 3 + TypeScript。

需要遵循的规则：
- 00_Core_Protocol.md
- 10_Frontend_Web.md
- 31_Lang_TypeScript.md
- 50_Edge_Cases.md (用于处理遗留代码)
```

## 🌟 主要特性

### 模块化 & 高效
- **按需加载**：仅加载与你的技术栈相关的规则
- **减少 Token 消耗**：比单体方案小 64%
- **更快的 AI 响应**：更少的噪音 = 更好的聚焦

### 全面覆盖
- ✅ 5 个前端框架（React、Vue、Angular、React Native、Flutter）
- ✅ 5 种编程语言（TypeScript、Python、Java、Go、Kotlin）
- ✅ 安全、性能、无障碍访问、测试
- ✅ 现代设计原则（灵感来自 Linear、Vercel、Stripe）

### 生产级标准
- 类型安全强制（避免 `any`，使用类型守卫）
- 错误处理优先级（MUST/SHOULD/MAY）
- 文件大小限制（500 行）& 函数限制（50 行）
- 安全检查清单（XSS、SQL 注入、密钥管理）
- Git 提交约定（Conventional Commits）

## 🛠️ 自定义

这些规则设计为**务实的，而非教条的**。你可以：
1. Fork 本仓库
2. 修改规则以匹配团队约定
3. 添加新的语言专属文件
4. 调整严格程度（🔴 必须 / 🟡 应该 / 🟢 可以）

## 📚 贡献

这是一份活文档，欢迎贡献！请：
1. 遵循现有的模块化结构
2. 保持规则简洁且可操作
3. 在适用的地方提供代码示例
4. 更新此 README 以包含任何新文件

## 📄 许可证

[MIT License](LICENSE) - 可自由用于个人或商业项目。

## 🙏 致谢

灵感来源于以下最佳实践：
- [Airbnb JavaScript 风格指南](https://github.com/airbnb/javascript)
- [Google TypeScript 风格指南](https://google.github.io/styleguide/tsguide.html)
- Robert C. Martin 的 [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
- 现代 SaaS 设计系统（Linear、Vercel、Stripe）

---

**注意：** 这些规则针对 AI 助手优化，但同样适用于人类开发者作为快速参考指南。
