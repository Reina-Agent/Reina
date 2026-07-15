<div align="center">

<img src="img/logo.png" alt="Reina" width="180" />

# Reina

### 桌面 AI 智能体 —— 多智能体协作、MCP 与 Skills、自带模型

[English](./README.md) · **中文**

[![Release](https://img.shields.io/github/v/release/Reina-Agent/Reina?color=blue)](https://github.com/Reina-Agent/Reina/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Reina-Agent/Reina/total?color=brightgreen)](https://github.com/Reina-Agent/Reina/releases)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](./LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-lightgrey.svg)](#-下载与运行)
![GitHub stars](https://img.shields.io/github/stars/Reina-Agent/Reina?style=social)

[下载](#-下载与运行) · [核心能力](#-核心能力) · [看懂它怎么写的](#-看懂它怎么写的) · [从源码构建](#-从源码构建)

</div>

---

<div align="center">
  <img src="img/demo.gif" alt="Reina 读取本地项目并回答" width="90%" />
</div>

---

**Reina 是一个开源的桌面 AI 智能体。** 它围绕你的本地工作区持续对话——理解项目、整理信息、推进多步骤任务；一双手不够用时，还能把工作拆给一组协同的子智能体。整个产品就是一个普通桌面应用：模型和 API Key 由你自己配置，不经过任何厂商后台。

> [!NOTE]
> Reina 自带模型接入层：你在设置里配置自己的模型与 API Key（存在本地 `~/.reina/`），由你决定接哪家。没有产品级 HTTP 服务，没有云端后台。

## ✨ 核心能力

- 🧠 **工作区级会话** —— 围绕本地项目、文件和任务组织持续对话。长会话经过上下文压缩也不忘最初目标，全部会话持久化，中途暂停可无缝继续。
- 🤝 **多智能体团队模式** —— 由协调者（coordinator）智能体把目标拆成子任务 DAG，通过阶段关卡（phase gate）调度 worker 智能体，所有分支收口才算完成——不会协调卡死，也不会提前收尾。
- 🧩 **MCP 与 Skills，自带市场** —— 通过内置市场接入 MCP 服务器、安装技能；智能体甚至能在任务中途自己搜索并安装新技能。
- 🔑 **自带模型与密钥** —— 任意 Provider 自由配置、按会话切换。API Key 存在 `~/.reina/`，绝不进入界面层，完全由你掌控。
- 🛡️ **可控与透明** —— 有副作用的操作走权限确认，全过程可见、可暂停、可继续。
- 🖥️ **多窗口桌面体验** —— 聊天 / 工作区 / 设置界面清晰分区，贴着本地工作流，而不是停在一个浏览器标签里。自动更新保持最新版本。

## 📚 看懂它怎么写的

想知道这样一个 coding agent 内部到底怎么实现？Reina 的核心机制——agent 循环、上下文压缩、缓存命中工程、子代理看门狗、权限审批、Provider 兼容层——都在 **[learn-agent](https://github.com/7-e1even/learn-agent)** 里被拆成 15 篇可跑的零依赖课程，每一篇都从本仓库的真实实现简化移植而来。读完课程，再回到这里找对应的真实实现。

## 📦 下载与运行

在 [Releases](https://github.com/Reina-Agent/Reina/releases) 下载与你系统匹配的版本：

- **Windows** —— 安装包（NSIS）与便携版。
- **macOS** —— DMG 或 ZIP。

下载后按系统提示安装或解压运行。首次使用：选择一个工作区 → 在设置里填入你的模型与 API Key → 直接输入目标或任务说明。

## 🛠️ 从源码构建

```bash
git clone https://github.com/Reina-Agent/Reina.git
cd reina
npm install
npm run build:desktop   # 构建主进程 + agent-host + 渲染层
npm run desktop         # 启动桌面应用
```

> [!TIP]
> 要求 Node.js >= 22。架构速览见下方折叠块。

> [!NOTE]
> 聊天界面会尊重系统的**"减少动态效果"**设置。当系统开启"减少动态"时，工具调用卡片展开等过渡动画会被有意关闭——想看到动画请在系统设置里关掉该选项（Windows：设置 → 辅助功能 → 视觉效果 → 动画效果）。

<details>
<summary>架构一览</summary>

```text
渲染层 (React + Tailwind v4：聊天 / 工作区 / 设置窗口)
  → 预加载桥 (preload)
  → 主进程 IPC (Electron main)
  → agent-host (Node 子进程，JSON-line stdio)
  → AgentEngine
  → 各模型 Provider 与本地工具
```

完整跑在本地桌面应用里：无产品级 HTTP 服务、无 CLI 产品入口。

</details>

## 🤝 参与贡献

欢迎 Issue 与 PR！新手可以从带 [`good first issue`](https://github.com/Reina-Agent/Reina/labels/good%20first%20issue) 标签的任务开始。

## 🔒 安全

发现安全问题请通过 [GitHub Security Advisories](https://github.com/Reina-Agent/Reina/security/advisories/new) 私下反馈，**不要**直接开公开 Issue。

## 📄 许可证

本项目采用 [AGPL-3.0](./LICENSE)。

你可以自由使用、修改、分发，但**任何修改版本——包括通过网络对外提供的服务——都必须以 AGPL-3.0 开放其完整源码**。如需在闭源 / 商业产品中使用，请联系作者获取商业授权。

---

<div align="center">
<sub>如果 Reina 对你有用，点个 ⭐ Star 支持一下 —— 这是对独立开发者最大的鼓励。</sub>
<br/>
<sub>Copyright © 2026 7-e1even</sub>
</div>
