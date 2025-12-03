# AI Rules - Modular Code Quality Guidelines for AI-Assisted Development

A comprehensive, modular set of rules designed to guide AI coding assistants (like GitHub Copilot, Claude, ChatGPT) in generating production-ready, maintainable, and secure code.

## 📖 Overview

This repository contains a curated collection of best practices, architectural guidelines, and coding standards organized into modular files. Instead of a monolithic 2000+ line rulebook, these rules are split into focused modules that you can mix and match based on your project's needs.

**Total Size:** ~2100 lines total (modular files)  
**Key Features:** Token efficiency, expert guidance, loss-cutting mechanisms, rule flexibility tiers

## 🗣️ Communication Language Configuration

**Where to set AI's communication language:**
- Located in `00_Core_Protocol.md` → Section 0: Communication Protocol
- Default: AI uses **Simplified Chinese** for communication
- Code (variables, comments, commits): **Always English**

**To change AI's language:**
1. Edit `00_Core_Protocol.md`
2. Find "Section 0. Communication Protocol (CRITICAL)"
3. Modify the language setting to your preference

## 📖 Overview

1. **Quality over Quantity:** Small, focused, well-tested code
2. **Security First:** Never compromise on security
3. **User-Centric:** Always prioritize user experience
4. **Pragmatic:** Rules are guidelines, not chains
5. **Continuous Improvement:** Adapt rules based on project needs

## 📁 File Structure

```
Modular_Rules/
├── 00_Core_Protocol.md          [348 lines] ⭐ Required for all projects
├── 10_Frontend_Web.md           [165 lines] Frontend frameworks & mobile
├── 11_UI_UX_Design.md           [ 53 lines] Design guidelines & accessibility
├── 20_Backend_General.md        [ 88 lines] Database, DevOps, API design
├── 30_Lang_Python.md            [ 42 lines] Python-specific rules
├── 31_Lang_TypeScript.md        [ 39 lines] TypeScript/Node.js rules
├── 32_Lang_Java.md              [ 20 lines] Java/Spring Boot rules
├── 33_Lang_Go.md                [ 25 lines] Go-specific rules
├── 34_Lang_Kotlin.md            [ 99 lines] Kotlin (Android/Backend)
├── 40_Testing.md                [250 lines] Testing standards & patterns
├── 50_Edge_Cases.md             [240 lines] Special scenarios & legacy code
└── 60_AI_Workflow.md            [1445 lines] AI communication & workflow
```

## 🚀 Quick Start

### For AI Assistants

Feed the appropriate combination of files based on the project type:

#### React Frontend Project
```
00_Core_Protocol.md + 10_Frontend_Web.md + 11_UI_UX_Design.md + 31_Lang_TypeScript.md
```
**Total context:** 302 + 166 + 43 + 40 = **551 lines**

#### Python Backend (FastAPI)
```
00_Core_Protocol.md + 20_Backend_General.md + 30_Lang_Python.md + 40_Testing.md
```
**Total context:** 302 + 89 + 43 + [TBD] = **~500 lines**

#### Android App (Kotlin + Jetpack Compose)
```
00_Core_Protocol.md + 34_Lang_Kotlin.md + 11_UI_UX_Design.md
```
**Total context:** 302 + 100 + 43 = **445 lines**

#### Full-Stack Next.js
```
00_Core_Protocol.md + 10_Frontend_Web.md + 11_UI_UX_Design.md + 20_Backend_General.md + 31_Lang_TypeScript.md
```
**Total context:** 302 + 166 + 43 + 89 + 40 = **640 lines**

### For Developers

Simply copy the relevant markdown files into your AI assistant's context window, or reference them in your custom instructions.

## 📋 File Descriptions

### Core (Always Required)
- **00_Core_Protocol.md** - Communication protocol, architecture principles, type safety, error handling, Git standards, security checklist, refactoring workflow, and documentation standards.

### Domain-Specific
- **10_Frontend_Web.md** - React, Vue, Angular, React Native, Flutter, performance patterns, accessibility (code examples).
- **11_UI_UX_Design.md** - Modern design aesthetics, color palettes, layout principles, responsive design, interaction feedback.
- **20_Backend_General.md** - SQL/NoSQL databases, Docker, CI/CD, caching strategies, API documentation, monitoring.

### Language-Specific
- **30_Lang_Python.md** - FastAPI/Django/Flask, Pydantic validation, async patterns, type hints.
- **31_Lang_TypeScript.md** - Node.js project structure, Zod/Joi validation, type safety, error handling.
- **32_Lang_Java.md** - Spring Boot, Lombok, Bean Validation, layered architecture.
- **33_Lang_Go.md** - Project structure, gofmt, explicit error handling.
- **34_Lang_Kotlin.md** - Android/Ktor, coroutines, Jetpack Compose, null safety, data classes, Hilt DI.

### Advanced Topics
- **40_Testing.md** - Testing strategies, coverage requirements, unit/integration patterns.
- **50_Edge_Cases.md** - Legacy code migration, i18n, WebSocket/SSE, performance optimization.
- **60_AI_Workflow.md** - How AI should communicate with users, task decomposition, self-correction.

## 💡 Usage Examples

### Example 1: Starting a New React Project
```markdown
I'm building a React 18 dashboard with TypeScript.

Rules to follow:
- 00_Core_Protocol.md
- 10_Frontend_Web.md
- 11_UI_UX_Design.md
- 31_Lang_TypeScript.md
```

### Example 2: Adding a Python Microservice
```markdown
I need to create a FastAPI microservice for user authentication.

Rules to follow:
- 00_Core_Protocol.md
- 20_Backend_General.md
- 30_Lang_Python.md
- 40_Testing.md
```

### Example 3: Refactoring Legacy Code
```markdown
I'm modernizing a Vue 2 app to Vue 3 with TypeScript.

Rules to follow:
- 00_Core_Protocol.md
- 10_Frontend_Web.md
- 31_Lang_TypeScript.md
- 50_Edge_Cases.md (for legacy code handling)
```

## 🌟 Key Features

### Modular & Efficient
- **Contextual Loading:** Only load rules relevant to your stack
- **Reduced Token Usage:** 64% smaller than monolithic alternatives
- **Faster AI Responses:** Less noise = better focus

### Comprehensive Coverage
- ✅ 5 frontend frameworks (React, Vue, Angular, React Native, Flutter)
- ✅ 5 programming languages (TypeScript, Python, Java, Go, Kotlin)
- ✅ Security, performance, accessibility, testing
- ✅ Modern design principles (inspired by Linear, Vercel, Stripe)

### Production-Ready Standards
- Type safety enforcement (avoid `any`, use type guards)
- Error handling priority levels (MUST/SHOULD/MAY)
- File size limits (500 lines) & function limits (50 lines)
- Security checklist (XSS, SQL injection, secret management)
- Git commit conventions (Conventional Commits)

## 🛠️ Customization

These rules are designed to be **pragmatic, not dogmatic**. You can:
1. Fork this repository
2. Modify rules to match your team's conventions
3. Add new language-specific files
4. Adjust strictness levels (🔴 MUST / 🟡 SHOULD / 🟢 MAY)

## 📚 Contributing

This is a living document. Contributions are welcome! Please:
1. Follow the existing modular structure
2. Keep rules concise and actionable
3. Provide code examples where applicable
4. Update this README with any new files

## 📄 License

[MIT License](LICENSE) - Feel free to use in personal or commercial projects.

## 🙏 Acknowledgments

Inspired by best practices from:
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)
- [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) by Robert C. Martin
- Modern SaaS design systems (Linear, Vercel, Stripe)

---

**Note:** These rules are optimized for AI assistants but are equally valuable for human developers as quick reference guides.
